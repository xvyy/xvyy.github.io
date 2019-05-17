---
bg: "photo36.jpg"
layout: page
permalink: /tags/
title: "Tags"
crawlertitle: "Articles Tags"
summary: "Articles Tags"
active: tag
---

{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

  <h2 class="category-key" id="{{ t | downcase }}">{{ t | capitalize }}</h2>

  <ul class="year">
    {% for post in posts %}
      {% if post.tags contains t %}
        <li>
          {% if post.lastmod %}
            <h3 href="{{ post.url | relative_url}}">{{ post.title }}</h3>
            <span class="date">{{ post.lastmod | date: "%d-%m-%Y"  }}</span>
          {% else %}
            <h3 href="{{ post.url | relative_url}}">{{ post.title }}</h3>
            <span class="date">{{ post.date | date: "%d-%m-%Y"  }}</span>
          {% endif %}
        </li>
      {% endif %}
    {% endfor %} 
  </ul>

{% endfor %}
