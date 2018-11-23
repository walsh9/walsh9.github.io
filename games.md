---
layout: page
title: "Games"
class: games
permalink: /games/
---

Here are some games I've made.

{% assign games = site.games | sort: 'sortorder' %}
{% for game in games %}
{% if game.font %}
<link href="http://fonts.googleapis.com/css?family={{ game.font }}&text={{ game.title }}" rel='stylesheet' type='text/css'>
{% endif %}
<article class="game-card">
    <h1 class="game-card__heading" style="font-family: '{{ game.font }}';"><a href="{{ game.home }}">{{ game.title }}</a></h1>
    {% if game.image %}
    <a href="{{ game.home }}"><img  class="game-card__image" alt="" src="../i/{{ game.image }}"/></a>
    {% endif %}

    <div class="game-card__description">{{game.content}}</div>
    {% if game.links %}
    <ul class="game-card__links">
    {% for link in game.links %}
        <li class="game-card__link"><a href="{{ link.url }}">{{ link.title }}</a></li>
    {% endfor %}
    </ul>
    {% endif %}
    {% if game.actions %}
    <ul class="game-card__buttons">
    {% for action in game.actions %}
        <li class="game-card__button"><a href="{{ action.url }}">{{ action.title }}</a></li>
    {% endfor %}
    </ul>
    {% endif %}
</article>
{% endfor %}