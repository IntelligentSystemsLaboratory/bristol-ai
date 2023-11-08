---
title: "Bristol.AI - People"
layout: gridlay
excerpt: "Bristol.AI: People"
sitemap: false
permalink: /people/
---

# People

{% assign number_printed = 0 %}
{% for person in site.data.people %}

{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ person.ID }}.jpg" class="img-responsive" width="25%" style="float: left" />
  <h4>[{{ person.name }}](mailto:{{ person.email }}?subject=Bristol.AI)</h4>
  <p><i>[{{ person.position }}]({{ person.web }})</i></p>
  <p>{{ person.role }}</p>
  {% if person.scholar %}
  [Google Scholar](https://scholar.google.com/citations?user={{ person.scholar }})
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



