---
layout: page
title: Tags

---

<div class="page-content wc-container">
	<div class="post">
	<h2>category</h2>
  {% for category in site.categories %}
  <h3>{{ category | first }}({{ category | last | size }})</span></h3>
  <ul class="arc-list">
    {% for post in category.last %}
        <li>{{ post.date | date:"%d/%m/%Y"}}<a href="{{ site.baseurl}}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
  </ul>
  {% endfor %}
	</div>
</div>
