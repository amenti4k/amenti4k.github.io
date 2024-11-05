---
layout: post
title: "Early AI Meditations 2"
date: 2023-11-24
tags: [ai]
---

## Tweet on my mind

[https://twitter.com/karpathy/status/1642607620673634304](https://twitter.com/karpathy/status/1642607620673634304)

## AI Trends I’m Interested In

- **Managed Retrieval Engines**
    - **Problem**
        - Semantic search gets you 90% of the way there for easy questions & answers, but only 30-40% for hard Q&A
        - The hard part is understanding *which documents* are relevant to the query you give to the LLM
    - **Why this is interesting to me**
        - I see two routes document retrieval could go
            - **Route #1 (Horizontal Retrieval):** One general engine is really good at document retrieval across industries and domains (Law, Medical, Real Estate, etc.). It has a reasoning engine that tells it where to look
            - **Route #2 (Verticalized Retrieval):** Specialized retrieval engines are needed who are experts at traversing law documents which are different than medical, real estate, etc.
        - I’m unsure which way it will go! I’m currently leaning towards #2
    - **Notes**
        - [Metal](https://getmetal.io/) (Managed Retrieval) just announced an [integration with LangChain](https://twitter.com/AI_Sensei_/status/1643632143845736448)
        - This topic likely deserves it’s own essay in the future. Here’s the TLDR of that essay already:
            - Full-stack retrieval goes like this:
                1. You have a raw corpus of documents (Held in the cloud)
                2. You split them into semanticly meaningful chunks (With LangChain or other text splitters)
                3. You convert them into some vector representation for easy comparison and searching (Using [OpenAI’s embeddings](https://platform.openai.com/docs/guides/embeddings)) 
                4. You store those vectors (using [Pinecone](https://www.pinecone.io/) or [Weaviate](https://weaviate.io/))
                5. You retrieve certain documents based on the task at hand (Metal?)
            - I’m unsure how much of that stack a [Pinecone.io](http://Pinecone.io) is going to want to take vs a company like Metal.
    - **Hypothesis**
        - The winner of this space will go full-stack and take over more document management / retrieval workflows
- **Developer Monetization with OpenAI Plugins**
    - **Problem**
        - In a market place you need adoption incentives on both sides to drive overall health. Without monetization for the plugin supply side (developers) it’s hard to get the demand
        - OpenAI has [100M+ users](https://www.reuters.com/technology/chatgpt-sets-record-fastest-growing-user-base-analyst-note-2023-02-01/), now they need to incentivize developers to build & maintain plugins
    - **Hypothesis**
        - There *might* be a use case for micro-transactions (very hesitant to use that word) for plugin use that happens through OpenAI
        - LLM Plugin access will become a standard feature line on pricing tiers for virtually every company. Starting at the top (enterprise/mid-market) and working it’s way down to SMBs as more SMB-friendly tools get built
    - **Notes:**
        - I shutter at the words ‘micro-transactions’ because with all the talk over the past few years we have yet to see them happen in a material way
        - Plugin [user level auth](https://platform.openai.com/docs/plugins/authentication) will make this seamless
- **Plugin Translators Dev Shops**
    - **Problem**
        - Businesses will want their services to be accessible to LLMs, but they won’t all have the skills required to create, maintain, and develop plugins
    - **Hypothesis**
        - There will be shops that specialize in creating and maintaining plugins for companies. A small dev shop could likely ‘translate’ thousands of APIs at a time
        - Monetization incentives (above) will drive this
        - PSO (Plugin Store Optimization) will evolve out of too much supply
    - **Notes**
        - An early look at what this world will look like:
        
        [https://twitter.com/matchaman11/status/1641502642219388928](https://twitter.com/matchaman11/status/1641502642219388928)
        
- **Unstructured Data > Structured**
    - **Problem**
        - Insights and data are valuable to businesses, but only when you have access to a source that the general market doesn’t. The harder a valuable piece of data is to grab, the more attractive it is
        - Many valuable pieces of data sit within unstructured text-based sources. It’s notoriously tedious and difficult to extract insights from them
            - Ex: Public filings, public records PDF, transcriptions
    - **Hypothesis**
        - There will be an addition to the data-service industry (like [CBInsights](https://www.cbinsights.com/)) enabled by LLMs. BUT you won’t hear about it because suppliers know that their data’s value is derived from it’s scarcity. It’s not in their best interests to tell you how it’s gathered
    - **Examples**
        - **Tech Extraction from Job Descriptions**
            - Sales teams often use job descriptions to parse which technologies or tools a company is using. This is usually a manual process. It’s like [BuiltWith](https://builtwith.com/) but for job descriptions. With LLMs it’s easy to parse JDs to get this information.
            - (Disclosure: I built this)
                
                [https://twitter.com/GregKamradt/status/1643027796850253824](https://twitter.com/GregKamradt/status/1643027796850253824)
                
        - **Community Moderation & Analytics (Discord/Slack/Support)**
            - **Analytics:** You have better ways to classify and report on conversations & requests in your community. Businesses would 100% pay for this if you give recommendations on how to increase health.
            - **Moderation**: Users post questions to the wrong channel. It would be nice to clean those up by going through them, classifying them, and moving them. Or stopping users from posting them all together
- **Reflection**
    - **Problem**
        - LLMs are good, but not always on their first draft of a response
    - **Solution**
        - It’s super easy to ask them, “are you sure?” and get a better answer back. It’s been [statistically proven](https://arxiv.org/abs/2107.03374) to increase quality of answers over a varying level of benchmarks
    - **Notes**
        - Unfortunately reflection increases costs and latency since you’re making another API call. This isn’t a problem for all use cases, but users can be time-insensitive.
    - **Resource: Great Video on the topic**
        
        [https://www.youtube.com/watch?v=5SgJKZLBrmg](https://www.youtube.com/watch?v=5SgJKZLBrmg)
        
- **Drag & Drop LLM/Chain Builders**
    - **Problem**
        - Not everyone is technical. Even if you are, it’s sometimes easier to drag and drop rectangles on a screen than write code
    - **Opportunity**
        - Create no code tools that string together LLM calls
        - Basically no-code [LangChain](https://langchain.readthedocs.io/)
    - **Notes**
        - Examples: [LangFlow](https://github.com/logspace-ai/langflow)
    - **Hypothesis**
        - I don’t think this will be as big as it may seem. Simple no-code use cases are easier (aka Zapier), but going deep requires technical ability (aka Bubble/webflow)
        - Opinion: It’s interesting eye-candy but I wouldn’t recommend investing here
- **Elad Gil: Species Level Take Over - [Link](https://blog.eladgil.com/p/ai-safety-technology-vs-species-threats)**
    - **Notes**
        - This is just thought-candy, but I thought Elad had an interesting framework to think about different tiers
        - “For AI to move from **merely another technology risk** (in the long line of tech risks we have survived and benefited from on net) to a potentially **existential species-level risk** (all humans can die from this), up to two technological breakthroughs need to happen (and (2) below - robotics, may be sufficient):”
            1. The AI needs to start coding itself and evolve: tool → digital life transition.
            2. Robotics need to advance: Digital→real world of atoms transition.
        - Species Level Competition
    
    ![Untitled](Early%20AI%20Meditations%202%2014f602f116e94c2488507a25296ecd62/Untitled.png)