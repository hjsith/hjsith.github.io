---
title: "Posts"
layout: splash
date: 2016-03-23T11:48:41-04:00
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/posts.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
excerpt: "A 20 year old software engineer at heart!"
intro:
  - excerpt: "Hi"
feature_row:
    {% for post in site.posts %}
    - image_path: /assets/images/posts.jpg
        alt: {{ post.name }}
        title: {{ post.name }}
        excerpt: {{ post.desc }}
        {% assign url = '/posts/' | append post.raw-name | append '.html' %}
        url: {{ url }}
        btn_label: "Read"
        btn_class: "btn--primary"
    {% endfor %}
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}
