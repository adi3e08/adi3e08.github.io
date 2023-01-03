---
layout: archive
permalink: /projects/
author_profile: False
---
{% include base_path %}
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
