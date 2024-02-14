---
title: "News"
layout: textlay
sitemap: false
permalink: /all_news.html
---

# News

{% for article in site.data.news %}
{{ article.date }} <br> {{ article.headline }}
{% endfor %}
