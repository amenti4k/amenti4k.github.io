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
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

.post-item {
  margin-bottom: 1rem;
}

.post-title {
  cursor: pointer;
  padding: 1rem;
  margin: 0;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  font-size: 1rem;
  font-weight: 500;
  color: var(--text-color);
}

.arrow {
  margin-right: 0.5rem;
  transition: transform 0.3s ease;
  display: inline-block;
}

.arrow.rotated {
  transform: rotate(90deg);
}

.post-date {
  margin-left: auto;
  font-size: 0.8rem;
  color: var(--secondary-text);
  font-weight: normal;
}

.post-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.5s ease-out, padding 0.5s ease;
  padding: 0 1rem;
}

.post-content.expanded {
  max-height: none;
  padding: 1rem;
  transition: max-height 0.5s ease-in, padding 0.5s ease;
}

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
