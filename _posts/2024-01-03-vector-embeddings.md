# Vector Embeddings - Hype from Excess Dry Power?

*Embeddings – A Hype Cycle Fueled by Excess Dry Powder?*

At the bottom of everything that I’m trying to do here, what I’m trying to do is evaluate whether AI companies are worth leaving everything being and betting on?

## Reflexivity Framework

I want to start off with the idea of reflexivity as I assume the best investors put their earnings and future (skin in the game) by predicting how the future goes. This relates as I’m looking if there is anything material in the AI space that will change the career direction I take. Investors don’t base their decisions on reality, but rather on their perceptions of reality instead. A framework is essential when looking at new technologies and the ecosystem it creates.

However, their actions from these perceptions have an impact on reality, or fundamentals, which then affects investors' perceptions and thus prices. The process is self-reinforcing and tends toward disequilibrium, causing prices to become increasingly detached from reality – ie. crypto.

People get used to things. People think about the world through the lenses provided by the status quo of the things they use. Then when the world changes, sometimes whole new ideas are possible. The strongest example of this is probably the Web. It enabled all kinds of ideas that people didn’t think of before. The network of interconnected computers provided a new mental model for them to work from to invent new things.

Social media didn’t immediately come with the web. Why not? It takes time for the new reflexive part of an innovation to arrive. To understand what is fully possible under the new technology paradigm, some people need to have worked in it natively for a few years so that they begin to break down the status quo way of thinking.

## Defensibility in Building

From a technical perspective it’s a huge breakthrough that will have lasting impacts. As technology makes doing more stuff faster and easier, it’s increasingly difficult to find areas of long-term defensibility in business models. The key position investors seem to be taking is that “context layers” that take these generative tools and put them into some point solution of a workflow is the place to make a bet.

It’s hard to make these defensible for two reasons:

1. **First**, there will be too many players because the barriers to entry are low and that drives a competitive dynamic that is unfavorable to investors.

2. **Second**, they risk competition with the foundation models themselves as those models improve. Not only could OpenAI boot your company off of their API, but they could also improve upon their model faster than you can build out the middle layer - rendering your improvements useless in a matter of days with a massive new update.

Sometimes, emboldened by the strength of immediate need, and feeling the pressure to raise money and execute quickly in a noisy market, founders will be quickly drawn to “defensible technical depth” as their narrative to investors. The risk is that they're not yet sure it's true, but they say it enough to convince themselves of a world model that's wrong. Counterintuitively, recognizing that no part of solving the immediate problem is hard forces a more useful ongoing search and paranoia. Maybe defensibility is overstated for most early-stage startups. At seed stage, the only defensibility is the quality of founders. Also, It’s actually irresponsible to *not* leverage GPT – similar to mobile/cloud. Startups are often a spread trade on new innovations before wider adoption. And especially salient with such a general purpose technology like LLMs — a rising tide.

Most $10B+ companies seem defensible now, but it took them several years... execution is the only real moat. It is wrongfully sought by investors, too. The problem with the "sell picks and shovels during a gold rush" analogy is that picks and shovels are fungible, and software products are not. Eventually, defaults do emerge. The risk of solving easy problems is that they're easy for other people to solve too. They can be solved by incumbents with a distribution advantage, or by other startups. That’s why leadership even in "temporary markets" is a valuable position, and "easy problems" can still be good entry points for startups to leverage. Almost any growing problem ends up deeper than it first appears – but you have to be cognizant of this going in.

## Unstructured Data > Structured

Insights and data are valuable to businesses, but only when you have access to a source that the general market doesn’t. The harder a valuable piece of data is to grab, the more attractive it is.

Many valuable pieces of data sit within unstructured text-based sources. It’s notoriously tedious and difficult to extract insights from them.

*Ex: Public filings, public records PDF, transcriptions*

Full-stack retrieval goes like this:

1. **You have a raw corpus of documents** (Held in the cloud)
2. **You split them into semantically meaningful chunks** (With LangChain or other text splitters)
3. **You convert them into some vector representation for easy comparison and searching** (Using OpenAI’s embeddings)
4. **You store those vectors** (Using Pinecone or Weaviate or Chroma)
5. **You retrieve certain documents based on the task at hand** (Metal?)

I’m unsure how much of that stack a Pinecone.io is going to want to take vs a company like Metal – which is a current YC.

## Contextualizing

We can’t build unique models, but we can change the data through embeddings and update them affordably. Initial OpenAI embeddings, and cosine ranking is subpar after the initial wow factor. So to improve on models in private data, we need fine-tuning models with domain, incorporate keyword ‘wut’ search, and have multiple ranking methods.

### Problem

Semantic search gets you 90% of the way there for easy questions & answers, but only 30-40% for hard Q&A.

The hard part is understanding which documents are relevant to the query you give to the LLM.

### Why This Is Interesting to Me

I see two routes document retrieval could go:

- **Route #1 (Horizontal Retrieval):** One general engine is really good at document retrieval across industries and domains (Law, Medical, Real Estate, etc.). It has a reasoning engine that tells it where to look.
- **Route #2 (Verticalized Retrieval):** Specialized retrieval engines are needed who are experts at traversing law documents which are different than medical, real estate, etc.

I’m unsure which way it will go! I’m currently leaning towards #2.

The winner of this space will go full-stack and take over more document management/retrieval workflows.

## Vector Embeddings

Learned matrix transformations that translate a dimensional space to another one while trying to go through a big information loss.

Most places don’t bother to define embeddings in general, or instead they describe the properties of the embeddings they want to use. Some want compression, some want cosine similarity.

At the end of the day, any medium that comes into these codes has to be converted to numerical vector. These conversions might be image converters, NLP text converters, audio converters, etc. Not only do embeddings allow us to analyze and process vast amounts of data, but it also has the added benefit of being language-agnostic. Embeddings are modular independent and anything that’s an input can be embedded.

The ability to vector match lets you have outcomes like “pink spiky fruit” mapping to dragonfruit instead of exact word matching that might lead to spiky fruit, or pink fruit, etc. Put easily, vector matching adds context. Basically, even if you have things that don’t have traditionally the same meaning, this will reduce it to points where the little amounts of nuance matter and we can match it to a specific part — meaning we can vector embed and capture meaning.

Given these vectors are essential, there is a need of databases for vectors that allow for storage, indexing, and servicing.

Vector search libraries help developers search through large collections of vectors for clusters or nearest neighbors. Popular ones include Google’s **ScaNN** or Facebook’s **Faiss**. Vector search libraries are great for vector search, but they’re not databases and have trouble at large scale.

### Con

There are currently a thousand “load embedding vectors into a vector database and selectively load results into the context window” startups right now—it's crazy.

### Gap in Market

#### Pros

There’s an issue with having an open source alternative that doesn’t let users log in with GitHub and spin up an index and upload their vectors.

#### Features and Integration

One pain point that we noticed with a lot of existing vector stores is they often involved connecting to an external server that stored the embeddings. While that is fine for putting applications into production, it does make it a bit tricky to easily prototype applications locally.

They found that these were mostly geared to other use-cases and access patterns, like large-scale semantic search. Additionally, they were often a hassle to set up and run, especially in a development environment.

Since Chroma is deployed locally it will have lower latency than a managed cloud service due to network latency.

#### Cons

The issue with unmanaged—self-hosted—vector databases:

Self-hosted vector databases are a big step up from vector search libraries, but they still require significant configuration from engineering teams to scale without affecting latency or availability. They don’t come with any security guarantees (i.e., GDPR or SOC 2 Type 2) and leave you with the operational overhead of maintaining additional infrastructure, monitoring additional services, and troubleshooting when things break. Solving these problems is where managed vector databases come into play.

### Open Sourcing

#### Pro

Can be the ability to move at the pace of AI. We don’t know what it’s bringing and the dimensional shifts it’s going to take. So to keep up with the directional momentum of the ground moving underneath, letting users determine and help us evolve the databases might be a better way.

AI is a landscape of shifting sands. What developers want today is not what they'll want in six months, and what they need to build demos is not what they need in production, is not what they'll need for integration into existing products. But demos could be the path to distribution.

#### Con

It’s like anything else, the risk-adjusted returns are great enough to justify the most probable outcome... at least in someone’s book. Not all of these companies are being built to generate cashflows, at least a few are grinding until they can be acquired by someone who has a vision for how to extract value. Big fan of LangChain, fwiw.

The projects are highly technical so if a layperson wants to use it they pay $$$ for a layperson dive into it.

Another thing I suspect is if you get major corps to use your tech then their lives depend on your team so they'll "donate". This is actually tax deductible for them.

## Product Progression

Vector databases naturally sit at a critical point in the machine learning toolchain; any company with a lot of customers there would be well positioned to expand along that toolchain with new products. In particular, we can easily imagine a future where Pinecone begins offering a model hosting service, allowing them to manage the entire vector data pipeline.

Eventually, to win, they can become a truly seamless database for storing, indexing, and serving unstructured data. Bring your data:

- **Vectorize**
- **Index**
- **Partition**
- **Store**
- **Query**

Eventually becoming an **OLAP (online analytical processing)** for unstructured data.

Every team wants to know the best way to leverage retrieval, how to chunk and embed their documents, which model they should use, how to ensure the retrieved data is relevant to the query — Chroma will answer these questions.

### Bigger Fitting

Modular and flexible framework for developing AI-native applications.

“The real power comes when you are able to combine [LLMs] with other things.”

LangChain aims to help with that by creating... a comprehensive collection of pieces you would ever want to combine... a flexible interface for combining pieces into a single comprehensive ‘chain’.

### Edge Over Others

### Pessimism

Qdrant, Weaviate—clearly didn't market as well as Pinecone. James Briggs did an amazing job and he should be hottest DevRel in the space right now! Their blogs have high recall and the `learn` series is often recommended.

## Hype Cycle and Market

The billion-dollar question is whether all this interest leads to any durable market.

The cycle to date has been something like this:

1. Models at scale have emergent behaviors that are magical and shocking.
2. Consumers experienced DALLE2, ChatGPT, and a small number of LLM products gained real traction rapidly (Copilot, Jasper, Midjourney, Character).
3. Startups have flocked to leverage these capabilities, VCs are funding them like it's 2021.
4. Many incumbent technology leadership teams are excitedly, anxiously resourcing AI projects.

Great companies can emerge from the morass of spaces like "LLMOps." But those that do will be teams that see the wedge for what it is, rather than misreading immediate momentum and interest for durable value. The distance between GitHub stars and Twitter likes and at-scale deployments and six-figure enterprise contracts is very far.

The question is not, "Do developers want LLMOps?" but instead, "Which segment of those users do I focus on? What do they really need, and in what order? What will make the product easy to adopt, and what objections will I face? What architecture will support those users, and what compounding advantages can I build?" (**** good hebbia starter email)

## Current Worry Among Every Thinking Person

Too many people are hunting for a neat strategic narrative of “which layer of the stack endures,” telling some clean story about “data moats,” or wringing their hands that large labs or incumbents are going to win the core modalities (text, code, image, etc.) — this kind of hand wringing is folly. The history of software markets is nondeterministic.

I believe the huge amount of value creation/capture out of the box for creative product folks is incredibly promising for startups. Time and effort is better spent understanding customer problems deeply, and understanding the state of the art, and leveraging the latter for the former. Who wins is based part on market structure, but also partly on who the players are, their execution, and how they redraw the software category lines.

### Intellectual Honesty Required

“Thin shims on foundation model APIs” have fallen prey to technical arrogance. Copilot became quickly essential because co figured out how to fit “passive” prediction into coding workflows in a way that made sense to developers. People building from the models/tools up (vs. from the customer back) are often unwilling to focus enough to do that last mile to make a product useful for customers. Extreme amounts of CUSTOMER FUCKING CENTRICITY and building backwards.

- Think about whether it will matter for the use case once models improve.
- Incorporate private data/customer data in the model context to improve outputs.
- Assume that incumbents in your space will at least adopt surface-level generative AI features and think about how you can go beyond those.

**Advantages of the incumbent:**

- Distribution
- Prop. Data
- Capital
- Talent

**Advantages of the startup:**

- Speed
- Focus
- Centralization of data
- Less reputational risk

Think about the right insertion point for your product and try to go deep into workflows while minimizing disruptions but bringing out the full value of AI.

## Props to Them

**Developer Marketing:** Clever move by Chroma. Marketing is the key vector for DB companies' success, particularly for Vector DBs as we are still in the hacker/experimental phase. Developers value familiarity and ease of use over technical features.

I don’t think the billions of LLM developers need to worry about scale. Chroma is moving vector infra out of data centers to the edge and your file system in an AI-first ecosystem. The reason why LangChain hackers preferred Chroma was that it was easy to use locally. Once you need to connect to an endpoint for scale, the complexity comes. There might be inability to scale...

Serving a customer's needs well—in this case usually developers and larger companies wanting to integrate AI to their systems—is often more important (and harder) to think about than defensibility. In many cases defensibility emerges over time—particularly if you build out a proprietary data set or become an ingrained workflow—which Chroma is likely to follow, or create defensibility via sales or other moats.

The less building and expansion of the product you do after launch, the more vulnerable you will be to other startups or incumbents eventually coming after and commoditizing you. Pace of execution and ongoing shipping post v1 matters a lot to building one forms of defensibility above.

Well, is DATA the new moat—building for these proprietary data sets???

Another thing to think about while servicing smaller customers on their ML Dev journey is the graduation issue—will they be too big to want to host it themselves, and can we scale alongside them (i.e., the Stripe phenomenon)?

## Enterprise Document Management

- By default, internal company documents (slides, docs, emails, messages, APIs) are not optimized for LLMs.
- Big companies will need custom solutions to organize all of their internal documents for LLMs to parse and retrieve.
- A company will emerge as “the first place for your LLMs to ingest your documents”.
- [Unstructured](https://www.unstructured.io/) might be the front runner.