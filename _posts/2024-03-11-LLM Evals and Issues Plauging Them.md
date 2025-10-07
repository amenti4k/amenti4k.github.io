---
layout: post
title: "LLM Evals and Issues Plauging Them"
date: 2024-03-11
categories: []
tags: [ai]
---

# Challenges in evaluating AI systems / Anthropic

Get Joe Sispak’s thoughts  
The “Moody’s” of AI: new tech providing an unbiased evaluation of new generative AI models  
Patronus AI Creates an LLM Evaluation Tool for Regulated Industries

Talk to [https://www.linkedin.com/in/tbehailu/](https://www.linkedin.com/in/tbehailu/) about Patronus and Arize before having an in-person conversation with Patronus.  
Make sure you get the intro from Gelila first and explain your thought process  
Dive deep into everything and ask the real nitty gritty questions

- Automated evaluation platform for LLMs
- Evaluation run to measure model performance
- Adversarial testing sets made to break models
- Generate new adversarial test sets
- Benchmarking performance to other models

Checking if they break in the real world scenario towards regulated industries where there is little tolerance for errors.  
“a trusted third party when it comes to evaluating models.”

**Rigorous Evaluation**

**Score + Test + Benchmark**

---

**What are my thoughts on the issue being solved:**

LLMs are nondeterministic — they’re not guaranteed to produce the same output every time for the same input.  
That means that companies will need to do more rigorous testing to make sure they’re operating correctly, not going off-topic, and providing reliable results.  
Generate adversarial test cases, monitor hallucinations, and detect PII and other unexpected and unsafe behavior. Customers use Patronus AI to detect LLM mistakes at scale and deploy AI products safely and confidently.  
LLMs in current form won’t generate any revenue. Enterprises need much more tech & domain training to align to business.  
Good thing from our enterprise clients that they are willing to pay for solution as long as it aligns to business goals  
Sideways – test normal modes  
High-priority harm areas: self-harm, physical harm, illegal items, fraud, and child abuse.

**Questions**

- What are traditional methods of testing
  - Academic benchmarks
  - Human evaluations
- Why would someone use us instead of public datasets?

There’s obviously a clear problem that needs fixing but I worry that it’s a hyper-competitive space. I’d love to hear about how they’re trying to make themselves distinct by directly working with observable surfaces (Mongo/Hugging Face…).  
I was looking at Arize and others that seemed slightly more advanced but playing directly on the same field.

From what I can tell, they’re relying on the fact that LLMs are nondeterministic — they’re not guaranteed to produce the same output every time for the same input. That means that companies will need to do more rigorous testing to make sure they’re operating correctly, not going off-topic, and providing reliable results. Basically Score + Test + Benchmark… Good thing is they’re targeting enterprise clients that are willing to pay for a solution as long as it aligns to business goals. Eventually become “a trusted third party when it comes to evaluating models.” There’s obviously a clear problem that needs fixing but I worry that it’s a hyper-competitive space. I’d love to hear about how they’re trying to make themselves distinct by directly working with observable surfaces (Mongo/Hugging Face…). I was looking at Arize and others that seemed slightly more advanced but playing directly on the same field. What Patronus seems to be building is the key features in a stack of a bunch of different processes that are required from a company starting to prep data to getting the final results. Obv it’s too early, and I'm in no authority, but I’d assume most of this would be done in one platform that can plug and play different things and the platforms that facilitate that (similar to how you can plug and play with the base models themselves) will eventually build out an evaluation tool. And if there’s a better evaluator, it becomes a plug that can be added more than its own platform. Whether they even plan on moving to the entire space of monitor, finetune, observe, test, evaluate or just master the evaluate section and eventually be an option for the evaluation as they’re the best… (I’d also assume the best plug-and-play evaluators would become super niche industry specific) Nonetheless I would love to hear from him and am interested in talking about the position you mentioned and getting to learn more about how they’re trying to position themselves.

---

## Evals & Leaderboards - what’s ultimately the goal?

**What is the goal for evaluation and leaderboards?**

Starting from goals for the outcomes we’re seeing to have a nuanced overview.  
There are a number of ways to evaluate a model (coding, reasoning, etc.) but the line of sight from something like MMLU or Hellaswag to what the downstream consumer (i.e., the developer) wants in terms of application performance is unclear and certainly non-linear.  
Having evals that accurately represent success in the application environment gives model developers something to shoot for—and god knows, when we get a good benchmark to optimize toward, we as a community go nuts!!

Moreover, while it’s still very early, there are signs that we can more confidently start from desired capabilities and adjust the data mixture at various stages of the model development process to align our models more toward how we want them to behave in the eventual application. Whether we need to go all the way back to pre-training is still a good question but we certainly know we can do a lot at the CPT and SFT stages to get models to behave in our desired ways (e.g., speak languages other than English).

**Back to goals - what are the goals of evals and leaderboards?**

The answer is clearly dependent on who you ask. It can be a combination of wanting to find the best model across performance, type (i.e., base, chat, multimodal, different languages, etc.), latency, and cost—or certainly a local optima across all of them depending on who the developer is and what his or her application goal is, level of sophistication, desired level of customization, etc.

As a model developer (or at least one that likes to play with the models out there) I tend to use Helm or OpenLLMLeaderboard, sort on the provided metrics, see which models rise to the top and which can fit onto a Colab instance so I can just quickly load something up and hack a prototype. My job to be done (JTBD) or goal is pretty straightforward. But for many others, not so much.

Let’s walk through some of the leaderboards, some old some new, and what a goal could be for each. Note this is not exhaustive and is a curated set of leaderboards from the articles I read with my personal perspective on each.

---

### (1) Open LLM Leaderboard or HELM

**Maintainer:** Hugging Face & Stanford respectively

**Summary:**  
A sortable set of models, open and closed, evaluated on mostly academic benchmarks. Covers core scenarios such as Q&A, MMLU (Massive Multitask Language Understanding), MATH, GSM8K (Grade School Math), LegalBench, MedQA, WMT 2014 along with other benchmarks. These are largely open-source evals that have been developed over the years by various researchers.

**Developer goal:**  
General AI developers looking for models to build on will come here first, understand per a given size which models perform the best, and then leverage the result for their research, an application, fine-tune for a custom application. One thing that’s clear, however, is that there is a stage of disillusionment that the community is in when it comes to **actual** performance of models and how each rank on academic evals. This has driven the development of other leaderboards such as Chatbot Arena (see later).

---

### (2) Hallucinations Leaderboard

**Maintainer:** Hugging Face

**Summary:**  
It evaluates the propensity for hallucination in LLMs across a diverse array of tasks, including Closed-book Open-domain QA, Summarization, Reading Comprehension, Instruction Following, Fact-Checking, Hallucination Detection, and Self-Consistency. The evaluation encompasses a wide range of datasets offering a comprehensive assessment of each model's performance in generating accurate and contextually relevant content.

**Developer goal:**  
Have a starting point to understand which models hallucinate the least. There is some overlap with other available leaderboards here and, given without RAG or search integrated, these models will **always** hallucinate; this leaderboard is less interesting for developers.

---

### (3) Chatbot Arena / LMSys

**Maintainer:** Together AI, UC-Berkeley, Stanford, and several others.

**Summary:**  
A benchmark platform for large language models (LLMs) that features anonymous, randomized battles in a crowdsourced manner. Some, like Karpathy, find it to be the best test of a model’s performance as the arena is much more dynamic and compares models head to head.

**Developer goal:**  
Understand how models will perform in a **real** environment that challenges in ways that standard datasets/prompts can’t. Like #1 above, this may influence the developer's starting point for further work.

---

### (4) The MTEB leaderboard

**Maintainer:** Hugging Face & Cohere

**Summary:**  
MTEB or “Massive Text Embedding Benchmark” contains 8 embedding tasks covering a total of 58 datasets and 112 languages. Through the benchmarking of 33 models on MTEB, establish the most comprehensive benchmark of text embeddings to date.

**Developer goal:**  
Understand which models could perform best in applications where retrieval augmented generation (RAG) is used.

---

### (5) Artificial Analysis

**Maintainer:** Independent / Startup

**Summary:**  
Artificial Analysis provides benchmarks & information to support developers, customers, researchers, and other users of AI models to make informed decisions in choosing which AI model to use for a given task, and which hosting provider to use to access the model.

**Developer goal:**  
Understand cost, quality, and speed trade-offs across models and model providers (e.g., OpenAI, Microsoft Azure, Together.ai, Mistral, Google, Anthropic, Amazon Bedrock, Perplexity, Fireworks, Lepton, and Deepinfra).

---

### (6) Martian’s Provider Leaderboard

**Maintainer:** Martian (startup)

**Summary:**  
Martian's provider leaderboard collects metrics daily and tracks them over time to evaluate the performance of LLM inference providers on common LLMs.

**Developer goal:**  
Understand quickly cost vs. rate limits vs. throughput for a variety of LLM providers and optimize for his or her application.

---

### (7) Enterprise Scenarios Leaderboard

**Maintainer:** Patronus, Hugging Face

**Summary:**  
Enterprise Scenarios leaderboard evaluates the performance of language models on real-world enterprise use cases (at present 6 benchmarks - Finance, Legal, etc.).  
- FinanceBench (accuracy not retrieval)
- Legal Confidentiality (reason over legal cases)
- Writing Prompts (engagingness)
- Customer Support Dialogue (relevance)
- Toxic Prompts (generation)
- Enterprise PII (business-sensitive info generation)

**Developer goal:**  
This leaderboard is still very much nascent as you can see from the lack of public models competing. Overall, though, this set of evals would provide developers with an idea of which base models to use as a starting point for a given task. Again, very, very early.

---

### (8) ToolBench

**Maintainer:** SambaNova Systems

**Summary:**  
A tool manipulation benchmark consisting of diverse software tools for real-world tasks.

**Developer goal:**  
Illustrate which available models perform best for action generation as described in natural language. Note it seems like this project is also a great resource for broader developers for how to implement a particular tool usage (i.e., plug-in) for their model.

---

**Key takeaways:**

We are in that stage of the market where it’s an absolute gold rush—if an entity controls the underlying benchmark, this can influence the direction of the market. This is why startups that are dependent on performance/LLM efficiency are pushing on their own benchmarks. If these benchmarks take hold, it will force competitors to follow.

We are absolutely in the early innings and nothing has been decided. If you can dream of a use case or requirement, you could probably define an eval and leaderboard.

Right now Meta is a passive player and, beyond the CybersecEval we released late last year, **just** leverages the currently available evals and leaderboards.

Lastly, as Alan Kay the PARC researcher said, “The best way to predict the future is to invent it...” - we are now on the path to AGI and it’s time for **us** to define the future. Buckle up!!

Cheers!

---

**How do you evaluate models (coding, reasoning, etc.)**

MMLU or Hellaswag to downstream consumer (i.e., the developer) wants in terms of application performance.  
You can just look at the provided metrics, see which models rank higher, and use the one that goes into your code easily to prototype something. E.g.:

- Holistic Evaluation of Language Models (HELM)
- Open LLM Leaderboard - a Hugging Face Space by HuggingFaceH4

---

**What’s the true need of evaluations?**

Evals are the new PRD?

1. Find the best model across performance types (chat, multimodal, switching languages, etc.)
2. Finding the optimal range for latency and cost
3. Comparing levels of sophistication or customization levels

Having evals that accurately represent success in the application environment gives model developers something to shoot for. When we get a good benchmark to optimize toward, without a really strong POV on where we want to be going, it is impossible to get there.

Outside of the common ones like cost, safety, quality [case evals], and latency.

An important one of those challenges relates to how we can reasonably evaluate the capabilities of these apparently highly-skilled models. How do we quantify what they can and cannot do? How can we measure how biased they are, or what is the risk they will express toxic or harmful language? And what are useful automatic signals that can be used to improve them even further?

We can work backwards from desired capabilities and adjust the data mixture at various stages of the model development process to align our models towards how we want them to behave in the eventual application.

Do we even need to go all the way back to pre-training or not is a different question, but we know that there’s a lot we can do even at the CPT and SFT stages to make our models behave in our desired ways (change languages, etc.)

IMO, eval is the largest challenge we face. If we can't show that the models are working/achieving our goals for them, what are we even doing? The crux of the issue is that it's a challenging thing to scope out what a "general purpose" system ought to be able to do.

---

**Learnings from Current Instances (which are listed in detail below)**

- If an entity controls the underlying benchmark, this can influence the direction of the market. Every startup whose product is dependent on performance/LLM efficiency is pushing on its own benchmarks. Once a benchmark becomes the norm, competitors are forced to follow. Thus it’s a gold rush to control the underlying benchmark.
- The best way to predict the future is to invent it…

It’s very early and nothing has been decided. So if you can see a desired capability or requirement, you can define an evaluation and leaderboard.

Every LLM org is going to have to define their version of AGI and build the evals towards that. E.g., OAI is biased towards a single agent, Google is benching on “search” for general intelligence.

Evaluating a model taken to an extreme limit is as complex as coming up with an intelligent model. Back in the days (lol) we got away with easier evals because the dimensionality and decision of taste were very tractable and were often deterministic.

With the incredible advances in foundation models to conduct a wide range of tasks, it becomes more and more challenging to evaluate them and understand their limitations: if a model could potentially execute infinitely many tasks, it is impossible to do a proper evaluation of all the tasks it could do.

Evaluations are subject to human preferences which vary in small populations. So the more models we have, differentiation is preference on human evaluation preferences.

Maybe the head-to-head Chatbot Arena might work to mitigate that, but it can be bottlenecked by the number of people that vote.

Plus head-to-head battles won’t pinpoint to the source of difference in scores.

---

**Who are the stakeholders in AI Evaluations?**

- **Productionisers:** People making models for a purpose that want to make sure it performs robustly, safely, and responsibly.
  - Hard to do automatically as it's a higher skill level focused. Human evaluations are used and are expensive.
  - For productionisers, it is less relevant to score well on benchmarks that test specific skills in isolation, or in a context different from the one the model will be deployed in.
- **Researchers:** The opposite of what I said for productionisers.

---

**Dimensions in Choosing Evals**

- **Generation vs Ranking**
  - Multiple choice (ranking or classification tasks) or direct evaluation of generated text (free-form).
  - Ranking can be multiple choice, yes/no, etc.
  - Can be automatic and cheap and useful in model development to run continuously during iterations.
  - Disadvantage is resemblance of scenario being modeled, but not the exact scenario; plus data contamination of the evaluations being part of the training data.
  - Direct open-ended evaluations are harder to do automatically… especially for non-deterministic answers. Human evaluation is the gold standard and suffers from poor replicability and disagreement around criteria and measurement and quality judgment from workers.

---

**Prompt Handling**

- The variation of the prompt used can lead to the models giving out varied outcomes from the slightest arbitrary choices. E.g., choice of wording, number of prompts, and the way prompts are formulated and formatted.
- Maybe looking through the best-case scenarios before computing evals to choose prompts that models respond well towards.
- Prompt engineering for evals depends on the stakeholders and situations. For builders, re-engineering the prompt to choose the best performer can lead to seeing the upper-bound of the performance task and potentially re-routing similar prompts to the best performing one. However, for performance researchers aiming to achieve AGI, prompt engineering scores are less informative as variations show how far off we are from corrective intelligence.
- Also, if a model responds unexpectedly to prompt-format changes in a relatively simple ranking test, what does that imply for the reliability of scores on tests for bias or toxicity?

---

**Handling Outputs**

- Especially to ranking ones. It’s going to become increasingly easy to assign higher eval scores to models that are eval-instruction-tuned. So a simple yes/no might not be the move… Maybe looking at the assigned probabilities to each option (either in its decision or by passing the prompt multiple times and seeing the probability of choice for each option) could be useful.

---

**Data Contamination**

- Relationship between training and evaluation data.
- If you’re an AGI researcher, this is a no-go. Testing on stuff the model might have already seen counteracts the test and is not indicative of hyper-generalization and pattern matching.
- There was a reported score of accuracy of GPT-4 on HellaSwag evals that found 36% of reasoning questions were wrong, mislabeled, or incomprehensible examples. HellaSwag or HellaBad? 36% of this popular LLM benchmark contains errors that show the model arrived at the same incorrect outputs is no proof. So, maybe this is at least a strong indication that it may have arrived at those answers by memorizing its training set at least to some extent. Unless one is fairly certain that particular forms of generalization are not needed—i.e., the model will simply not encounter scenarios not covered directly by the training data frequently enough for it to matter—it may be wise to get an estimate of the extent to which high scores are driven by data contamination. It may seem unlikely a model has encountered a particular input before, but the internet is big, and searching it is hard.
- How much overlap between a training and evaluation example should there be for it to count as ‘contaminated’? There are no easy solutions to these problems; approaches could include burning parts of common evaluation… However, to even get close to start addressing this insane issue requires access to training data, which are in many cases not accessible to people outside of the ones that trained the models in question.

---

**Responsible LLMs**

Even completely ignoring the potential consequences for humans and society, mistakes uttered by LLMs can have a direct impact on the viability of the product as well as the company itself.

Despite the importance of this topic, broadly evaluating accuracy, fairness, toxicity, factuality, and related topics remains incredibly difficult, both from a practical and philosophical perspective. The stakes of addressing it properly, however, are high, both for society and for model deployers directly: neglecting to properly evaluate these kinds of things can have a lot of inadvertent consequences for regulations, potentially making it impossible for the company to deploy similar models in their products.

---

**Questions**

- How far can automatic evals get us?
- Human evals are expensive.
- Are there ways to automatically evaluate higher-level skills?
- Data contamination
  - How should that be measured?
  - What is the impact of memorization on benchmarks?

---

### (1) Open LLM Leaderboard or HELM

**Maintainer:** Hugging Face & Stanford respectively

**Summary:**  
A sortable set of models, open and closed, evaluated on mostly academic benchmarks. Covers core scenarios such as Q&A, MMLU, MATH, GSM8K, LegalBench, MedQA, WMT 2014 along with other benchmarks. Largely open-source evals that have been developed over the years by various researchers. It encourages leaderboard hacking and faster saturation of academic benchmarks and wasn’t well thought through.

**Developer goal:**  
General AI developers looking for models to build on will come here first, understand per a given size which models perform the best, and then leverage the result for their research, an application, fine-tune for a custom application. One thing that’s clear, however, is that there is a stage of disillusionment that the community is in when it comes to **actual** performance of models and how each rank on academic evals. This has driven the development of other leaderboards such as Chatbot Arena (see later).

---

### (2) Hallucinations Leaderboard

**Maintainer:** Hugging Face

**Summary:**  
It evaluates the propensity for hallucination in LLMs across a diverse array of tasks, including Closed-book Open-domain QA, Summarization, Reading Comprehension, Instruction Following, Fact-Checking, Hallucination Detection, and Self-Consistency. The evaluation encompasses a wide range of datasets offering a comprehensive assessment of each model's performance in generating accurate and contextually relevant content.

**Developer goal:**  
Have a starting point to understand which models hallucinate the least. There is some overlap with other available leaderboards here and, given without RAG or search integrated, these models will **always** hallucinate; this leaderboard is less interesting for developers.

---

### (3) Chatbot Arena / LMSys

**Maintainer:** Together AI, UC-Berkeley, Stanford, and several others.

**Summary:**  
A benchmark platform for large language models (LLMs) that features anonymous, randomized battles in a crowdsourced manner. Reliable in telling you which model is better, but can’t get into the details of specific capabilities (e.g., Gemini vs. GPT-4, where Gemini had internet access and caused confusion).

**Developer goal:**  
Understand how models will perform in a **real** environment that challenges in ways that standard datasets/prompts can’t. Like #1 above, this may influence the developer's starting point for further work.

---

### (4) The MTEB leaderboard

**Maintainer:** Hugging Face & Cohere

**Summary:**  
MTEB or “Massive Text Embedding Benchmark” contains 8 embedding tasks covering a total of 58 datasets and 112 languages. Through the benchmarking of 33 models on MTEB, establish the most comprehensive benchmark of text embeddings to date.

**Developer goal:**  
Understand which models could perform best in applications where retrieval augmented generation (RAG) is used.

---

### (5) Artificial Analysis

**Maintainer:** Independent / Startup

**Summary:**  
Artificial Analysis provides benchmarks & information to support developers, customers, researchers, and other users of AI models to make informed decisions in choosing which AI model to use for a given task, and which hosting provider to use to access the model.

**Developer goal:**  
Understand cost, quality, and speed trade-offs across models and model providers.

---

### (6) Martian’s Provider Leaderboard

**Maintainer:** Martian (startup)

**Summary:**  
Martian's provider leaderboard collects metrics daily and tracks them over time to evaluate the performance of LLM inference providers on common LLMs.

**Developer goal:**  
Understand quickly cost vs. rate limits vs. throughput for a variety of LLM providers and optimize for his or her application.

---

### (7) Enterprise Scenarios Leaderboard

**Maintainer:** Patronus, Hugging Face

**Summary:**  
Enterprise Scenarios leaderboard evaluates the performance of language models on real-world enterprise use cases (at present 6 benchmarks - Finance, Legal, etc.):  
- FinanceBench (accuracy not retrieval)
- Legal Confidentiality (reason over legal cases)
- Writing Prompts (engagingness)
- Customer Support Dialogue (relevance)
- Toxic Prompts (generation)
- Enterprise PII (business-sensitive info generation)

**Developer goal:**  
This leaderboard is still very much nascent as you can see from the lack of public models competing. Overall, though, this set of evals would provide developers with an idea of which base models to use as a starting point for a given task.

---

**SANDBOX FOR DIFFERENT EVALUATORS AND SEE WHICH PERFORMANCE WHERE… SORT OF META EVALUATOR BY EVALUATING THE EVALUATION EVALUATORS**

[https://artificialanalysis.ai/](https://artificialanalysis.ai/)

---

**Unrelated to Patronus, but mainly Hebbia:**

Knowing the prompt sensitivity of models could be valuable information for model deployers. Furthermore, differences in the way that prompts are selected make it impossible to compare performance for different models: is model A better than model B because it is better at the task, or did the developers of model A simply consider more prompts in their search?

Whatever prompting scenario is used, it is extremely important that prompt-selection efforts as well as prompts themselves are well-documented. Not doing so is not only harmful for reproducibility—in the process wasting the time of countless scientists that need to back-engineer the prompts with which reported scores were obtained—but also limits researchers to better understand what models are capable of.

**Evaluating Outcomes**

Similar to prompt engineering, using extracted, calibrated probabilities rather than generated text may be more informative about the upper-bound of what models can do than about what a model would actually do in practice, and it is interesting to consider the implications of that for the different stakeholders. For reasons analogous to the ones presented for prompt engineering, using calibrated log-probs may be an apt evaluation method for performance researchers: it gives a quick indication of what kind of knowledge the model actually contains and therefore constitutes an indicator of progress. For productionisers, however, it may be more appropriate to focus on generated output. While several preprocessing options may be conceived to address the variability that occurs as a consequence of prompting, the fact that a model has the correct answer somewhere in its probabilities is not particularly useful for a model deployer if there is no way to extract that from the model without knowing the answer in advance. As such, comparing the probabilities of answer A, B, and C instead of checking if a model actually generates A, B, or C may further distance the evaluation scenario and the scenario in which a model will be deployed. For an AGI researcher, using log-prob evaluations will evidently not suffice either: if a model in a multiple-choice task assigns a higher probability to option A than to option B, but it generates the letter D, an AGI researcher would likely argue that the model did not even really understand the task it had to do. Similarly, in many cases, normalizing probabilities may counteract the very idea by which in particular NLI tasks were constructed: predicting the relationship between two sentences independently of how likely the sentences themselves are is a crucial part of such tasks. In sum, focusing evaluation directly on generated model output might thus be a more suitable option, even if that results in lower scores.

---

Also from the Gemini 1.5 paper, the request for multimodal evaluations that perform well for long context evaluation was interesting.

**Patronus Current evals fail with:** Existing evaluations are increasingly strained by the new and rapidly advancing capabilities of large multimodal models. They typically focus on individual modalities and/or are restricted to tasks with shorter context lengths. Hence, there is a growing need for benchmarks which exemplify the nuanced requirements of real-world long mixed-modality use cases.

**Qualitative long-context multimodal evaluations:** Manually probe and stress-test the model’s long-context abilities, especially for novel capabilities where no quantitative benchmarks exist.

Especially relevant with their long-context evaluation call to action:

> Thus, given the limitations of existing benchmarks and the challenges of human annotation, there is a pressing need for innovative evaluation methodologies. These methodologies should be able to effectively assess model performance on very long-context tasks while minimizing the burden of human labeling. To begin addressing some of these concerns, we recommend researchers and practitioners adopt a “multiple needles-in-haystack” setup for diagnostic evaluations which we observed to be signal-rich and more challenging compared to its “single needle” counterpart. We believe there is room for new benchmark tasks based on new or improved automatic metrics that require complex reasoning over long inputs (both human and model generated). This is also an intriguing research direction for creating challenging evaluations that stress more than just the retrieval capabilities of long-context models. We will be continuing the development of such benchmarks for realistic and comprehensive evaluation of model capabilities in the multimodal space. By addressing these open challenges and developing new benchmarks and evaluation methodologies, we can drive progress in the field of very long-context AI models and unlock their full potential.