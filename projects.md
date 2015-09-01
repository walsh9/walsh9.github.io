---
layout: page
title: "Projects"
class: projects
permalink: /projects/
---

Here are some cool things I've made.
{% assign projects = site.projects | sort: 'sortorder' %}
{% for project in projects %}
<article class="project">
    <h1><a href="{{ project.home }}">{{ project.title }}</a></h1>
    {% if project.image %}
    <a href="{{ project.home }}"><img src="../i/{{ project.image }}"/></a>
    {% endif %}

    <p>{{project.content}}</p>
    {% if project.links %}
    <ul>
    {% for link in project.links %}
        <li>{{ link.title }}: <a href="{{ link.url }}">{{ link.url }}</a></li>
    {% endfor %}
    </ul>
    {% endif %}
</article>
{% endfor %}