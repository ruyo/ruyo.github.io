---
title: "ギャラリー"
toc: false
---

----

VRM4Uの利用例や検証結果です。Twitterで貼ったものからピックアップしています。

下に行くほど古いです。

----

{% for image in site.static_files reversed %}
  {% if image.path contains 'gallery/' %}
    {% if image.path contains '.png' or image.path contains '.jpg' %}
<img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
    {% endif %}
    {% if image.path contains '.mp4' %}
<video src="{{ site.baseurl }}{{ image.path }}" controls></video>
    {% endif %}
  {% endif %}
{% endfor %}


----
