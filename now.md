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
  margin-top: 0;
}

.command-line {
  margin: 3rem 0 2rem 0;
  color: var(--text-color);
  font-family: monospace;
  font-size: 15px;
  line-height: 1.7;
}

.command-line:first-child {
  margin-top: 0;
}

.command-line .prompt {
  color: var(--secondary-text-color);
  margin-right: 0.75rem;
}

.output-section {
  margin: 2.5rem 0;
  padding-left: 1.5rem;
  border-left: 2px solid var(--border-color);
}

.output-section h3 {
  color: var(--secondary-text-color);
  font-size: 16px;
  margin-bottom: 1.25rem;
  text-transform: lowercase;
  font-weight: 600;
  letter-spacing: 0;
}

.output-section p {
  line-height: 1.7;
  font-size: 15px;
}

.output-section ul {
  list-style: none;
  padding-left: 0;
  margin: 0;
}

.output-section li {
  margin-bottom: 0.75rem;
  line-height: 1.7;
}

.output-section li:before {
  content: "→ ";
  color: var(--secondary-text-color);
  margin-right: 0.75rem;
}

.output-text {
  color: var(--secondary-text-color);
  font-size: 14px;
  padding-left: 1.5rem;
  line-height: 1.6;
}
</style>
