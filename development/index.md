---
layout: default
title: "Development"
description: 개발과 관련하여 정리하고 싶은 내용이나 남겨두고 싶은 이야기.
main: true
project-header: true
header-img: img/developer.jpg
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.development == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>