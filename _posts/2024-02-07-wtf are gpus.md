---
layout: post
title: "WTF Are GPUs?"
date: 2024-02-07
tags: [business, ai]
---

*A deep dive into the GPU supply and demand bottleneck that's shaking up AI development.*

*All credit goes to Clay Pascal and the GPU Utils team for their research, analysis, and excellent article.*

---

Last week, a [fantastic article](https://gpus.llm-utils.org/nvidia-h100-gpus-supply-and-demand) dropped, exploring the wild world of GPU supply and demand. If you've got the time, I highly recommend giving it a full read. But if you're strapped for time or just want the highlights (with my own twist), stick around.

Curious about what the community thinks? Check out this [Hacker News thread](https://news.ycombinator.com/item?id=36951872) for some lively discussions.

![GPU Journey](https://images.squarespace-cdn.com/content/v1/64cc384cc6842038c1408de8/311355d4-d31b-4959-b475-3c23711c9db1/gpu-journey-large.jpg)

---

## Why Should You Care?

Let's cut to the chase: GPUs are the backbone of modern AI. They're the horsepower behind the Large Language Models (LLMs) that are revolutionizing everything from chatbots to data analysis. Without these powerful chips, we'd be stuck in the digital Stone Age.

But here's the kicker—GPUs are running out. This shortage isn't just a minor hiccup; it's a massive roadblock that's:

1. **Slowing Down Innovation**: Fewer GPUs mean slower progress in building and training new AI models.
2. **Creating Gatekeepers**: Access becomes limited to a privileged few, effectively gatekeeping AI development.

We're caught in a vicious cycle where GPU scarcity leads to hoarding, which in turn exacerbates the shortage. This is dangerous territory, pushing innovation costs sky-high and concentrating power in the hands of tech giants like the FAANG companies.

The startup scene is buzzing like never before, and while that's awesome, we need to keep our eyes on the real-world constraints. Otherwise, we risk pouring time and energy into endeavors hamstrung by hardware limitations.

---

## The GPU Supply and Demand Journey Through the Lens of ChatGPT

1. **ChatGPT Is a Hit**: Users can't get enough of it. It's probably raking in over $500 million in annual recurring revenue.
2. **Powered by GPT-4 and GPT-3.5**: These are the brains behind ChatGPT.
3. **GPUs Fuel These Models**: And they need a *ton* of them. OpenAI wants to roll out more features but is hitting a wall due to GPU shortages.
4. **Shopping for GPUs**: OpenAI buys loads of Nvidia GPUs via Microsoft Azure, specifically the Nvidia H100—the latest and greatest.
5. **Making the H100 GPUs**:
   - **Fabrication**: Nvidia uses [TSMC](https://en.wikipedia.org/wiki/TSMC) for manufacturing.
   - **Packaging**: Utilizes TSMC's CoWoS (Chip on Wafer on Substrate) tech.
   - **Memory**: Relies primarily on [SK Hynix](https://en.wikipedia.org/wiki/SK_Hynix) for HBM3 (High Bandwidth Memory).

But OpenAI isn't the only player in the game. Other companies are jumping on the AI bandwagon, eager to train their own large models. Some have legit use cases; others are riding the hype train. This surge in demand is pushing GPU prices skyward and leading to hoarding behavior.

### The Rush to Build New LLMs

1. **The Big Idea**: Companies recognize huge opportunities in AI. They want to train LLMs on their own data, either for internal use or to sell access.
2. **The GPU Quest**: They know they need GPUs—lots of them.
3. **Cloud Hopping**: They approach the big clouds (Azure, Google Cloud, AWS) but find out that getting a substantial GPU allocation is like finding a unicorn.
4. **Plan B**: They turn to other providers like [CoreWeave](https://www.coreweave.com/), [Oracle](https://www.oracle.com/cloud/compute/gpu/), [Lambda](https://lambdalabs.com/), and [FluidStack](http://fluidstack.io/). Some even consider buying GPUs outright.
5. **Acquiring the Goods**: They manage to secure GPUs one way or another.
6. **Chasing Product-Market Fit**: Now comes the hard part—making something people actually want.

The problem? Unlike OpenAI, which achieved product-market fit with smaller models before scaling up, these companies need to outdo OpenAI right off the bat. That means needing *more* GPUs from the get-go.

---

## The Demand Side: What's Fueling the Frenzy?

### Key Insights and Questions

- **Is There a GPU Shortage?**  
  Absolutely. For companies looking to snag hundreds or thousands of H100s, Azure and GCP are basically tapped out. AWS isn't far behind.

- **Who's Hoarding Thousands of GPUs?**
  - **Startups Training LLMs**: OpenAI (via Azure), Anthropic, Inflection (via Azure and CoreWeave), Mistral AI.
  - **Cloud Service Providers (CSPs)**: The big three—Azure, GCP, AWS—as well as Oracle, CoreWeave, and Lambda.
  - **Big Players**: Tesla, Jane Street, ByteDance, Tencent, and others.

- **Which GPUs Are in Demand?**  
  Mainly the Nvidia H100s. They're the fastest for both training and inference of LLMs. Specifically, the 8-GPU HGX H100 SXM servers.

- **What's the Damage ($$$)?**  
  One DGX H100 (with 8 H100 GPUs) will set you back about **$460,000**, including $100k in required support.

- **How Many GPUs Are We Talking About?**
  - **GPT-4 Training**: Likely used between 10,000 to 25,000 A100s.
  - **Meta**: Around 21,000 A100s.
  - **Tesla**: Approximately 7,000 A100s.
  - **Stability AI**: About 5,000 A100s.
  - **Falcon-40B Model**: Trained on 384 A100s.
  - **Inflection**: Used 3,500 H100s for a GPT-3.5 equivalent model; aiming for 22,000 by December.
  - **Cloud Capacities**:
    - GCP: ~25,000 H100s.
    - Azure: Probably between 10,000–40,000 H100s, mostly allocated to OpenAI.
    - CoreWeave: Around 35,000–40,000 H100s based on bookings.

- **What Are Startups Ordering?**  
  For fine-tuning: dozens to low hundreds. For full-scale training: thousands.

### Why Not Use AMD GPUs or Other AI Chips?

Great question. George Hotz (the guy who hacked the first iPhone and was briefly a Twitter intern) argues that the only way to start an AI chip company is by starting with the software. Many AI chip companies failed because they didn't develop decent frameworks for their hardware. Nvidia, on the other hand, built CUDA—a robust software stack that became the industry standard.

AMD is playing catch-up but is accelerating its efforts. Companies like MosaicML are exploring training LLMs with AMD GPUs: [Training LLMs with AMD MI250 GPUs and MosaicML](https://www.mosaicml.com/blog/amd-mi250).

### How Many H100s Do Companies Want?

- **OpenAI**: Might want around 50,000.
- **Inflection**: Wants 22,000.
- **Meta**: Possibly 25,000, maybe even 100,000+.
- **Big Clouds**: Approximately 30,000 each for Azure, GCP, AWS, and Oracle.
- **Private Clouds**: Lambda, CoreWeave, and others might want a combined 100,000.
- **Other Startups**: Anthropic, Helsing, Mistral, Character.ai might want around 10,000 each.

Totaling that up gets us to about **432,000 H100s**. At roughly $35,000 a pop, we're talking about **$15 billion** worth of GPUs. And that doesn't even include Chinese giants like ByteDance, Baidu, and Tencent, who will want plenty of H800s (the Chinese-market version of the H100).

Financial firms like Jane Street, JP Morgan, Two Sigma, and Citadel are also entering the fray, deploying anywhere from hundreds to thousands of GPUs.

---

## The Supply Side: Why Can't We Just Make More GPUs?

### Key Insights and Questions

- **Can Nvidia Use Other Manufacturers Besides TSMC?**  
  Not in the short term. They've partnered with Samsung in the past, but for H100s, it's TSMC or bust. Future collaborations with Intel or Samsung might happen, but they won't solve today's shortages.

- **How Long Does Production Take?**  
  Roughly **six months** from the start of production to a ready-to-ship H100.

- **Who's Making the Memory?**  
  Nvidia primarily uses HBM3 memory from SK Hynix. Samsung might be in the mix, but Micron is likely not a player for H100s.

- **What Other Components Are Bottlenecks?**  
  - **Metals**: Copper, Tantalum, Gold, Aluminum, Nickel, Tin, Indium, Palladium.
  - **Silicon**: The cornerstone of semiconductors.
  - **PCBs**: The backbone that holds all components together.

- **Who Sells H100s?**
  - **OEMs**: Dell, HPE, Lenovo, Supermicro, and Quanta.
  - **GPU Clouds**: CoreWeave and Lambda buy from OEMs and rent to startups.
  - **Hyperscalers**: Azure, GCP, AWS, and Oracle work more directly with Nvidia but still involve OEMs.

- **Build or Colocate?**  
  Building your own datacenter is time-consuming, expensive, and requires specialized expertise. Most opt for colocation to get up and running faster.

- **How Do the Big Clouds Stack Up?**
  - **Oracle**: Less reliable infrastructure but offers more hands-on support.
  - **Networking Differences**: AWS and GCP have been slower to adopt InfiniBand, which is crucial for high-performance computing.
  - **Availability**: Azure's H100s are mostly dedicated to OpenAI; GCP is struggling to get H100s.

- **Nvidia's Allocation Preferences**  
  Nvidia seems to prefer not to give large allocations to companies developing competing chips (like AWS Inferentia and Tranium, Google TPUs, or Azure's Project Athena).

- **Who Uses Which Cloud?**
  - **OpenAI**: Azure.
  - **Inflection**: Azure and CoreWeave.
  - **Anthropic**: AWS and GCP.
  - **Cohere**: AWS and GCP.
  - **Hugging Face**: AWS.
  - **Stability AI**: CoreWeave and AWS.
  - **Character.ai**: GCP.
  - **X.ai**: Oracle.
  - **Nvidia**: Azure.

---

## So, How Do You Get More GPUs?

The ultimate gatekeeper is Nvidia. They control the allocations, and they care *a lot* about who the end customer is. Cloud providers might score extra units if Nvidia likes the customer—preferably well-known brands or startups with solid reputations.

Nvidia is less inclined to help out companies directly competing with them in the AI chip arena. But if you show them the money—commit to a big deal, have a low-risk profile—you might just get a bigger slice of the pie.

---

## The Road Ahead

The GPU shortage is real and isn't going away anytime soon—likely persisting through the rest of 2023. This scarcity is shaping the AI landscape in significant ways, potentially consolidating power among the giants and making it harder for newcomers to break in.

If you're as fascinated by this unfolding saga as I am and want more in-depth analysis, consider [signing up to get notified](https://airtable.com/shr411VWRbl9og1xb) about LLM Utils' new posts.

---

Stay tuned, stay savvy, and let's navigate this wild GPU ride together.