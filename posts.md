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
  - image_path: { { include.base_img_url } }
    alt: { { include.base_name } }
    title: { { include.name } }
    excerpt: { { include.desc } }
    url: { { include.base_url } }
    btn_label: "Read More"
    btn_class: "btn--primary"
---

{% include feature_row id="intro" type="center" %}

{% for post in site.posts %}
{% include feature_row base_name={post.base_name} base_url={post.base_url} base_img_url={post.base_img_url} name={post.name} desc={post.desc} date={post.date} %}
{% endfor %}
