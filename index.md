---
layout: page
title: The TechBlog of ArcTanSusan
---
{% include JB/setup %}

## About Susan Tan
I'm a Python software engineer in San Francisco. I lived my first 18 years of life in NYC.

Previously, I worked as a web application software engineer at Flixster with Rotten Tomatoes. In Summer 2012, I graduated from a small liberal arts-engineering college in Southern California called Harvey Mudd College.

On the open-source side, I contribute to large Python projects, including Django and the IPython notebook. I also work on open source Django web applications such as OpenHatch.org and Air.Mozilla.Org.

I can be found @ArcTanSusan on Twitter and on IRC. My email is susan.tan.fleckerl@gmail.com.

## About This Blog
This blog contains technical post-it notes, insightful essays, and observations of a software engineer in San Francisco.

## Past Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
