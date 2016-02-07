---
layout: page
title: A Blog of ArcTanSusan
---
{% include JB/setup %}

## About Susan Tan
Since Fall 2012, I've lived and worked in San Francisco. I've lived my first 18 years of life in Brooklyn, NYC.

## About This Blog
This static blog contains technical post-it notes and random observations of a software engineer in San Francisco. I blog 
about books that I've read, ballet, art museums, and software engineering topics here. The blog posts here are in chronological order. None of my posts are organized by topic.


## How to Contact Me
Twitter: @ArcTanSusan
IRC @ArcTanSusan
Email: susan.tan.fleckerl@gmail.com.


## Past Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
