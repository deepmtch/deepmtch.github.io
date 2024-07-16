---
layout: page
title: Tools
---
<div class="tools-container">
  <div class="tools-grid">
    {% for item in site.static_files %}
      {% if item.path contains 'tools/' and item.path contains '/index.html' and item.path != 'tools/index.html' %}
        {% assign tool_name = item.path | split: '/' | slice: -2 | first %}
        <div class="tool-item">
          <a href="{{ site.baseurl }}{{ item.path | remove: 'index.html' }}">
            <div class="icon-container">
              <i class="fas fa-tools"></i>
            </div>
            <h3>{{ tool_name | capitalize }}</h3>
          </a>
        </div>
      {% endif %}
    {% endfor %}
  </div>
</div>

<style>
  .tools-container {
    display: flex;
    justify-content: center;
    width: 100%;
    padding: 20px;
    box-sizing: border-box;
  }
  .tools-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 30px;
    max-width: 1000px;
    width: 100%;
  }
  .tool-item {
    background-color: #f8f9fa;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    padding: 20px;
    text-align: center;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    width: 200px;
  }
  .tool-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
  }
  .icon-container {
    background-color: #007bff;
    color: white;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 auto 15px;
  }
  .icon-container i {
    font-size: 24px;
  }
  .tool-item h3 {
    margin: 0;
    color: #333;
    font-size: 18px;
  }
  .tool-item a {
    text-decoration: none;
    color: inherit;
  }
</style>

<!-- Add Font Awesome for icons -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">