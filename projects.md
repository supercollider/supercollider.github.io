---
layout: page
title : Projects
bootstrap: true
---

<div class="row mt-4">
{% for item in site.data.gallery %}
  <div class="col-md-6 mb-5">
    {% include gallery_card.md %}
  </div>
  {% endfor %}
</div>
