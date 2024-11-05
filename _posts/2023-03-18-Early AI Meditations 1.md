# Early AI Meditations 1

## Tweet on my mind

[https://twitter.com/blader/status/1640387925912477698](https://twitter.com/blader/status/1640387925912477698)

## AI Trends I’m Interested In

- 🧠 **AI Memory** - LLMs are great reasoning engines, not great at memory. Major opportunity for players to provide infra to help with this. Likely will be verticalized
    - **Problem**
        - In-context learning works, however you need to elegantly select the right context you’d like your model to have.
        - Similarity search only goes so far. Most solutions only do top-N results. Lack of connecting ideas.
    - **Solutions today**
        - Similarity search via Pinecone, Weaviate, etc.
    - **Hypothesis**
        - Different verticals will need different knowledge graph expertise. Law vs medical vs sales vs product vs user research. Verticalized players will likely emerge
    - **Notes:**
        - **OpenAI mentions better memory on their [plugin’s next steps](https://github.com/openai/chatgpt-retrieval-plugin#future-directions)** - “Integrating more optional services, such as summarizing documents or pre-processing documents before embedding them, could enhance the plugin's functionality and quality of retrieved results. These services could be implemented using language models and integrated directly into the plugin, rather than just being available in the scripts.”
- 🏗️ **LLM Coordinators (ex: LangChain) -** Organizing, customizing and providing modularity to LLM applications
    - **Problem**
        - Developers needs ways to customize how their product consumes and instructs language models.
        - All developers run through the same friction when building apps. Prompt templating, retries, parsing output.
    - **Solution today**
        - Build your own ergonomics
        - Use a library ([LangChain](https://docs.langchain.com/docs/), [LLama Index](https://gpt-index.readthedocs.io/en/latest/index.html))
    - **Notes**
        - Libraries like LangChain make it easier to work with LMMs. It’s unclear how much OpenAI and other companies will strategically build product into the space. Ex: LangChain and LLama index are great at document loading. Developers now need to choose if they load docs through them or use an OpenAI Plugin.
    - Model swapping, finer tuned control over agents, definitely needed.
- 🌆 **Internal company APIs** - Proprietary Plugins for internal company use
    - **Notes**
        - Plugins could are a beautiful way for LLMs to chat with external facing apps. A cute and demo worth example of this is ChatGPT booking a [dinner reservation](https://openai.com/blog/chatgpt-plugins).
    - **Hypothesis**
        - My hypothesis is that companies will have an internal LLM that carries out instructions with internal facing apps and plugins.
        - While large enterprise might do this themselves to start, my hypothesis is that Mid market/SMB will outsource this to products that do it for them
    - **Example applications**
        - Some companies are so massive that it’s difficult to know what is going on around the org. It would be great if there was an LLM that was watching a feed and only alerted me of what I needed
        - Trained specifically on a company’s code base and could make recommendations
        - Could train product marketing to better articulate how code works
        - Keep up technical documentation up to date
        - This will be similar
- 🤖 **No code ways to make your own apps** - Big opportunity to empower people to make their own apps powered by AI.
    - **Problem**
        - Non-technical people have great ideas, but can’t build apps to execute them
    - **Hypothesis**
        - Low-code and no-code has already been around, but the barrier to entry is still too high. [As english becomes a programming language](https://twitter.com/ShaanVP/status/1640372877718618113) more SMB owners will build apps that have a solid use case
        - Micro-SaaS acquisition could likely heat up here. If not to purchase a company, then for start up that can execute better to run with their idea.
- 🎯 **Offshoots of Plugin Store** - ~~Apple~~ AI App Store
    - **Notes**
        - OpenAI decided to use an open API specification format, where every API provider hosts a text file on their website saying how to use their API.
        - This means even this plugin ecosystem isn’t a closed off that only a first mover controls
    - **Hypothesis**
        - Most of the infrastructure and support we see around the apple app store will likely follow the plugin store
- 🔐 **LLM Privacy** - The Signal of LLMs
    - **Notes**
        - The company to crack a private LLM (Ex: Get the reasoning power of an LLM but with complete privacy) will gain massive traction.
    - **Hypothesis**
        - This is a horizontal feature that would likely be extremely attractive to OpenAI and other providers

- Can we reduce the security threats present in the way we treat llms