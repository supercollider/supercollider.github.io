<div class="card-deck">
  <div class="card h-100">
    {% if item.type == 'vimeo' %}
      {% include vimeo.md id=item.id %}
    {% elsif item.type == 'youtube' %}
      {% include youtube.md id=item.id %}
    {% elsif item.type == 'image' %}
      <img class="card-img-top" src="{{ '/images/gallery/' | append: item.image | relative_url }}" alt="{{ item.image }}" title="{{ item.image }}">
    {% endif %}
    <div class="card-body">
      <h5 class="card-title">{{ item.title }}</h5>
      <p class="card-text">
        {{ item.text }}
        {% if item.author %}<br />By {{ item.author }}{% endif %}
      </p>
      {% if item.link %}
      <p class="card-text"><a href="{{ item.link }}" target="_blank">{{ item.link }}</a></p>
      {% endif %}
    </div>
  </div>
</div>
