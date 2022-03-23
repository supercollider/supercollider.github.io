---
layout: page
title : Projects
bootstrap: true
---

<div class="row">
{% for item in site.data.gallery %}
  <div class="col-md-6 mb-4">
    {% include gallery_card.md %}
  </div>
  {% endfor %}
</div>
