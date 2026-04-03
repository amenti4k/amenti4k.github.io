---
layout: post
title: "How I'm Thinking About Percepta"
date: 2026-04-03
tags: [business, ai]
hidden: true
permalink: /percepta/
---

*Healthcare lens throughout, but most of this generalizes.*

## Three premises I'm treating as given

- **PR1:** Models will keep getting better and the improvement is compounding. Scaling laws have delivered since 2012, and now models are being used to improve the training of the next generation, so the curve feeds on itself. <span class="marginnote">METR task duration doubles every 4 months.</span> The thing that's hard to internalize: plan for a world where the model is meaningfully better in 12 months and dramatically better in 24.

- **PR2:** People and organizations will defer more and more decisions to models. Already happening in consumer (search, writing, coding), beginning in enterprise. The trend is one-directional. As models get more capable the surface area of delegation expands. The bottleneck shifts from "can the model do this" to "can the organization hand this off." That handoff is the hard part.

- **PR3:** Two problems stay hard and get harder as models improve — these are the durable seams:

  - **Observability.** When an agent takes an action you need to know what it did, why, and whether the outcome was correct. UI/UX for making agent behavior legible to humans. Plotting multi-agent trajectories when the state space explodes. This problem gets worse with capability. More powerful models take more actions across more domains, which means more to watch. <span class="marginnote">The verification inversion: checking the work gets harder as the worker gets smarter.</span>

  - **Verifiability conversion.** Most of what organizations do is not structured in a way an AI can execute and a human can verify the result. The work is messy, implicit, embedded in human judgment and social context. The core question: <span class="question-text">how do you take a process that currently lives in someone's head (or in the space between three people's heads) and convert it into something where you can check whether the AI did it right? How do you get the human in the loop to actually verify, not rubber-stamp, but meaningfully confirm?</span> I think this is the binding constraint right now. The model can already do enormous amounts of work in many domains. Whether anyone can confirm it was done correctly is what's actually gating deployment.

- If these premises hold, the company that matters most is the one that solves the third problem. Not the best model (those commoditize) and not the best vertical tool (delegation moves faster than any single tool). The one that can make organizations legible and their processes verifiable. <span class="marginnote">I could be wrong about this being the binding constraint. Maybe the real bottleneck is organizational identity, political resistance, or just that institutions move on generational timescales regardless of what's technically possible.</span> But I'm betting it's verifiability.

## Percepta is distinct from the labs

- Intelligence trains centrally but deploys at the edge. Context degrades the further it travels from where it was generated. Running a frontier model from the cloud to manage a hospital's billing exceptions is wasteful for the same reason you wouldn't stream HD to a cloud for a security camera when an edge chip does it at 25x less energy. Percepta is the lab's edge in healthcare.

- The complementarity is structural. Anthropic sells tokens, Percepta minimizes token burn per outcome. <span class="marginnote">Percepta generates domain-specific training data from trusted deployments that Anthropic can't get from API usage logs. It comes from inside institutions, with consent, in structured form. That data may be worth more to Anthropic than the token revenue.</span>

- The question I'm less sure about: <span class="question-text">is this arrangement permanent?</span> Labs are already hiring forward-deployed teams. The labs are building enterprise deployment capability. McGrew (ex-OpenAI head of research) says each enterprise integration problem is "too small" for a frontier lab, <span class="question-text">but if it gets lucrative enough, do they come for it anyway?</span> I'm betting the lab business model makes granular institutional work permanently unattractive. Honest that it's a bet.

- One version of where this goes looks like the OpenAI/Thrive deal. Lab researchers embedded in healthcare deployments, producing training data they can't get elsewhere, Percepta getting capabilities nobody else has. Both locked in. <span class="marginnote">Alma matters here too. Deploying inside systems GC owns means you observe context at the source instead of negotiating for access.</span>

## Percepta is not a holding company

- The holdcos (LLMH, Thrive, Sequence) buy businesses first, then try to transform them. Many of them have patient capital structures, that's the whole thesis, holding these businesses long-term with capital designed for it. The operational improvements are real (tasks that took 10 hours now take 1, margins genuinely expand). The question they haven't answered: <span class="question-text">does the market eventually reclassify an AI-transformed services company, or does the services label stick? If margins go from 10% to 40%, at what point does the market treat it differently?</span> I don't have a confident answer to that. The core difference from Percepta is the sequence, not the capital structure. They have to pick targets before they deeply understand what's transformable.

- Percepta does it in reverse. Deploy into organizations, build the transformation toolkit, map what's actually possible, THEN GC can decide what to buy. Percepta has information the holdcos don't have at the point of acquisition. Transform first, own what you've converted. <span class="question-text">Does having the deepest understanding of a business make you the natural owner or just the most informed advisor?</span> Open question, but at minimum it means you have information nobody else has at the point of acquisition.

- I keep coming back to this optionality: Percepta can become a holdco in the future, but it gets to build the engine meticulously first. Try things out, learn what works, understand what's actually transformable, before buying anything. The holdcos are doing the reverse and are forced to be rushed where Percepta can be methodical.

- GC's capital leverage makes this possible. GC doesn't have permanent capital in the Berkshire sense, but it has the scale and fund structure to make bets that pure venture can't. Like buying a hospital. Partnering with major acquirers to deploy into enterprises going private removes quarterly earnings pressure entirely.

- The distinction between automation and amplification matters here. Rollups automate to cut costs, which cannibalizes the labor revenue they bought. Percepta should be doing something different. Not making the hospital cheaper but making it capable of things that weren't possible before at any price. <span class="marginnote">I keep thinking of it as an exoskeleton rather than a replacement.</span>

## Percepta is not a typical AI startup

- Most AI startups converge on the same idea: build a vertical tool and compete for enterprise attention. Meanwhile the labs eat the bigger horizontal problems from above and capabilities double on 12-18 month cycles.

- There's a black hole effect happening underneath this. Every vertical AI app, regardless of industry, is being pulled toward the same center of gravity: context management, system integrations, agent runbooks and SOPs, eval sets, tooling. <span class="marginnote">A legal AI company and a healthcare AI company end up building surprisingly similar underlying infrastructure because the problems converge: managing context, integrating with existing systems, maintaining agent operating procedures, evaluating output quality.</span> The vertical differentiation dissolves. If that's true, a horizontal approach that captures the convergence might be better positioned than being locked into one vertical racing against the model.

- But there is a massive and growing delta between what the latest models can do and how organizations actually use them. <span class="marginnote">42% of enterprise AI initiatives discontinued in 2024, up from 17% the year before — more capability producing more failures, which is counterintuitive until you think about it.</span> You can see the computer age everywhere except in the productivity statistics. The intelligence keeps expanding and organizations aren't absorbing it.

- The question that separates real from performative in this space: <span class="question-text">can you generate $1 of real EBITDA for your customers?</span> A lot of companies show compelling demos and pitch decks. Fewer can point to concrete economic value that materialized because of what they built. The ones that can seem to have something in common: they went into the institution and did the work. Not from the screen. Sitting with operators, earning trust, watching people mark up printouts with highlighters. <span class="question-text">Does that pattern hold universally or just in the verticals I've been looking at?</span> Less sure about that.

## The "every company becomes an API" thesis is insufficient

- One framing of the future: capabilities are here, just automate everything. That framing captures something real. Automation is happening, capabilities are expanding. But it's incomplete. You need to actually deploy these things into organizations that were not designed for them. <span class="question-text">How much depth do you need for each domain? Is 80% from outside enough for most use cases, or does the last 20% where institutional reality lives matter disproportionately?</span> <span class="marginnote">I think it's the latter in healthcare and government. Less sure about other verticals.</span>

- What FDE teams are really doing is making organizations machine-readable. Workflows made explicit, decision criteria and exception paths documented. Converting companies from human-social structures into something AI can execute against. The hospital that's been made legible can participate in whatever comes next. The one that hasn't is invisible to it.

- But this conversion can't happen from outside. A hospital's 42-step billing process wasn't designed by an idiot. It's organizational scar tissue that encodes real institutional knowledge, built after something went wrong, probably multiple times. Each step is a lesson about a failure mode nobody documented any other way. The process IS the documentation. You can't automate it from outside. You have to understand why each step exists, which are load-bearing and which are vestigial, and then convert the load-bearing ones into forms an AI can execute and a human can verify.

## The product is amorphous on purpose

- I haven't seen or used Mosaic, Lattice, or any of Percepta's internal tooling. What follows is what I think winning looks like based on the worldview above. My vision of what the product should be, not a description of what it is.

- The way I think about the tooling: treat it all as a treasure hunter's assets. Mosaic, Lattice, whatever comes next. These aren't products you sell to clients. They're what make smart FDEs superpowered at the actual work. Understand flows (how does this institution actually operate, not the org chart version). Connect systems fast without months of integration setup. Get an overview of where agents are needed and where the bottlenecks live. Convert messy implicit processes into verifiable tasks. Build eval sets that capture what "good" looks like for this specific institution. Extract and organize workflows into machine-legible formats.

- The deeper question about all this tooling:

  - For tasks that are already verifiable: deploy AI, monitor, iterate.
  - For tasks that aren't verifiable: this is where the real work lives. Breaking down non-verifiable things into chunks of verifiable tasks. Taking a messy, judgment-heavy, socially-embedded process and converting it into discrete steps an AI can execute and a human can meaningfully confirm. I think that decomposition is Percepta's core intellectual work. <span class="question-text">Can it be systematized into a platform, or does it always require senior judgment?</span> <span class="marginnote">That's what determines if Percepta scales or stays boutique.</span>

- There's a real question underneath this about whether the decomposition skill transfers across verticals. The industry has mostly converged on single-vertical integration (one company for legal, one for healthcare, one for insurance). That assumes what you learn making a hospital legible doesn't help you make a government agency legible. I'm not sure that's right. The specific domain knowledge doesn't transfer, but the methodology of decomposing processes into verifiable tasks, building golden datasets of what "good" looks like, and running reinforcement loops where operators improve the AI as they go, that might compound across domains. If it does, Percepta's multi-vertical approach is an advantage. If it doesn't, spreading across verticals is dilution. <span class="marginnote">The answer probably depends on whether Mosaic captures the methodology or just the domain-specific outputs.</span>

- The observability layer gets harder, not easier:

  - Agent behavior needs to be legible to humans in real time.
  - When multiple agents interact across a healthcare system, the state space explodes. You need tools to follow what happened, why, and whether the outcome was right.
  - Human-in-the-loop is an architectural decision, not an afterthought. Design the entire system so human verification is meaningful and efficient, not a rubber stamp bolted on at the end.

- Traditional view of the FDE: go implement software at the client. Better view: Mosaic and whatever other tools Percepta creates are abstractions weaponized by FDEs. The goal is to get systems, processes, interactions, everything a company does operationally, into something legible by the model and verifiable by the model.

- Deployment complexity gets WORSE with better models. Context velocity (how fast the AI system learns from resolved exceptions) is nearly asymptotic. Meaning velocity (how fast humans metabolize that into trust) is not. Approval chains, sign-offs, processes with legally fixed minimum durations. Better models speed up context velocity without touching meaning velocity. The gap between what AI can do and what institutions will allow widens with each capability jump. This is why I think the FDE role evolves but doesn't disappear. From deploying AI to governing it to evolving how governance itself works. <span class="marginnote">This could be wrong. It's possible institutions adapt faster than I'm giving them credit for, or that some threshold of model capability makes the trust gap collapse. But the 42% and rising discontinuation rate suggests we're not there yet.</span>

- Every playbook written to onboard employee #50 is a Mosaic feature in disguise. Every decision framework that lets a junior FDE act without calling Hirsh is actual IP. If the company treats scaling as overhead rather than product development, the most important IP gets thrown away. That conversion capability is the product, or at least it should be.

## What I'd be watching

- Whether the research lab connects to the deployment business or stays academic. Percepta's specific advantage over Distyl and Brain Co: in-house research doing model-level work PLUS embedded teams generating curated domain data the labs can't access. If those connect, that's a flywheel nobody else can build.

  - There's growing evidence that models trained on curated, credentialed sources outperform general models in domains like healthcare. If that holds, the highest-value research isn't general architecture but specialized models from curated clinical data.
  - Without deployment data, the research is academic. Without proprietary research, the deployment is just consulting. I don't know what the combination becomes but it's clearly different from either one alone.
  - If the lab's published work has no production connection to deployments after six months, it's window dressing.

- Whether Mosaic is actually learning or just accumulating the feeling of learning. Playbooks get written, dashboards fill up. <span class="question-text">Does deployment six take less time than deployment one because of something in Mosaic, or because the team got experienced and the playbooks are just a record of that. If the experienced people leave, what does Mosaic actually contain?</span>

- The self-obsolescence problem. Successful deployments train the client to not need you. The better the team, the faster knowledge transfers. Palantir had Foundry creating platform lock-in. Percepta builds on a foundation model it doesn't own. The client can hire their own engineers and point them at the same model. Each engagement has a ceiling unless Mosaic accumulates institutional intelligence faster than the client absorbs it.

- The people question. This might matter more than any of the structural analysis above and I can't evaluate it from outside.

- Whether the structural thesis is right about the world but wrong about who captures the value. Deployment complexity persists. That doesn't mean a startup owned by a holding company is the entity that captures it. <span class="marginnote">I keep wanting to collapse "thesis is right" into "Percepta wins" and I don't trust how good that feels.</span>

- The uncomfortable version of the GC relationship: Percepta does the work, GC's assets get smarter, GC captures most of the upside. I don't know how you think about that from inside.

## One more thing I keep thinking about

- Follow the premises far enough and you get somewhere uncomfortable. If intelligence commoditizes on the timeline I described, talent eventually stops being the main differentiator for company outcomes. Not immediately. Right now the specific people in the room are why Percepta works. But past a certain point it becomes more about hard power. Capital. Distribution. Owned assets. Institutional relationships. Data captured over years in structured form.

- GC's balance sheet, the hospital, the Anthropic partnership — those are hard-power assets. Most AI companies are betting entirely on talent. Percepta has both, and the hard-power side is the part that survives commoditization. <span class="marginnote">I find that reassuring and slightly unsettling at the same time, since I'm joining for the team. But it might be the strongest version of the positioning and I'm not sure anyone is framing it that way yet.</span>
