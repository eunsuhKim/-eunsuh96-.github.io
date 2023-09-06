---
layout: archive
title: "Category"
permalink: /category/
author_profile: true
---

{% for category in site.categories %}
  <h2 id="{{ category | first }}">{{ category[0] | replace:'-', ' ' }}</h2>
  <ul>
    {% for post in category.last %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}