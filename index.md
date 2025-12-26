---
layout: default
title: Home
---

# Welcome to the Lab

This is my dark little corner of the internet.

---

Posts found: **{{ site.posts | size }}**

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span> — {{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>
