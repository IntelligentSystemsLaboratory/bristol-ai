---
title: "Bristol.AI - People"
layout: gridlay
sitemap: false
permalink: /people/
---

# People @ Bristol.AI

**Disclaimer**: Work in progress. If you have any concerns or want to provide additional information, please follow the *Get Involved* link at the top of this page. 

Sorted alphabetically on last name. 

{% assign number_printed = 0 %}
{% assign people_sorted = site.data.people | sort:'last' %}
{% for person in people_sorted %}

{% assign even_odd = number_printed | modulo: 2 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

{% assign image_path = "/images/teampic/" | append: person.ID | append: ".jpg" %}
{% assign placeholder_path = "/images/teampic/person.jpg" %}



<div class="col-sm-6 clearfix">
  <img src="{{ site.url }}{{ site.baseurl }}/images/teampic/{{ person.ID }}.jpg" class="img-responsive team-member-image" width="25%" style="float: left" />
  <h4>[{{ person.title }} {{ person.first }} {{ person.last }}](mailto:{{ person.email }}?subject=Bristol.AI)</h4>
  <p><i>[{{ person.position }}]({{ person.web }})</i></p>
  <p>{{ person.role }}</p>
  
  {% assign pub_links = "" %}
  {% if person.scholar %}
    {% assign pub_links = pub_links | append: '<a href="https://scholar.google.com/citations?user=' | append: person.scholar | append: '">Scholar</a>' %}
  {% endif %}
  {% if person.orcid %}
    {% assign pub_links = pub_links | append: '<a href="https://orcid.org/' | append: person.orcid | append: '">ORCID</a>' %}
  {% endif %}
  {{ pub_links | replace: '</a><a', '</a> - <a' | markdownify }}

  {% assign member_groups = "Member of: " %}
  {% assign add_comma = false %}

  {% for group in site.data.groups %}
    {% if group.members contains person.ID %}
        {% assign member_groups = member_groups | append: '<a href="' | append: group.link.url | append: '">' | append: group.acronym | append: '</a>' %}
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

<script>
  window.onload = function () {
    var images = document.querySelectorAll('.team-member-image');

    images.forEach(function (image) {
      checkImage(image);
    });

    function checkImage(image) {
      if (image.complete && image.naturalWidth === 0) {
        // Image has already loaded but with an error, replace with the default image
        image.src = '{{ site.url | append: site.baseurl }}/images/teampic/person.jpg';
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


