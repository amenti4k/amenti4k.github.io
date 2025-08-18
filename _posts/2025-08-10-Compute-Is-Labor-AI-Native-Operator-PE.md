---
layout: post
title: "Compute Is Labor: How AI-Native Operator-PE Will Reprice the Cost Side of the Economy"
date: 2025-08-10
categories: [ai, economics, private-equity]
tags: [ai, automation, private-equity, labor-economics, autonomous-work]
excerpt: "The thing that changes you isn't brilliance; it's exhaustion. It's 11:30 PM, another workflow has failed, and you're staring at a dashboard that feels like a mirror. The discovery that AI should orchestrate software—not be embedded in it—revealed an uncomfortable economic truth: we weren't selling software features; we were replacing labor."
---

# Compute Is Labor: How AI-Native Operator-PE Will Reprice the Cost Side of the Economy

## The Discovery

The thing that changes you isn't brilliance; it's exhaustion. It's 11:30 PM, another workflow has failed, and I'm staring at a dashboard that feels like a mirror. Every knob I added to save myself yesterday is the debt I'll pay tomorrow. Every "customer-specific flag" is an IOU from reality. I've been building AI systems the way we build software systems: deterministic flows that call "smart" functions. Then someone, half-asleep on Slack, asks the question that flips the room: why are we still telling the AI what to do? Isn't that literally its job?

That inversion—letting AI orchestrate software rather than embedding AI inside software—wasn't a philosophical shift. It was survival. As I detailed in ["Building on Quicksand"](/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html), it dissolved a thousand brittle configurations into a handful of durable capabilities. It turned failure from catastrophe into state. It made the system honest about its nature: a distributed system where one of the services is non-deterministic.

It also revealed an uncomfortable economic truth. The industry isn't selling software features; it's replacing labor. The capture rate is minimal because the market doesn't know how to price this fundamental transformation.

What follows is the capital formation thesis built on that discovery: how an AI-native Operator-PE—part dealmaker, part infra scheduler, part process engineer—can underwrite the adoption gap, install autonomy as an operating capability, and systematically manufacture margin across a portfolio. This isn't "SaaS-enabled PE." It's a new archetype, the successor to the raider, the activist, and the ESG steward: the operator of autonomous work.

## The $10 Trillion Mispricing

### The mispricing of autonomy

The numbers reveal an interesting dynamic. When procurement flows become truly autonomous, end-to-end success can stabilize around 94% with a deliberately designed 6% human-in-the-loop for genuine novelty. The economic transformation is striking: what once required significant human labor converts into compute and resilient workflows. Yet the market struggles to price this transformation—there's a massive gap between the value created and what the market will pay for automation tools.

The macro numbers are staggering: Goldman Sachs projects AI could replace 300 million full-time jobs globally. McKinsey estimates $2.6-4.4 trillion in annual value creation. In January 2025, professional services job openings hit 13-year lows while 40% of white-collar job seekers couldn't secure a single interview. The white-collar recession isn't coming—it's here.

Why is that wedge so large? Because the market still thinks "software using AI," not "AI using software." Buyers anchor on seat counts and feature lists; they do not price throughput under reliability SLAs. CFOs will happily pay for buttons, less so for fewer humans. Boards will applaud a demo; they will defer the messy process refactor that turns the demo into dependable throughput.

The mispricing persists because the adoption path is hard: data plumbing, SOP redesign, change management, safety and audit, new operating habits. That is the J-curve of complementary investments. Most management teams will postpone it. Control investors don't have to.

An AI-native Operator-PE exists to compel and stage that transition. It prices the pain into the model. It treats "compute becomes labor" as a capital formation strategy, not a product sales tactic.

## The Production Truth

### Why the demos lie—and what finally works

As I wrote in ["Building on Quicksand"](/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html), the production reality is harsh: the seductive demo of a perfect extraction gives way to 1,000+ configuration flags, retries of retries, and a hall of mirrors called "fallback logic." The architectural inversion I discovered—letting AI orchestrate software rather than embedding AI in pipelines—was survival, not philosophy.

What worked was giving the agent tools to invoke (Parse, Validate, CheckBudget, RouteApproval, CreateOrder, AskHuman) against a context that could be extended on demand. We gave failure a place to live through durable execution. Temporal-style orchestration preserved state, retried idempotently, resumed exactly where we left off. This alone bent the cost curve: resume-on-failure versus retry-from-zero is the difference between stable unit economics and quietly lighting money on fire.

At scale, the economics become clear. Durable execution fundamentally changes the cost structure by eliminating redundant work. The difference between retry-from-zero and resume-from-failure isn't just technical elegance—it's the difference between sustainable unit economics and burning capital.

My work with [Stagehand](/2025/08/12/stagehand-browser-automation-production.html) proved the same pattern in browser automation. Traditional RPA breaks when a button's class changes from `submit-btn` to `submit-button`. Semantic actions—"Click the Submit button," "Open purchase order A300807"—plus strategy retries, session pooling, and observability flipped the reliability curve. Per operation, AI-powered RPA was 7–8x slower. End-to-end, it completed 11x more work. Reliability, not raw speed, is the shape of production truth.

These aren't anecdotes; they're the mechanics of autonomy in brownfield environments. They are the only route that scales beyond a handful of bespoke heroes and late-night Slack channels.

## The Technical Architecture

### The Autonomous Work Stack: how compute becomes labor

Once you accept the inversion, the system almost designs itself.

At the top sits an orchestrator where AI chooses the next action. Software presents as tools: validated, idempotent, and safe. A tool registry is not a toy catalog; it is a contract—inputs, outputs, side effects, invariants. Beneath it is durable execution: retries with exponential backoff, idempotency keys, deterministic replay. Failures aren't bugs to hide; they're states to resume.

Context is curated. You don't pour the data lake into the prompt. You extract patterns—"usual order size," "frequent items," "approval history"—and attach callable hooks: get_specific_order, check_budget, build_approval_chain. The agent gets a map and a way to ask for directions. The million-token context myth dies here. Retrieval wins.

Safety and governance are on the hot path. High-risk operations—bulk updates, mass emails, payments—are scored. Above a threshold, the system asks a human through a first-class task with clear options and audit-grade consent. Every decision—AI or human—leaves a rationale trail with inputs, outputs, and safeguards.

Humans aren't a fallback; they're part of the system. Tasks arrive where people live (often email) with one-click actions that flow back into the workflow. The point isn't to eliminate people; it's to elevate them to the 6–10% of cases where their judgment compounds value rather than mops up ambiguity.

Observability is non-negotiable. Screenshots, DOM snapshots, structured logs, and replayable traces make midnight debugging tractable and compliance conversations boring. "You can't fix what you can't see" is a cliché until a regulator asks, "What did the system know, and why did it decide that?"

This stack is the substrate for turning compute into dependable labor. It collapses the configuration surface from thousands of brittle flags to dozens of reusable primitives. It bends the token economics by resuming instead of repeating. It's opinionated where it matters and agnostic where it must be.

## The Operating Philosophy

### Serve one, then scale: the only honest way to grow

The internet taught us to scale abstractions; autonomy teaches us to scale reliability. The path mirrors Waymo's strategy: they mastered San Francisco's chaos—every hill, every fog pattern, every double-parked Uber—before expanding. Not because SF represents everywhere, but because mastering one city's complete complexity creates patterns that actually transfer. They didn't build a car that works sometimes everywhere; they built one that works always somewhere, then expanded that somewhere.

This is how autonomy scales: serve one customer to near-perfect autonomy, then modularize what made it possible. Take a few design partners and automate everything—not 80%, everything automatable. Learn their specific chaos completely. Then extract the patterns, build the modules, and only then expand to customer two.

The operational discipline is simple to say and hard to live. Baseline the work: touches per transaction, exception taxonomy, cycle time, SLA penalties, unit cost per closed case. Ship two or three flagship workflows. Publish reliability SLOs and error budgets. Do not expand until end-to-end success holds above 94% for sixty days with human intervention stable around 6%. Treat recurring exceptions as a product backlog: every week, retire the top two by converting them into tools, evals, or safety rails. Expand only when your primitives are demonstrably reusable. Reliability gates growth; never scale chaos.

This method can collapse per-customer configuration from ~2,000 lines to ~50. It's also the only path that preserves trust with customers and regulators. It looks slower. It is faster.

## The Competitive Moat

### Process power: the moat that compounds

What compounds across a portfolio is not model weights; it's process. Hamilton Helmer's "process power" is the accumulation of proprietary activity sets that produce outcomes competitors can't easily match. In autonomy, those activity sets are hardened tools (validators, negotiators, risk guards), golden datasets aligned to line-of-business SLAs, and eval harnesses that measure what matters: touches per case, exception rates, cycle times, safe-ops compliance.

Add to that governance that regulators actually prefer: rationale logs for consequential decisions, immutable audit trails, red-team harnesses for brittleness, drift monitors that trigger rollbacks. That bundle is a moat because it is operationally expensive for incumbents to copy. It requires cannibalizing internal fiefdoms and re-platforming processes near the core. It's counter-positioning: if they embrace it, they embarrass their org chart.

Stratechery's "end of the beginning" framing is helpful. Distribution moats won the last era. This one is about operations. The scarce asset isn't access to users; it's the capability to make non-deterministic systems dependable inside deterministic businesses. It's the difference between a demo and a decision you're willing to put your signature under.

## The New Capital Formation Model

### The Operator-PE archetype: underwriting the J-curve

The investor who will own this era's cost side looks different. The 1980s raider used debt and discipline—Milken's junk bonds enabling Icahn's raids. The 2000s activist used governance and metrics—Ackman's slides, Loeb's letters. The ESG steward used purpose and license—Fink's stakeholder capitalism. The AI-native operator uses capability installation: autonomy as an operating system, not a slide.

The early movers are already proving the model:
- Apollo: 40% cost reduction in content production at Cengage
- Blackstone: 50+ data scientists across 70 portfolio companies
- Carlyle: CEO calls AI "important driver of growth and scale"

But they're still thinking features, not architecture. The next wave will think differently.

The playbook starts before close. Select ops-heavy, document-heavy, compliance-heavy businesses with stable demand and measurable SLAs: insurance services (TPAs, SIU, subrogation), healthcare RCM and ASC/MSO platforms, specialty finance ops and regional banks, logistics brokers and 3PLs, back-office BPOs and field services roll-ups. Baseline the work, run shadow evaluations to estimate autonomy potential, and budget the J-curve of data, SOP, and governance. Write reliability gates into the plan.

Post-close, stand up a PlatformCo that runs the autonomy stack with strict data separation and cross-portfolio standards. Ship a small set of flagship workflows, publish SLOs, and refuse to expand until error budgets allow. Instrument everything. Turn exceptions into assets. Expand only when primitives are demonstrably reusable. Price outcomes rather than seats. Report margin manufacturing instead of vibes.

The cadence is dull by design: weekly throughput and exception burn-down; monthly capability backlog, governance review, drift and brittleness; quarterly expansion only when SLOs hold. Boring is a feature. It's also why it works.

## The Financial Engineering

### How the economics actually pencil

Autonomy's unit economics hinge on a few levers. Resuming from failure instead of repeating work bends cost curves. Semantic strategy retries—asking the same intent in different ways—often lifts success more than stuffing bigger contexts into bigger models. Session pools, caching, and pre/post invariants do more to stabilize runtime than switching models. And above all, reliability compounds throughput. A system that's 7–8x slower per operation but 94% reliable beats a 2-second sprint that fails 40% of the time, because only one of those will finish the job.

The financial engineering follows a pattern. Traditional PE looks at a business with 10% EBITDA margins and sees cost-cutting opportunities. AI-native PE sees something different: the ability to fundamentally restructure how work gets done. When SG&A can be transformed from human labor to compute, margin expansion isn't incremental—it's structural.

The key insight isn't about multiple expansion. It's about manufacturing margin through capability installation, then letting the market recognize that the cost structure has permanently changed.

## The Fund Structure

AI-Native Operator-PE Fund I:
- Size: $2-5B (sweet spot for operational transformation)
- Check size: $50-200M (control positions in $100-500M EV targets)
- Portfolio construction: 15-20 companies over 4 years
- Hold period: 3-5 years (J-curve requires patience)
- Team: 30% ex-operators, 30% engineers, 20% traditional PE, 20% domain experts
- Platform investment: $50M centralized infrastructure serving all portfolios

How you charge inside the portfolio matters. Per-outcome pricing—per claim adjudicated under SLA, per case resolved, per purchase order processed—aligns incentives. Labor-share models—say 25–40% of independently verified savings with floors and collars—make upside shared and downside bounded. "Autonomy credits," capacity-constrained bundles tied to reliability SLOs and audit guarantees, give you a unit that maps to throughput and governance. Seats and features are for demos. Throughput and reliability are for businesses.

## The Sector Playbooks

### Where the wedge shows up first

Insurance services already creak under intake volume, doc triage, and coverage validation. Agentic workflows that combine LLMs with vision and rules can compress cycle times and loss-adjustment expense. Subrogation discovery becomes a repeatable pattern when toolkits and evals are portfolio assets. Industry stats: $3/invoice processing cost, 30-45 day claims cycles, 15-30% expense ratios begging for compression.

Healthcare RCM remains a maze of prior auth, coding, and appeals. GenAI promises to do what v1 RPA never managed: handle the messy in-between of unstructured, multi-party workflows, if and only if governance and HITL are first-class. Done right, write-offs fall, DSO falls from 65 to 35 days, throughput climbs, and clinical edge cases get routed to humans—with explainable rationales the payer can accept. $125B wasted annually on administrative complexity.

Logistics brokers and 3PLs still burn human time on quoting, freight classing, and exception communications. Agentic AI can handle most of this with higher reliability than selectors, especially when session pools and semantic retries are standard. The payoff is fewer touches per load and faster cash cycles. C.H. Robinson already using agents for LTL classification.

Specialty finance ops and regional banks grapple with KYC/KYB, servicing, and collections atop legacy cores that will not modernize on your timeline. Wrapping core functions with API shells and installing autonomy at the edges—backed by rationale logs and safe-ops gates—improves compliance optics while cutting opex. Regulators care less about your adjectives than your audit trails. 40-year-old core systems, $2-3M annual maintenance, 60% manual processes.

Back-office BPOs are the cleanest arbitrage: transition pricing from seats to outcomes and turn a services multiple into a software-enabled margin story—without pretending you're a software company.

## The Risk Management

### Governance is a product surface

If Matt Levine's ambient rule is that "anything bad is also securities fraud," then safety is not a memo. Reliability SLOs and error budgets must gate expansion. Red-team harnesses should break your own system on purpose. Drift and brittleness dashboards should trigger rollbacks without a meeting. High-risk operations should have pre-approved human gates and immutable consent logs. Every consequential decision should be explainable after the fact with inputs, outputs, and rationale.

Treat governance as product and it accelerates go-lives, especially in regulated domains. Treat it as theater and it will slow you down precisely when you most need speed.

### Risks, failure modes, and how adults handle them

Models drift, UIs change, vendors have bad days. Multi-model strategies with evaluation-backed selection and reserved capacity are not luxuries; they're table stakes. On-prem and regional redundancy matters more than a press release. Change monitors on critical surfaces should be cheap and loud.

Legal and regulatory incidents are mitigated by safe-ops subsets, human-approval gates, and evidentiary logs. Change resistance inside the business is met with earnouts tied to verified savings, a Transition Council for job redesign, and real budgets for reskilling and redeployment. This is autonomy with a social license, not Taylorism with better branding.

## The Platform Extraction

### From portfolio to platform

The genius isn't in the first fund—it's in what emerges from it. After 15-20 implementations, patterns crystallize:
- Tool orchestration becomes a service
- Context management becomes a framework
- Durable execution becomes infrastructure
- Governance becomes a product

This is the AWS moment: what you built for yourself becomes what everyone needs. The portfolio companies become the proof points. The PlatformCo becomes the product. The fund returns become the appetizer. The platform exit becomes the meal.

The platform extraction opportunity is compelling. After multiple implementations, the patterns crystallize into reusable infrastructure. What starts as portfolio optimization becomes a platform play—the AWS moment where internal tools become the product.

## The Historical Moment

### The new control operator

This archetype isn't "consulting with AI." It is a repeatable capability: AI orchestrating software; durable execution and curated context; safety and audit on the hot path; humans designed in rather than duct-taped on. It manufactures margin and sells throughput with reliability SLOs. It compounds process power across properties. It builds a PlatformCo that acts more like a shared operating system than a center of excellence. It exits when the market can see that the cost per transaction is structurally lower and the SLA is structurally higher.

It looks, from the outside, like certainty. Inside, it feels like humility: stop fighting reality, and architect for it.

We're at a unique moment. The technology has reached production viability—94% autonomous completion is achievable with the right architecture. The economics are becoming clear as early implementations demonstrate the value creation potential. The arbitrage between labor costs and compute costs represents one of the largest economic transformations in history. The capital markets are ready with unprecedented dry powder. The talent pool is forming from multiple sources—engineers who've learned the hard lessons, operators who've seen what works, and a workforce in transition.

Most importantly, the social contract is breaking anyway. 40% of white-collar workers can't get interviews. The Department of Government Efficiency is offering federal buyouts. The white-collar recession is here. The only question is who captures the value: the companies being disrupted, the workers being displaced, or the operators installing the future.

## The Emerging Patterns

The industry is discovering several truths simultaneously. Builders are learning that selling outcomes under SLOs works better than selling features and seats. The inversion—letting agents decide flow while software provides tools—is becoming standard practice. The focus is shifting from context maximization to better retrieval and tool design.

Operators are learning to underwrite the J-curve of transformation. They're discovering that reliability must be boring and governance must be a product surface, not compliance theater. The margin manufacturing happens through capability installation, not cost cutting.

Capital allocators are seeking teams that understand both the technical reality of production AI and the financial engineering of operational transformation. The best teams emerge from the intersection—those who've lived through the production reality and understand the economic opportunity.

The 3 AM discovery—that AI should orchestrate software rather than be embedded in it—feels obvious in retrospect. Yet it represents a fundamental shift in how we think about autonomous systems.

The choice facing the industry is between building another vertical SaaS or creating the substrate for autonomous work itself. One path is well-understood. The other is still being written.

---

The patterns are becoming clear. Reliability gates expansion. Exceptions become a product backlog. Governance transforms from burden to feature. Humans aren't bugs in the system—they're part of its design.

The next KKR won't be built on Madison Avenue. It will be built by those who understand that exhaustion teaches what brilliance cannot: the difference between what should work and what actually does. The transformation of compute into labor isn't just a technical achievement—it's an economic restructuring waiting to happen.