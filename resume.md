---
layout: page
title: /resume
permalink: /resume/
---

<div class="resume-container">
  <div class="resume-header">
    <div class="command-prompt">
      <span class="prompt">$</span> cat ~/resume.txt
    </div>
  </div>

  <div class="resume-content">
    <!-- Name and Contact -->
    <section class="resume-section">
      <div class="section-header">
        <h1>Amenti Kenea</h1>
        <div class="contact-links">
          <a href="https://twitter.com/amenti4k" target="_blank">twitter</a> //
          <a href="https://linkedin.com/in/amenti-kenea" target="_blank">linkedin</a> //
          <a href="https://github.com/amenti4k" target="_blank">github</a> //
          <a href="mailto:amenti@uni.minerva.edu">email</a>
        </div>
        <div class="location">NYC (via Addis Ababa → SF)</div>
      </div>
    </section>

    <!-- Experience -->
    <section class="resume-section">
      <h2 class="section-title"># Experience</h2>

      <div class="job-entry">
        <div class="job-header">
          <span class="job-title">Founding Engineer</span>
          <span class="job-company">@ Didero AI</span>
          <span class="job-date">2025 - Present</span>
        </div>
        <div class="job-location">New York, NY</div>
        <ul class="job-description">
          <li>Building autonomous AI systems for procurement - discovered it's really a distributed systems problem</li>
          <li>Processing large volumes of purchase orders daily through AI agents</li>
          <li>Architecting systems that handle procurement complexity better than traditional workflows</li>
        </ul>
      </div>

      <div class="job-entry">
        <div class="job-header">
          <span class="job-title">Data Scientist</span>
          <span class="job-company">@ Meta</span>
          <span class="job-date">2022 - 2024</span>
        </div>
        <div class="job-location">Core Ads Team - New York, NY</div>
        <ul class="job-description">
          <li>Built anomaly detection systems monitoring 140+ metrics for $100B+ annual revenue stream</li>
          <li>Led Thailand revenue investigation, preventing $1.76M/day revenue loss</li>
          <li>Developed executive reporting frameworks translating complex data insights for leadership</li>
          <li>Created production ML systems for ad performance optimization</li>
        </ul>
      </div>
    </section>

    <!-- Education -->
    <section class="resume-section">
      <h2 class="section-title"># Education</h2>

      <div class="education-entry">
        <div class="education-header">
          <span class="degree">B.S. Computer Science & Data Science</span>
          <span class="school">@ Minerva University</span>
          <span class="edu-date">2018 - 2022</span>
        </div>
        <div class="education-details">
          <div class="cities">San Francisco • Seoul • Hyderabad • Berlin • London</div>
          <div class="note">Rotational global campus program (<2% acceptance rate)</div>
        </div>
      </div>
    </section>

    <!-- Skills -->
    <section class="resume-section">
      <h2 class="section-title"># Technical Skills</h2>

      <div class="skills-grid">
        <div class="skill-category">
          <span class="skill-label">Languages:</span>
          <span class="skill-list">Python, SQL, JavaScript, R</span>
        </div>
        <div class="skill-category">
          <span class="skill-label">ML/AI:</span>
          <span class="skill-list">PyTorch, LangChain, Anthropic Claude, OpenAI APIs</span>
        </div>
        <div class="skill-category">
          <span class="skill-label">Data:</span>
          <span class="skill-list">Spark, Presto, BigQuery, Pandas, Statistical Modeling</span>
        </div>
        <div class="skill-category">
          <span class="skill-label">Tools:</span>
          <span class="skill-list">Git, Docker, AWS, Airflow, Jupyter</span>
        </div>
      </div>
    </section>

    <!-- Projects & Writing -->
    <section class="resume-section">
      <h2 class="section-title"># Projects & Interests</h2>

      <div class="project-entry">
        <div class="project-header">
          <span class="project-name">dontwalkinsoho</span>
          <span class="project-link"><a href="https://dontwalkinsoho.netlify.app" target="_blank">→ link</a></span>
        </div>
        <p class="project-desc">Founded NYC run club building community through movement</p>
      </div>

      <div class="project-entry">
        <div class="project-header">
          <span class="project-name">aava.club</span>
          <span class="project-link"><a href="https://aava.club" target="_blank">→ link</a></span>
        </div>
        <p class="project-desc">Online radio station curating music from Ethiopian jazz to UK garage</p>
      </div>

      <div class="project-entry">
        <div class="project-header">
          <span class="project-name">Technical Writing</span>
        </div>
        <p class="project-desc">Write about AI systems, data engineering, and developer tools</p>
      </div>
    </section>

    <!-- Footer -->
    <div class="resume-footer">
      <div class="command-prompt">
        <span class="prompt">$</span> <span class="footer-text">last updated: {{ site.time | date: "%B %Y" }}</span>
      </div>
      <div class="print-note">→ Use Cmd/Ctrl + P to print or save as PDF</div>
    </div>
  </div>
</div>

<style>
/* Resume Container */
.resume-container {
  max-width: 100%;
  margin: 0 auto;
  padding: 0;
}

.command-prompt {
  font-family: monospace;
  margin-bottom: 3rem;
  color: var(--secondary-text-color);
  font-size: 15px;
  line-height: 1.7;
}

.command-prompt .prompt {
  margin-right: 0.75rem;
}

/* Header */
.resume-header {
  margin-bottom: 3rem;
}

.section-header h1 {
  font-size: 32px;
  margin-bottom: 1rem;
  font-weight: 700;
  line-height: 1.2;
}

.contact-links {
  margin: 1rem 0 0.5rem;
  font-size: 15px;
  line-height: 1.7;
}

.contact-links a {
  color: var(--text-color);
  text-decoration: none;
  border-bottom: 1px solid var(--border-color);
  transition: border-color 0.2s;
}

.contact-links a:hover {
  border-bottom-color: var(--text-color);
}

.location {
  color: var(--secondary-text-color);
  font-size: 14px;
  margin-top: 0.5rem;
}

/* Sections */
.resume-section {
  margin-bottom: 4rem;
}

.section-title {
  font-size: 22px;
  margin-bottom: 2rem;
  color: var(--text-color);
  font-weight: 700;
  border-bottom: 1px solid var(--border-color);
  padding-bottom: 0.75rem;
  letter-spacing: -0.02em;
}

/* Job Entries */
.job-entry {
  margin-bottom: 3rem;
  padding-left: 1.5rem;
  border-left: 2px solid var(--border-color);
}

.job-header {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 0.75rem;
  margin-bottom: 0.5rem;
}

.job-title {
  font-weight: 600;
  font-size: 17px;
}

.job-company {
  color: var(--secondary-text-color);
  font-size: 15px;
}

.job-date {
  margin-left: auto;
  color: var(--secondary-text-color);
  font-size: 14px;
}

.job-location {
  color: var(--secondary-text-color);
  font-size: 14px;
  margin-bottom: 1rem;
}

.job-description {
  list-style: none;
  padding-left: 0;
  margin: 0;
}

.job-description li {
  margin-bottom: 0.75rem;
  padding-left: 1.5rem;
  position: relative;
  line-height: 1.7;
}

.job-description li:before {
  content: "→";
  position: absolute;
  left: 0;
  color: var(--secondary-text-color);
}

/* Education */
.education-entry {
  margin-bottom: 2rem;
  padding-left: 1.5rem;
  border-left: 2px solid var(--border-color);
}

.education-header {
  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 0.75rem;
  margin-bottom: 0.75rem;
}

.degree {
  font-weight: 600;
  font-size: 17px;
}

.school {
  color: var(--secondary-text-color);
  font-size: 15px;
}

.edu-date {
  margin-left: auto;
  color: var(--secondary-text-color);
  font-size: 14px;
}

.education-details {
  font-size: 14px;
  line-height: 1.7;
}

.cities {
  color: var(--secondary-text-color);
  margin-bottom: 0.5rem;
}

.note {
  color: var(--secondary-text-color);
  font-style: italic;
}

/* Skills */
.skills-grid {
  display: grid;
  gap: 1rem;
  padding-left: 1.5rem;
}

.skill-category {
  display: flex;
  gap: 1rem;
  line-height: 1.7;
}

.skill-label {
  font-weight: 600;
  min-width: 110px;
  color: var(--text-color);
  font-size: 15px;
}

.skill-list {
  color: var(--secondary-text-color);
  font-size: 15px;
}

/* Projects */
.project-entry {
  margin-bottom: 2rem;
  padding-left: 1.5rem;
}

.project-header {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  margin-bottom: 0.5rem;
}

.project-name {
  font-weight: 600;
  font-size: 16px;
}

.project-link a {
  color: var(--secondary-text-color);
  font-size: 14px;
  text-decoration: none;
  border-bottom: 1px solid transparent;
  transition: border-color 0.2s;
}

.project-link a:hover {
  border-bottom-color: var(--secondary-text-color);
}

.project-desc {
  color: var(--secondary-text-color);
  margin: 0;
  padding-left: 1.5rem;
  position: relative;
  line-height: 1.7;
  font-size: 15px;
}

.project-desc:before {
  content: "→";
  position: absolute;
  left: 0;
  color: var(--secondary-text-color);
}

/* Footer */
.resume-footer {
  margin-top: 5rem;
  padding-top: 2.5rem;
  border-top: 1px solid var(--border-color);
}

.footer-text {
  color: var(--secondary-text-color);
  font-size: 15px;
}

.print-note {
  margin-top: 1rem;
  color: var(--secondary-text-color);
  font-size: 14px;
  line-height: 1.6;
}

/* Print Styles */
@media print {
  .resume-container {
    max-width: 100%;
    padding: 0;
  }

  .command-prompt {
    display: none;
  }

  .print-note {
    display: none;
  }

  .resume-section {
    page-break-inside: avoid;
  }

  .job-entry, .education-entry, .project-entry {
    page-break-inside: avoid;
  }

  a {
    color: inherit;
    text-decoration: none;
  }

  .section-title {
    border-bottom: 1px solid #333;
  }

  .job-entry, .education-entry {
    border-left-color: #333;
  }
}

/* Mobile Responsiveness */
@media (max-width: 600px) {
  .job-header, .education-header {
    flex-direction: column;
    gap: 0.25rem;
  }

  .job-date, .edu-date {
    margin-left: 0;
  }

  .skill-category {
    flex-direction: column;
    gap: 0.25rem;
  }

  .skill-label {
    min-width: auto;
  }
}
</style>
