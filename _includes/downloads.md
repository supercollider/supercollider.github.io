The current version is **{{ site.data.downloads.current_version }}**:

<div class="row">
  {% for os in site.data.downloads.os %}
  <div class="col-md-4">
    <div class="card">
      <h3 class="text-center">{{ os.slug }}</h3>
      {% assign current = os.categories | where: 'key', 'current_version' | first %}
      {% for download in current.downloads limit:1 %}
        <p>{{ download.name }}</p>
        <a href="{{ download.link }}" class="btn btn-info">
          Get SuperCollider for {{ os.name }}
        </a>
      {% endfor %}
    </div>
  </div>
  {% endfor %}
  <p class="mt-5 pl-3">
    Can't find your OS or version? See all available versions on the <a href="{{ '/downloads' | relative_url }}">Downloads</a> page.
  </p>
</div>
