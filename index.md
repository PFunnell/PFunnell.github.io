---
layout: home
title: Paul's Notes & Notebooks
---

👋 **Hi, I’m Paul.** Welcome to my digital notebook.

Here’s where I share:

- 🧠 **Projects** — explorations in Python, AI, Obsidian workflows, and knowledge engineering
- ✍️ **Musings** — thoughts on neurodivergence, systems, ethics, and technology
- 💡 **Insights** — discoveries that emerge from conversations and curiosity

---

## ✍️ Latest Posts

{% for post in site.posts limit: 5 %}
- 📝 [**{{ post.title }}**]({{ post.url | relative_url }})  
  <small>{{ post.date | date: "%b %-d, %Y" }}</small>
{% endfor %}

[→ View all posts](/)

---

## 🗒 Latest Notes

{% assign notes = site.notes | sort: 'date' | reverse %}
{% for note in notes limit: 5 %}
- 📄 [**{{ note.title }}**]({{ note.url | relative_url }})  
  <small>{{ note.date | date: "%b %-d, %Y" }}</small>
{% endfor %}

[→ View all notes](/notes/)

---

## 📬 About This Site

This is a hybrid space — a blog, a lab notebook, and a collection of letters to myself.

If you're building things with language models, thinking about thinking, or reimagining systems — you're in good company.
