---
layout: page
title: Category
permalink: /category/
sitemap: false
---

<div>
    {% assign categories = site.categories | sort %}
    {% for category in categories %}
        <span class="site-tag">
            <a href="#{{ category | first | slugify }}">
                    {{ category[0] | replace:'-', ' ' }} ({{ category | last | size }})
            </a>
        </span>
    {% endfor %}
</div>

<div id="index">
    {% for category in categories %}
        <a name="{{ category[0] }}"></a>
        <h2 class="post-list-heading">{{ category[0] | replace:'-', ' ' }} ({{ category | last | size }})</h2>
        {% assign sorted_posts = site.posts | sort: 'date' %}
        <ul class="post-list">
        {% for post in sorted_posts %}
            {%if post.categories contains category[0]%}
                <li>
                   <a href="{{ site.url }}{{ site.baseurl }}{{ post.url }}" title="{{ post.title }}">{{ post.title }} </a>
                </li>
            {%endif%}
        {% endfor %}
        </ul>
    {% endfor %}
</div>
