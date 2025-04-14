---
layout: home
title: Paul's Notes & Notebooks
---

Welcome. I'm Paul — I use this space to share:

- 🧠 **Code projects** I'm building (often AI or Python focused)
- 📝 **Reflective notes** inspired by conversation, curiosity, and lived experience
- 📚 **Blog posts** about tools like Obsidian, ChatGPT, and knowledge work

---

### ✍️ Latest Posts

{% for post in site.posts limit: 5 %}
- [{{ post.title }}]({{ post.url | relative_url }}) <small>{{ post.date | date: "%b %-d, %Y" }}</small>
{% endfor %}

[→ View all posts](/)

---

### 🗒 Latest Notes

{% assign notes = site.notes | sort: 'date' | reverse %}
{% for note in notes limit: 5 %}
- [{{ note.title }}]({{ note.url | relative_url }}) <small>{{ note.date | date: "%b %-d, %Y" }}</small>
{% endfor %}

[→ View all notes](/notes/)
