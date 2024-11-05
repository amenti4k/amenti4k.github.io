---
layout: protected
title: /research
permalink: /research/
---

<div class="post-list">
  {% for post in site.categories.research %}
    <div class="post-item">
      <h2 class="post-title" onclick="togglePost(this)" id="post-{{ post.title | slugify }}">
        <span class="arrow">›</span>
        <span class="title-text">{{ post.title }}</span>
        <span class="post-date">{{ post.date | date: "%Y-%m-%d" }}</span>
      </h2>
      <div class="post-content">
        {{ post.content }}
      </div>
    </div>
  {% endfor %}
</div>
