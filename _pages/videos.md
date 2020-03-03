---
layout: page
title: Videos
permalink: /videos
comments: false
---

<div class="article-post">
    <div class="row justify-content-between">
        <div class="col-md-8 pr-5">

            <!-- Get all the categories of posts with the tag video -->

            {% assign video_categories =  site.posts | where:"tags","video" | map: 'categories' | join: ',' | join: ',' | split: ',' | sort | uniq %}

            {% for video_category in video_categories %}

                {% assign total = 0 %}
                {% for post in site.posts %}
                    {% if post.categories contains video_category and post.tags contains "video"%}
                        {% assign total = total | plus: 1 %}
                    {% endif %}
                {% endfor %}

                <a href="/videos/{{video_category | replace:" ","" | downcase }}">{{ video_category }}</a> [{{total}}]
                <br/>
            {% endfor %}

        </div>

        <div class="col-md-4">
            <div class="sticky-top sticky-top-80"></div>
        </div>
    </div>
</div>
