---
layout: page
title : Examples
bootstrap: true
---

<div class="row">
  {% for snippet in site.data.code_snippets %}
    {% include code_snippet.html snippet=snippet %}
  {% endfor %}
</div>
