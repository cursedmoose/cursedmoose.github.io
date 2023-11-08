---
layout: default
title: Sheogorath
---

Yes it is I, Sheogorath. Behold my legally gray artwork!

<h2>Recent Paintings</h2>
<p style="width: 1660px; margin-left: -430px">
  {% assign filtered_posts = site.categories.painting %}
  {% for post in filtered_posts %}
    <a href="{{ post.url }}">
      <img src="{{post.image}}" width="400" alt="{{post.reward}}" />
    </a>
  {% endfor %}
</p>