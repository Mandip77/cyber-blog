---
layout: default
---

## 🛠 Featured Projects & Labs
<div class="post-grid">
  {% for post in site.posts %}
    {% if post.categories contains 'pentesting' or post.categories contains 'labs' %}
    <div class="post-card">
      <a href="{{ post.url | relative_url }}" class="post-link">{{ post.title }}</a>
      <div class="post-meta">{{ post.date | date: "%b %-d, %Y" }} • [{% for cat in post.categories %}{{ cat }}{% if forloop.last == false %}, {% endif %}{% endfor %}]</div>
      <div class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 25 }}</div>
    </div>
    {% endif %}
  {% endfor %}
</div>

<br><br>

## 🎓 Academic Research & Presentations
<div class="post-grid">
  {% for post in site.posts %}
    {% if post.categories contains 'security' or post.categories contains 'presentation' %}
    <div class="post-card">
      <a href="{{ post.url | relative_url }}" class="post-link">{{ post.title }}</a>
      <div class="post-meta">{{ post.date | date: "%b %-d, %Y" }} • [{% for cat in post.categories %}{{ cat }}{% if forloop.last == false %}, {% endif %}{% endfor %}]</div>
      <div class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 25 }}</div>
    </div>
    {% endif %}
  {% endfor %}
</div>

<br><br>

## 🛡 Certifications
<div class="post-grid" style="grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));">
  {% for cert in site.data.certs %}
  <div class="post-card" style="align-items: center; text-align: center;">
    <h3 style="margin: 0;">{{ cert.title }}</h3>
    <div class="post-meta" style="margin-bottom: 0;">{{ cert.status }}</div>
  </div>
  {% endfor %}
</div>
