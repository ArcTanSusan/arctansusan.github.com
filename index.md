---
layout: page
title: An Unremarkable TechBlog
---
{% include JB/setup %}

## About Susan Tan
I am a software engineer at Flixster with Rotten Tomatoes, where I work on the web application layer. I program in Python, Javascript, and Java. I live
and work in the great technology city of San Francisco, CA. I have previously lived in the glorious city known as New York City. I graduated from
a small liberal arts-engneering college in sunny Southern California.

On the open-source side, so as to incorporate more of the joys of Python in my life, I contribute to large Python projects, including Open Hatch, Django, and
the IPython notebook.

I can be found @ArcTanSusan on Twitter and on IRC. My email is susan.tan.fleckerl@gmail.com.

## About This Blog
This blog contains technical post-it notes, insights, and observations of a software engineer in Silicon Valley.

## Past Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
