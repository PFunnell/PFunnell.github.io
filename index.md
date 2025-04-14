# Welcome

Here you'll find a mix of:
- 🧠 AI/code explorations ([see all posts](/))
- ✍️ Personal reflections ([see all notes](/notes/))

---

## Latest Posts

{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url }}) <small>{{ post.date | date: "%b %-d, %Y" }}</small>
{% endfor %}
