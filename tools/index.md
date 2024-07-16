---
layout: page
title: Tools
---

<div class="tools-grid">
  {% for item in site.static_files %}
    {% if item.path contains 'tools/' and item.path contains '/index.html' and item.path != 'tools/index.html' %}
      {% assign tool_name = item.path | split: '/' | slice: -2 | first %}
      <div class="tool-item">
        <a href="{{ site.baseurl }}{{ item.path | remove: 'index.html' }}">
          <img src="{{ site.baseurl }}/tools/{{ tool_name }}/icon.png" alt="{{ tool_name }} icon">
          <h3>{{ tool_name | capitalize }}</h3>
        </a>
      </div>
    {% endif %}
  {% endfor %}
</div>

<style>
  .tools-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
  }
  .tool-item {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
  }
  .tool-item img {
    max-width: 100px;
    height: auto;
  }
</style>