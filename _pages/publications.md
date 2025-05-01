---
title: "QIT @ ICFO - Publications"
layout: gridlay
excerpt: "QIT @ ICFO -- Publications."
sitemap: false
permalink: /publications/
---

# Publication Highlights

{% for publi in site.data.publist %}

<div class="row">

<div class="clearfix">
 <div class="well">
  <pubtit>{{ publi.title }}</pubtit>
  <p>{{ publi.description }}</p>
  <p><em>{{ publi.authors }}</em></p>
  <p><strong><a href="{{ publi.link.url }}">{{ publi.link.display }}</a></strong></p>
  <p class="text-danger"><strong> {{ publi.news1 }}</strong></p>
  <p> {{ publi.news2 }}</p>
 </div>
</div>

</div>

{% endfor %}


