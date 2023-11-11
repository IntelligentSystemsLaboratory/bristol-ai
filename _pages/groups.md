---
title: "Bristol.AI - Groups"
layout: gridlay
excerpt: "Bristol.AI -- Groups."
sitemap: false
permalink: /groups/
---


# AI Groups @ Bristol.AI

{% assign number_printed = 0 %}
{% for group in site.data.groups %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if group.core == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
 <div class="well">
  <grpstyle>{{ group.name }} ({{ group.acronym }})</grpstyle>
  <img src="{{ site.url }}{{ site.baseurl }}/images/grouppic/{{ group.image }}" class="img-responsive" width="33%" style="float: left" />
  <p>{{ group.description }}</p>
  <p>
  {% assign members_array = group.members | split: ',' %}{% for memberID in members_array %}{% for person in site.data.people %}{% if memberID == person.ID %}[{{ person.title }} {{ person.first }} {{ person.last }}]({{ person.web }}), {% endif %}{% endfor %}{% endfor %}{{ group.members2 }}
  </p>
  <p><strong><a href="{{ group.link.url }}">{{ group.acronym }} website</a></strong></p>
  <p class="text-danger"><strong> {{ group.news1 }}</strong></p>
  <p> {{ group.news2 }}</p>
 </div>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}

<p> &nbsp; </p>


## Associated AI groups

{% for group in site.data.groups %}
{% if group.core == 0 %}

  {{ group.title }} <br />
  <em>{{ group.members }} </em><br /><a href="{{ group.link.url }}">{{ group.link.display }}</a>

{% endif %}
{% endfor %}
