---
name: prose
description: Writing and editing standard for essays and blog posts in this repo. Use whenever drafting, rewriting, reviewing, or editing any post in _posts/ or any essay-length prose for Amenti. Encodes the anti-AI-prose discipline developed across the Compute-Is-Labor rewrite, the holdco essay, Work-to-Rule, and the Benn Stancil "frontier fails the Turing test" critique.
---

# Prose: the compile test and the causal chain

This skill exists because AI prose fails in a specific, catalogued way: it produces
insight-shaped text without the causal chain behind it ("Nobody was moved by a thought
or a feeling before it wrote those words. They just fell out." — Benn Stancil). The
editor model regrows this style even while removing it — in one session it produced a
minted aphorism *about not minting aphorisms*, and independently generated "The problem
has a shape, and the shape is a clock," a near-verbatim match for Stancil's parody of AI
writing. The style is the model's reward landscape, not a habit. Defense is therefore
procedural and external, never stylistic and internal.

## Rule 0 — The compile test

Every sentence must paraphrase into a plain claim someone could dispute, a checkable
fact, an attributable quote, or a real event. If the paraphrase comes out empty, the
sentence is exhaust — cut it regardless of how good it sounds.

- SURVIVES: "The gap between the rules and the institution is where mercy, favors, and
  every unrecorded negotiation lived" (names contents; disputable).
- FAILS: "The traces must not supersede the roots." / "The line isn't a line. It's a
  clock." (revelation gesture, no cargo).
- Every metaphor must be cashed: name what's inside it within a sentence or two.
  A gap must have named contents; a ledger must have named entries.

## Rule 1 — The causal chain stays human

The model NEVER drafts experience. Scenes, memories, leans, irritations, and first-person
claims come from the author's own words or his published record — verbatim or lightly
compressed, never invented, never embellished with sensory detail he didn't supply.
If a passage needs a war story that doesn't exist yet, leave a bracketed request for it;
do not synthesize one. The model is quarantined to verifiable work: facts, sources,
structure, contradictions, counting, cold-read decoding.

## Rule 2 — The tell catalog (hard budgets per essay)

Count before shipping. Use grep; do not trust the eye that wrote it.

| Tell | Budget | Notes |
|---|---|---|
| Em-dashes (—) | ≤ 5 | pairs count double; prefer commas, colons, parens, periods |
| "not X, it's Y" / negation-definition | ≤ 2 | keep only ones doing real disambiguation |
| Aphorism paragraph-closers | ≤ 3 | build-build-snap four-for-four is the loudest fingerprint |
| Reader directives (notice / watch / sit with / consider) | ≤ 1 | |
| Performed honesty ("to be honest", "the honest version", "I'll flag") | ≤ 1 | disclosure once, then just be careful |
| Superlative-plus-frame ("the most X I've seen") | 0 | let the material rank itself |
| Announce-the-punchline (framing a quote as profound before it lands) | 0 | end cold on the quote |
| Banned words | 0 | substrate, load-bearing, crux, altitude, "the quiet part", quietly, delve, tapestry |
| Balanced twin fragments ("Trains run late. Offices back up.") | ≤ 1 | replace one twin with a documented case |
| Universal claims ("always", "everywhere it's tried", "nobody is asking") | 0 unless literally true | replace with the mechanism or a falsifiable version |
| Stock closers (chiasmus, "only one of those questions...", "nobody is asking") | 0 | end on a question, an image, or a flat fact |

Also: no uniform paragraph blocks (170–290 words, four-for-four) — at least one
one-sentence paragraph, one section break, one deliberately flat sentence per page.
Sameness of polish is itself a tell.

## Rule 3 — Verification requirements

- Every number, date, deal, and named claim gets checked against a source before
  publishing. Numbers that can't be sourced get cut or explicitly labeled as the
  author's own estimate with its basis.
- Quotes are verbatim against the source, or they are not quotes.
- Employer material (Percepta, Decagon, Didero) is public-facts-only: nothing beyond
  what the company or the author has already published. When in doubt, cite the
  public page.
- Never fabricate a URL. Link only pages verified to exist; otherwise attribute in
  prose without a link.
- Misattribution check: when summarizing a thinker (Scott, Simon, Chollet, Coase),
  state their actual claim accurately, and if the essay's version is sharper, claim
  the extra step explicitly as the author's — do not launder original ideas through
  borrowed authority.

## Rule 4 — Shipping checklist

An essay does not ship unless it contains:
1. One thing that actually happened (from the author's record, verbatim-faithful).
2. One number a reader could check.
3. One prediction that could fail, with named win/lose criteria.
4. A cold-read pass: every proper noun decodable at first mention by a stranger
   (the Nightingale/Florence failure); every referent resolvable.
5. Tic counts within budget (Rule 2 table), via grep, recorded in the commit message
   or PR notes if asked.

## Rule 5 — Repo mechanics

- No in-body `# H1`: `_layouts/post.html` renders `page.title` as the page H1.
- Marginnotes (`<span class="marginnote">`) go AFTER the sentence they annotate
  (site JS walks backward). Marginnotes define or cite; they never praise the essay.
- Preserve URLs: filename slug + categories determine the permalink
  (`/:categories/:year/:month/:day/:title.html`). Changing either breaks published links.
- The excerpt must not repeat the essay's opening hook verbatim; give it different
  material.
- Internal links use the full category path (e.g.
  `/ai/2025/07/15/Building-on-Quicksand-The-Reality-of-Production-AI-Systems.html`).

## Rule 6 — Editing process and convergence

Draft (or receive draft) → compile-test pass → tic count → fact check → cold read →
fix → recount. When reviewing with subagents, verify every finding against the text
(quote + location) and kill generic advice; protect a do-not-touch list of the essay's
human material before editing begins.

Convergence rule: a pass over an already-good essay should produce FEW edits. If every
pass generates many changes, the editor is the noise source — stop editing. Never
"improve" protected material (the author's scenes, deadpan details, earned closers).
The goal is prose where something is at stake and every gesture is cashed — a sharp
human on a good day, not a system at its ceiling.
