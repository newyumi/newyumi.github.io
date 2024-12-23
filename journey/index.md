---
layout: default
title: "Journey"
description: 아주 가끔씩 관심 분야의 글을 올려요.
main: true
project-header: true
header-img: images/journey-bg.jpg
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.journey == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>