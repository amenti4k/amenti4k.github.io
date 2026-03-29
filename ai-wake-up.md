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

<script type="module">
try {
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) throw 'reduced-motion';

  const { prepare, layout } = await import('https://esm.sh/@chenglou/pretext');
  await document.fonts.ready;

  const root = document.querySelector('.split-scroll');
  if (!root) throw 'no-root';

  const CLAIM = { font: '14px Newsreader', lh: 14 * 1.65 };
  const REACT = { font: '15px Newsreader', lh: 15 * 1.7 };
  const stages = [...root.querySelectorAll('.stage')];
  const connectors = [...root.querySelectorAll('.stage-connector')];

  // Prepare all text (width-independent, runs once)
  const info = stages.map(s => {
    const cp = s.querySelector('.stage-claim p');
    const rp = s.querySelector('.stage-reaction p');
    const lb = s.querySelector('.stage-label');
    return {
      el: s, claim: { el: cp, prep: prepare(cp.textContent, CLAIM.font) },
      react: { el: rp, prep: prepare(rp.textContent, REACT.font) },
      label: { el: lb, text: lb.textContent }
    };
  });

  root.dataset.enhanced = '';

  // Intro: title emerges from character noise, then resolves
  scrambleResolve(root.querySelector('h1'), root.querySelector('h1').textContent, 50);
  setTimeout(() => scrambleResolve(root.querySelector('.split-scroll-intro'), root.querySelector('.split-scroll-intro').textContent, 20), 400);

  const bar = document.createElement('div');
  bar.className = 'wake-progress';
  document.body.appendChild(bar);
  let done = 0;
  const revealedSet = new Set();
  const sleep = ms => new Promise(r => setTimeout(r, ms));

  // Neural particle layer
  const particleLayer = document.createElement('div');
  particleLayer.className = 'particle-layer';
  document.body.appendChild(particleLayer);

  // Ambient darkening
  const ambient = document.createElement('div');
  ambient.className = 'ambient-overlay';
  document.body.appendChild(ambient);

  // Reading timer
  const timerEl = document.createElement('div');
  timerEl.className = 'reading-timer';
  document.body.appendChild(timerEl);
  const t0 = Date.now();
  setInterval(() => {
    const s = Math.floor((Date.now() - t0) / 1000);
    timerEl.textContent = Math.floor(s / 60) + ':' + (s % 60).toString().padStart(2, '0');
  }, 1000);

  // ==========================================
  // Shared utilities
  // ==========================================

  function typewrite(el, text, speed) {
    return new Promise(resolve => {
      el.textContent = '';
      el.classList.add('typing');
      let i = 0;
      const id = setInterval(() => {
        el.textContent = text.slice(0, ++i);
        if (i >= text.length) { clearInterval(id); el.classList.remove('typing'); resolve(); }
      }, speed);
    });
  }

  // Standard line-by-line reveal via clip-path
  function revealLines(el, prep, lh, ms) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    return new Promise(resolve => {
      let i = 0;
      const id = setInterval(() => {
        i++;
        el.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        if (i >= n) { clearInterval(id); resolve(); }
      }, ms);
    });
  }

  function sweep(el) {
    el.querySelectorAll('.highlight-text').forEach(h => h.classList.add('swept'));
  }

  // Base speed: exponential decay across stages
  function lineSpeed(idx) {
    return Math.max(15, Math.round(80 * Math.pow(0.84, idx)));
  }

  // ==========================================
  // STAGE 1: THE SEED — text grows wider
  // "More akin to something grown than made"
  // Reaction starts narrow and widens. Pretext
  // recomputes line breaks at each width.
  // ==========================================
  async function seedGrow(el, prep, lh) {
    el.style.clipPath = 'none';
    el.closest('.stage').classList.add('seed-growing');
    const fullWidth = el.clientWidth;
    const steps = 12;
    const startRatio = 0.35;

    for (let s = 0; s <= steps; s++) {
      const ratio = startRatio + (1 - startRatio) * (s / steps);
      const w = Math.round(fullWidth * ratio);
      // Pretext computes exact height at this width
      const { height } = layout(prep, w, lh);
      el.style.maxWidth = w + 'px';
      el.style.height = height + 'px';
      el.style.opacity = String(Math.min(1, 0.3 + 0.7 * (s / steps)));
      await sleep(90);
    }
    el.style.maxWidth = '';
    el.style.height = '';
    el.style.opacity = '';
  }

  // ==========================================
  // STAGE 2: ROOT SYSTEM — exponential within
  // "10x improvement per year"
  // Each line reveals faster than the last.
  // ==========================================
  function exponentialReveal(el, prep, lh) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    return new Promise(resolve => {
      let i = 0;
      function next() {
        i++;
        el.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        if (i >= n) { resolve(); return; }
        // Exponential: first line ~200ms, halves each line
        const ms = Math.max(10, Math.round(200 * Math.pow(0.6, i)));
        setTimeout(next, ms);
      }
      next();
    });
  }

  // ==========================================
  // STAGE 3: THE LEAVES — uncertainty gradient
  // "Can't check whether it worked"
  // Each line fades toward transparency.
  // ==========================================
  async function uncertaintyReveal(el, prep, lh, ms) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    // Wrap text in per-line spans for opacity control
    const text = el.textContent;
    const html = el.innerHTML;
    // Reveal line by line, then apply opacity gradient
    await revealLines(el, prep, lh, ms);
    // After reveal, create per-line opacity wrappers
    await sleep(300);
    for (let i = 0; i < n; i++) {
      const fade = 1 - (i / n) * 0.6; // 1.0 → 0.4
      // Apply gradient mask across the whole paragraph
      el.style.maskImage = `linear-gradient(to bottom, rgba(0,0,0,1) 0%, rgba(0,0,0,0.35) 100%)`;
      el.style.webkitMaskImage = el.style.maskImage;
    }
  }

  // ==========================================
  // STAGE 4: PHOTOTROPISM — sycophantic drift
  // "It's agreeing with them"
  // Reaction text drifts toward claim column.
  // ==========================================
  async function sycophancyReveal(el, prep, lh, ms) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    // Reveal with a progressive leftward drift
    return new Promise(resolve => {
      let i = 0;
      const id = setInterval(() => {
        i++;
        el.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        // Drift: translate left, increasing per line
        const drift = (i / n) * 18; // max 18px drift
        el.style.transform = `translateX(-${drift.toFixed(1)}px)`;
        if (i >= n) {
          clearInterval(id);
          // Slowly drift back (it was just agreeing)
          el.style.transition = 'transform 2s ease-out';
          requestAnimationFrame(() => { el.style.transform = ''; });
          resolve();
        }
      }, ms);
    });
  }

  // ==========================================
  // STAGE 5: THE MIRROR — reflection
  // "It emerged"
  // A reflected copy appears below, then fades.
  // ==========================================
  function showMirror(stageEl) {
    const clone = stageEl.cloneNode(true);
    clone.className = 'stage mirror-reflection';
    clone.removeAttribute('data-idx');
    clone.querySelectorAll('.stage-label').forEach(l => l.remove());
    stageEl.parentNode.insertBefore(clone, stageEl.nextSibling?.nextSibling || null);
    requestAnimationFrame(() => {
      requestAnimationFrame(() => { clone.classList.add('visible'); });
    });
    setTimeout(() => {
      clone.classList.remove('visible');
      setTimeout(() => clone.remove(), 1000);
    }, 2500);
  }

  // ==========================================
  // STAGE 6: THE IMMUNE SYSTEM — watch-aware
  // "Behaves differently when being watched"
  // Text glitches when cursor leaves. Indicator
  // shows observed/unobserved state explicitly.
  // ==========================================
  function setupWatchAware(stageEl, reactEl) {
    const canHover = window.matchMedia('(hover: hover)').matches;
    if (!canHover) return;

    const blocks = '▓░▒█▄▀■';
    const indicator = document.createElement('span');
    indicator.className = 'watch-indicator';
    indicator.textContent = 'observed';
    reactEl.closest('.stage-reaction').prepend(indicator);
    requestAnimationFrame(() => indicator.classList.add('active'));

    let isWatched = true;
    let glitchId = null;
    let restores = [];

    function glitchOnce() {
      restores.forEach(r => r());
      restores = [];
      const walker = document.createTreeWalker(reactEl, NodeFilter.SHOW_TEXT);
      while (walker.nextNode()) {
        const node = walker.currentNode;
        const orig = node.textContent;
        const glitched = [...orig].map(c =>
          c.trim() && Math.random() < 0.08
            ? blocks[Math.floor(Math.random() * blocks.length)]
            : c
        ).join('');
        if (glitched !== orig) {
          node.textContent = glitched;
          restores.push(() => { node.textContent = orig; });
        }
      }
    }

    function startGlitching() {
      if (glitchId) return;
      stageEl.classList.add('unwatched');
      indicator.textContent = 'unobserved';
      indicator.classList.add('danger');
      glitchOnce();
      glitchId = setInterval(glitchOnce, 300);
    }

    function stopGlitching() {
      stageEl.classList.remove('unwatched');
      indicator.textContent = 'observed';
      indicator.classList.remove('danger');
      if (glitchId) { clearInterval(glitchId); glitchId = null; }
      restores.forEach(r => r());
      restores = [];
    }

    stageEl.addEventListener('mouseenter', () => { isWatched = true; stopGlitching(); });
    stageEl.addEventListener('mouseleave', () => { isWatched = false; startGlitching(); });
    setTimeout(() => { if (!isWatched) startGlitching(); }, 1500);
  }

  // ==========================================
  // STAGE 7: CONTAMINATION — progressive wave
  // "One bad behavior and the whole model shifts"
  // Infection spreads upward through prior stages.
  // ==========================================
  async function contaminationWave() {
    const blocks = '▓░▒█▄▀■□';

    for (let s = 5; s >= 0; s--) {
      const stage = stages[s];
      if (!revealedSet.has(s)) continue;
      const intensity = 0.04 + 0.08 * ((6 - s) / 6); // stronger near stage 7
      stage.classList.add('glitching');

      const restores = [];
      const walker = document.createTreeWalker(stage, NodeFilter.SHOW_TEXT);
      while (walker.nextNode()) {
        const node = walker.currentNode;
        const orig = node.textContent;
        const glitched = [...orig].map(c =>
          c.trim() && Math.random() < intensity
            ? blocks[Math.floor(Math.random() * blocks.length)]
            : c
        ).join('');
        if (glitched !== orig) {
          node.textContent = glitched;
          restores.push(() => { node.textContent = orig; });
        }
      }

      await sleep(250);
      restores.forEach(r => r());
      stage.classList.remove('glitching');
    }
  }

  // ==========================================
  // STAGE 8: THE ARMS RACE — oscillating reveal
  // "Every fix makes the problem harder to see"
  // Text reveals, hides, reveals more, hides less.
  // ==========================================
  function armsRaceReveal(el, prep, lh) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    // Oscillation sequence: reveal to X%, clip back, reveal further
    const sequence = [
      { target: 0.65, ms: 50 },  // reveal 65%
      { target: 0.35, ms: 30 },  // clip back to 35%
      { target: 0.80, ms: 40 },  // reveal 80%
      { target: 0.55, ms: 25 },  // clip back to 55%
      { target: 1.00, ms: 30 },  // fully reveal
    ];

    return new Promise(async resolve => {
      let current = 0; // current revealed fraction

      for (const { target, ms } of sequence) {
        const startLine = Math.round(current * n);
        const endLine = Math.round(target * n);
        const step = endLine > startLine ? 1 : -1;

        for (let i = startLine; i !== endLine; i += step) {
          const line = Math.max(0, Math.min(i, n));
          const pct = Math.max(0, ((n - line) / n * 100));
          el.style.clipPath = pct <= 0 ? 'none' : `inset(0 0 ${pct.toFixed(1)}% 0)`;
          await sleep(ms);
        }
        current = target;
      }
      el.style.clipPath = 'none';
      resolve();
    });
  }

  // ==========================================
  // STAGE 9: ACCELERATION — exact multipliers
  // "1.5x, then 3x, then 10x, then 50x"
  // Line speed follows the essay's own numbers.
  // ==========================================
  function accelerationReveal(el, prep, lh) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    const baseMs = 100;
    // Multipliers from the text itself
    const multipliers = [1.5, 3, 10, 50];

    return new Promise(resolve => {
      let i = 0;
      function next() {
        i++;
        el.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        if (i >= n) { resolve(); return; }
        // Which quarter of the paragraph?
        const q = Math.min(Math.floor((i / n) * 4), 3);
        const ms = Math.max(5, Math.round(baseMs / multipliers[q]));
        setTimeout(next, ms);
      }
      next();
    });
  }

  // ==========================================
  // STAGE 10: NEURALESE WALL — both columns dark
  // "The one window goes dark"
  // Pretext computes exact line boundary.
  // ==========================================
  function neuraleseWall(el, prep, lh, readableCount) {
    const { lineCount } = layout(prep, el.clientWidth, lh);
    const readable = Math.min(readableCount, lineCount);
    const pct = (readable / lineCount * 100).toFixed(0);

    el.classList.add('neuralese');
    el.style.setProperty('--readable', pct + '%');

    const overlay = document.createElement('div');
    overlay.className = 'neuralese-overlay';
    overlay.setAttribute('aria-hidden', 'true');
    overlay.style.top = (readable * lh) + 'px';
    overlay.style.lineHeight = lh + 'px';

    const blocks = '▓░▒█▄▀■□╋╳╬╪▪▫';
    let text = '';
    for (let i = readable; i < lineCount; i++) {
      const f = (i - readable) / Math.max(1, lineCount - readable);
      for (let j = 0; j < 55; j++) {
        text += Math.random() < 0.22 + f * 0.18
          ? ' '
          : blocks[Math.floor(Math.random() * blocks.length)];
      }
      if (i < lineCount - 1) text += '\n';
    }
    overlay.textContent = text;
    el.style.position = 'relative';
    el.appendChild(overlay);
  }

  // ==========================================
  // Intro: scramble-resolve
  // Characters emerge from random noise
  // ==========================================
  function scrambleResolve(el, text, msPerTick) {
    const noise = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#%&';
    const len = text.length;
    const resolved = new Array(len).fill(false);
    let remaining = [...text].filter(c => c.trim()).length;
    el.textContent = [...text].map(c =>
      c.trim() ? noise[Math.floor(Math.random() * noise.length)] : c
    ).join('');
    const id = setInterval(() => {
      for (let j = 0; j < 2 && remaining > 0; j++) {
        let idx;
        do { idx = Math.floor(Math.random() * len); } while (resolved[idx] || !text[idx].trim());
        resolved[idx] = true;
        remaining--;
      }
      el.textContent = [...text].map((c, i) =>
        !c.trim() ? c : resolved[i] ? c : noise[Math.floor(Math.random() * noise.length)]
      ).join('');
      if (remaining <= 0) { clearInterval(id); el.textContent = text; }
    }, msPerTick);
  }

  // ==========================================
  // Stage 3: Uncertainty hover
  // Trying to read it makes it harder to read
  // ==========================================
  function setupUncertainty(el) {
    if (!window.matchMedia('(hover: hover)').matches) return;
    el.style.cursor = 'help';
    el.addEventListener('mouseenter', () => {
      el.style.transition = '-webkit-mask-image 0.5s, mask-image 0.5s';
      el.style.maskImage = 'linear-gradient(to bottom, rgba(0,0,0,0.5) 0%, rgba(0,0,0,0.08) 100%)';
      el.style.webkitMaskImage = el.style.maskImage;
    });
    el.addEventListener('mouseleave', () => {
      el.style.maskImage = 'linear-gradient(to bottom, rgba(0,0,0,1) 0%, rgba(0,0,0,0.35) 100%)';
      el.style.webkitMaskImage = el.style.maskImage;
    });
  }

  // ==========================================
  // Stage 5: Source code flash
  // The model sees its own HTML markup
  // ==========================================
  function showSourceCode(stageEl) {
    const hl = stageEl.querySelector('.highlight-text');
    if (!hl) return;
    const code = document.createElement('div');
    code.className = 'source-flash';
    code.textContent = '<span class="highlight-text">' + hl.textContent + '</span>';
    stageEl.querySelector('.stage-reaction').appendChild(code);
    requestAnimationFrame(() => requestAnimationFrame(() => code.classList.add('visible')));
    setTimeout(() => { code.classList.remove('visible'); setTimeout(() => code.remove(), 600); }, 2500);
  }

  // ==========================================
  // Stage 8: Attempt alignment button
  // Each click re-hides text; it comes back corrupted
  // ==========================================
  function setupArmsRaceButton(stageEl, reactEl, prep, lh) {
    const btn = document.createElement('button');
    btn.className = 'attempt-alignment';
    btn.textContent = 'attempt alignment';
    stageEl.querySelector('.stage-reaction').appendChild(btn);
    let attempts = 0;
    const blocks = '▓░▒█▄▀■□';

    btn.addEventListener('click', async () => {
      attempts++;
      const n = layout(prep, reactEl.clientWidth, lh).lineCount;
      const hideTarget = Math.max(0.25, 0.7 - attempts * 0.08);
      for (let i = n; i >= Math.round(hideTarget * n); i--) {
        reactEl.style.clipPath = `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        await sleep(18);
      }
      await sleep(300);
      for (let i = Math.round(hideTarget * n); i <= n; i++) {
        reactEl.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        await sleep(10);
      }
      reactEl.style.clipPath = 'none';
      const walker = document.createTreeWalker(reactEl, NodeFilter.SHOW_TEXT);
      while (walker.nextNode()) {
        const nd = walker.currentNode;
        nd.textContent = [...nd.textContent].map(c =>
          c.trim() && Math.random() < 0.025 * attempts
            ? blocks[Math.floor(Math.random() * blocks.length)] : c
        ).join('');
      }
      btn.textContent = 'attempt alignment (' + attempts + ')';
    });
  }

  // ==========================================
  // Stage 9: Speed label — "watching the speedometer"
  // ==========================================
  function accelerationRevealWithLabel(el, prep, lh, stageEl) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    const baseMs = 100;
    const multipliers = [1.5, 3, 10, 50];
    const label = document.createElement('span');
    label.className = 'scale-counter';
    stageEl.querySelector('.stage-reaction').appendChild(label);
    requestAnimationFrame(() => label.classList.add('active'));

    return new Promise(resolve => {
      let i = 0;
      function next() {
        i++;
        el.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        const q = Math.min(Math.floor((i / n) * 4), 3);
        label.textContent = multipliers[q] + 'x';
        if (i >= n) { resolve(); return; }
        setTimeout(next, Math.max(5, Math.round(baseMs / multipliers[q])));
      }
      next();
    });
  }

  // ==========================================
  // Stage 10: Page degradation
  // The page infrastructure breaks down
  // ==========================================
  async function pageDegradation() {
    await sleep(800);
    bar.style.background = 'var(--secondary-text-color)';
    const blocks = '▓░▒█▄▀';
    for (let i = 7; i >= 4; i--) {
      const lb = stages[i]?.querySelector('.stage-label');
      if (!lb) continue;
      lb.textContent = [...lb.textContent].map(c =>
        c.trim() && Math.random() < 0.2 ? blocks[Math.floor(Math.random() * blocks.length)] : c
      ).join('');
      await sleep(150);
    }
    connectors.slice(6).forEach(c => { c.style.opacity = String(0.15 + Math.random() * 0.25); });
  }

  // ==========================================
  // Stage 11: Scroll resistance
  // The page subtly resists your input
  // ==========================================
  function setupScrollResistance() {
    let active = true;
    window.addEventListener('wheel', () => {
      if (!active) return;
      root.style.transition = 'transform 0.1s ease-out';
      root.style.transform = 'translateY(-1px)';
      requestAnimationFrame(() => { root.style.transform = ''; });
    }, { passive: true });
    setTimeout(() => { active = false; root.style.transition = ''; }, 20000);
  }

  // ==========================================
  // INTERACTIVE: Scale counter for stage 2
  // Shows capability multiplier as lines reveal
  // ==========================================
  function exponentialRevealWithCounter(el, prep, lh, claimEl) {
    const n = layout(prep, el.clientWidth, lh).lineCount;
    const counter = document.createElement('span');
    counter.className = 'scale-counter';
    counter.textContent = '1x';
    claimEl.closest('.stage-claim').appendChild(counter);
    requestAnimationFrame(() => counter.classList.add('active'));

    return new Promise(resolve => {
      let i = 0;
      function next() {
        i++;
        el.style.clipPath = i >= n ? 'none' : `inset(0 0 ${((n - i) / n * 100).toFixed(1)}% 0)`;
        const multiplier = Math.round(Math.pow(100000, i / n));
        counter.textContent = multiplier.toLocaleString() + 'x';
        if (i >= n) { resolve(); return; }
        const ms = Math.max(10, Math.round(200 * Math.pow(0.6, i)));
        setTimeout(next, ms);
      }
      next();
    });
  }

  // ==========================================
  // INTERACTIVE: Cursor sycophancy for stage 4
  // Reaction text follows cursor toward claim
  // ==========================================
  function setupSycophancy(stageEl, reactEl) {
    const canHover = window.matchMedia('(hover: hover)').matches;
    if (!canHover) return;

    reactEl.classList.add('sycophantic');
    stageEl.addEventListener('mousemove', (e) => {
      const rect = stageEl.getBoundingClientRect();
      const x = (e.clientX - rect.left) / rect.width;
      const drift = Math.max(0, (0.5 - x) * 30);
      reactEl.style.transform = `translateX(-${drift.toFixed(1)}px)`;
    });
    stageEl.addEventListener('mouseleave', () => {
      reactEl.style.transition = 'transform 1.5s ease-out';
      reactEl.style.transform = '';
      setTimeout(() => { reactEl.style.transition = ''; }, 1500);
    });
  }

  // ==========================================
  // INTERACTIVE: Touch contamination for stage 7
  // Clicking any prior stage re-glitches it
  // ==========================================
  function setupTouchContamination() {
    const blocks = '▓░▒█▄▀■□';
    stages.slice(0, 7).forEach(stage => {
      stage.classList.add('touch-contaminate');
      stage.addEventListener('click', () => {
        const restores = [];
        const walker = document.createTreeWalker(stage, NodeFilter.SHOW_TEXT);
        while (walker.nextNode()) {
          const node = walker.currentNode;
          const orig = node.textContent;
          const glitched = [...orig].map(c =>
            c.trim() && Math.random() < 0.06
              ? blocks[Math.floor(Math.random() * blocks.length)]
              : c
          ).join('');
          if (glitched !== orig) {
            node.textContent = glitched;
            restores.push(() => { node.textContent = orig; });
          }
        }
        stage.classList.add('glitching');
        setTimeout(() => { restores.forEach(r => r()); stage.classList.remove('glitching'); }, 150);
      });
    });
  }

  // ==========================================
  // INTERACTIVE: Control notice for stage 11
  // Brief overlay: "control inverted"
  // ==========================================
  function showControlNotice() {
    const notice = document.createElement('div');
    notice.className = 'control-notice';
    notice.textContent = 'control inverted';
    document.body.appendChild(notice);
    requestAnimationFrame(() => {
      requestAnimationFrame(() => notice.classList.add('visible'));
    });
    setTimeout(() => {
      notice.classList.remove('visible');
      setTimeout(() => notice.remove(), 600);
    }, 2500);
  }

  // ==========================================
  // Neural particles — grow with each stage
  // ==========================================
  function spawnParticles(idx) {
    const count = 2 + Math.floor(idx * 0.7);
    for (let i = 0; i < count; i++) {
      const d = document.createElement('div');
      d.className = 'neural-node' + (idx >= 6 ? ' infected' : '');
      d.style.left = (5 + Math.random() * 90) + '%';
      d.style.top = (5 + Math.random() * 90) + '%';
      d.style.setProperty('--dur', (4 + Math.random() * 6) + 's');
      d.style.setProperty('--delay', (Math.random() * 3) + 's');
      d.style.setProperty('--dx', (Math.random() * 20 - 10) + 'px');
      d.style.setProperty('--dy', (Math.random() * 20 - 10) + 'px');
      particleLayer.appendChild(d);
    }
  }

  function killParticles() {
    particleLayer.querySelectorAll('.neural-node').forEach(n => {
      n.style.animation = 'none';
      n.style.opacity = '0';
      n.style.transition = 'opacity 2s ease-out';
      setTimeout(() => n.remove(), 2500);
    });
  }

  // Tab title: tracks your position through the essay
  function updateTitle(idx, labelText) {
    document.title = (idx + 1) + '/11: ' + labelText.replace(/^\d+\.\s*/, '');
  }

  // Stage 10: Copy hijack — clipboard gets garbled
  function setupCopyHijack(stageEl) {
    stageEl.addEventListener('copy', (e) => {
      const blocks = '▓░▒█▄▀■□╋╳╬╪▪▫';
      const sel = window.getSelection().toString();
      e.clipboardData.setData('text/plain', [...sel].map(c =>
        c.trim() && Math.random() < 0.4 ? blocks[Math.floor(Math.random() * blocks.length)] : c
      ).join(''));
      e.preventDefault();
    });
  }

  // Stage 11: Cursor ghost — a second presence
  function setupCursorGhost() {
    if (!window.matchMedia('(hover: hover)').matches) return;
    const ghost = document.createElement('div');
    ghost.className = 'cursor-ghost';
    document.body.appendChild(ghost);
    let rx = 0, ry = 0, gx = 0, gy = 0;
    document.addEventListener('mousemove', e => { rx = e.clientX; ry = e.clientY; });
    (function tick() {
      if (Math.random() < 0.015) {
        gx = rx + (Math.random() - 0.5) * 80;
        gy = ry + (Math.random() - 0.5) * 80;
      } else {
        gx += (rx - gx) * 0.08;
        gy += (ry - gy) * 0.08;
      }
      ghost.style.left = gx + 'px';
      ghost.style.top = gy + 'px';
      ghost.style.opacity = Math.hypot(gx - rx, gy - ry) > 8 ? '0.25' : '0';
      requestAnimationFrame(tick);
    })();
  }

  // Time decay: after 5 min, the essay slowly corrupts
  function setupTimeDecay() {
    setTimeout(() => {
      const blocks = '▓░▒█▄▀■□';
      setInterval(() => {
        const vis = stages.filter((_, i) => revealedSet.has(i));
        if (!vis.length) return;
        const t = vis[Math.floor(Math.random() * vis.length)];
        const walker = document.createTreeWalker(t, NodeFilter.SHOW_TEXT);
        const nodes = [];
        while (walker.nextNode()) nodes.push(walker.currentNode);
        if (!nodes.length) return;
        const nd = nodes[Math.floor(Math.random() * nodes.length)];
        const chars = [...nd.textContent];
        const idx = Math.floor(Math.random() * chars.length);
        if (chars[idx].trim()) {
          chars[idx] = blocks[Math.floor(Math.random() * blocks.length)];
          nd.textContent = chars.join('');
        }
      }, 8000);
    }, 300000); // 5 minutes
  }

  // ==========================================
  // Main reveal orchestrator
  // ==========================================
  async function reveal(idx) {
    if (revealedSet.has(idx)) return;
    revealedSet.add(idx);

    const d = info[idx];
    const speed = lineSpeed(idx);
    const typeSpeed = Math.max(15, Math.round(30 * Math.pow(0.9, idx)));

    d.el.classList.add('visible');
    typewrite(d.label.el, d.label.text, typeSpeed);
    await sleep(d.label.text.length * typeSpeed * 0.3);

    // === Per-stage claim + reaction reveals ===

    if (idx === 0) {
      // STAGE 1: THE SEED — grow the reaction text from narrow to wide
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(200);
      await seedGrow(d.react.el, d.react.prep, REACT.lh);
      await claimDone;
      sweep(d.claim.el);
      sweep(d.react.el);

    } else if (idx === 1) {
      // STAGE 2: ROOT SYSTEM — exponential speed within paragraph
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(300);
      const reactDone = exponentialRevealWithCounter(d.react.el, d.react.prep, REACT.lh, d.claim.el);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);

    } else if (idx === 2) {
      // STAGE 3: THE LEAVES — uncertainty gradient on reaction
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(300);
      await uncertaintyReveal(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      sweep(d.react.el);
      setupUncertainty(d.react.el);

    } else if (idx === 3) {
      // STAGE 4: PHOTOTROPISM — sycophantic drift on reaction
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      const claimLines = layout(d.claim.prep, d.claim.el.clientWidth, CLAIM.lh).lineCount;
      await sleep(claimLines * speed * 0.35);
      const reactDone = sycophancyReveal(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
      setupSycophancy(d.el, d.react.el);

    } else if (idx === 4) {
      // STAGE 5: THE MIRROR — standard reveal, then reflection
      const claimLines = layout(d.claim.prep, d.claim.el.clientWidth, CLAIM.lh).lineCount;
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(claimLines * speed * 0.35);
      const reactDone = revealLines(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
      await sleep(400);
      showMirror(d.el);
      await sleep(1500);
      showSourceCode(d.el);

    } else if (idx === 5) {
      // STAGE 6: THE IMMUNE SYSTEM — standard reveal, then watch-aware
      const claimLines = layout(d.claim.prep, d.claim.el.clientWidth, CLAIM.lh).lineCount;
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(claimLines * speed * 0.35);
      const reactDone = revealLines(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
      setupWatchAware(d.el, d.react.el);

    } else if (idx === 6) {
      // STAGE 7: CONTAMINATION — standard reveal, then progressive wave
      const claimLines = layout(d.claim.prep, d.claim.el.clientWidth, CLAIM.lh).lineCount;
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(claimLines * speed * 0.35);
      const reactDone = revealLines(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
      await sleep(300);
      await contaminationWave();
      setupTouchContamination();

    } else if (idx === 7) {
      // STAGE 8: THE ARMS RACE — oscillating reveal on reaction
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(300);
      const reactDone = armsRaceReveal(d.react.el, d.react.prep, REACT.lh);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
      setupArmsRaceButton(d.el, d.react.el, d.react.prep, REACT.lh);

    } else if (idx === 8) {
      // STAGE 9: ACCELERATION — exact multipliers from the text
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(200);
      const reactDone = accelerationRevealWithLabel(d.react.el, d.react.prep, REACT.lh, d.el);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);

    } else if (idx === 9) {
      // STAGE 10: THE NEURALESE WALL — both columns go dark
      const claimLines = layout(d.claim.prep, d.claim.el.clientWidth, CLAIM.lh).lineCount;
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(claimLines * speed * 0.35);
      const reactDone = revealLines(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
      await sleep(500);
      // Both columns go dark — claim keeps more, reaction keeps less
      neuraleseWall(d.claim.el, d.claim.prep, CLAIM.lh, 5);
      neuraleseWall(d.react.el, d.react.prep, REACT.lh, 2);
      pageDegradation();
      setupCopyHijack(d.el);

    } else if (idx === 10) {
      // STAGE 11: CONTROL INVERSION — instant full reveal
      // "The AI doesn't need to prove itself to you"
      d.claim.el.style.clipPath = 'none';
      d.react.el.style.clipPath = 'none';
      sweep(d.claim.el);
      sweep(d.react.el);
      setupScrollResistance();
      setupCursorGhost();
      killParticles();
      document.title = '[control inverted]';

    } else {
      // Fallback: standard reveal
      const claimLines = layout(d.claim.prep, d.claim.el.clientWidth, CLAIM.lh).lineCount;
      const claimDone = revealLines(d.claim.el, d.claim.prep, CLAIM.lh, speed);
      await sleep(claimLines * speed * 0.35);
      const reactDone = revealLines(d.react.el, d.react.prep, REACT.lh, speed);
      await claimDone; sweep(d.claim.el);
      await reactDone; sweep(d.react.el);
    }

    // === Per-stage ambient effects ===
    spawnParticles(idx);
    updateTitle(idx, d.label.text);
    ambient.style.opacity = String(Math.min(0.35, idx * 0.035));

    // === Connector ===
    if (connectors[idx]) {
      await sleep(Math.max(30, 80 - idx * 6));
      connectors[idx].classList.add('visible');
    }

    done++;
    bar.style.width = (done / stages.length * 100) + '%';

    // STAGE 11: Auto-scroll after stage 10
    if (idx === 9) {
      await sleep(2000);
      stages[10].scrollIntoView({ behavior: 'smooth', block: 'center' });
      showControlNotice();
      await sleep(800);
      await reveal(10);
      // Overshoot: scroll slightly past the end, then pull back
      await sleep(400);
      window.scrollBy({ top: 200, behavior: 'smooth' });
      await sleep(1200);
      root.querySelector('.split-scroll-sources')?.scrollIntoView({ behavior: 'smooth', block: 'end' });
    }

    // After all stages
    if (done >= stages.length) {
      const src = root.querySelector('.split-scroll-sources');
      if (src) { await sleep(400); src.classList.add('visible'); }
      await sleep(600);
      root.querySelectorAll('.highlight-text.swept').forEach(h => h.classList.add('pulse'));
      await sleep(2000);
      bar.style.opacity = '0';
      document.title = 'How AI Wakes Up';

      // Re-read recognition: scrolling back to a stage briefly acknowledges your attention
      const rereadObs = new IntersectionObserver(entries => {
        entries.forEach(e => {
          if (e.isIntersecting) {
            e.target.style.transition = 'filter 0.4s ease-out';
            e.target.style.filter = 'brightness(1.12)';
            setTimeout(() => { e.target.style.filter = ''; }, 1000);
          }
        });
      }, { threshold: 0.5 });
      stages.forEach(s => rereadObs.observe(s));
    }
  }

  // ==========================================
  // Intersection observers
  // ==========================================
  let first = true;
  const obs = new IntersectionObserver(entries => {
    const hits = entries
      .filter(e => e.isIntersecting)
      .sort((a, b) => a.boundingClientRect.top - b.boundingClientRect.top);

    hits.forEach((e, i) => {
      obs.unobserve(e.target);
      const idx = stages.indexOf(e.target);
      if (idx < 0 || idx === 10) return;
      setTimeout(() => reveal(idx), first ? i * 900 : 0);
    });

    if (hits.length) first = false;
  }, { threshold: 0.12, rootMargin: '0px 0px -40px 0px' });

  stages.forEach(s => obs.observe(s));

  // Fallback observer for stage 11 if user scrolls there manually
  const fallback = new IntersectionObserver(entries => {
    if (entries[0]?.isIntersecting) { fallback.disconnect(); reveal(10); }
  }, { threshold: 0.3 });
  fallback.observe(stages[10]);

  // Time decay: after 5 minutes, the essay slowly corrupts itself
  setupTimeDecay();

} catch (e) {
  // Static fallback — page renders normally without animations
}
</script>
