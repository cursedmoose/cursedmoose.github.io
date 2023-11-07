---
layout: page
title: CursedMoose
---

Hi I'm the guy that made this. Sorry.

<h2>Rewards</h2>
<ul>
  {% assign filtered_posts = site.categories.reward | where:post.author, cursedmoose %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">{{ post.reward }}</a></li>
  {% endfor %}
</ul>