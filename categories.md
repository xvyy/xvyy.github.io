---
bg: "cate.jpg"
layout: page
permalink: /categories/
title: "Categorie"
crawlertitle: "Articles Categories"
summary: "Articles Categories"
active: categories
---

{% for categories in site.categories %}
  {% assign t = categories | first %}
  {% assign posts = categories | last %}

  <h2 class="category-key" id="{{ t | downcase }}">{{ t | capitalize }}</h2>

  <ul class="year">
    {% for post in posts %}
      {% if post.categories contains t %}
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
