---
layout: archive
title: "Research"
permalink: /research/
author_profile: False
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

<!-- {% for post in site.portfolio reversed %}
  {% include archive-single.html %}
{% endfor %} -->

<h2>Research</h2>
{% for post in site.portfolio reversed %}
  {% if post.type == 'research' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}

<h2>Theses</h2>
{% for post in site.portfolio reversed %}
  {% if post.type == 'thesis' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}

<h2>Other Projects</h2>
{% for post in site.portfolio reversed %}
  {% if post.type == 'others' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}
