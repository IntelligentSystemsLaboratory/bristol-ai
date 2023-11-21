---
title: "Bristol.AI - People"
layout: gridlay
excerpt: "Bristol.AI: People"
sitemap: false
permalink: /people/
---

# People @ Bristol.AI

Sorted alphabetically on last name. 

{% assign number_printed = 0 %}
{% assign people_sorted = site.data.people | sort:'last' %}
{% for person in people_sorted %}

{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ person.ID }}.jpg" class="img-responsive" width="25%" style="float: left" />
  <h4>[{{ person.title }} {{ person.first }} {{ person.last }}](mailto:{{ person.email }}?subject=Bristol.AI)</h4>
  <p><i>[{{ person.position }}]({{ person.web }})</i></p>
  <p>{{ person.role }}</p>
  {% if person.scholar %}
  [Google Scholar](https://scholar.google.com/citations?user={{ person.scholar }})
  {% endif %}

  {% assign member_groups = "" %}
  {% assign add_comma = false %}

  {% for group in site.data.groups %}
    {% if group.members contains person.ID or group.members2 contains person.ID %}
        {% assign member_groups = member_groups | append: '<a href="' | append: group.link.url | append: '">' | append: group.name | append: '</a>' %}
    {% endif %}
  {% endfor %}

  {% assign assigned_groups = "" %}

  {% for group in member_groups %} 
    {% assign assigned_groups = assigned_groups | append: group %}
    {% assign add_comma = true %}
  {% endfor %}

  {% if member_groups != "" %}
  {{ member_groups | replace: '</a><a', '</a>, <a' | append: '.' | markdownify }}
  {% endif %}


  {% if person.orcid %}
  [ORCID](https://orcid.org/{{ person.orcid }})
  {% endif %}


  <ul style="overflow: hidden">

  {% if person.number_educ == 1 %}
  <li> {{ person.education1 }} </li>
  {% endif %}

  {% if person.number_educ == 2 %}
  <li> {{ person.education1 | markdownify}} </li>
  <li> {{ person.education2 | markdownify}} </li>
  {% endif %}

  </ul>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}




