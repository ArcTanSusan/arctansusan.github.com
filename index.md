---
layout: page
title: A Blog of ArcTanSusan
---
{% include JB/setup %}

## About Susan Tan
I'm a software engineer and tea drinker in San Francisco. I have a special ability to turn tea into code. I code in Python and Javascript on both proprietary code bases and open source projects. I attend and give talks at technical conferences every year. This is a [list of past technical talks](speaker_resume.html) that I've given at various meetup groups and conferences.

Since Fall 2012, I've been living and working in the city of San Francisco. Before I moved to San Francisco, I've lived my first 22 years of life in Brooklyn, NYC. I love living in cities, because I believe in being physically close to everything around me and avoid ever having to use a car in my life.

## About This Blog
This static blog contains technical post-it notes and random observations of a software engineer in San Francisco. I blog 
about books that I've read, ballet, art museums, and software engineering topics here. The blog posts here are in chronological order. None of my posts are organized by topic. This is a large unorganized pile of my thoughts pertaining to the craft of software engineering, my thoughts on ballet performances, my thoughts on art museum exhibits in various cities.

## How to Contact Me
* Email: susan.tan.fleckerl@gmail.com
* IRC freenode: @ArcTanSusan
* [Twitter](https://www.twitter.com/ArcTanSusan), [LinkedIn](https://www.linkedin.com/in/susan-tan-31748421), [Github](https://www.github.com/onceuponatimeforever)

## Past Blog Posts
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
