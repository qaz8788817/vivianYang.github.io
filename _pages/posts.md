---
layout: archive
title: "Blog Posts"
permalink: /posts/
author_profile: true
---

<style>
  /* 1. 統一縮圖大小與比例 */
  .archive__item-teaser {
    width: 100%;
    height: 180px; /* 固定高度 */
    object-fit: cover; /* 裁切以填滿，不變形 */
    border-radius: 8px;
  }

  /* 2. 確保標題完整顯示，不重疊 */
  .archive__item-title {
    margin-top: 10px !important;
    line-height: 1.4;
    word-wrap: break-word;
  }

  /* 3. 限制摘要長度 (只留 2 行) */
  .archive__item-excerpt {
    font-size: 0.9em;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
    margin-top: 5px;
  }

  /* 4. 懸停效果增強 */
  .archive__item {
    padding: 10px;
    border-radius: 10px;
    transition: background 0.3s;
  }
  .archive__item:hover {
    background: rgba(0, 0, 0, 0.03);
  }

  /* 5. 分類詳情樣式 (收納效果) */
  details summary {
    cursor: pointer;
    padding: 10px;
    background: #f2f2f2;
    border-radius: 5px;
    margin-bottom: 10px;
    list-style: none;
    font-weight: bold;
  }
  details summary:hover { background: #e6e6e6; }
</style>

<div class="entries-grid">
  {% for post in site.posts %}
    {% include archive-single.html type="grid" %}
  {% endfor %}
</div>

<hr style="margin: 40px 0;">

<h3 class="archive__subtitle">View by Category</h3>

{% for category in site.categories %}
  <details>
    <summary>{{ category[0] }} ({{ category[1].size }})</summary>
    <div class="entries-grid">
      {% for post in category[1] %}
        {% include archive-single.html type="grid" %}
      {% endfor %}
    </div>
  </details>
{% endfor %}