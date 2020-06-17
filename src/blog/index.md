---
title: Blog
navorder: 3
---

These are latest news from [Pack11ty]{.pack11ty} :

<div class="stack">

{% for entry in collections.blog %}

  <article class="blog">
    <h2 class="blog__title"><a href="{{ entry.url }}">{{ entry.data.title }}</a></h2>
    <p class="blog__meta">{{ entry.date | date("Do MMMM YYYY") }}</p>
  </article>
{% endfor %}

</div>