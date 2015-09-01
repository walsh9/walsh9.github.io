---
layout: page
title: "Blog Posts"
class: blog-index
permalink: /blog/
---

<ul>
{% for post in site.posts %} 
    <li>
        <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date: "%m/%d/%Y" }}</time> 
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
    </li>
{% endfor %}
</ul>
<p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p>