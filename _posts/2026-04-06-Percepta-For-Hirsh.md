---
layout: post
title: "How I'm Thinking About Percepta"
date: 2026-04-06
tags: [business, ai]
hidden: true
permalink: /percepta-for-hirsh/
---

*Healthcare lens throughout, but most of this generalizes.*

## Three premises I'm treating as given

- **PR1:** Models will keep getting better and the improvement is compounding. <span class="marginnote">METR task duration doubles every few months, accelerating.</span> It's universally accepted (although still tricky) to plan for a world where the model is meaningfully better in 12 months and dramatically better in 24.

- **PR2:** People and organizations will defer more and more decisions to models. As models get more capable the surface area of delegation expands. The bottleneck shifts from "can the model do this" to "can the organization hand this off", and that handoff is where things break.

- **PR3:** Two problems stay hard and get harder as models improve. These are the durable seams:

  - **Observability.** When an agent takes an action you need to know what it did, why, and whether the outcome was correct. Method for making agent behavior legible to humans. Plotting multi-agent trajectories when the state space explodes. This problem gets worse with capability. As models get more capable they take actions across wider domains, and there's just more to watch. <span class="marginnote">The verification inversion: checking the work gets harder as the worker gets smarter.</span>

  - **Verifiability conversion.** Most of what organizations do is not structured in a way an AI can execute and a human can verify the result. The work is messy and implicit, embedded in human judgment and social context. <span class="question-text">How do you take a process that currently lives in someone's head (or in the space between three people's heads) and convert it into something where you can check whether the AI did it right?</span> I think this is the binding constraint right now. The model can already do enormous amounts of work in many domains. Whether anyone can confirm it was done correctly is what's actually gating deployment. Regulated environments make this worse. In healthcare the AI can/possibly will technically do the work, but no regulatory framework permits autonomous execution. Someone still has to be legally accountable for the decision. That's a different problem from verification and it doesn't compress with better models.

- If these premises hold, there's a desperate need for a company that solves the third problem. Not the best model (those will continue to get better, competition will potentially commoditize them, and we might hit a certain level of intelligence where the marginal returns on getting it better might not be essential for enterprise work) and not the best vertical tool (delegation moves faster than any single tool). The one that makes organizations legible and their processes verifiable. <span class="marginnote">I could be wrong about verifiability being the binding constraint. Maybe the real bottleneck is organizational identity, political resistance, or just that institutions move on generational timescales regardless of what's technically possible.</span>

## Not a lab

- Intelligence trains centrally but deploys at the edge. Context degrades the further it travels from where it was generated. Running a frontier model from the cloud to manage a hospital's billing exceptions is wasteful for the same reason you wouldn't stream HD to a cloud for a security camera when an edge chip does it at 25x less energy. Percepta is a lab's edge in healthcare.

- The complementary nature with the labs might be structural. Labs sell tokens, Percepta minimizes token burn per outcome. <span class="marginnote">Percepta generates domain-specific training data from trusted deployments that labs can't get from API usage logs. It comes from inside institutions, with consent, in structured form. Models trained on their own outputs degrade. The thing that prevents this is signal from real institutional contexts where humans make decisions with actual consequences. That data may be worth more to the lab than the token revenue.</span>

- Whether this arrangement is permanent is an open question. Labs are already hiring forward-deployed teams and building enterprise deployment capability. You could argue specific enterprise integration problems are "too small" for a frontier lab. I think the deeper issue is cultural. Labs work on what researchers find intellectually compelling and can advance the frontier. Healthcare billing optimization will never compete with math olympiad problems or competitive programming for researcher attention. The work goes unbuilt because nobody at a frontier lab wants to do it, not because it's too small. That's a cultural claim about labs, and I'm betting on it holding. <span class="marginnote">Honestly, this is a bet.</span>

- One version of where this goes looks like the OpenAI/Thrive deal. Lab researchers embedded in healthcare deployments, producing training data they can't get elsewhere, Percepta getting capabilities nobody else has (or earlier). Both locked in. <span class="marginnote">Alma matters here too. Deploying inside systems GC owns means you observe context at the source instead of always negotiating for access through some enterprise sales process.</span>

## Not a holding company

- The holdcos (LLMH, Thrive, Sequence) buy businesses first, then try to transform them. Many have patient capital structures, that's the whole thesis. The hope is there's valuable operational improvements that are real (tasks that took 10 hours now take 1, margins genuinely expand). <span class="question-text">Does the market eventually reclassify an AI-transformed services company, or does the services label stick? If margins go from 10% to 40%, at what point does the market treat it differently?</span> The holdcos haven't answered that. The core difference from Percepta is the sequence, not the capital structure. They have to pick targets before they deeply understand what's transformable.

- Percepta does it in reverse. Deploy into organizations, build the transformation toolkit, map what's actually possible, then GC can decide what to buy. Percepta has information the holdcos don't have at the point of acquisition. (purely speculative if this is even a direction you guys want to go in) <span class="question-text">Does having the deepest understanding of a business make you the natural owner or just the most informed advisor?</span> At minimum it means you have information nobody else has when it matters.

- The optionality: Percepta can become a holdco in the future, but it gets to build the engine first. Try things out, learn what works, understand what's actually transformable before buying anything. The holdcos are doing the reverse and are forced to be rushed where Percepta can be methodical and build compounding tools first.

- GC's capital leverage makes this possible. GC doesn't necessarily have the same permanent capital, but it has the scale and fund structure to make bets that pure venture can't. Like buying a hospital. Partnering with major acquirers to deploy into enterprises going private removes quarterly earnings pressure entirely.

- The distinction between automation and amplification matters here. Once you have fully bought a business, there's always the risk of automating to cut costs, which cannibalizes the labor revenue they bought. Percepta has the option to avoid that trap and be doing something different. The hospital's costs might not change much, but it starts doing things that weren't possible before at any staffing level or budget. <span class="marginnote">Exoskeleton, not replacement.</span>

## Not a vertical AI startup

- Most AI startups converge on the same idea: build a vertical tool and compete for enterprise attention. Meanwhile the labs eat the bigger horizontal problems from above and capabilities double on 12-18 month cycles.

- There's a black hole effect I keep on feeling. Every vertical AI app, regardless of industry, is being pulled toward the same center of gravity: context management, system integrations, agent runbooks and SOPs, eval sets, tooling (even the admins of these apps is looking more and more similar). <span class="marginnote">A legal AI company and a healthcare AI company end up building surprisingly similar underlying infrastructure. The vertical differentiation dissolves, or at least starts looking thin.</span> If that's true, a horizontal approach that captures the convergence is better positioned than being locked into one vertical racing against the model.

- There is a massive and growing delta between what the latest models can do and how organizations actually use them. As the ambition of the clients grow, so does the surface area of the vertical applications... However, more capability producing more failures. <span class="marginnote">The Solow paradox: you can see the computer age everywhere except in the productivity statistics. Organizations aren't structured to absorb intelligence at the rate it's being produced.</span>

- <span class="question-text">Can you generate real EBITDA for your customers?</span> A lot of companies show compelling POCs, but fewer can point to concrete economic value. The ones that can seem to have something in common: they went into the institution and did the work (or the work to be done was simple enough/unambitious). Not from the screen. Sitting with operators, earning trust, watching people mark up printouts with highlighters.

## The automation thesis is incomplete

- One framing of the future: capabilities are here, just automate everything. That captures something real, and what I usually feel, but it's incomplete. You need to actually deploy into organizations that were not designed for this. <span class="question-text">Is 80% from outside enough for most use cases, or does the last 20% where institutional reality lives matter disproportionately?</span> I think it's the latter in healthcare and government. Less sure about other verticals.

- Self-driving works because roads already exist. Standardized and predictable. Institutions have nothing like that for AI agents. FDE teams are building that infrastructure. Making organizations machine-readable. <span class="marginnote">Workflows made explicit, decision criteria and exception paths documented. Converting companies from human-social structures into something AI can execute against.</span> The hospital that's been made legible can participate in whatever comes next. Without that, you're just not in the picture.

- But this conversion can't happen from outside. A hospital's 42-step billing process wasn't designed by an idiot. It's organizational scar tissue that encodes real institutional knowledge, built after something went wrong, probably multiple times. Those processes are how the institution remembers what went wrong. You have to understand why each step exists, which are load-bearing and which are vestigial, and then convert the load-bearing ones into forms an AI can execute and a human can verify.

## The product (as I imagine it)

- I haven't seen or used Mosaic, Lattice, or any of Percepta's internal tooling. What follows is what I think winning looks like based on the worldview above. My vision of what the product should be, not a description of what it is.

- The way I think about the tooling: treat it all as a treasure hunter's assets. Not products you sell to clients. They're what make smart FDEs superpowered at the actual work. <span class="marginnote">Understand flows (how does this institution actually operate). Connect systems fast. Get an overview of where agents are needed. Convert messy processes into verifiable tasks. Build eval sets that capture what "good" looks like. Extract workflows into machine-legible formats.</span>

- The deeper question about all this tooling:
  - For tasks that are already verifiable: deploy AI, monitor, iterate.
  - For tasks that aren't verifiable: this is where the real work lives. Breaking non-verifiable things into chunks of verifiable tasks. The tasks AI has conquered first (math, coding) all had cheap, dense verification signals built in. The institutional processes it hasn't conquered lack those signals entirely. FDEs decomposing processes into verifiable chunks are building the feedback loops that make RL work in those domains. The deployment work and the research infrastructure turn out to be the same thing. <span class="marginnote">Most AI agency in institutional settings is accidental. Models picked it up from text describing what agents do, not from operating in real environments. RL environments for healthcare exist in research (retrospective datasets, narrow simulators) but none capture how institutions actually operate. A growing startup ecosystem is building RL training infrastructure for AI agents, but focused on coding and enterprise workflows, not regulated institutional settings. Building the equivalent for healthcare requires being inside.</span>

- I think that decomposition is Percepta's core intellectual work. The gap between "works in a pilot" and "works at institutional scale" is where most of the real judgment lives. Which edge cases matter for this specific hospital, when the model is good enough for this workflow. What "correct" even means when the context changes between floors. <span class="question-text">Can the decomposition be systematized into a platform, or does it always require senior judgment?</span> That determines whether Percepta scales or stays boutique.

- <span class="question-text">Does the decomposition skill transfer across verticals?</span> The industry has mostly converged on single-vertical integration. That assumes what you learn making a hospital legible doesn't help you make a government agency legible. I'm not sure that's right. The specific domain knowledge doesn't transfer, but the methodology might compound across domains. <span class="marginnote">If it does, Percepta's multi-vertical approach is an advantage. If it doesn't, spreading across verticals is dilution. Depends on whether Mosaic captures the methodology or just the domain-specific outputs.</span>

- The observability layer keeps getting harder. Agent behavior needs to be legible to humans in real time. When multiple agents interact across a healthcare system, the state space explodes. Human-in-the-loop has to be designed in from the start.

- Deployment gets harder as models improve. <span class="marginnote">Context velocity (how fast the AI system learns from resolved exceptions) is nearly asymptotic. Meaning velocity (how fast humans metabolize that into trust) is not. Approval chains, sign-offs, legally fixed minimum durations.</span> The gap between what AI can do and what institutions will allow widens with each capability jump. I think the FDE role evolves but doesn't disappear. <span class="marginnote">This could be wrong. Institutions may adapt faster than I expect, or some threshold of capability might collapse the trust gap.</span>

- Every playbook written to onboard employee #50 is a Mosaic feature in disguise. Same with decision frameworks that let a junior FDE act without calling Hirsh. That's actual IP. <span class="question-text">Does that absorption happen automatically, or only when someone has time to document what they did?</span> If the learning is structural, built into how the tools work so every resolved exception gets absorbed as it happens, that's real compounding. If it depends on writeups after the fact, most of it gets lost when people leave.

## What I'd be watching

- Whether the research lab connects to the deployment business or stays academic. Percepta's specific advantage: in-house research doing model-level work PLUS embedded teams generating curated domain data the labs can't access. If those connect, that's a flywheel nobody else can build. <span class="marginnote">There's growing evidence that models trained on curated, credentialed sources outperform general models in domains like healthcare. If that holds, the highest-value research isn't general architecture but specialized models from curated clinical data.</span>
  - I keep circling this one. Research without deployment data drifts toward academic paper mills. On the deployment side, without proprietary research you're basically consulting with better tooling. What happens when they actually connect is less clear to me, but it's obviously something neither piece produces on its own.
  - If the lab's published work has no production connection to deployments after six months, it's window dressing.

- Whether Mosaic is actually learning or accumulating the feeling of learning. Playbooks get written, dashboards fill up. <span class="question-text">Does deployment six take less time than deployment one because of something in Mosaic, or because the team got experienced and the playbooks are just a record of that? If the experienced people leave, what does Mosaic actually contain?</span>

- The self-obsolescence problem. Successful deployments train the client to not need you. Some deployment companies create platform lock-in with proprietary infrastructure. Percepta builds on the foundation model directly. The client can hire their own engineers and point them at the same model. Each engagement has a ceiling unless Mosaic accumulates institutional intelligence faster than the client absorbs it. <span class="marginnote">There's a mirror version of this. When Percepta makes a hospital legible, it extracts the hospital's operational knowledge into structured form. The exception paths, the decision criteria, the stuff that lives between three people's heads. Who owns that? If Percepta deploys at a second hospital, how much carries over? The hospital is handing over the thing that makes it function.</span>

- The people question. This might matter more than any of the structural analysis above and I can't evaluate it from outside.

- Whether the structural thesis is right about the world but wrong about who captures the value. Deployment complexity persists. That doesn't mean a startup owned by a holding company is the entity that captures it. <span class="marginnote">I keep wanting to collapse "thesis is right" into "Percepta wins" and I don't trust how good that feels.</span>

- The uncomfortable version of the GC relationship: Percepta does the work, GC's assets get smarter, GC captures most of the upside. I don't know how you think about that from inside.

## What would change my mind

- Deployment six takes the same resources as deployment one. Compounding isn't happening.
- Headcount linear with revenue. It's consulting.
- Research has no production connection to deployments in six months. Decorative.
- A near-term model walks a generalist through compliant healthcare deployment end-to-end. Quality gap closed.
- The four GC pieces (capital, assets, deployment, research) don't connect as a system. It's a holding company with a consulting subsidiary.

<span class="marginnote">I don't know whether Percepta is unforkable today. That bothers me more than anything on this list. But I think the trajectory is right and the window is open.</span>

## One more thing

- Follow the premises far enough and you get somewhere uncomfortable. If intelligence commoditizes on the timeline I described, talent eventually stops being the main differentiator for company outcomes. Not immediately. Right now the specific people in the room are why Percepta works. But past a certain point it becomes more about hard power. Capital. Distribution. Owned assets. Institutional relationships. Data captured over years in structured form.

- GC's balance sheet, the hospital, the lab partnership, those are hard-power assets. Most AI companies are betting entirely on talent. Percepta has both, and the hard-power side is the part that survives commoditization. <span class="marginnote">I find that reassuring and slightly unsettling at the same time, since I'm joining for the team. But it might be the strongest version of the positioning and I'm not sure anyone is framing it that way yet.</span>
