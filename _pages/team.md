---
title: "QIT @ ICFO - Team"
layout: gridlay
excerpt: "QIT @ ICFO - Team"
sitemap: false
permalink: /team/
---

{% assign positions = "" %}
{% for member in site.data.team_members %}
{% unless positions contains member.position %}
{% assign positions = positions | append: member.position | append: "," %}
{% endunless %}
{% endfor %}
{% assign positions = positions | split: "," %}

Filter by position:
<div class="btn-group btn-group-justified" data-toggle="buttons">
{% for position in positions %} <label class="btn btn-default active filter">
<input class="position" type="checkbox" autocomplete="on" checked onchange="somethingChanged()"> {{ position }}
</label>{% endfor %}
</div>
<button type="button" class="btn btn-default" onclick="setCheckboxes(true,'position')">All</button>
<button type="button" class="btn btn-default" onclick="setCheckboxes(false,'position')">None</button>
<br>

{% assign topics = "" %}
{% for member in site.data.team_members %}
{% for topic in member.topics %}
  {% unless topics contains topic %}
    {% assign topics = topics | append: topic | append: "," %}
  {% endunless %}
{% endfor %}
{% endfor %}
{% assign topics = topics | split: "," %}

Filter by topic:
<div class="btn-group btn-group-justified" data-toggle="buttons">
{% for topic in topics %}<label class="btn btn-default active filter">
<input class="topic" type="checkbox" autocomplete="on" checked onchange="somethingChanged()"> {{ topic }}
</label>{% endfor %}
</div>
<button type="button" class="btn btn-default" onclick="setCheckboxes(true,'topic')">All</button>
<button type="button" class="btn btn-default" onclick="setCheckboxes(false,'topic')">None</button>

<script>

    // Called when one of the filters is changed
    function somethingChanged() {
        var allowedPositions = [];
        var allowedTopics = [];
        document.querySelectorAll('input[type="checkbox"].position').forEach((cb) => {
            if (cb.checked) {
                allowedPositions.push(cb.nextSibling.textContent.trim().replace(/ /g, "-"));
            }
        });
        document.querySelectorAll('input[type="checkbox"].topic').forEach((cb) => {
            if (cb.checked) {
                allowedTopics.push(cb.nextSibling.textContent.trim().replace(/ /g, "-"));
            }
        });
        console.log(allowedPositions);
        console.log(allowedTopics);
        document.querySelectorAll('.person').forEach((row) => {
            var hasPosition = false;
            var hasTopic = false;
            allowedPositions.forEach((position) => {
                if (row.classList.contains(position)) {
                    hasPosition = true;
                }
            });
            allowedTopics.forEach((topic) => {
                if (row.classList.contains(topic)) {
                    hasTopic = true;
                }
            });
            if (hasPosition && hasTopic) {
                row.style.display = 'inline-block';
            } else {
                row.style.display = 'none';
            }
        });
    }

    // When one of the all/none buttons is pressed, set all checkboxes to the value
    function setCheckboxes(value, section) {
        document.querySelectorAll('input[type="checkbox"]').forEach((cb) => {
            if (section && cb.classList.contains(section)) {
                cb.checked = value;
                cb.parentElement.classList.toggle('active', value);
            }
        });
        somethingChanged();
    }

</script>

{% for position in positions %}<h2 id=header{{ position | replace: " ","_" }}>{{ position }}</h2>
{% assign number_printed = 0 %}
{% for member in site.data.team_members %}
{% if member.position == position %}
<!--{% assign even_odd = number_printed | modulo: 2 %}-->
<!--{% if even_odd == 0 %}-->
<!--<div class="row">-->
<!--{% endif %}-->
<div class="col-sm-6 clearfix person {{ member.position | replace: " ", "-" }} {{ member.topics | join: "," | replace: " ", "-" | replace: ",", " " }}">
<img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ member.photo }}" class="img-responsive" width="25%" style="float: left" />
<h4>{{ member.name }}</h4>
<i>{{ member.info }}<br><{{ member.email }}></i>
<ul style="overflow: hidden">
{% for topic in member.topics %}{% if topic != "" %}<li> {{ topic }} </li>{% endif %}{% endfor %}
</ul>
</div>
<!--{% assign number_printed = number_printed | plus: 1 %}-->
<!--{% if even_odd == 1 %}-->
<!--</div>-->
<!--{% endif %}-->
{% endif %}
{% endfor %}
<!--{% assign even_odd = number_printed | modulo: 2 %}-->
<!--{% if even_odd == 1 %}-->
<!--</div>-->
<!--{% endif %}-->
{% endfor %}

