---
title: "Bristol.AI - Groups"
layout: gridlay
excerpt: "Bristol.AI -- Groups."
sitemap: false
permalink: /groups/
---


# Research Groups @ Bristol.AI

**Disclaimer**: Work in progress. If you have any concerns or want to provide additional information, please follow the *Get Involved* link at the top of this page. 


## Core AI groups

> Researchers in these groups publish in core AI conferences and journals. 

{% assign number_printed = 0 %}
{% for group in site.data.groups %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if group.core == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6">
 <div class="well" style="height: 325px">
  <grpstyle>{{ group.name }} {% if group.acronym %} (<a href="{{ group.link.url }}">{{ group.acronym }}</a>) {% endif %}</grpstyle>

  <img src="{{ site.url }}{{ site.baseurl }}/images/grouppic/{{ group.GID }}.jpg" class="img-responsive group-image" width="45%" style="float: left" />

  <p><i>{{ group.description }}<i></p>
  <p>
  {% assign members_array = group.members | split: ',' %}{% for memberID in members_array %}{% for person in site.data.people %}{% if memberID == person.ID %}[{{ person.title }} {{ person.first }} {{ person.last }}]({{ person.web }}), {% endif %}{% endfor %}{% endfor %}{{ group.members2 }}
  </p>
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



## Associated AI groups

> Researchers in these groups employ state-of-the-art AI in their primary research domains. 

<ul>
{% for group in site.data.groups %}
{% if group.core == 0 %}

  <li>{{ group.name }} (<a href="{{ group.link.url }}">{{ group.acronym }})</a>
  <p><i>{{ group.description }}</i></p></li>

{% endif %}
{% endfor %}

<script>
  window.onload = function () {
    var images = document.querySelectorAll('.group-image');

    images.forEach(function (image) {
      checkImage(image);
    });

    function checkImage(image) {
      if (image.complete && image.naturalWidth === 0) {
        // Image has already loaded but with an error, replace with the default image
        image.src = '{{ site.url | append: site.baseurl }}/images/grouppic/group.png';
      } else if (!image.complete) {
        // Image is still loading, wait for the 'load' event
        image.onload = function () {
          if (image.naturalWidth === 0) {
            // Image loaded with an error, replace with the default image
            image.src = '{{ site.url | append: site.baseurl }}/images/teampic/person.jpg';
          }
        };
      }
    }
  };
</script>