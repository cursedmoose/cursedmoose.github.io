---
layout: page
title: CursedMoose
user: cursedmoose
---

Hi I'm the guy that made this. Sorry.

<h2>Activity</h2>
<ul>
  {% assign filtered_posts = site.posts | where: "author", page.user %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">[{{post.category}}] {{ post.reward }}</a></li>
  {% endfor %}
</ul>