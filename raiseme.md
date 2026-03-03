---
layout: page
title: "RaiseMe — Business Development Intern"
permalink: /raiseme/
---

**San Francisco, Summer 2019**

[RaiseMe](https://www.raise.me) was an ed-tech platform where high school students earned micro-scholarships toward college by completing activities like maintaining good grades, participating in community service, and attending AP classes. At the time, 400,000+ students were on the platform with 200+ college partners ranging from Arizona State to Carnegie Mellon. RaiseMe was later acquired by CampusLogic in 2020.

----

### The Role

Business development intern on the Finance team. The internship started with one open-ended prompt: *"Improve product reach through user insights."* From there, I narrowed focus, formulated questions, built context with data, and delivered product recommendations.

### What I Worked On

**Platform Expansion to Community Colleges**

RaiseMe had built its product around the high school to four-year college pipeline, but community colleges — serving nearly half of all US undergraduates — were an untapped segment. I remodeled features of the core platform to fit this expansion, rethinking how micro-scholarships could work for transfer students whose journeys don't follow the traditional path. This meant adjusting the financial aid checklists, comparison tools, and onboarding flows to account for how transfer students actually navigate enrollment.

**User Research & Diagnostics**

Thirty percent of college students drop out, and more than half cite finances as the reason. To understand what was happening on RaiseMe's end, I ran surveys and interviews with college students who had used the platform in high school. The sampling was deliberate — stratified across regions, age, enrollment date, GPA, test scores, ethnicity, wealth index, and scholarship amount — to keep findings generalizable while only reaching out to users who had opted in.

The questions were open-ended and focused on three things: whether working toward a scholarship changed how dedicated students were to schoolwork, how likely they'd be to use a college version of RaiseMe, and what caused last-minute drop-offs for students who were close to converting. I used tree classification to group respondents and avoided loaded questions to get genuine, varied responses.

**Retention — Observational Study & Modeling**

The core of the internship was building the case for "Retention" — extending RaiseMe's platform beyond getting students into college to keeping them there. I built an observational study comparing students who extended their membership into college vs. those who dropped off after high school. To isolate the effect, I constructed synthetic control groups — matching on college, age, GPA, test scores, ethnicity, wealth index, and scholarship amount — to produce counterfactual outcomes that let us draw causal inference from non-experimental data. Robustness checks involved removing individual groups from the synthetic unit to test for sensitivity.

The results were clear: financial incentives delivered as scholarships improved graduation rates, and the effect was strongest for students most dependent on the aid. Low-income students saw dropout rates decrease by 8%, compared to 3% for higher-income peers. This tracked with the broader literature on financial incentives in education — studies consistently show that performance-based scholarships change behavior, but the mechanism matters as much as the money.

From there, I built a model using historical data to assign weights to each activity's impact on reducing dropout likelihood. The highest-impact levers weren't dramatic — they were things like attending orientation on time, not missing classes in a given week, and engaging with campus community events. Activities that integrated students into campus life early drove consistency, which drove retention. Group activities, surprisingly, were less effective — tardiness or dropout by one member could break the chain for others.

**Predictive Analysis**

I modeled Summer Melt Withdrawal predictions across 78% of US universities. Summer melt — when admitted students fail to enroll in the fall — is one of the biggest leakage points in the pipeline. The analysis identified the window between a student depositing their admission fee and actually enrolling as the highest-impact zone for onboarding. Students engaged on the platform during this gap were significantly more likely to follow through on their activities and earn scholarships, as it became part of their routine before the semester even started.

### Outcome

Product recommendations were piloted at [Wayne State University](https://today.wayne.edu/news/2019/09/27/wayne-state-university-raiseme-launch-first-ever-micro-scholarship-program-for-student-success-34308) and Stetson University. Completed the internship with an "expectations exceeded" result and a full-time return offer.

----

*Related reading: [Retention Campaign at RaiseMe](/2019/05/01/RaiseMe-Retention.html)*

----

### Research Bibliography

The work drew on a body of research on financial incentives and educational outcomes:

- Levitt, List & Sadoff — [The Effect of Performance-Based Incentives on Educational Achievement](http://rady.ucsd.edu/docs/Levitt_List_Sadoff_Incentives_Education_NBER_WP22107.pdf) (NBER)
- Barrow & Rouse — [Financial Incentives and Educational Investment: The Impact of Performance-Based Scholarships on Student Time Use](http://www.nber.org/papers/w19351) (2013)
- Henry & Rubenstein — [Paying for Grades: Impact of Merit-based Financial Aid on Educational Quality](http://econpapers.repec.org/article/wlyjpamgt/v_3a21_3ay_3a2002_3ai_3a1_3ap_3a93-109.htm) (2002)
- Pallais — [Taking a Chance on College: Is the Tennessee Education Lottery Scholarship Program a Winner?](https://scholar.harvard.edu/files/pallais/files/2447.pdf) (2009)
- Jackson — [The Effects of an Incentive-Based High-School Intervention on College Outcomes](http://www.nber.org/papers/w15722) (2010)
- Fryer — [Financial Incentives and Student Achievement: Evidence from Randomized Trials](http://www.nber.org/papers/w15898) (2010)
- Levitt, List, Neckermann & Sadoff — [The Behavioralist Goes to School: Leveraging Behavioral Economics to Improve Educational Performance](http://www.nber.org/papers/w18165.pdf) (2012)
