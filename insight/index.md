---
layout: default
title: "Insight"
description: PM 플레이북
main: true
project-header: true
header-img: images/insight2.jpg
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.insight == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>
