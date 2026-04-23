---
layout: single
title: "Research Library"
permalink: /research/
author_rpfile: true
---

這裡是我的研究知識庫，包含 dMRI 指標、機器學習與臨床應用。

{% assign research_groups = site.research | group_by: 'topic' %}

{% for group in research_groups %}
  ## {{ group.name }}
  <ul>
    {% for item in group.items %}
      <li>
        <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}