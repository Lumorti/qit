---
title: "QIT @ ICFO - Photos"
layout: piclay
excerpt: "QIT @ ICFO -- Photos"
permalink: /pictures/
---

# Photos

These aren't in chronological order, and I did my best to try to include some of everyone. If you want any of these taking down, don't hesitate to contact me (or someone else who has access to the site).

{% assign number_printed = 0 %}
{% for pic in site.data.pictures %}
<h3>{{ pic.title }}</h3>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/{{ pic.image }}" class="img-responsive"  style="display: block; max-height: 600px; ">{% endfor %}

