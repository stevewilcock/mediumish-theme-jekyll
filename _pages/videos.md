---
layout: page
title: Videos
permalink: /videos
comments: false
---

<div class="row justify-content-between">
    <div class="col-md-8 pr-5">
        {% assign sorted_cats = site.categories | sort %}
        {% for category in sorted_cats %}
            <a href="#">{{ category[0] }}</a>
            <br/>
        {% endfor %}

    </div>

    <div class="col-md-4">
        <div class="sticky-top sticky-top-80"></div>
    </div>
</div>
