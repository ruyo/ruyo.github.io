---
title: "a5"
toc: false
---


----

{% for image in site.static_files %}
  {% if image.path contains 'gallery/' %}
    <figure>
    <img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
    </figure>
  {% endif %}
{% endfor %}


----
