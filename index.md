---
layout: page
title: The TechBlog of ArcTanSusan
---
{% include JB/setup %}
## About This Blog
This static blog contains technical post-it notes, insightful essays, and observations of a software engineer in San Francisco.

## About Susan Tan
I'm a Python software engineer in San Francisco. I lived my first 18 years of life in NYC.

Previously, from March 2013 to April 7, 2014, I was a web application software engineer at Flixster with Rotten Tomatoes, a movie-tech company in SF. In Summer 2012, I graduated with a degree in General Engineering from a small liberal arts-engineering undergraduate college called Harvey Mudd College located in forever-sunny Southern California.

On the open-source side, I contribute to large Python projects, including Django and the IPython notebook. I also work on open source Django web applications such as OpenHatch.org and Air.Mozilla.org. Why? Because Python.

I can be found @ArcTanSusan on Twitter and on IRC. My email is susan.tan.fleckerl@gmail.com.

## Past Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
