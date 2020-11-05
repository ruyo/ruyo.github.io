---
title: "VRM4Uで扱うと楽しいデータ"
toc: false
---


----

{% for image in site.static_files %}
    {% if image.path contains 'asset/gallery' %}
        <img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
    {% endif %}
{% endfor %}


----
