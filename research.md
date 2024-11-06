---
layout: protected
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
      <div class="post-content" style="display: none;">
        {{ post.content }}
      </div>
    </div>
  {% endfor %}
</div>

<script>
function checkAccessAndToggle(element) {
  const postId = element.id;
  const accessMap = JSON.parse(localStorage.getItem('documentAccess') || '{}');
  const savedEmail = accessMap[postId];
  
  if (!savedEmail) {
    const email = prompt("Please enter your email to access this document:");
    if (email) {
      verifyEmailForPost(email, postId, element);
    }
  } else {
    togglePost(element);
  }
}

function verifyEmailForPost(email, postId, element) {
  // This should match the allowed_emails in your post frontmatter
  const allowedEmails = {
    'research-document': ['amenti4k@gmail.com'],
    // Add more documents and their allowed emails here
  };
  
  if (allowedEmails[postId]?.includes(email)) {
    const accessMap = JSON.parse(localStorage.getItem('documentAccess') || '{}');
    accessMap[postId] = email;
    localStorage.setItem('documentAccess', JSON.stringify(accessMap));
    togglePost(element);
  } else {
    alert('Access denied. Please contact the administrator.');
  }
}

function togglePost(element) {
  const content = element.nextElementSibling;
  const arrow = element.querySelector('.arrow');
  const isVisible = content.style.display === 'block';
  
  if (!isVisible) {
    content.style.display = 'block';
    arrow.classList.add('rotated');
  } else {
    content.style.display = 'none';
    arrow.classList.remove('rotated');
  }
}
</script>
