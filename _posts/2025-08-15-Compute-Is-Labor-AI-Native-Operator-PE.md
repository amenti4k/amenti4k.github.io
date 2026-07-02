---
layout: post
title: "The Three-Week PO: Context Moves at Machine Speed. Trust Doesn't."
date: 2025-08-15
categories: [economics, ai, transformation]
tags: [ai-orchestration, procurement, trust, decision-rights, didero-ai, ai-rollups]
excerpt: "Same agent, same two-line PO mismatch. One company resolved it in forty seconds; the other took three weeks, because nobody there had ever decided an agent was allowed to act."
---

# The Three-Week PO

Last spring I watched the same AI agent resolve the same problem at two different companies. The problem was small: a purchase order and an invoice disagreed by two lines. The agent read both documents, found the discrepancy, pulled the contract terms, drafted the correction, and staged it for commit.

At the first company, the fix went through in about forty seconds.

At the second company, the identical fix sat in a queue for three weeks.

Nothing technical separated the two. Same model, same integration, same confidence score. At the first company, someone with authority had decided that an agent may act on two-line mismatches below a dollar threshold. At the second company, nobody had. Same inputs, same output, and a different answer to the only question that mattered: who's allowed to touch the database. The first org had rewired its decision rights so that tools propose, the system routes, and humans sign where it matters. The second still believed work flows up the pyramid until a sufficiently credentialed person clicks approve.

I should say up front where I'm standing: I was a founding engineer at [Didero](https://didero.ai), where we build AI agents that run procurement. Purchase orders, invoices, vendor email, about $600K of order volume flowing through the system daily when I last counted. I sell the thing this essay describes. Discount accordingly.

But the three-week PO taught me something no benchmark could: the binding constraint on AI autonomy is not what models can do. It's the speed at which institutions reassign decision rights. Most of what gets diagnosed as "AI adoption failure" is the gap between those two speeds.

## The Bureaucracy Was Real Work

It's fashionable to say the approvals and reconciliations of corporate life were always theater. Mostly they weren't, and the difference matters.

Here's what one purchase order actually is: three systems of record, five email threads, a contract PDF, a CSV invoice, two carrier portals, and a vendor rep who only answers the phone on Thursdays. The information a single correct decision requires is scattered across finance, risk, ops, and a supplier's inbox. Multiply that by hundreds of vendors and a few thousand exceptions a year, and no single person can hold the map. No team can either.

So we did the only thing available: we broke the map into pieces small enough for one head to hold, and built procedures to pass the pieces around. The approval chain, the weekly sync, the reconciliation-of-reconciliations. These were coping mechanisms for cognitive saturation. We created committees to pool context, and then, over the years, mistook the committee for the work.<span class="marginnote">Herbert Simon called this <span class="inline-code">bounded rationality</span>: humans satisfice because we can't hold the full decision context. The org chart is what satisficing looks like at company scale.</span>

Coase said firms exist where coordinating inside the walls is cheaper than transacting across them. Most of what a middle layer does all day is that internal coordination cost made visible: ferrying context from the silo that has it to the decision that needs it.

But not every approval is a context ferry, and this is the concession the excited version of the argument always skips. Some approvals exist because of fraud, SOX, segregation of duties, professional licensure. Those are control requirements, and they survive automation. An orchestrated system doesn't get to delete them; it has to re-implement them as evidence: traces, attestations, reversible commits. Keep that distinction in view. The economics of the whole shift live inside it.

## What Flipping Orchestration Actually Did

"AI-powered" hides the distinction that matters, so let me define it in a way you can test against any real system.

**Assistive AI**: humans own the control flow. The workflow is human-designed, and the model fills slots inside it. Extract this field, draft this reply, summarize this thread. When something unexpected happens, a human decides what happens next.

**Orchestrative AI**: the model owns the control flow. It gets a goal ("process this order correctly") plus tools, budgets, and escalation rules, and it decides what happens next: act, fetch, ask, retry, escalate. Humans are one of the callable steps.

The test is the exception path. Whoever handles the unexpected owns the process.

At Didero, we started on the wrong side of this line and didn't know it. We tried to brute-force autonomy with configuration: if this customer, then that approval path; if this vendor, then that tolerance. I've [written about this failure in detail](/ai/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html). We accumulated over 1,000 configuration parameters, encoding things like "Tom approves on Thursdays, but not over $7,500, unless it's a preferred vendor." It worked, until it didn't. Context slipped through the cracks. Edge cases multiplied faster than we could write branches for them. We had built the world's most expensive state machine and were calling it AI.

The flip came when we stopped telling the system what to do and gave it the goal, the tools, and a router that priced its own uncertainty.<span class="marginnote"><span class="inline-code">Confidence routing</span>: the system scores its own certainty on each decision, auto-executes above a threshold, asks for missing context in the middle band, and escalates to a human below it, with the thresholds set in dollars rather than vibes.</span> What dissolved was the context-ferrying: the status-check emails, the re-keying between systems, the human whose job was to notice that the invoice and the PO disagreed. The approvals on high-risk commits, the audit evidence, and the human name on consequential calls all stayed, on purpose.

From our own deployment: roughly 85% of tasks auto-resolve without a human touch, counted by task rather than dollar value. That's procurement only, our customers only; generalize at your own risk. Onboarding a new customer stopped meaning three weeks of hand-written configuration. Our engineers stopped babysitting workflows. And the failures were real: the system once decided "net 30" meant thirty items, net weight. That single error is why every consequential write in our stack is staged and reversible, and why I flinch when a demo claims full autonomy.

This is also where the strongest objection lands, and I'd rather take it head-on. Nathan Benaich and Nikola Mrkšić have argued that most "AI rollup" pitches confuse operational improvement with a new business model, and assume public markets will hand services EBITDA a software multiple. The market evidence is currently on their side: when Capgemini agreed to buy WNS this summer, it offered a services price, not a SaaS one. Their question is the right filter: are you actually changing the unit economics, or just narrating?

My answer is the definition above. If the gains come from headcount reduction with a chatbot bolted on, they decay the moment you stop staring, and the skeptics win. If the orchestrator owns the control flow, every resolved exception makes the next one cheaper, and costs keep falling after you look away. That difference is checkable in any diligence. Ask who handles the exception path. Ask whether cost per successful outcome fell last quarter without a hiring freeze to explain it. I can't publish my customers' before-and-after P&Ls; NDAs are real. The two questions don't need my numbers, though. Anyone can put them to any company claiming this transformation.

## The Trust Boundary

If orchestration works, why doesn't any deployment I know of run at 100% autonomy?

Because companies live inside institutions: customers, regulators, auditors, insurers. Correct is table stakes. The system also has to be accountable, and accountability has a legal shape: someone must be licensable, insurable, suable. A doctor signs because society needs a name to sue. A controller wants the trace because she knows what an auditor will ask: "Who decided this, and on what basis?"

I used to sneer at this as trust theater. I've stopped. Theater is how institutions change without shattering. The job is to make it visible and cheap: named humans on the high-risk commits, automatic receipts for everything else.

In practice, closing the gap between what the model could do and what the institution will accept comes down to unglamorous mechanics. Writes are two-phase wherever they matter: the agent proposes, a deterministic tool stages, and the commit happens only when the risk budget or a human says go. Decision traces read like a narrative instead of a stack trace: which model believed what, which context it saw, which thresholds were in force, why it didn't escalate. Each workflow gets a kill switch owned by the business side, terrifying the first week and liberating the second.

Exceptions get a library with human names. Not <span class="inline-code">ERR_419</span>, but "carrier portal renumbers its fields on Tuesdays," each entry carrying a minimal repro, a safe default, and a resolution recipe. Good fixes get promoted to global memory; local overrides live where regulation genuinely differs. And the bar to ship is defined in cash: auto-execute above this confidence, clarify in this band, escalate below it, human review capacity capped at some percentage, cost per successful outcome under some dollar figure including rework. The thresholds will be wrong at first. Version them and move on.

Do this and the autonomy ceiling rises on its own, because every escalation teaches the router. Skip it and you end up hiring a second company to babysit the first.

One more thing about the humans handling the escalations, because their role is routinely misread. The escalation queue looks like quality control from the outside. From the inside, it's four jobs the machine can't hold: accountability, exception discovery, relationships, legitimacy. In the [Quicksand essay](/ai/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html) I put it as "humans are the product": the system's job is to make them superhuman, not to replace them. This essay is the same claim seen from the institutional side. The humans who remain are the interface through which an organization consents to what its software is doing.

## Context Velocity, Meaning Velocity

The most useful frame I've found for why flawless demos become failed deployments is a race between two speeds.

Context velocity is how fast the system learns. A vendor quirk gets resolved for one customer on Monday; by Tuesday morning it's the default resolution for every customer the pattern applies to. No meeting happened. I've watched that propagation, but only within procurement, across customers who share an exception taxonomy. Whether it transfers across industries, whether a freight fix teaches an insurance workflow anything, I don't know, and I haven't seen evidence that anyone else does either. Process shapes rhyme across industries (document-extraction quirks, portal failure modes, escalation heuristics look similar everywhere), which makes transfer plausible. For now it's a hypothesis.

Meaning velocity is how fast humans turn the change into trust. People need to see the same lesson land a few times before they release the wheel. That's caution doing its job. Institutions protect themselves from confident errors this way, including, occasionally, mine.

The gap between the two speeds is where deployments die. The system converges a little more every week; the humans need to see the same lesson three times. A month of "can we just loop in Legal?" after a perfect pilot is meaning velocity doing its work, and the deployments that survive are engineered for it, with receipts, kill switches, and named accountability, rather than built to outrun it.

Capital has noticed the same gap and is betting on closing it by buying the decision rights outright. Slow Ventures gave the move a name, Growth Buyouts: if persuading incumbents to adopt is the bottleneck, acquire the incumbent and install the system from the inside. Metropolis ran the play in physical space. After selling computer-vision parking software proved slow, it raised roughly $1.8 billion in financing and bought SP+, the largest parking operator in North America, for about $1.5 billion. General Catalyst stood up HATCo and agreed to acquire a health system outright, Summa Health in Ohio, to modernize care delivery from the ownership position rather than the vendor position. And the thirty-year control group predates AI entirely: Constellation Software has made roughly a thousand vertical-software acquisitions since 1995, almost never selling, compounding by centralizing capital allocation while leaving domain knowledge local.

Whether the AI-native versions of this earn software economics is exactly Benaich and Mrkšić's open question, and my dataset doesn't answer it. What the acquisitions do tell you is where the bottleneck is perceived to be. Nobody spends $1.5 billion to avoid a sales cycle unless they believe the technology works and the permission is the scarce asset. Each of these deals is a bet that it's cheaper to buy authority than to persuade it.

## What We Stapled Our Worth To

There's an uncomfortable part of this I'm not going to dress up, mostly because I felt it myself before I could name it.

If a large share of a coordination job was ferrying context between silos, and the system now ferries it better, what exactly were we doing all those years? Some of it was skill. A lot of it was identity. We stapled a sense of worth to the keystrokes and called it a career. When the keystrokes evaporate, the person doesn't.

The risk in front of us is that institutions pocket the gains and call the rest "upskilling." The opportunity is to tell the truth about what changed: much of that work never deserved a human life, and the humans who did it are now free for the parts that always did. The judgment call nobody can spec. The vendor who only picks up for someone she knows. The exception nobody has seen before. Getting from the risk to the opportunity is a design problem, and the trust mechanics above are its load-bearing parts.

Which brings me back to the three-week PO. The company that resolved it in forty seconds didn't have better engineers or a newer model. It had done the slow, human work of deciding, explicitly and with names attached, where an agent may act, where it must ask, and who owns the consequences. It moved its decision rights at a speed its people could own. The other company bought the same capability and granted it no authority.

That's the choice in front of every company deploying this stuff, and it has nothing to do with model selection. Move decision rights into software at the speed your people can metabolize, and autonomy compounds workflow by workflow. Move slower than that, and the demo keeps winning while the identical fix sits in a queue for three weeks, waiting for a signature the org chart can't produce. Everyone will blame the model.
