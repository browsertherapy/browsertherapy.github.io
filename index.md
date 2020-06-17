---
layout: home
toc: true
author_profile: true
---
{% for post in site.tags.featured %}
  <h1>{{ post.title }}</h1>  
  {{ post.content }}
{% endfor %}