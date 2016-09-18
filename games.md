---
layout: page
title: "Games"
class: games
permalink: /games/
---

Here are some games I've made.

{% assign games = site.games | sort: 'sortorder' %}
{% for game in games %}
<article class="project">
    <h1><a href="{{ game.home }}">{{ game.title }}</a></h1>
    {% if game.image %}
    <a href="{{ game.home }}"><img src="../i/{{ game.image }}"/></a>
    {% endif %}

    <p>{{game.content}}</p>
    {% if game.links %}
    <ul>
    {% for link in game.links %}
        <li>{{ link.title }}: <a href="{{ link.url }}">{{ link.url }}</a></li>
    {% endfor %}
    </ul>
    {% endif %}
</article>
{% endfor %}