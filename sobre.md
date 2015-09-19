---
layout: page
permalink: /sobre/index.html
title: A OntheFrontLine
tags: [OntheFrontLine]
chart: true
---

{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}

Estamos contentes por tê-lo nesta página, este blog foi criado para compartilhar alguns tutoriais, lifehacks, bugs e tricks que definitivamente serão úteis para você. Atualmente temos {{ site.posts | size }} postagens em {{ site.categories | size }} categorias, combinadas temos um total de {{ total_words }} palavras, um leitor médio conseguiria ler em aproximadamente <span class="time">{{ total_readtime }}</span> minutos. {% if featuredcount != 0 %} Há um post em destaque - <a href="{{ site.url }}/featured">{{ featuredcount }} featured posts</a>, você definitivamente deveria lê-lo.{% endif %} A postagem mais recente é {% for post in site.posts limit:1 %}{% if post.description %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}">"{{ post.title }}"</a>{% else %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}" title="Leia mais sobre {{ post.title }}">"{{ post.title }}"</a>{% endif %}{% endfor %} publicada em {% for post in site.posts limit:1 %}{% assign modifiedtime = post.modified | date: "%Y%m%d" %}{% assign posttime = post.date | date: "%Y%m%d" %}<time datetime="{{ post.date | date_to_xmlschema }}" class="post-time">{{ post.date | date: "%d %b %Y" }}</time>{% if post.modified %}{% if modifiedtime != posttime %} e modificada   <time datetime="{{ post.modified | date: "%Y-%m-%d" }}" itemprop="dateModified">{{ post.modified | date: "%d %b %Y" }}</time>{% endif %}{% endif %}{% endfor %}. O último commit foi {{ site.time | date: "%A, %d %b %Y" }} as {{ site.time | date: "%I:%M %p" }} [UTC](http://en.wikipedia.org/wiki/Coordinated_Universal_Time "Temps Universel Coordonné").

