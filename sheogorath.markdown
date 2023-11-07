---
layout: default
title: Sheogorath
---

Yes it is I, Sheogorath. Behold my artwork!

<h2>Recent Paintings</h2>
<ul>
  {% assign filtered_posts = site.categories.painting | where: post.author, sheogorath %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">{{ post.reward }}</a></li>
  {% endfor %}
</ul>

