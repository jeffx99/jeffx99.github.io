---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: musicalmorphisms
---

<h1 style="font-size: 70px; line-height: 85px; font-family: Cinzel; font-weight: normal; text-align: center; margin: 0;">Mm</h1>
<hr style="margin: auto">

_This page is still under construction..._


## Recent posts
<ul style="list-style:none; padding:0">
  {% for post in site.posts limit:5 %}
    {% unless post.categories contains 'composition' %}
      <li class="post-card">
        <a href="{{ post.url }}" style="text-decoration:none; font-size: 20px; font-weight: medium">{{ post.title }}</a>
        <br>
        {{ post.excerpt | strip_html | strip | append: ".." }}
      </li>
    {% endunless %}
  {% endfor %}
</ul>
