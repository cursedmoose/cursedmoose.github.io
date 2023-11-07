---
name: CursedMoose
---
Hi I'm the guy that made this. Sorry.

{% assign image_files = site.static_files | where: "image", true %}
{% for myimage in image_files %}
  <h1>{{ myimage.basename }}</h1>{{ myimage.modified_time }}

  ![{{ myimage.basename }}]({{ myimage.path }})
{% endfor %}