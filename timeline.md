---
bg: "photo68.jpg"
layout: page
permalink: /time/
title: "Timeline"
crawlertitle: "Timeline"
summary: "Timeline"
active: date
---

{% for date in site.date %}
  {% assign d = date | first %}
  {% assign posts = date | last %}

  <h2 class="category-key" id="{{ t | downcase }}">{{ t | capitalize }}</h2>

  <ul class="year">
    {% for post in posts %}
      {% if post.date contains d %}
        <li>
          {% if post.lastmod %}
            <a href="{{ post.url | relative_url}}">{{ post.title }}</a>
            <span class="date">{{ post.lastmod | date: "%Y-%m-%d"  }}</span>
          {% else %}
            <a href="{{ post.url | relative_url}}">{{ post.title }}</a>
            <span class="date">{{ post.date | date: "%Y-%m-%d"  }}</span>
          {% endif %}
        </li>
      {% endif %}
    {% endfor %} 
  </ul>

{% endfor %}
