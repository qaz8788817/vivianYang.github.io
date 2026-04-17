<!-- ---
layout: archive
title: "Blog Posts"
permalink: /posts/
author_profile: true
entries_layout: grid
---
<div class="entries-list">
  {% for post in site.posts %}
    {% include archive-single.html %}
  {% endfor %}
</div> -->

---
layout: archive
title: "Blog Posts"
permalink: /posts/
author_profile: true
entries_layout: grid
---

{% include group-by-array collection=site.posts field="categories" %}