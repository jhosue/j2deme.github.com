---
layout: page
title: Archivo
comments: false
sharing: false
footer: false
icon: book
---

<div id="blog-archives">
{% for post in site.posts reverse %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  <div class="row">
    <div class="col-md-2">
      {% unless year == this_year %}
        {% assign year = this_year %}
        <h2>{{ year }}</h2>
      {% endunless %}
    </div>
    <div class="col-md-7">
      <article>
        {% include archive_post.html %}
      </article>
    </div>
  </div>
{% endfor %}
</div>
