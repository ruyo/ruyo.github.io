---
title: "VRM4Uで扱うと楽しいデータ"
toc: false
---


----

{% assign image_files = site.static_files | where: "image", true %}
{% for myimage in image_files %}
  {{ myimage.path }}
  {% if myimage.path contains '/gallery/' %}
    <figure class="image">
      <img src="{{ site.baseurl }}{{ myimage.path }}" alt="image" />
    </figure>
  {% endif %}
{% endfor %}

----
