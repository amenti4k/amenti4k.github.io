---
layout: page
title: "Kakao Ventures — Venture Research Intern"
permalink: /kakao-ventures/
---

**Seoul, September 2019 – January 2020**

[Kakao Ventures](https://www.kakao.vc/en) is Korea's most active seed-stage VC, a fully owned independent subsidiary of Kakao Corp with 190+ portfolio companies and $300M+ AUM, investing across deep tech, mobile, digital healthcare, and gaming. The firm was established in 2012 as K Cube Ventures and rebranded in 2017.

----

### The Role

Venture research intern working on the theme: *"Expanding the VC's network and operations globally, given its strengths in the regional market."* I led two distinct workstreams — one quantitative and product-facing, the other exploratory and strategic.

### 1. Fellowship Landing Page — A/B Testing

Kakao Ventures runs a competitive summer fellowship for students. The hypothesis was that the landing page wasn't doing enough to signal the prestige associated with the Kakao name, and that a redesign emphasizing brand equity could meaningfully increase application rates.

I designed and ran a controlled A/B test to measure the effect. The sample size calculation required 737 participants per variation — 1,474 total — at 80% statistical power and a 5% significance level, calibrated to detect a meaningful lift without overfitting to noise. Students were randomly split across the two page versions. Returning applicants who already had an account stayed on whichever version they'd originally seen, to keep their experience consistent and avoid contamination.

Both versions ran concurrently to control for confounds — web traffic fluctuations, seasonal variation in application volume, and other counterfactuals that would distort results if the tests were staggered. The treatment effect was estimated by taking the difference in means across the two groups, and I ran repeated averaging to strengthen the causal claim.

Result: **20% increase in fellowship application participation.**

### 2. African Venture Ecosystem — Market Research

The second workstream was a strategic question: should Kakao Ventures expand into Africa, and if so, where and how? In US and European markets, platforms like PitchBook and Crunchbase make it straightforward to map the investment landscape. Nothing comparable existed for the African ecosystem at the time. The first challenge was simply building the dataset.

**Data Collection & Evidence Building**

I started with a concrete list of the top 50 venture firms operating on the continent. From there, I scraped firm websites to identify portfolio companies, then used APIs to pull funding round sizes, number of participants, and valuations where available. The deep analysis was scoped to four markets — Egypt, Kenya, Nigeria, and South Africa — because they had the most developed online databases and reporting infrastructure. Companies like BriterBridges were beginning to aggregate metadata, but individual firms' portfolios were often only partially public. Building a reliable picture required cross-referencing multiple fragmented sources.

**Market Sizing**

Estimating total VC capital deployed in each market required Fermi estimation — there was no authoritative number to pull. I narrowed down by orders of magnitude, then ran multiple rounds of sensitivity checking to validate the bounds. For example, if total VC rounds raised in a quarter for the continent came out below $50M or above $400M, the model was out of range. These guardrails weren't arbitrary — they were grounded in comparable regional benchmarks and my own experience growing up in the ecosystem. The goal was to give Kakao a reliable order-of-magnitude read on where the market stood and how key investments during this period were shaping the landscape.

**Stakeholder Interviews**

The quantitative work needed to be grounded in how these markets actually function. I held meetings with Ethiopian, Nigerian, and South African entrepreneurs and investors to understand the texture that data alone doesn't capture — regulatory environments, cultural attitudes toward outside capital, the practical mechanics of deal flow in each market.

Being born and raised in Ethiopia gave me insider knowledge of the East African ecosystem, but it also introduced bias. I was aware of the favoritism that proximity creates, so I applied the same evaluation metrics across all four markets and used my regional expertise defensively — to flag pitfalls and validate assumptions rather than to advocate for one geography over another.

**Key Findings**

The African market showed a clear pattern: surplus of founders and startups, deficiency of capital. The demand for VC funding was visible in the growing number and quality of startups, while the supply side — competing VCs, government-backed funds, and LP capital — remained thin. Formal barriers echoed those of other emerging markets: lack of financial regulations, underdeveloped capital markets, weak investment protection laws. But the structural direction was promising, particularly in markets like Nigeria and Kenya where reform-minded governments were creating more favorable conditions for foreign investment.

Exit strategy remained the biggest structural constraint. IPO markets and acquisition channels were underdeveloped or nonexistent in most regions, making it harder for seed and early-stage investors to realize returns on the timeline they're accustomed to.

### Outcome

Delivered a final report and presentation with key findings and recommended entry points to the continent, including detailed market entry strategies per region. Adapted to the Korean office's collaboration style — shifting from my default of working independently until conclusions are reached to biweekly check-ins showing work in progress, recent findings, and directional thinking to keep the team aligned throughout.

----

*Related reading: [Venture Capital and Globalization](/research/)*
