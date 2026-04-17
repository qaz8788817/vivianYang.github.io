---
layout: archive
title: "Research Projects"
permalink: /projects/
author_profile: true
---

<style>
  /* 讓專案列表看起來更像專業作品集 */
  .project-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    margin-top: 20px;
  }
  .project-card {
    border: 1px solid #eee;
    border-radius: 12px;
    overflow: hidden;
    transition: all 0.3s ease;
    text-decoration: none !important;
    color: inherit;
  }
  .project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
  }
  .project-img {
    width: 100%;
    height: 180px;
    object-fit: cover;
  }
  .project-info {
    padding: 15px;
  }
</style>

<div class="project-grid">
  {% for project in site.projects %}
    <a href="{{ project.url | relative_url }}" class="project-card">
      <img src="{{ project.header.teaser | relative_url }}" class="project-img">
      <div class="project-info">
        <h3 style="margin:0;">{{ project.title }}</h3>
        <p style="font-size: 0.9em; color: #666;">{{ project.excerpt }}</p>
      </div>
    </a>
  {% endfor %}
</div>