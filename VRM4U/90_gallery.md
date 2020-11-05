---
title: "a6"
toc: false
---


----

{% assign files = site.static_files | sort | reverse %}

{% for image in files %}
  {% if image.path contains 'gallery/' %}
<figure>

    {% if image.path contains '.png' or image.path contains '.jpg' %}
<img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
    {% endif %}
    {% if image.path contains 'gallery/' %}
<video src="{{ site.baseurl }}{{ image.path }}" controls preload="none"></video>
    {% endif %}

</figure>
<br>
  {% endif %}
{% endfor %}


----
