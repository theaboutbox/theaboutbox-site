---
layout: default
---
<aside class="sidebar">
  {% if site.blog_index_asides.size %}
    {% include_array blog_index_asides %}
  {% else %}
    {% include_array default_asides %}
  {% endif %}
</aside>
