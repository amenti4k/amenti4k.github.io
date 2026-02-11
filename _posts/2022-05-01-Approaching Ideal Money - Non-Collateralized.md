---
layout: post
title: "Part 1 - Are Algorithmic Stablecoins Possible? Mapping the Design Space of Digital Money"
date: 2022-05-01
tags: [research]
---

*This is Part 1 of a two-part deep dive into algorithmic stablecoins, drawn from my undergraduate research. This essay maps the design space and builds the theoretical framework. [Part 2](/2022/05/02/Algorithmic-Stablecoin-Issues.html) dives into specific implementations, from Hayek Money to FRAX, with statistical validation.*

---

## Money Is Technology

Here's a question most people don't ask: what makes money, money?

Not "what gives money value." That's Econ 101. I mean the *design* question. When you strip away thousands of years of convention, money is a piece of technology. It's an information system designed to solve three problems simultaneously: measuring value (unit of account), storing value across time (store of value), and enabling exchange (medium of exchange).

Every monetary system in history (cowrie shells, gold coins, tally sticks, paper notes, digital entries on a bank's server) is a different engineering attempt at solving these three problems. And every single one involved design tradeoffs.

Gold was scarce, durable, and verifiable, making it a remarkable store of value. But gold is heavy and hard to subdivide. Try buying bread with gold dust. So we invented gold certificates: paper IOUs backed by physical metal in a vault. Far more convenient, but now you've introduced a dependency. You have to trust the vault operator. Then governments centralized these vaults into central banks, and we had to trust those institutions instead.

In 1944, the Bretton Woods agreement formalized this into a global hierarchy. Forty-four nations pegged their currencies to the US dollar at fixed exchange rates, and the dollar was pegged to gold at $35 per ounce. A nested chain of trust: you trust your local currency, your currency trusts the dollar, the dollar trusts gold.

Then on August 15, 1971, Nixon unilaterally closed the gold window. The dollar was no longer redeemable for gold. By March 1973, the entire fixed exchange rate system had collapsed into floating rates. We went from "your money represents gold" to "your money is good because we say so." Pure fiat.

Here's the remarkable thing: it worked. The dollar didn't collapse. The global economy kept growing. This suggests something deep about money: it doesn't actually *need* intrinsic backing to function. It needs sufficient collective trust. Thomas Schelling would call the $1 value a "focal point" — a coordination equilibrium that holds because everyone expects it to hold. The gold was always a coordination device, not the actual source of value.

This brings us to the present question. Bitcoin proved in 2009 that you could create a monetary system without any central authority. No government, no central bank, no trusted vault operator. Just code and cryptography. But Bitcoin's volatility, routinely swinging 10-20% in a single day, makes it impractical as everyday money. You can't price a hamburger in something that might cost twice as much by dinner.

Stablecoins emerged as the answer: digital currencies pegged to a stable reference, usually $1 USD. By early 2022, the stablecoin market has grown to over $160 billion. But the design space for building them is far larger and more varied than most people realize, and the design choices matter enormously.

So let me map it out.

---

## The Impossible Trilemma: Stablecoins' Fundamental Constraint

In the early 1960s, economists Robert Mundell and Marcus Fleming independently developed what became known as the "Impossible Trinity": a country cannot simultaneously maintain free capital flows, a fixed exchange rate, and an independent monetary policy. You get to pick any two. Never all three.

The United States post-1971 chose free capital flows and independent monetary policy, sacrificing fixed exchange rates (the dollar floats). China for decades chose a fixed exchange rate and independent monetary policy, sacrificing free capital flows (strict capital controls). Eurozone members chose free capital flows and fixed exchange rates (the euro), sacrificing independent monetary policy (the ECB controls rates for everyone).

I argue this maps directly onto stablecoins, but with different vertices. The stablecoin trilemma:

1. **Price Stability** — maintaining a reliable peg
2. **Decentralization** — no central party that can freeze funds, censor transactions, or be shut down by regulators
3. **Capital Efficiency** — not requiring more collateral locked up than the value created

```
The Stablecoin Trilemma:

                        Price Stability
                              △
                             ╱ ╲
                            ╱   ╲
                           ╱     ╲
                  USDC/   ╱  ???   ╲   DAI
                  USDT   ╱         ╲   MakerDAO
                        ╱           ╲
                       ╱             ╲
                      ▽───────────────▽
              Capital                   Decentralization
              Efficiency

    USDC/USDT: Stable + Efficient, but Centralized
      → Circle/Tether can freeze your funds
      → Regulators can shut them down
      → You're trusting traditional banks

    DAI: Stable + Decentralized, but Inefficient
      → Requires 150%+ collateral in smart contracts
      → $1.50 locked to create $1 of stablecoin
      → Limits scalability

    Algorithmic: Efficient + Decentralized, but... Stable?
      → The trillion-dollar question
```

Every stablecoin project is essentially choosing which vertex to sacrifice, or more ambitiously, trying to optimize all three. The history of algorithmic stablecoins is largely a history of attempts to cheat the trilemma.

---

## A Taxonomy of Stablecoins

Before we can evaluate whether algorithmic stablecoins can work, we need a proper map of the design space. Through my research, I found it useful to classify stablecoins across four independent axes:

**Axis 1: What Are You Pegged To?**

Not all stablecoins target $1 USD. The peg target is itself a design choice:

- **Fiat currency**: Most common. USDC, USDT, DAI all target $1 USD. Simple and legible, but tethers you to the monetary policy of the underlying fiat.
- **Commodity**: Paxos Gold (PAXG) pegs to one troy ounce of gold. Real asset backing, but inherits commodities' volatility.
- **Consumer Price Index (CPI)**: The theoretical ideal. Track purchasing power directly rather than a single currency. A CPI-pegged stablecoin would maintain your ability to buy a fixed basket of goods, regardless of what happens to the dollar. FRAX has explored this direction.
- **Cryptocurrency basket**: Target relative stability within crypto. Less common, niche use cases.

The distinction between pegging to USD and pegging to CPI is more important than it seems. A dollar-pegged stablecoin inherits inflation. If the dollar loses 3% purchasing power per year, so does your stablecoin. A CPI-pegged stablecoin would actually maintain purchasing power over time, getting closer to Nash's vision of ideal money. More on this in Part 2.

**Axis 2: What Type of Collateral?**

- **Fiat / traditional assets**: USD in a bank account. USDC holds cash and short-term US treasuries. USDT claims a mix of cash, commercial paper, and other assets. Simple but centralized.
- **Cryptocurrency**: ETH, BTC, or other crypto assets locked in smart contracts. DAI pioneered this through MakerDAO's Collateralized Debt Positions (CDPs). Decentralized but volatile collateral introduces liquidation risk.
- **Commodity**: Physical gold in vaults (PAXG). Combines real-world asset stability with crypto accessibility, but requires trusted custodians.
- **Endogenous / algorithmic**: The protocol's own governance token or pure algorithmic mechanisms. Ampleforth uses rebasing. Basis used bonds and shares. FRAX uses a mix of USDC collateral and burned FXS governance tokens. This is where things get creative — and dangerous.

**Axis 3: How Much Collateral?**

This might be the most consequential design choice:

- **Over-collateralized (>100%)**: DAI requires 150%+ collateral. If you deposit $150 in ETH, you can mint at most $100 DAI. Safe but capital-inefficient. $1.50 of value sitting idle for every $1 of stablecoin.
- **Fully collateralized (100%)**: USDC claims 1:1 dollar backing. Each USDC in circulation has $1 sitting in a bank account (or in short-term treasuries). Capital efficient relative to over-collateralization, but still ties up dollar-for-dollar.
- **Fractionally collateralized (<100%)**: FRAX operates at roughly 85% collateral ratio, where each FRAX is backed by $0.85 in real collateral plus $0.15 in algorithmic mechanisms. This is the interesting middle ground.
- **Non-collateralized (0%)**: Pure algorithmic. AMPL, Basis, Empty Set Dollar. No collateral backing whatsoever. Stability comes entirely from mechanism design and incentives. This is crypto's holy grail and its biggest graveyard.

**Axis 4: Who Governs?**

- **Centralized entity**: Circle (USDC), Tether Limited (USDT). A company makes decisions, holds reserves, can blacklist addresses. Regulatory clarity but defeats crypto's core premise.
- **DAO governance**: MakerDAO (DAI), Frax Share holders (FXS). Token holders vote on parameters like collateral ratios, accepted collateral types, stability fees. Decentralized but slow and susceptible to governance attacks.
- **Algorithmic / autonomous**: Hard-coded rules with minimal or no governance override. Ampleforth's rebase mechanism runs automatically based on oracle price feeds. Maximally decentralized but inflexible when things go wrong.

```
Stablecoin Design Space:

                  Centralized ←── Governance ──→ Algorithmic
                       │                              │
Over-collateralized    │             DAI              │
  (>100%)              │          (MakerDAO)          │
                       │                              │
Fully collateralized ──┤── USDC, USDT                 │
  (100%)               │                              │
                       │                              │
Fractional ────────────┤────────────── FRAX ──────────│
  (<100%)              │                              │
                       │                              │
Non-collateralized ────┤──────── Basis ───── AMPL, ESD│
  (0%)                 │                              │
                       │                              │

       ↑ Less risk, less capital efficient
       ↓ More risk, more capital efficient
```

This taxonomy reveals something important: as you move toward the bottom-right corner (less collateral, more algorithmic governance) you gain capital efficiency and decentralization but lose the safety nets that prevent catastrophic failure. The entire bottom-right quadrant is littered with failed experiments.

---

## The Landscape: $160 Billion and Counting

As of early 2022, the stablecoin market tells a clear story about which designs have survived.

Tether (USDT), launched in 2014 as the first major stablecoin, dominates with approximately $80 billion in market cap. It's the simplest possible design: fiat in a bank account, tokens on a blockchain. It's also the most controversial, with persistent questions about its actual reserve composition. Circle's USDC, launched in 2018 with a focus on regulatory compliance and transparent attestations, holds roughly $50 billion. Together, these two centralized, fully-collateralized stablecoins account for over 80% of the entire market.

MakerDAO's DAI, the largest decentralized stablecoin, sits at around $10 billion. It achieves decentralization through over-collateralization. Users lock ETH or other approved crypto assets worth at least 150% of the DAI they mint in Collateralized Debt Positions. If the collateral value drops too close to the debt, the position gets automatically liquidated. It works, but the capital inefficiency is brutal. To support $10 billion in stablecoins, you need $15+ billion in collateral sitting there doing nothing else.

FRAX, launched in December 2020, has grown to roughly $2.5 billion in market cap. It's the largest fractional-algorithmic stablecoin, operating at approximately 85% collateral ratio. Each FRAX is backed by $0.85 in USDC and $0.15 in burned FXS governance tokens. The ratio adjusts algorithmically based on market demand.

Then there's the algorithmic end of the spectrum. Ampleforth, which launched in 2019 and implements daily supply rebasing. Empty Set Dollar (ESD), which launched in August 2020 and has struggled to maintain peg stability. Fei Protocol, which locked up $1.3 billion in ETH during its April 2021 launch only to immediately break below peg due to a flawed incentive mechanism. And dozens of other experiments that have launched, struggled, and often died.

The pattern is stark. The closer to "pure algorithmic," the lower the survival rate. This isn't coincidence. It reflects a deep structural vulnerability that I think is best understood through the lens of bank runs.

---

## Bank Runs at the Speed of Code

In 1983, economists Douglas Diamond and Philip Dybvig published what became one of the most influential models in financial economics. Their model demonstrated that bank runs are self-fulfilling prophecies: if depositors believe others will withdraw, it's rational for each individual to withdraw too, even if the bank is fundamentally solvent. The mere *expectation* of a run causes the run. The equilibrium is fragile; confidence is a coordination game, and "everyone trusts the bank" and "everyone runs on the bank" are both stable equilibria. The question is which one you're in.

Traditional banks manage this through external backstops: FDIC deposit insurance (guaranteeing $250,000 per depositor), the Federal Reserve's discount window (lender of last resort), and suspension of convertibility in emergencies. These are trust anchors outside the system itself. They exist precisely to make the "bank run" equilibrium inaccessible.

Algorithmic stablecoins have none of these. When confidence wavers, there's no Fed to step in. No deposit insurance. No circuit breakers. And because blockchain transactions are global, permissionless, and operate 24/7, the feedback loop between falling confidence and falling price operates at the speed of code — not the speed of humans standing in line outside a bank branch.

The dynamics look like this:

1. Some external shock pushes the stablecoin slightly below peg
2. Holders start selling, pushing the price further down
3. The protocol's stabilization mechanism kicks in (burning tokens, issuing bonds, adjusting supply)
4. If the mechanism isn't fast or credible enough, more holders lose confidence
5. The selling overwhelms the mechanism
6. The mechanism itself becomes a source of panic (e.g., flooding the market with governance tokens to fund redemptions)
7. Complete collapse

```
Confidence Dynamics in Algorithmic Stablecoins:

  Stable State          Wobble              Death Spiral

  ┌─────────┐      ┌───────────┐      ┌──────────────────┐
  │ Price    │      │ Price     │      │ Price drops      │
  │ = $1.00 │─────>│ = $0.97   │─────>│ = $0.50 → $0.01 │
  │         │      │           │      │                  │
  │ Trust   │      │ Some sell │      │ Everyone sells   │
  │ = High  │      │ ↓         │      │ ↓                │
  │         │      │ Mechanism │      │ Mechanism fails  │
  │ Mech.   │      │ activates │      │ or accelerates   │
  │ = Idle  │      │ ↓         │      │ the collapse     │
  └─────────┘      │ Recovery? │      │ ↓                │
                   └─────┬─────┘      │ No recovery      │
                         │            └──────────────────┘
                    IF mechanism
                    is credible:      IF mechanism is too
                    → Return to       slow or not credible:
                      stable state    → Death spiral
```

Thomas Schelling's concept of focal points is central to understanding why this happens. In his 1960 book "The Strategy of Conflict," Schelling showed that coordination equilibria often depend on shared expectations rather than fundamental value. The $1 peg is a Schelling focal point: everyone values 1 stablecoin at $1 because everyone else does.

But unlike the dollar in your wallet, which has the US military, the IRS, legal tender laws, and 250 years of institutional credibility reinforcing its focal point, an algorithmic stablecoin's focal point can shatter in hours. The coordination equilibrium has no external anchor.

The June 2021 collapse of Iron Finance's TITAN token demonstrated this vividly. Iron Finance operated a partially-collateralized model: IRON stablecoin backed by 75% USDC and 25% TITAN governance token. On June 16, large holders began selling TITAN. The price dropped, reducing the effective collateral behind IRON. This triggered IRON redemptions, which required minting new TITAN to pay the 25% algorithmic portion, flooding the market with TITAN and crashing its price further. A textbook reflexive spiral. TITAN went from $65 to near-zero in under 24 hours.

The design worked exactly as coded. The design itself was the problem.

---

## Why Build Algorithmic Stablecoins At All?

Given all this (the failed experiments, the death spirals, the structural vulnerabilities) why would anyone try to build a non-collateralized algorithmic stablecoin? Is the whole endeavor futile?

I don't think so. And the answer requires stepping back to first principles.

**The Case from Monetary Theory**

John Nash — yes, the "Beautiful Mind" Nash — spent the last decades of his life working on a concept he called "Ideal Money." His argument: money should maintain stable purchasing power over time without being subject to political manipulation. Government-controlled fiat systematically fails this test because governments have persistent incentives to inflate. It's easier to print money than to raise taxes or cut spending. Nash proposed that currencies could evolve toward an ideal standard through competitive pressure. Currencies that depreciate too fast would lose users to more stable alternatives.

Friedrich Hayek made a parallel argument in his 1976 book "Denationalisation of Money." Hayek proposed eliminating the government monopoly on money entirely. Private institutions would issue competing currencies, and market forces would reward those maintaining the most stable purchasing power. The mechanism would be Gresham's Law in reverse. Rather than "bad money drives out good" (which applies when exchange rates are fixed by law), free competition would let good money drive out bad. Users would voluntarily migrate to currencies that best preserve their purchasing power.

Algorithmic stablecoins are the first serious attempt to build Hayek's vision. Not metaphorically — literally. Private, competing, non-governmental currencies, algorithmically governed, available globally to anyone with an internet connection.

**The Case from Capital Efficiency**

DAI's over-collateralization model doesn't scale. Locking up $150 to create $100 in stablecoins means the stablecoin market can never exceed the available collateral pool. And that collateral is doing nothing productive while it sits in CDPs. It's dead capital. At $10 billion DAI outstanding, that's $15+ billion of ETH immobilized.

Algorithmic stablecoins, if they work, could create stable money without locking up any capital. Infinitely scalable in theory. This matters if you believe stablecoins should eventually serve the global economy, not just DeFi traders.

**The Case from Decentralization**

USDC has a blacklist function. Circle can freeze any address holding USDC, and has done so, complying with law enforcement requests. Tether has done the same. This means fiat-backed stablecoins aren't censorship-resistant. They inherit the control structures of the traditional financial system. If your use case requires genuinely permissionless money (no admin keys, no blacklist, no single point of regulatory capture) then centralized stablecoins are fundamentally unsuitable.

**The Case from History**

Here's the argument I find most compelling: the US dollar itself followed the exact trajectory that fractional-algorithmic stablecoins are attempting.

The dollar started fully backed by gold. The Bretton Woods system was, structurally, a "fractional-collateralized stablecoin": $35 per ounce of gold, with the US holding gold reserves that backed only a fraction of total dollars in circulation. The collateral ratio declined steadily through the 1950s and 1960s as dollars proliferated faster than gold reserves grew. When the collateral was removed entirely in 1971, the system survived. Not because the mechanism was sound (though it was), but because sufficient trust had been built over decades.

If a national currency can graduate from full collateral to zero collateral, why can't a digital one?

The counterargument is obvious: the dollar had the US military, the IRS, legal tender laws, and two centuries of institutional credibility backing the transition. An algorithmic stablecoin has code and game theory.

But that's exactly what makes this interesting. It's a test of whether carefully designed incentive mechanisms can generate sufficient trust to sustain a monetary system without traditional enforcement infrastructure. And if FRAX's early trajectory is any guide, maintaining 97% peg stability with only 85% collateral, the answer might be yes, with the right approach.

---

## So, Are Algorithmic Stablecoins Possible?

After a year of research, my answer is: yes, but with a critical caveat.

Pure algorithmic stablecoins (zero collateral from day one, stability maintained entirely through incentive mechanisms) have a near-zero survival rate. The evidence from Basis, Empty Set Dollar, Fei, and others is damning. The Schelling focal point of $1 is too fragile when there's nothing backing it during stress. Diamond-Dybvig dynamics take over, and the bank run plays out in hours.

But fractional approaches, starting with substantial collateral and algorithmically reducing it as confidence grows, show genuine promise. FRAX has maintained remarkable peg stability while operating at 85% collateral, performing statistically comparable to fully-collateralized stablecoins. The evolutionary approach mirrors the dollar's own history: build trust incrementally rather than demanding it upfront.

The design space I've mapped here (the trilemma, the four-axis taxonomy, the bank run dynamics, the landscape of survivors and casualties) provides the framework. But the real test is in the mechanisms. How exactly do rebasing systems work? What killed seigniorage shares? Why does FRAX's fractional model succeed where Iron Finance's failed?

That's what [Part 2](/2022/05/02/Algorithmic-Stablecoin-Issues.html) is about. I break down the three major theoretical approaches (Hayek Money, Seigniorage Shares, and Fractional Reserves), trace their real-world implementations, and present statistical evidence on their performance.

The dawn of ideal digital money isn't a matter of if, but when and how. And understanding the design space is the first step.

---

*This is Part 1 of a two-part analysis. [Part 2: "Building Ideal Money: From Hayek to FRAX"](/2022/05/02/Algorithmic-Stablecoin-Issues.html) covers the specific theoretical approaches, real-world implementations, and statistical validation.*
