---
layout: page
permalink: /posts/
title: my blog
description: Mostly tech stuff, old journalistic writing, and mad ranting
---

<ul class="post-list">
  {% for post in site.posts %}
      <li>
          <h2><a class="post-title" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h2>
          <p class="post-meta">{{ post.date | date: '%B %-d, %Y — %H:%M' }}</p>
        </li>
  {% endfor %}
</ul>
