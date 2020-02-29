---
layout: page
title: Videos
permalink: /videos
comments: false
---

<div class="row justify-content-between">
    <div class="col-md-8 pr-5">

        <!-- Get all the categories of posts with the tag video -->
        {% assign video_categories =  site.posts | where:"tags","video" | map: 'categories' | join: ',' | join: ',' | split: ',' | sort | uniq %}

        {% for video_category in video_categories %}
            {{ video_category }}
            <br/>
        {% endfor %}

    </div>

    <div class="col-md-4">
        <div class="sticky-top sticky-top-80"></div>
    </div>
</div>
