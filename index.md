---
layout: page
title: A Blog of ArcTanSusan
---
{% include JB/setup %}
## About This Blog
This static blog contains technical post-it notes, insightful reviews, and random observations of a software engineer in San Francisco.

## About Susan Tan
I live and work in San Francisco. I've lived my first 18 years of life in Brooklyn, NYC. I sometimes blog about books and art here.

I can be found @ArcTanSusan on Twitter and on IRC. My email is susan.tan.fleckerl@gmail.com.

## Past Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
