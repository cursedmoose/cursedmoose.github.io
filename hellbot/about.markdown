---
layout: page
title: About
permalink: /about/
---

This is the homepage for Hellbot, an AI powered Twitch assistant created by CursedMoose.
This website describes the capabilities and showcases the creations of Hellbot.

<ul>
    {% for img in site.assets.images %}
      <li>
        <h2><a href="{{ user.url }}">{{ user.name }}</a></h2>
        <p>{{ user.content | markdownify }}</p>
      </li>
    {% endfor %}
</ul>