---
bg: "tags.jpg"
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
            <a href="{{ post.url | relative_url}}">{{ post.title }}</a>
            <span class="date">{{ post.lastmod | date: "%m-%d-%Y"  }}</span>
          {% else %}
            <a href="{{ post.url | relative_url}}">{{ post.title }}</a>
            <span class="date">{{ post.date | date: "%m-%d-%Y"  }}</span>
          {% endif %}
        </li>
      {% endif %}
    {% endfor %} 
  </ul>

{% endfor %}
