---
layout: archive
title: Projects
permalink: /projects/
author_profile: False
---
{% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %}

{% include base_path %}

<h2>Research</h2>
{% for post in site.portfolio reversed %}
  {% if post.project_type == 'research' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}

<h2>Theses</h2>
{% for post in site.portfolio reversed %}
  {% if post.project_type == 'thesis' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}

<h2>Miscellaneous</h2>
{% for post in site.portfolio reversed %}
  {% if post.project_type == 'others' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}
