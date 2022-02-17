---
layout: page
title : Projects
bootstrap: true
---

<div class="row">
{% for item in site.data.gallery %}
  <div class="col-md-6 mb-4">
    <div class="card-deck">
      <div class="card h-100">
        <img class="card-img-top" src="{{ '/images/gallery/' | append: item.image | relative_url }}" alt="{{ item.image }}" title="{{ item.image }}">
        <div class="card-body">
          <h5 class="card-title">{{ item.title }}</h5>
          <p class="card-text">{{ item.text }}</p>
          <p class="card-text"><a href="{{ item.link }}" target="_blank">{{ item.link }}</a></p>
        </div>
      </div>
    </div>
  </div>
  {% endfor %}
</div>
