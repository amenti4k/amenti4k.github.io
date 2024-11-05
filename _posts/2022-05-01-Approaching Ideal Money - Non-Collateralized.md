---
layout: post
title: "Are Algorithmic Stablecoins Possible? A Deep Dive Into Crypto's Holy Grail"
date: 2022-05-01
tags: [business]
---

## TL;DR
After extensive research and analysis, I conclude that non-collateralized algorithmic stablecoins are possible, but with a major caveat: they need to earn their way to becoming fully algorithmic rather than starting that way from day one. Through analysis of historical attempts, game theory modeling, and statistical validation, I show that the optimal path is starting with partial collateralization and gradually reducing it as market confidence grows - similar to how the US dollar evolved away from the gold standard. FRAX's fractional-algorithmic approach demonstrates this is viable, maintaining remarkable stability while reducing collateral requirements based on market demand.

## Introduction

The holy grail of crypto has always been building the perfect digital money - a currency that's stable enough for everyday use but free from government control. Bitcoin showed us that decentralized digital money is possible, but its volatility makes it impractical for buying coffee or getting paid a salary. Stablecoins emerged as a solution, but most rely on traditional financial system collateral, defeating the purpose of crypto's promise of true decentralization.

This led me down a rabbit hole: are truly decentralized, non-collateralized algorithmic stablecoins actually possible? Or are they just a pipe dream?

It's a deceptively complex question that touches on game theory, monetary policy, market psychology, and mechanism design. After diving deep into historical attempts, analyzing their failures, and studying successful approaches, I've developed a perspective I'm excited to share.

## The Quest for Ideal Money

Before we can determine if algorithmic stablecoins are possible, we need to define what "ideal money" actually looks like. Drawing from economist John Nash's work, I argue ideal money needs to solve the fundamental conflict between short-term and long-term interests in creating a stable digital currency.

Breaking this down, money serves three core functions:
1. Unit of Account - A consistent way to measure value
2. Store of Value - A reliable way to save wealth over time  
3. Medium of Exchange - An efficient way to transact

The key insight is that these functions need to work across different time horizons. USD works great as a medium of exchange in the short term, but inflation erodes its store of value over decades. Gold maintains long-term value but is impractical for daily transactions.

Ideal money would excel at all three functions both in the short and long term. It would also need to be:
- Independent from government control
- Globally scalable
- Capital efficient 

This is a high bar! But it gives us a framework to evaluate different approaches.

## Why Focus on Algorithmic Stablecoins?

Through process of elimination, I found that non-collateralized algorithmic stablecoins are theoretically the closest to ideal money:

- Bitcoin/ETH: Great for decentralization but too volatile
- Fiat-backed stablecoins (USDC): Stable but rely on traditional banking
- Crypto-collateralized stablecoins (DAI): Capital inefficient due to overcollateralization
- Commodity-backed stablecoins: Hard to scale, tendency toward centralization
- Algorithmic stablecoins: Potentially stable, scalable, and truly decentralized

The problem? Building them is HARD. Really hard. I identified three core challenges:

1. Actually maintaining stability - The mechanisms need to reliably keep the peg
2. Building sufficient network effects (Lindy Effect) - Need to become "money-like" enough that people trust them
3. Overcoming the "Paradox of Stability" - Need speculation to grow but speculation creates instability

## Learning from Failed Attempts

To understand if these challenges can be overcome, I analyzed two prominent approaches and their real-world implementations:

### The Rebase Approach (Ampleforth)

Ampleforth tried to maintain stability by automatically adjusting everyone's wallet balances based on the price. If AMPL is trading at $2, everyone's balance doubles but each token is worth $1. Sounds clever right?

The problem is this doesn't actually create stability - it just masks volatility. Your wallet might show 100 AMPL tokens worth $1 each today and 50 AMPL tokens worth $1 each tomorrow, but your purchasing power still fluctuated! The stability is an illusion.

Through game theory analysis, I showed how the incentives ultimately lead to speculation rather than true stability.

### The Seigniorage Shares Approach (Basis)

Basis tried a multi-token model where "bond" and "share" tokens would absorb volatility to keep the main stablecoin pegged. When price is high, new stablecoins are minted and given to shareholders. When price is low, bonds are sold at a discount to remove stablecoins from circulation.

While more sophisticated, I identified fatal flaws in the mechanism:
- Bonds expire after 5 years, creating dangerous cliffs
- Lack of fungibility in bonds reduces their effectiveness
- Circular dependency in incentives (need faith in future growth to maintain current stability)

The project ultimately shut down due to regulatory concerns, but the fundamental economic issues would have likely caused problems anyway.

## A Better Way: The FRAX Approach

After seeing how pure algorithmic approaches failed, I analyzed FRAX's hybrid "fractional-algorithmic" design. Rather than starting fully algorithmic, FRAX begins fully collateralized and algorithmically reduces the collateral ratio based on market demand.

The key innovations:

1. Market-Driven Collateral Ratio - When demand is high and price is above peg, collateral requirements automatically decrease. When confidence falls, collateral increases.

2. Programmatic Market Operations - Similar to how central banks conduct open market operations, but fully automated and transparent.

3. Progressive Decentralization - Starts with training wheels (collateral) but systematically removes them as the system proves itself.

The game theory checks out - there are clear incentives for arbitrageurs to maintain the peg while the collateral provides a confidence backstop. The mechanism allows for a gradual building of trust rather than requiring it from day one.

## Statistical Validation

To validate these theoretical arguments, I conducted statistical analysis comparing volatility across different stablecoin designs. The results were striking:

- FRAX showed volatility levels comparable to fully-collateralized stablecoins despite much lower collateral requirements
- Failed algorithmic stablecoins like Basis and Ampleforth showed significantly higher volatility
- FRAX's price movements were more correlated with established stablecoins than other algorithmic attempts

This empirically supports the theory that the fractional-algorithmic approach can deliver true stability.

## Conclusion: Evolution Over Revolution 

So are non-collateralized algorithmic stablecoins possible? Yes, but they have to earn their way there rather than starting from zero.

The key insight is that money is fundamentally about trust. The US dollar didn't start as pure fiat currency - it evolved from gold-backing as faith in the system grew. Similarly, algorithmic stablecoins need to build trust before removing their collateral training wheels.

FRAX shows this is possible by:
1. Starting with full collateral to bootstrap confidence
2. Systematically reducing collateral as market demand proves sustainability
3. Maintaining clear incentives and transparency throughout the process

The end goal of fully algorithmic stablecoins may be achievable, but the path there is through evolution rather than revolution. We need to recognize that while code is law, money is ultimately a social technology built on trust.

## Looking Forward

This research opens up exciting future directions:
- How can we optimize the collateral reduction process?
- What role will these systems play in the broader financial system?
- Can we create better price oracles and stability mechanisms?

But the core conclusion remains: algorithmic stablecoins are possible if we take the right approach. By learning from past failures and embracing progressive decentralization, we can work toward truly ideal money.

The dawn of algorithmic money isn't a matter of if, but when and how. And that's pretty exciting.

---

*This post summarizes research I conducted for my undergraduate thesis. For the full academic analysis including detailed game theory modeling and statistical validation, check out the full paper [link].*