---
title: "ギャラリー"
toc: false
---

----

VRM4Uの利用例や検証結果です。Twitterで貼ったものからピックアップしています。

下に行くほど古いです。

----

{% assign files2 = site.static_files %}

{% for image in files2 %}
  {% if image.path contains 'gallery/' %}
<figure>

    {% if image.path contains '.png' or image.path contains '.jpg' %}
<img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
    {% endif %}
    {% if image.path contains '.mp4' %}
<video src="{{ site.baseurl }}{{ image.path }}" controls preload="none"></video>
    {% endif %}

</figure>
<br>
  {% endif %}
{% endfor %}


----
