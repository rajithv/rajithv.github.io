---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

For a complete and up-to-date list of my publications, please visit my <u><a href="https://scholar.google.com/citations?user=ZRSyjGIAAAAJ&hl=en">Google Scholar profile</a></u>.

{% for post in site.publications reversed %}
  <hr>
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p><em>{{ post.venue }}, {{ post.date | date: "%Y" }}</em></p>
  <p>{{ post.excerpt }}</p>
{% endfor %}
