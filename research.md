---
layout: default
title: /research
permalink: /research/
---

<div class="post-list">
  {% for post in site.categories.research %}
    <div class="post-item">
      <h2 class="post-title" onclick="checkAccessAndToggle(this)" id="post-{{ post.title | slugify }}">
        <span class="arrow">›</span>
        <span class="title-text">{{ post.title }}</span>
        <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      </h2>
      <div class="post-content">
        <div id="auth-{{ post.title | slugify }}" class="auth-form" style="display: none;">
          <h3>Enter your email to access this document</h3>
          <input type="email" placeholder="Enter your email">
          <button onclick="verifyEmailForPost(this, '{{ post.title | slugify }}')">Submit</button>
        </div>
        <div class="content-wrapper" style="display: none;">
          {{ post.content }}
        </div>
      </div>
    </div>
  {% endfor %}
</div>

<script>
function checkAccessAndToggle(element) {
  const postId = element.id;
  const content = element.nextElementSibling;
  const accessMap = JSON.parse(localStorage.getItem('documentAccess') || '{}');
  const savedEmail = accessMap[postId];
  const arrow = element.querySelector('.arrow');
  const isVisible = content.classList.contains('expanded');
  
  // First collapse all posts
  document.querySelectorAll('.post-content').forEach(post => {
    post.classList.remove('expanded');
  });
  document.querySelectorAll('.arrow').forEach(arr => {
    arr.classList.remove('rotated');
  });
  
  if (!isVisible) {
    content.classList.add('expanded');
    arrow.classList.add('rotated');
    if (savedEmail) {
      content.querySelector('.auth-form').style.display = 'none';
      content.querySelector('.content-wrapper').style.display = 'block';
    } else {
      content.querySelector('.auth-form').style.display = 'block';
      content.querySelector('.content-wrapper').style.display = 'none';
    }
  } else {
    content.classList.remove('expanded');
    arrow.classList.remove('rotated');
  }
}

function verifyEmailForPost(button, postId) {
  const email = button.previousElementSibling.value;
  const allowedEmails = ['amenti4k@gmail.com'];
  
  if (allowedEmails.includes(email)) {
    const contentDiv = button.closest('.post-content');
    contentDiv.querySelector('.auth-form').style.display = 'none';
    contentDiv.querySelector('.content-wrapper').style.display = 'block';
    
    const accessMap = JSON.parse(localStorage.getItem('documentAccess') || '{}');
    accessMap[postId] = email;
    localStorage.setItem('documentAccess', JSON.stringify(accessMap));
  } else {
    alert('Access denied. Please contact the administrator.');
  }
}
</script>

<style>
.post-list {
  max-width: 650px;
  margin: 0 auto;
  font-size: 14px;
}

.post-item {
  margin-bottom: 1rem;
}

.post-title {
  cursor: pointer;
  padding: 0.5rem 0;
  margin: 0;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  font-size: 14px;
  font-weight: normal;
  color: var(--text-color);
}

.post-title:hover {
  background: var(--highlight-color);
}

.arrow {
  margin-right: 0.5rem;
  display: inline-block;
  color: var(--secondary-text-color);
}

.arrow.rotated {
  transform: rotate(90deg);
}

.post-date {
  margin-left: auto;
  font-size: 13px;
  color: var(--secondary-text-color);
  font-weight: normal;
}

.post-content {
  max-height: 0;
  overflow: hidden;
  padding: 0;
}

.post-content.expanded {
  max-height: none;
  padding: 1rem 0;
  font-size: 14px;
  line-height: 1.6;
}

.auth-form {
  text-align: center;
  padding: 1.5rem;
}

.auth-form h3 {
  margin-top: 0;
}

.auth-form input, .auth-form button {
  margin: 0.5rem;
  padding: 0.5rem;
  border: 1px solid var(--border-color);
  font-family: inherit;
  font-size: 14px;
  background-color: var(--background-color);
  color: var(--text-color);
}

.auth-form button {
  cursor: pointer;
  background: var(--text-color);
  color: var(--background-color);
}

.auth-form button:hover {
  background: var(--highlight-color);
  color: var(--text-color);
}
</style>
