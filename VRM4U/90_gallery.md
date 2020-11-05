---
title: "ギャラリー"
toc: false
---

----

VRM4Uの利用例や検証結果です。
Twitterで貼ったものからピックアップしています。

先頭は新しいもの、下に行くほど古いです。

----

<style type="text/css">
<!--
video {max-width: 100%;}
-->
</style>

{% for image in site.static_files reversed %}
  {% if image.path contains 'small/' %}
    {% continue %}
  {% endif %}
  {% if image.path contains 'gallery/' %}
    {% if image.path contains '.png' or image.path contains '.jpg' %}
<a href="{{ site.baseurl }}{{ image.path }}"><img src="{{ site.baseurl }}{{ image.path | replace: 'gallery/', 'gallery/small/' | replace: '.png', '.jpg' }}" alt="" /></a>
    {% endif %}
    {% if image.path contains '.mp4' %}
<video src="{{ site.baseurl }}{{ image.path }}" controls></video>
    {% endif %}
<hr />
  {% endif %}
{% endfor %}


----
