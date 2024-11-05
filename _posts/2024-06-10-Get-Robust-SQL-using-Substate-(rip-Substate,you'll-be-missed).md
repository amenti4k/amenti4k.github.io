---
layout: post
title: "Building a Natural Language to SQL Query Generator with Substrate"
description: "An exploration of building a robust system for generating SQL queries from natural language using Substrate and modern LLMs"
date: 2024-11-05
categories: [machine-learning, nlp]
tags: [sql, llm, substrate, python, pydantic, openai]
---

# Building a Natural Language to SQL Query Generator

*Purpose: To build a system that generates syntactically and contextually correct SQL queries from natural language inputs.*

This is my experiment to play around with [Substrate](https://www.substrate.run/) that reduces the complexity of multi-model systems by supporting a graph SDK.

## Why Do I Love Substrate?

I think Substrate has several compelling advantages:

- There should be a platform that takes open source models, optimizes them relentlessly, provides an API, and offers the most competitive pricing with great uptime
- Long-term benefits from economies of scale with GPUs and optimization processes
- High demand exists currently, with many users requiring high API volumes
- Potential to train specialized, less powerful models optimized for cost/latency to counter foundation model companies focused primarily on capability

### Counterpoints to Consider

While promising, there are some concerns:

- Sustainability question: Will large model builders become quickly commoditized? Many startups may compete for the same developer dollars
- Community optimization might outpace proprietary optimizations, similar to creating custom optimized PHP versions in 2001 - technical possibility but challenging business case

## Implementation Details

Writing SQL with LLMs presents multiple challenges with hallucinations, not necessarily due to SQL generation itself, but due to contextual misuse.

With larger context windows, the problem becomes more pronounced as dumping all rows and context to prompts consumes excessive tokens for even simple queries.

The idea is to find a combination of **`Syntax`** and **`Context`** that's both robust and efficient through:

1. Mapping of the table being used
2. Providing NLP-style SQL objects to combine for syntax

## Setting Up the Environment

First, let's set up our development environment by installing the necessary Python packages. We'll use Pydantic for data validation and schema definition.

```python
pip install pydantic
from pydantic import BaseModel, Field
from typing import Optional, Union, List
from enum import Enum
```

## Defining Column Types and Enumerations

Let's define enumerations for our database columns and SQL operations to ensure type safety:

```python
class Departments(str, Enum):
    IT = "IT"
    SALES = "SALES"
    ACCOUNTING = "ACCOUNTING"
    CEO = "CEO"

class EmpLevel(str, Enum):
    JUNIOR = "JUNIOR"
    SEMISENIOR = "SEMISENIOR"
    SENIOR = "SENIOR"

class column_names(str, Enum):
    EMPLOYEE_ID = "employee_id"
    FIRST_NAME = "first_name"
    LAST_NAME = "last_name"
    DEPT_ID = "dept_id"
    MANAGER_ID = "manager_id"
    SALARY = "salary"
    EXPERTISE = "expertise"

class TableColumns(BaseModel):
    employee_id: Optional[int] = Field(None, title="Employee ID", description="The ID of the employee")
    first_name: Optional[str] = Field(None, title="First Name", description="The first name of the employee")
    last_name: Optional[str] = Field(None, title="Last Name", description="The last name of the employee")
    dept_id: Optional[Departments] = Field(None, title="Department ID", description="The department ID of the employee")
    manager_id: Optional[int] = Field(None, title="Manager ID", description="The ID of the manager")
    salary: Optional[int] = Field(None, title="Salary", description="The salary of the employee")
    expertise: Optional[EmpLevel] = Field(None, title="Expertise Level", description="The expertise level of the employee")
```

## Defining SQL Syntax Models

Next, we'll define models for SQL operations, comparisons, logic operators, and ordering:

```python
class sql_type(str, Enum):
    SELECT = "SELECT"
    INSERT = "INSERT"
    UPDATE = "UPDATE"
    DELETE = "DELETE"

class sql_compare(str, Enum):
    EQUAL = "="
    NOT_EQUAL = "!="
    GREATER = ">"
    LESS = "<"
    GREATER_EQUAL = ">="
    LESS_EQUAL = "<="

class sql_logic_operator(str, Enum):
    AND = "AND"
    OR = "OR"

class sql_order(str, Enum):
    ASC = "ASC"
    DESC = "DESC"

class sql_comparison(BaseModel):
    column: column_names = Field(..., title="Table Column", description="Column in the Table")
    compare: sql_compare = Field(..., title="Comparison Operator", description="Comparison Operator")
    value: Union[str, Departments, EmpLevel] = Field(..., title="Value", description="Value to Compare")

class sql_logic_condition(BaseModel):
    logic: sql_logic_operator = Field(..., title="Logic Operator", description="Logic Operator")
    comparison: sql_comparison = Field(..., title="Comparison", description="Comparison")

class SQLQuery(BaseModel):
    sql: sql_type = Field(..., title="SQL Type", description="SQL Type")
    columns: list[column_names] = Field(..., title="Columns", description="Columns to Select")
    table: str = Field(..., title="Table", description="Table Name")
    conditions: List[sql_logic_condition] = Field(..., title="Conditions", description="List of Conditions with Logic")
    order: Optional[sql_order] = Field(None, title="Order", description="Order")
    limit: Optional[int] = Field(None, title="Limit", description="Limit")
```

## Generating SQL Query Structure

Now we'll create a function to generate the SQL query structure using OpenAI's GPT-3.5 model:

```python
pip install openai
import openai
import json

openai.api_key = 'your-api-key-here'

def generate_sql_json(question: str) -> dict:
    prompt = f"""
    Generate a JSON structure for an SQL query based on the following question:
    {question}

    Use the following JSON schema:
    {json.dumps(SQLQuery.model_json_schema(), indent=2)}

    Respond only with the JSON structure, nothing else.
    """

    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "You are a helpful assistant that generates SQL query structures in JSON format."},
            {"role": "user", "content": prompt}
        ]
    )

    return json.loads(response.choices[0].message['content'])

# Example usage
question = "Can you provide me with the amount of employee id and salary in the Account department that has a salary greater than 50000 in descending order?"
json_response = generate_sql_json(question)

# Parse and validate the response
query_formatted = SQLQuery(**json_response)
```

## Formatting the SQL Query

Finally, let's create a function to format the SQLQuery object into a proper SQL string:

```python
def format_sql_query(query: SQLQuery) -> str:
    # Generate the initial Base Query with no comparisons
    generated_query = f"{query.sql} {', '.join([col.value for col in query.columns])} FROM {query.table}"

    # Check for additional conditions
    if query.conditions:
        # Replace first logical operator with WHERE
        generated_query += " WHERE "

        # For each condition, append it the query in the correct format
        for i, condition in enumerate(query.conditions):
            if i > 0:
                generated_query += f" {condition.logic} "
            generated_query += f"{condition.comparison.column} {condition.comparison.compare} '{condition.comparison.value}'"

    # if there is an ordering rule, then format and append
    if query.order:
        generated_query += f" ORDER BY {', '.join([col.value for col in query.columns])} {query.order}"

    # if there is a limit, then format and append
    if query.limit:
        generated_query += f" LIMIT {query.limit}"

    return generated_query

# Generate the final SQL query
final_query = format_sql_query(query_formatted)
print(final_query)
```

This system allows us to generate SQL queries from natural language inputs in a structured and type-safe manner. By using Pydantic models, we ensure that our generated queries adhere to the correct format and data types.

## Production Considerations

When implementing this system in a production environment, remember to:

- Handle potential errors, such as invalid inputs or API failures
- Add more complex query capabilities (JOINs, nested queries) as needed
- Implement proper error logging and monitoring
- Consider rate limiting and API usage optimization
- Add proper security measures for SQL injection prevention