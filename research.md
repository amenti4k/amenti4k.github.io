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
        <div id="auth-{{ post.title | slugify }}" class="auth-form">
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
  
  if (savedEmail) {
    content.querySelector('.auth-form').style.display = 'none';
    content.querySelector('.content-wrapper').style.display = 'block';
  }
  togglePost(element);
}

function verifyEmailForPost(button, postId) {
  const email = button.previousElementSibling.value;
  const allowedEmails = ['amenti4k@gmail.com']; // Hardcoded allowed email
  
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

function togglePost(element) {
  const content = element.nextElementSibling;
  const arrow = element.querySelector('.arrow');
  const isVisible = content.classList.contains('expanded');
  
  if (!isVisible) {
    content.classList.add('expanded');
    arrow.classList.add('rotated');
  } else {
    content.classList.remove('expanded');
    arrow.classList.remove('rotated');
  }
}
</script>

<style>
.auth-form {
  text-align: center;
  padding: 20px;
}

.auth-form input, .auth-form button {
  margin: 10px;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid var(--border-color);
}

.auth-form button {
  cursor: pointer;
  background: none;
  transition: all 0.2s ease;
}

.auth-form button:hover {
  background: var(--text-color);
  color: white;
}
</style>
