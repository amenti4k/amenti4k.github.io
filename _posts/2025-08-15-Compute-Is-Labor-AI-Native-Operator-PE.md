---
layout: post
title: "Compute Is Labor: How AI-Native Operator-PE Will Reprice the Cost Side of the Economy"
date: 2025-08-15
categories: [ai, economics, private-equity]
tags: [ai, automation, private-equity, labor-economics, autonomous-work]
excerpt: "The thing that changes you isn't brilliance; it's exhaustion. It's 11:30 PM, another workflow has failed, and you're staring at a dashboard that feels like a mirror. The discovery that AI should orchestrate software—not be embedded in it—revealed an uncomfortable economic truth: we weren't selling software features; we were replacing labor."
---

# Compute Is Labor: How AI-Native Operator-PE Will Reprice the Cost Side of the Economy

## The Discovery

The thing that changes you isn't brilliance; it's exhaustion. It's 11:30 PM, another workflow has failed, and I'm staring at a dashboard that feels like a mirror. Every knob I added to save myself yesterday is the debt I'll pay tomorrow. Every "customer-specific flag" is an IOU from reality. I've been building AI systems the way we build software systems: deterministic flows that call "smart" functions. Then someone, half-asleep on Slack, asks the question that flips the room: why are we still telling the AI what to do? Isn't that literally its job?

That inversion—letting AI orchestrate software rather than embedding AI inside software—wasn't a philosophical shift. It was survival. As I detailed in ["Building on Quicksand"](/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html), it dissolved a thousand brittle configurations into a handful of durable capabilities. It turned failure from catastrophe into state. It made the system honest about its nature: a distributed system where one of the services is non-deterministic.

It also revealed an uncomfortable economic truth. The industry isn't selling software features; it's replacing labor. The capture rate is minimal because the market doesn't know how to price this fundamental transformation.

What follows is the economic thesis built on that discovery: a new type of private equity firm that doesn't just cut costs but fundamentally changes how work gets done. Instead of selling software to companies, they buy companies and replace the actual work with AI. This isn't another tech-enabled buyout shop. It's something new: firms that understand automation as infrastructure, not product.

## The $10 Trillion Mispricing

### The mispricing of autonomy

The numbers reveal an interesting dynamic. When procurement flows become truly autonomous, end-to-end success can stabilize around 94% with a deliberately designed 6% human-in-the-loop for genuine novelty. The economic transformation is striking: what once required significant human labor converts into compute and resilient workflows. Yet the market struggles to price this transformation—there's a massive gap between the value created and what the market will pay for automation tools.

The macro numbers are staggering: Goldman Sachs projects AI could replace 300 million full-time jobs globally. McKinsey estimates $2.6-4.4 trillion in annual value creation. In January 2025, professional services job openings hit 13-year lows while 40% of white-collar job seekers couldn't secure a single interview. The white-collar recession isn't coming—it's here.

Why is that wedge so large? Because the market still thinks "software using AI," not "AI using software." Buyers anchor on seat counts and feature lists; they do not price throughput under reliability SLAs. CFOs will happily pay for buttons, less so for fewer humans. Boards will applaud a demo; they will defer the messy process refactor that turns the demo into dependable throughput.

The mispricing persists because making AI actually work is messy: cleaning data, rewriting processes, managing change, building safety rails. Most management teams will postpone this pain forever. But if you own the company? You can force the transition.

This new type of PE firm doesn't wait for adoption. They buy the company and install the automation themselves. They're not selling the future—they're building it inside portfolio companies.

## The Production Truth

### Why the demos lie—and what finally works

As I wrote in ["Building on Quicksand"](/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html), the production reality is harsh: the seductive demo of a perfect extraction gives way to 1,000+ configuration flags, retries of retries, and a hall of mirrors called "fallback logic." The architectural inversion I discovered—letting AI orchestrate software rather than embedding AI in pipelines—was survival, not philosophy.

What worked was simple: give AI a toolbox and let it figure out what to use. Instead of programming every step, we gave it actions it could take—parse this, check that budget, get human approval—and let it decide the order. When things failed (and they always fail), the system remembered where it was and picked up from there, not from the beginning. This one change—resuming from failure instead of starting over—cut our costs by 90%.

At scale, the economics become clear. Durable execution fundamentally changes the cost structure by eliminating redundant work. The difference between retry-from-zero and resume-from-failure isn't just technical elegance—it's the difference between sustainable unit economics and burning capital.

My work with [Stagehand](/2025/08/12/stagehand-browser-automation-production.html) proved the same pattern in browser automation. Traditional RPA breaks when a button's class changes from `submit-btn` to `submit-button`. Semantic actions—"Click the Submit button," "Open purchase order A300807"—plus strategy retries, session pooling, and observability flipped the reliability curve. Per operation, AI-powered RPA was 7–8x slower. End-to-end, it completed 11x more work. Reliability, not raw speed, is the shape of production truth.

These aren't anecdotes; they're the mechanics of autonomy in brownfield environments. They are the only route that scales beyond a handful of bespoke heroes and late-night Slack channels.

## The Technical Architecture

### The Autonomous Work Stack: how compute becomes labor

Once you accept the inversion, the system almost designs itself.

The architecture is straightforward: AI at the top deciding what to do next, software tools it can call to get things done. Each tool is simple and safe—it does one thing and can't break anything else. When something fails, the system doesn't panic or start over. It just tries again from where it left off, like a human would.

You don't dump everything into the AI and hope. You give it patterns—this customer usually orders 50 units, these items go together, this person approves purchases over $10K. Then you give it a way to look up specific things when needed. It's like the difference between memorizing every street in a city versus having a map and a phone.

Dangerous operations—sending money, mass emails, deleting records—trigger human review. Not as an error, but as a designed checkpoint. The system says: "I want to send $50K to this vendor, here's why, click to approve." Every decision, whether AI or human, gets logged with the reasoning.

Humans aren't a fallback; they're part of the system. Tasks arrive where people live (often email) with one-click actions that flow back into the workflow. The point isn't to eliminate people; it's to elevate them to the 6–10% of cases where their judgment compounds value rather than mops up ambiguity.

You log everything. Screenshots, decisions, reasoning. Not for compliance theater but for survival. When something breaks at 3 AM, you need to see exactly what the AI saw and why it did what it did. When the auditor asks why you paid that invoice twice, you need an answer better than "the AI thought it was right."

This setup turns compute into reliable workers. Instead of thousands of special cases and exceptions, you have a few dozen tools that combine in different ways. Instead of burning money retrying from scratch, you resume from failure. The system has strong opinions about safety and reliability, but doesn't care about your specific business logic.

## The Operating Philosophy

### Serve one, then scale: the only honest way to grow

The internet taught us to scale abstractions; autonomy teaches us to scale reliability. The path mirrors Waymo's strategy: they mastered San Francisco's chaos—every hill, every fog pattern, every double-parked Uber—before expanding. Not because SF represents everywhere, but because mastering one city's complete complexity creates patterns that actually transfer. They didn't build a car that works sometimes everywhere; they built one that works always somewhere, then expanded that somewhere.

This is how autonomy scales: serve one customer to near-perfect autonomy, then modularize what made it possible. Take a few design partners and automate everything—not 80%, everything automatable. Learn their specific chaos completely. Then extract the patterns, build the modules, and only then expand to customer two.

The discipline is brutal but simple. Measure everything: how many times humans touch each order, what breaks, how long things take. Start with just two or three workflows. Don't add more until those work 94% of the time for two months straight. Every week, take the top two things that keep breaking and fix them permanently. Only grow when your tools work for multiple customers without changes. Never scale chaos.

This method can collapse per-customer configuration from ~2,000 lines to ~50. It's also the only path that preserves trust with customers and regulators. It looks slower. It is faster.

## The Competitive Moat

### Process power: the moat that compounds

What matters isn't having the best AI model—everyone uses the same ones anyway. What matters is the boring stuff: tools that actually work, data that's actually clean, measurements that actually matter. After you've processed a million insurance claims, you know exactly what breaks and how to fix it. After you've automated a hundred workflows, you have tools that work everywhere.

This experience compounds. Every implementation teaches you what fails. Every failure becomes a permanent fix. Every fix works for the next customer. Competitors can copy your prompts but they can't copy two years of fixing edge cases.

The moat isn't technology. It's knowing that insurance companies need 48-hour claim processing but logistics companies need 4-hour quotes. It's having already built the tool that handles both. It's the difference between a demo that works once and a system that works every day.

## The New Capital Formation Model

### The Operator-PE archetype: underwriting the J-curve

The investor who wins this era looks different. The 1980s raiders used debt to buy companies and cut costs. The 2000s activists used PowerPoints to demand changes. The ESG crowd used social pressure. The AI-native operator does something new: they buy companies and replace the work itself.

The early movers are already proving the model:
- Apollo: 40% cost reduction in content production at Cengage
- Blackstone: 50+ data scientists across 70 portfolio companies
- Carlyle: CEO calls AI "important driver of growth and scale"

But they're still thinking features, not architecture. The next wave will think differently.

The playbook is straightforward. Buy businesses drowning in paperwork: insurance claims processors, medical billing companies, freight brokers, back-office outsourcers. Before buying, measure exactly what humans do all day. Count every email, every data entry, every approval.

After buying, install the same automation stack everywhere. Start with three workflows that cause the most pain. Don't add more until those three work perfectly. Track everything that breaks. Fix it. When something works at one company, use it at all of them. Charge for results, not software licenses.

The cadence is dull by design: weekly throughput and exception burn-down; monthly capability backlog, governance review, drift and brittleness; quarterly expansion only when SLOs hold. Boring is a feature. It's also why it works.

## The Financial Engineering

### How the economics actually pencil

The economics are counterintuitive. Our AI is 7-8x slower than traditional automation per operation. But it works 94% of the time versus 40%. Do the math: slow and reliable processes more work than fast and broken. When something fails, asking the same question differently often works better than using a smarter model. Keeping browser sessions open saves more money than you'd think. The boring optimizations matter more than the fancy ones.

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

Pricing should match reality. Charge per claim processed, per invoice paid, per order fulfilled. Or take a percentage of the labor costs eliminated. Don't charge for software seats or features—charge for work completed. A processed claim is worth $50 whether a human or AI does it. That's the price.

## The Sector Playbooks

### Where the wedge shows up first

Insurance services already creak under intake volume, doc triage, and coverage validation. Agentic workflows that combine LLMs with vision and rules can compress cycle times and loss-adjustment expense. Subrogation discovery becomes a repeatable pattern when toolkits and evals are portfolio assets. Industry stats: $3/invoice processing cost, 30-45 day claims cycles, 15-30% expense ratios begging for compression.

Healthcare RCM remains a maze of prior auth, coding, and appeals. GenAI promises to do what v1 RPA never managed: handle the messy in-between of unstructured, multi-party workflows, if and only if governance and HITL are first-class. Done right, write-offs fall, DSO falls from 65 to 35 days, throughput climbs, and clinical edge cases get routed to humans—with explainable rationales the payer can accept. $125B wasted annually on administrative complexity.

Logistics brokers and 3PLs still burn human time on quoting, freight classing, and exception communications. Agentic AI can handle most of this with higher reliability than selectors, especially when session pools and semantic retries are standard. The payoff is fewer touches per load and faster cash cycles. C.H. Robinson already using agents for LTL classification.

Specialty finance ops and regional banks grapple with KYC/KYB, servicing, and collections atop legacy cores that will not modernize on your timeline. Wrapping core functions with API shells and installing autonomy at the edges—backed by rationale logs and safe-ops gates—improves compliance optics while cutting opex. Regulators care less about your adjectives than your audit trails. 40-year-old core systems, $2-3M annual maintenance, 60% manual processes.

Back-office BPOs are the cleanest arbitrage: transition pricing from seats to outcomes and turn a services multiple into a software-enabled margin story—without pretending you're a software company.

## The Risk Management

### Governance is a product surface

As Matt Levine says, "anything bad is also securities fraud." So safety isn't optional. Set reliability targets and don't expand until you hit them. Break your own system on purpose to find weaknesses. When things drift, roll back immediately. Put humans in the loop for anything involving money. Log every decision with enough detail that a lawyer could defend it.

Treat governance as product and it accelerates go-lives, especially in regulated domains. Treat it as theater and it will slow you down precisely when you most need speed.

### Risks, failure modes, and how adults handle them

Everything that can break will break. AI models change behavior overnight. Websites redesign without warning. APIs go down. You need backup models, backup regions, backup everything. Monitor the pages you depend on. When they change, alarms should go off. This isn't paranoia—it's Thursday.

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

This isn't McKinsey with ChatGPT. It's a repeatable system: AI running the show, software as its tools, humans as quality control. It doesn't cut costs—it eliminates work. It doesn't optimize margins—it restructures them. The platform built for portfolio companies becomes more valuable than the companies themselves. The exit comes when the market realizes the cost structure has permanently changed.

It looks, from the outside, like certainty. Inside, it feels like humility: stop fighting reality, and architect for it.

We're at a unique moment. The technology has reached production viability—94% autonomous completion is achievable with the right architecture. The economics are becoming clear as early implementations demonstrate the value creation potential. The arbitrage between labor costs and compute costs represents one of the largest economic transformations in history. The capital markets are ready with unprecedented dry powder. The talent pool is forming from multiple sources—engineers who've learned the hard lessons, operators who've seen what works, and a workforce in transition.

Most importantly, the social contract is breaking anyway. 40% of white-collar workers can't get interviews. The Department of Government Efficiency is offering federal buyouts. The white-collar recession is here. The only question is who captures the value: the companies being disrupted, the workers being displaced, or the operators installing the future.

## The Emerging Patterns

The industry is waking up to several truths at once. Builders are learning to sell work completed, not software seats. The inversion—letting AI run things instead of following scripts—is becoming obvious. Everyone's realizing that giving AI everything doesn't work; giving it the right things does.

Operators are learning that transformation hurts before it helps. They're discovering that boring reliability beats exciting features. That real governance means tracking decisions, not writing memos. That margin comes from doing less work, not paying less for it.

Money is looking for teams who've been in the trenches. Not AI researchers or McKinsey partners, but people who've actually made this stuff work at 3 AM when everything's on fire. People who understand both why the AI failed and why the invoice still needs to be paid.

The 3 AM discovery—that AI should orchestrate software rather than be embedded in it—feels obvious in retrospect. Yet it represents a fundamental shift in how we think about autonomous systems.

The choice facing the industry is between building another vertical SaaS or creating the substrate for autonomous work itself. One path is well-understood. The other is still being written.

---

The patterns are becoming clear. Reliability gates expansion. Exceptions become a product backlog. Governance transforms from burden to feature. Humans aren't bugs in the system—they're part of its design.

The next KKR won't be built on Madison Avenue. It will be built by those who understand that exhaustion teaches what brilliance cannot: the difference between what should work and what actually does. The transformation of compute into labor isn't just a technical achievement—it's an economic restructuring waiting to happen.