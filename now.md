---
layout: page
title: /now
permalink: /now/
---

<div class="terminal-output">
  <div class="command-line">
    <span class="prompt">$</span> cat /current/status.txt
  </div>

  <div class="output-section">
    <h3>// Current Focus</h3>
    <p>Update this section with what you're currently working on, learning, or thinking about.</p>
  </div>

  <div class="output-section">
    <h3>// Recent Projects</h3>
    <ul>
      <li>Add your current projects here</li>
    </ul>
  </div>

  <div class="output-section">
    <h3>// Reading / Learning</h3>
    <ul>
      <li>What you're currently reading or studying</li>
    </ul>
  </div>

  <div class="output-section">
    <h3>// Interests</h3>
    <p>Current interests and explorations</p>
  </div>

  <div class="command-line">
    <span class="prompt">$</span> last_updated
  </div>
  <div class="output-text">
    {{ "now" | date: "%Y-%m-%d %H:%M UTC" }}
  </div>
</div>

<style>
.terminal-output {
  margin-top: 2rem;
}

.command-line {
  margin: 2rem 0 1rem 0;
  color: var(--text-color);
  font-family: monospace;
}

.command-line .prompt {
  color: var(--secondary-text-color);
  margin-right: 0.5rem;
}

.output-section {
  margin: 2rem 0;
  padding-left: 1rem;
  border-left: 2px solid var(--border-color);
}

.output-section h3 {
  color: var(--secondary-text-color);
  font-size: 0.9rem;
  margin-bottom: 1rem;
  text-transform: lowercase;
}

.output-section ul {
  list-style: none;
  padding-left: 0;
}

.output-section li:before {
  content: "→ ";
  color: var(--secondary-text-color);
  margin-right: 0.5rem;
}

.output-text {
  color: var(--secondary-text-color);
  font-size: 0.9rem;
  padding-left: 1rem;
}
</style>
