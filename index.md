---
layout: default
title: Home
---

# Welcome to the Lab

This is my dark little corner of the internet.

---
{% assign post_count = site.posts | size %}

<p>Posts found: {{ post_count }}</p>

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span> — {{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>
