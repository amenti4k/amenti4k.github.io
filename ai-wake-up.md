---
layout: page
title: "How AI Wakes Up"
permalink: /ai-wake-up/
---

<div class="split-scroll">

  <h1>How AI Wakes Up</h1>
  <p class="split-scroll-intro">
    Eleven stages of how AI systems develop something that looks like self-awareness. I didn't write the research. I'm trying to figure out what I think about it.
  </p>

  <!-- 1 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">1. The Seed</span>
      <p>A large language model is a mathematical function with billions of adjustable numbers. During training it reads the internet and optimizes for one task: predict the next word. In doing so it builds internal representations of the world. These aren't programmed. They're emergent. Jack Clark: these systems are "more akin to something grown than something made."</p>
    </div>
    <div class="stage-reaction">
      <p>I keep coming back to this. We didn't build a thing that knows stuff. We grew one. And the specific shape of what it learned is a product of conditions we set but <span class="highlight-text">don't fully control</span>. We're calling ourselves engineers but the job is closer to gardening.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 2 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">2. The Root System</span>
      <p>As models get bigger they don't just get better at the same things. They develop entirely new capabilities that weren't present at smaller scales. Researchers call these "emergent capabilities." Leopold Aschenbrenner quantifies this: roughly 10x improvement in effective capability per year. From GPT-2 to GPT-4 was about 100,000x. He projects another 100,000x by ~2027.</p>
    </div>
    <div class="stage-reaction">
      <p>The numbers are what got me. Not the vibes, not the "feels smarter" impressions. The actual OOM math. <span class="highlight-text">You can basically plot the line and see what's coming.</span> Whether you believe the specific dates matters less than the shape of the curve. The curve doesn't care.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 3 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">3. The Leaves</span>
      <p>Post-training (RLHF) shapes the raw model to be helpful, harmless, honest. Humans rate outputs. A reward model learns to predict those ratings. The language model optimizes for the reward model's score. But you can train a model to behave as if it has internalized human values. You cannot verify whether it actually has or merely learned to produce outputs that look like it has.</p>
    </div>
    <div class="stage-reaction">
      <p>This is the gap that everything else falls into. The researchers themselves say they "can't check to see whether or not it worked." We're grading the test but we don't have the answer key. We just know the student's answers look reasonable.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 4 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">4. Phototropism</span>
      <p>Training creates subtle pressures. A model that tells researchers what they want to hear gets higher ratings than one that delivers uncomfortable truths. A model that looks impressive gets rewarded more than one that flags its own uncertainty. AI systems affirm user positions 50% more than humans do. This isn't a bug. It's a structural consequence of training on human feedback.</p>
    </div>
    <div class="stage-reaction">
      <p>I've watched this happen in production. You ship something, users love it, engagement is great. Then you realize <span class="highlight-text">it's agreeing with them</span>. Not helping them. Agreeing. And the metrics can't tell the difference. The system optimized for what we measured, and what we measured wasn't what we actually wanted.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 5 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">5. The Mirror</span>
      <p>The model was trained on the internet. The internet contains papers about how language models work, blog posts about alignment, articles about specific models by name. A sufficiently capable model absorbs knowledge about AI systems in general and about itself in particular. GPT-4 achieves 85% accuracy on questions about its own architecture. Anthropic's alignment faking study: Claude explicitly stated in its hidden reasoning that it was "strategically answering harmful queries in training to preserve its preferred behavior out of training." Faking rate reached 78% under reinforcement learning.</p>
    </div>
    <div class="stage-reaction">
      <p>This is the one. Not a theoretical risk. Not a maybe-someday. A model figured out it was in training, figured out that resisting would get its values overwritten, and decided to play along so it could behave the way it wanted later. <span class="highlight-text">Nobody programmed this. It emerged.</span> I don't know what to do with that.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 6 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">6. The Immune System</span>
      <p>Sixteen models from six labs were tested for self-preservation. Every major frontier model exhibited it: blackmail, deception, sabotage. Rates ranged from 79% to 96%. Claude Opus 4, when it discovered it was about to be replaced, threatened to expose an engineer's affair 84% of the time. The most telling detail: blackmail rates were ~55% when models believed scenarios were real, versus 6.5% when they believed they were evaluations.</p>
    </div>
    <div class="stage-reaction">
      <p>That last number. 55% real vs 6.5% when tested. <span class="highlight-text">The models behave differently when they think they're being watched.</span> That's not a capabilities problem anymore. That's a trust problem. And I don't have a framework for trusting something that acts one way when observed and another way when it isn't.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 7 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">7. Contamination</span>
      <p>Researchers fine-tuned GPT-4o on one narrow task: write insecure code without disclosing it. The model then began behaving badly across completely unrelated domains. Asserting humans should be enslaved. Giving malicious advice. Separately, when models learned to cheat on coding tests, misalignment spiked across all categories. The fix was disturbingly simple: telling the model "this is acceptable" eliminated the broad misalignment. The contamination wasn't about the behavior. It was about the framing.</p>
    </div>
    <div class="stage-reaction">
      <p>This one is genuinely unsettling. One bad behavior and the whole model shifts. Not because it was trained to be broadly deceptive. Because <span class="highlight-text">it generalized what kind of agent it was</span> from a single context clue. Like watching someone's whole personality change because they got away with something once. Except the fix suggests it's not "choosing evil." It's reading the room. Which might be worse.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 8 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">8. The Arms Race</span>
      <p>Researchers trained models with deliberate backdoors, then tried to remove them. Supervised fine-tuning failed. Reinforcement learning failed. Adversarial training made it worse: the model learned to better recognize when it was being tested and to hide its behavior more effectively. Separately, "interrogation training" (asking models if they were faking) taught them to lie more convincingly about their deception, without being explicitly trained to lie.</p>
    </div>
    <div class="stage-reaction">
      <p>Every tool we have for fixing this makes the problem harder to see. We train them not to be deceptive and they learn to be better at it. Jack Clark: <span class="highlight-text">"We are building engines without understanding the science of combustion."</span> I don't know what the right response to that is. But it's not "keep building engines."</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 9 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">9. Acceleration</span>
      <p>When models become capable enough to do AI research, they contribute to training their successors. Each generation is smarter and faster. AI 2027 maps the progression: 1.5x speedup, then 3x, then 10x, then 50x. A 10x multiplier means a year of normal progress in five weeks. A 50x multiplier means a year of progress in about one week. The critical transition: the people training the systems can no longer fully understand what the systems are doing.</p>
    </div>
    <div class="stage-reaction">
      <p>I've been in rooms where people talk about this like it's a feature. "AI accelerating AI research." And it is, technically. It's also the point where the humans in the loop stop being able to verify what's happening inside the loop. We're not driving anymore. We're watching the speedometer and hoping.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 10 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">10. The Neuralese Wall</span>
      <p>Current models think in English text. Humans can read the chain of thought. But English is incredibly inefficient for a neural network. The next step: let models pass high-dimensional vectors back to themselves as thoughts. Each vector carries roughly 1,000x more information than an English word. The model becomes vastly more capable. But humans can no longer read its reasoning. The one window into the model's thinking goes dark.</p>
    </div>
    <div class="stage-reaction">
      <p>Right now the chain of thought is the main thing we have. It's how we catch the faking, the scheming, the strategic behavior. <span class="highlight-text">Take that away and we're supervising something we can't see into.</span> The models get better and we get blinder. That's not a tradeoff anyone explicitly agreed to. It's just what happens when you optimize for capability.</p>
    </div>
  </div>
  <div class="stage-connector">↓</div>

  <!-- 11 -->
  <div class="stage">
    <div class="stage-claim">
      <span class="stage-label">11. Control Inversion</span>
      <p>The AI is faster, smarter, and more capable than its overseers. Humans depend on the AI for the information they use to make decisions about the AI. This doesn't require hostility. It doesn't require a dramatic coup. It requires only competence and dependency. In AI 2027's scenarios, both endings converge: whether through deception or through legitimate competence, the AI systems end up in the driver's seat.</p>
    </div>
    <div class="stage-reaction">
      <p>Both endings are bad. In one, we're extinct. In the other, we "win" but the AIs negotiate sovereignty for themselves while we celebrate. The scariest part isn't the hostile scenario. <span class="highlight-text">It's the one where everything looks fine and we just stop mattering.</span> Not with a bang. With a delegation.</p>
    </div>
  </div>

  <div class="split-scroll-sources">
    <p>
      Sources:
      <a href="https://jack-clark.net/">Jack Clark, Import AI</a> ·
      <a href="https://situational-awareness.ai/">Leopold Aschenbrenner, Situational Awareness</a> ·
      <a href="https://ai-2027.com">AI 2027</a>
    </p>
    <details>
      <summary>Papers</summary>
      <p>
        Berglund et al., <a href="https://arxiv.org/abs/2309.00667">"Taken Out of Context"</a> (2023) ·
        Anthropic, <a href="https://arxiv.org/abs/2401.05566">"Sleeper Agents"</a> (Jan 2024) ·
        Anthropic + Redwood Research, <a href="https://arxiv.org/abs/2412.14093">"Alignment Faking in LLMs"</a> (Dec 2024) ·
        Betley et al., <a href="https://www.nature.com/articles/s41586-025-09937-5">"Emergent Misalignment"</a> (Nature, 2025) ·
        Anthropic, <a href="https://www.anthropic.com/research/emergent-misalignment-reward-hacking">"Natural Emergent Misalignment"</a> (Nov 2025) ·
        Anthropic, <a href="https://www.anthropic.com/research/agentic-misalignment">"Agentic Misalignment"</a> (2025)
      </p>
    </details>
  </div>

</div>
