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
---

{% include feature_row id="intro" type="center" %}

{% for post in site.posts %}
{include feature_row image_path={{post.base_img_url}}}
{% endfor %}
