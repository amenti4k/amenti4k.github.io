---
layout: post
title: "Building on Quicksand: The Reality of Production AI Systems"
description: "We built it wrong. Not in the fun, 'let's try something crazy and see what happens' way. In the pedestrian, 'we've been writing if-else statements for six months and calling it AI' way."
date: 2025-07-15
categories: [ai]
tags: [autonomous-systems, ai-engineering, production-ai, temporal, distributed-systems, didero-ai]
---

# Building on Quicksand: The Reality of Production AI Systems

We built it wrong. Not in the fun, "let's try something crazy and see what happens" way. In the pedestrian, "we've been writing if-else statements for six months and calling it AI" way. We treated language models like smarter regex. We thought we were building the future. We were building the world's most expensive state machine.

Here's what nobody tells you about building autonomous procurement systems: it's not an AI problem. It's a distributed systems problem wearing an AI costume. And until you accept that, you'll keep burning API tokens trying to parse "please send the usual plus 20%" while your customers slowly realize your "AI-powered" solution is just their old workflow with more steps and higher latency.

## The Seductive Lie of the Demo

Every procurement automation startup begins the same way. You feed a clean purchase order to GPT-4. It extracts the data perfectly. The investors nod. The check clears. You are, briefly, a genius.

Then reality arrives in the form of actual procurement data:
- Email threads where the actual order is in message #31 of 47
- PDFs of scanned printouts of emails with handwritten corrections
- "Please process ASAP per our discussion" with no context
- Excel sheets embedded in PowerPoint embedded in PDFs
- Vendors who send price updates via WhatsApp screenshots

Your beautiful demo becomes:

```python
def process_purchase_order(po):
    # Started as 10 lines
    # Now 2,000 lines of scar tissue
    
    if customer.id == 37:
        # Tom only approves on Thursdays
        # But not if amount > 7500
        # Unless it's a preferred vendor
        # But preferred vendor list changes based on...
        # ... 47 more conditions
```

We had over 1,000 configuration parameters. Not because we were stupid. Because we were smart in exactly the wrong way. We thought we could deterministically handle chaos. We thought configuration was the same as intelligence.

## The Law of Leaky Abstractions, AI Edition

Joel Spolsky wrote about how all non-trivial abstractions leak. With AI, they don't just leak - they hemorrhage. 

TCP can hide packet loss until it can't. SQL can hide query planning until it can't. But AI? AI can hide its complete lack of understanding until you're in production and it decides that "net 30" means "30 items net weight."

The abstraction of "AI understands business documents" is so leaky it's more hole than roof. And the leaks are non-deterministic. TCP fails predictably. AI fails creatively.

Here's what actually happens in production:

```python
# What you think you're building
result = ai.extract(document)

# What you're actually building
result = ai.extract(document)
if result.confidence < 0.8:
    result = ai.extract_with_different_prompt(document)
    if still_looks_wrong(result):
        result = try_different_model(document)
        if completely_nonsensical(result):
            result = handwritten_regex_fallback(document)
            if result is None:
                create_human_task("AI is confused")
```

Each retry burns tokens. Each fallback adds complexity. Each human task erodes the "autonomous" in your "autonomous system."

## The Architectural Inversion Nobody Explains Properly

Here's what every blog post about agents gets wrong: they focus on the AI. The AI is the easy part. The hard part is accepting that you're not building a pipeline. You're building a distributed system where one of your services happens to be non-deterministic.

Traditional software architecture with AI:
```
Input → Parse → Validate → Business Logic → Output
         ↓
       (AI helps with parsing)
```

This is using a spaceship as a bus. You're constraining the most flexible part of your system to the most rigid role.

What actually works:
```
Input → Agent (with tools) → Output
          ↓
    Can invoke: Parse, Validate, 
    CheckBudget, RouteApproval,
    CreateOrder, AskHuman
```

The agent decides the flow. You provide the tools. This isn't some philosophical insight about AI creativity. It's accepting that your business logic is too complex to express as code, so let something that can handle ambiguity figure it out.

## Why Temporal (Or Something Like It) Isn't Optional

Every AI workflow is a distributed transaction. Your AI calls will fail. Not might fail. Will fail. Rate limits, context overflows, model updates that change behavior, solar flares that make GPT-4 think it's a pirate - I've seen it all.

Without durable execution, here's your life:

```
[2024-03-15 02:34:21] Starting workflow PO-48291
[2024-03-15 02:34:23] Extracted vendor: ACME Corp
[2024-03-15 02:34:25] Extracted items: 47 items
[2024-03-15 02:34:27] Validating against business rules...
[2024-03-15 02:34:28] ERROR: OpenAI rate limit exceeded
[2024-03-15 02:34:29] Starting workflow PO-48291 (retry 1)
[2024-03-15 02:34:31] Extracted vendor: ACME Corp ($0.15)
[2024-03-15 02:34:33] Extracted items: 47 items ($0.22)
[2024-03-15 02:34:35] Validating against business rules... ($0.18)
[2024-03-15 02:34:36] ERROR: Context length exceeded
[2024-03-15 02:34:37] Starting workflow PO-48291 (retry 2)
```

You're paying to redo work you already did. At scale, this is burning money for the privilege of being slow.

With durable execution:

```python
@workflow.defn
class PurchaseOrderWorkflow:
    @workflow.run
    async def run(self, po_data):
        # This persists across failures
        extraction = await workflow.execute_activity(
            extract_po_data,
            po_data,
            retry_policy=RetryPolicy(
                maximum_attempts=3,
                backoff_coefficient=2.0
            )
        )
        
        # If we fail here, we resume HERE
        # Not from the beginning
        # extraction is still in memory
        validation = await workflow.execute_activity(
            validate_business_rules,
            extraction
        )
```

This isn't over-engineering. This is accepting that distributed systems require distributed systems thinking. The fact that one of your services is a large language model doesn't change the fundamental nature of the problem.

## The Context Window Is A Lie

Everyone talks about million-token context windows like they solved something. They didn't. They moved the problem. It's like celebrating that your database can handle petabyte tables while ignoring that your queries now take seventeen hours.

Here's what happens when you try to use those million tokens:

1. Performance degrades non-linearly
2. Costs explode (million tokens = $30 per request)
3. The model gets confused and starts hallucinating
4. You get rate limited because you're that customer

Real context management looks like this:

```python
def prepare_context(po_data, full_history):
    # You cannot dump everything
    # The model will cherry-pick random details
    # And ignore what matters
    
    vendor = identify_vendor(po_data)
    
    # Get RELEVANT history
    recent_orders = get_orders(vendor, days=90)
    
    # Extract PATTERNS not data
    patterns = {
        "usual_order_size": stats.median(recent_orders.totals),
        "common_items": extract_frequent_items(recent_orders),
        "approval_patterns": get_approval_history(vendor)
    }
    
    # Include APPLICABLE rules only
    rules = filter_rules(
        all_rules,
        vendor_type=vendor.type,
        amount_range=po_data.estimated_total
    )
    
    return {
        "vendor_context": summarize(vendor),
        "patterns": patterns,
        "rules": rules,
        # This is the key - hooks to get more
        "retrieval_functions": {
            "get_specific_order": lambda id: fetch_order(id),
            "check_budget": lambda: current_budget_status(),
            "get_approval_chain": lambda: build_approval_chain(po_data)
        }
    }
```

You're not giving the AI everything. You're giving it a map and a phone to call for directions.

## Human-in-the-Loop: Tasks as First-Class Citizens

The biggest lie in automation is that humans are the fallback. Humans aren't the fallback. Humans are the product. Your system's job is to make humans superhuman, not to replace them.

We learned this after building a system where humans were an afterthought. "The AI will handle it, humans will deal with exceptions." Except everything is an exception when you're dealing with the beautiful chaos of real business.

Here's what we built instead:

```python
@dataclass
class TaskTypeV2:
    """
    Not a notification. Not an error state.
    A first-class part of the workflow.
    """
    name: str = "PRICE_CHANGE_CONFIRMATION"
    title: str = "Price increased {percentage}% on PO #{po_number}"
    description: str = "{vendor_name} increased prices. New total: ${new_total}"
    
    # This is the key - actions are explicit
    actions: List[TaskAction] = [
        TaskAction(
            type="APPROVE_PRICE_CHANGE",
            title="Accept new pricing",
            handler=approve_price_change,
            execution_params=["po_id", "new_total"]
        ),
        TaskAction(
            type="REQUEST_CLARIFICATION",
            title="Ask vendor why",
            handler=create_vendor_email,
            params=["draft_reason"]
        )
    ]
```

Every task is:
- **Contextual**: Shows what the AI did and why it needs help
- **Actionable**: Clear options, not just "review this"
- **Traceable**: Every decision is logged for the audit trail
- **Integrated**: Actions flow back into the workflow

And because humans don't live in your app:

```python
def generate_task_action_token(task_action, user):
    """
    Make tasks actionable via email
    Because nobody wants another dashboard
    """
    # One-time token to prevent replay attacks
    nonce = uuid4()
    payload = {
        'task_id': task_action.task.id,
        'action_id': task_action.id,
        'user_id': user.id,
        'nonce': nonce,
        'expires': time.time() + (7 * 24 * 60 * 60)
    }
    
    # Store nonce to ensure single use
    ActionTokenNonce.objects.create(
        nonce=nonce,
        task_action=task_action
    )
    
    return signing.dumps(payload, salt=settings.TASK_ACTION_SALT)
```

Click "Approve" in the email. Done. No login. No context switching. The system works with humans, not despite them.

## The Multi-Agent Pattern That Actually Works

Everyone's building "multi-agent systems" now. Most are just multiple API calls with extra steps and a conference talk. Here's what actually works:

```python
class ProcurementOrchestrator:
    """
    Not agents for the sake of agents
    Agents because specialization works
    """
    def __init__(self):
        self.agents = {
            'router': Agent(
                "Determine what type of procurement this is",
                tools=[ClassifyDocument, IdentifyVendor]
            ),
            'extractor': Agent(
                "Extract data from any format",
                tools=[OCRTool, ParseEmail, ExtractFromPDF]
            ),
            'validator': Agent(
                "Validate against business rules",
                tools=[CheckBudget, ValidateApproval, VerifyVendor]
            ),
            'negotiator': Agent(
                "Handle vendor communications",
                tools=[DraftEmail, AnalyzeTerms, CompareHistoricalPricing]
            )
        }
```

The key insight: agents aren't magical. They're specialized functions that happen to use LLMs. The magic is in the orchestration, and the orchestration is just good old-fashioned distributed systems design.

## Safety Rails: Your AI Will Try to Destroy Everything

Not maliciously. Stupidly. Like a very smart toddler with database access.

```python
class SafetyNet:
    """
    Because your AI will eventually try to:
    - Update every record in the database
    - Send emails to the entire vendor list
    - Approve a million dollar order for paper clips
    - Delete production data (ask Replit)
    """
    
    PATTERNS_OF_DOOM = [
        r"UPDATE.*WHERE\s+1\s*=\s*1",
        r"DELETE\s+FROM(?!\s+WHERE)",
        r"DROP\s+TABLE",
        r"TRUNCATE",
        r"(.+@.+){50,}",  # Mass email attempt
    ]
    
    async def execute(self, operation, context):
        risk_score = self.calculate_risk(operation)
        
        if risk_score > 0.7:
            # Don't block - create a task
            task = await create_task(
                type="HIGH_RISK_OPERATION",
                title=f"AI wants to: {operation.summary}",
                actions=[
                    TaskAction("APPROVE", "Allow operation", "red"),
                    TaskAction("DENY", "Block operation", "green"),
                    TaskAction("MODIFY", "Suggest changes", "blue")
                ]
            )
            
            await workflow.wait_for_task(task.id)
            
            if task.selected_action != "APPROVE":
                raise OperationDenied(
                    f"Human denied operation: {task.denial_reason}"
                )
        
        # Audit everything
        await self.audit_log.record({
            'operation': operation,
            'risk_score': risk_score,
            'context': context,
            'approval': task.id if risk_score > 0.7 else 'automatic'
        })
        
        # Execute in transaction
        # So we can roll back when things go wrong
        async with self.transaction():
            result = await operation.execute()
            
            # Sanity check
            if self.looks_insane(result):
                await self.alert_humans(
                    "Operation succeeded but result looks wrong",
                    operation=operation,
                    result=result
                )
                raise RollbackTransaction()
                
            return result
```

## The Truth About Token Economics

Everyone talks about AI costs in terms of tokens per dollar. That's like measuring car efficiency by how much gas you can buy for $20. The real question is: how much value are you extracting per token?

Here's real production math:

**Naive approach:**
- Process PO: 10K tokens ($0.30)
- Fails at step 8 of 10
- Retry from start: 10K tokens ($0.30)
- Fails again (different error)
- Retry from start: 10K tokens ($0.30)
- Success
- Total: 30K tokens ($0.90) for one PO

**With proper architecture:**
- Process PO: 10K tokens ($0.30)
- Fails at step 8
- Resume from step 8: 2K tokens ($0.06)
- Success
- Total: 12K tokens ($0.36)

At 1,000 POs/day, that's $540/day saved. But that's not the real win.

The real win is that you can actually handle 1,000 POs/day without your system falling over. The real win is that when you onboard a new customer, you don't spend three weeks writing custom configuration. The real win is that your engineers can work on features instead of babysitting workflows.

## The Implementation Path That Actually Works

Looking back, here's what we should have done:

**Week 1: Accept the Nature of the Problem**
- This is a distributed systems problem
- AI is a non-deterministic service in your system
- Plan for failure from day one

**Week 2: Build on Proven Primitives**
- Use Temporal or equivalent (not optional)
- Treat workflows as first-class entities
- Every external call needs retry logic

**Week 3: Design for Humans**
- Tasks are not errors, they're features
- Every decision point needs an escape hatch
- Make everything actionable where humans already are

**Week 4: Implement Safety First**
- Audit everything
- Sandbox dangerous operations
- Build rollback into the architecture

**Week 5: Optimize Intelligently**
- Monitor token usage per workflow step
- Build smart context preparation
- Cache what's cacheable

## What Nobody Wants to Admit

Building autonomous systems is harder than building traditional software. Not easier. Harder.

With traditional software, you can reason about behavior. You can write tests that mean something. You can debug with logic instead of vibes.

With AI systems, you're building on quicksand. The model you're using today will behave differently tomorrow. The prompt that works for one customer will hallucinate for another. The context that fits today will overflow next week.

But here's the thing: the value is also 10x higher. A traditional procurement system might save a company 20% on processing costs. An autonomous system that actually works can eliminate 90% of the work entirely.

The key is accepting that you're not building a SaaS tool. You're building a new kind of system that combines the flexibility of human judgment with the scale of software. It's harder than either alone. But when it works, it changes everything.

## The Architecture That Actually Works

After all the mistakes, here's what we run in production:

```python
class AutonomousProcurement:
    """
    This is $10M+ of hard-won knowledge
    compressed into a few dozen lines
    """
    def __init__(self):
        # Three pillars - all required
        self.orchestrator = AgentOrchestrator()
        self.durability = TemporalClient()
        self.safety = SafetyNet()
        
        # Not optional
        self.task_system = TaskSystem()
        self.audit_log = AuditLog()
        self.monitoring = ObservabilityStack()
    
    async def process(self, input_data):
        # Everything is a workflow
        workflow = await self.durability.start_workflow(
            ProcurementWorkflow,
            input_data,
            id=f"proc-{generate_id()}",
            retry_policy=RetryPolicy(
                maximum_attempts=3,
                backoff_coefficient=2.0,
                non_retryable_errors=[
                    "BusinessLogicViolation",
                    "HumanInterventionRequired"
                ]
            )
        )
        
        return await workflow.result()

@workflow.defn
class ProcurementWorkflow:
    @workflow.run
    async def run(self, input_data):
        # Let the agent figure out what to do
        agent = Agent(
            goal="Process this procurement data correctly",
            tools=self.load_tools(),
            constraints=self.load_business_rules(),
            safety=self.safety_net
        )
        
        # Process with escape hatches
        result = await workflow.execute_activity(
            agent.process,
            input_data,
            start_to_close_timeout=timedelta(minutes=10),
            heartbeat_timeout=timedelta(seconds=30)
        )
        
        # Humans are part of the flow, not exceptions to it
        if result.needs_human_input:
            task = await self.create_task_from_result(result)
            
            # This waits for human action
            # Could be minutes, hours, or days
            await workflow.wait_for_task_completion(task.id)
            
            # Incorporate human decision
            human_input = await self.get_task_result(task.id)
            result = await agent.continue_with_human_input(
                result,
                human_input
            )
        
        # Final safety check
        if not await self.validate_result(result):
            raise WorkflowError(
                "Result failed validation",
                result=result,
                recovery_hint="Check business rules"
            )
        
        return result
```

That's it. Not 2,000 lines of configuration. Not hundreds of if-else statements. Just the right architecture for a fundamentally hard problem.

## The Bottom Line

We thought we were building AI-powered procurement. We were actually solving distributed systems problems, designing human-computer collaboration, implementing durable execution patterns, and building safety rails around non-deterministic services.

The AI part was the easiest piece.

If you're building autonomous systems, stop thinking about prompts and start thinking about architecture. Stop trying to eliminate humans and start empowering them. Stop pretending AI is deterministic and start building systems that thrive on uncertainty.

The patterns exist. The tools exist. You just have to stop believing the demo and start engineering for reality.

And reality is a 47-email thread where the purchase order is a screenshot of a whiteboard posted in message #31, and somehow your system needs to handle it.

Welcome to the future. It's messier than the blog posts promised.