---
layout: post
title: "Load-Bearing Nothing"
date: 2026-02-08
tags: [business, ai]
---

- In structural engineering there's a thing called <span class="highlight-text">parasitic load</span>. The weight of a building that only exists to support the building itself. Beams holding up beams. Floors that exist so you can put columns on them to hold up other floors. In a good structure it's maybe fifteen percent. In a bad one the building is mostly just holding itself up. <span class="marginnote">In real structures, parasitic load is unavoidable. The question is always how much of it is actually necessary vs. how much is just inherited from the last guy's constraints.</span>

- Nobody designs it that way on purpose. It accretes. Steel bends, concrete cracks, and the next engineer inherits the last one's constraints. The engineers who built those beams weren't stupid. They were solving real problems with what they had.

- For a long time that's how I understood the white collar economy. Approvals that exist to authorize other approvals. Reconciliations that exist because the handoffs between teams create discrepancies that need reconciling. Entire coordination layers whose job is managing the complexity that previous coordination layers introduced. It looked parasitic but it felt necessary, because no one person could hold the full picture in their head. We needed the handoffs. We needed the sign-offs. People can only hold so much context and the work outgrew what any individual could track.

- We built entire industries around this. SaaS to manage the load. Consultancies to audit it. Business schools to train people to sit on top of it without ever asking whether the beams are holding anything up.

- The conventional wisdom was that the complexity was structural. Cost of doing business. Weight of the building. I believed this for a long time.

- I've built the proof. Orchestration layers, autonomous agents. First time I watched one consume an entire workflow I expected it to just do the work faster. Approval chains, exception handling for exception handling, a shared spreadsheet that three people understood and two of them had quit. <span class="highlight-text">The agent didn't do it faster. It skipped most of it.</span> Not cutting corners. The corners just didn't need to exist. <span class="marginnote">This is the part that's hard to convey to people who haven't seen it. The agent doesn't optimize the workflow. It renders most of the workflow unnecessary. Different thing entirely.</span>

- The reconciliations were reconciling discrepancies the handoffs created. The approvals were authorizing work that only needed authorizing because it had been split across people who couldn't see each other's context. The load wasn't supporting the operation. It was supporting the fact that humans were running the operation.

- Remove the cognitive bottleneck and most of those load-bearing walls turn out to be vestigial.

- I used to think the craft in AI was building around the model. Scaffolding, retrieval systems, the careful engineering that makes something actually work in production. I spent years getting good at it. Then I watched every system I built get swallowed by the next model. Not metaphorically. Every workaround, every clever pipeline. Gone. The only thing that survived was what I knew about the domain, the failure modes, the edge cases, the texture of what "good" means in a specific context. <span class="highlight-text">Most AI engineering is building depreciating assets and calling it craft.</span> The thing that compounds is the problem definition itself. <span class="marginnote">Think about it like this: <span class="inline-code">RAG</span> pipelines, custom <span class="inline-code">chain-of-thought</span> scaffolding, fine-tuned routing layers — all of it gets absorbed into the next foundation model release. The only durable thing is knowing what the system should actually do and why.</span>

- Second time I watched it happen, different industry, same thing, faster. I'd already learned which walls were decorative. Third time, faster still.

- The value doesn't go to whoever sells the tool. The tool is commodity. Some other team running the same model with a different pitch deck undercuts you by Wednesday. <span class="highlight-text">The value goes to whoever owns the operation underneath.</span> Vendor captures a licensing fee. Owner captures everything the building was wasting on itself.

- And the weight is enormous. Operations running on single-digit margins because they've been spending most of their energy holding themselves up.

- The interesting part isn't the cost reduction in any one operation. It's what happens when you do it across multiple operations and the learning starts to compound. Each one teaches you something about why operations carry unnecessary weight, and the patterns keep showing up. The failure modes keep repeating. Second building is easier than the first because you've already seen how billing workflows create their own reconciliation overhead. By the tenth you're spotting the decorative walls before anyone shows you the floor plan.

- When intelligence flows between structures, when every decorative wall you find in one teaches you to spot the next one faster, what you're building is a learning system that happens to own buildings. The accumulated understanding of which loads are real and which ones we invented is the thing that actually compounds. <span class="marginnote">This is closer to how <span class="inline-code">transfer learning</span> works than how holding companies work. Each new context isn't starting from scratch, it's starting from everything you already know about unnecessary weight.</span>

- But there's a wall it hits and I've watched smart people pretend it's not there. Someone still has to sit across from a board member furious about a landscaping bill who will never care that an algorithm optimized the vendor selection. Someone has to sign the thing, hold the liability, absorb the specific species of anger that has nothing to do with outcomes and everything to do with not feeling heard by a person.

- The system can handle the problem. What it can't handle is the person who has the problem.

- So a thin human layer of trust persists, because people need to believe someone with a pulse is accountable when things go wrong. The intelligence does the work and the humans are there so someone can be sued.

- Underneath that, the compounding continues in industry after industry still priced for an era where the load was the business.

- I keep thinking about the engineers who designed the original beams though. They weren't wrong. They solved real problems and they were genuinely good at it. The problem just stopped being real. And their expertise, hard-won and legitimate, is still sitting there. <span class="highlight-text">Load-bearing nothing.</span>
