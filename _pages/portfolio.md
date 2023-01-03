---
layout: archive
permalink: /projects/
author_profile: False
---
<h1>Research</h1>
{% for post in site.portfolio reversed %}
  {% if post.project_type == 'research' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}

<h1>Theses</h1>
{% for post in site.portfolio reversed %}
  {% if post.project_type == 'thesis' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}

<h1>Miscellaneous</h1>
{% for post in site.portfolio reversed %}
  {% if post.project_type == 'others' %}
      {% include archive-single.html %}
  {% endif %}
{% endfor %}
