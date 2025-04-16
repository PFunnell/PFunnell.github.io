---
layout: post
title:  "Building a Semantic Knowledge Graph from ChatGPT Conversations in Obsidian"
date:   2025-04-14 10:00:00 +0000
categories: [obsidian, ai, python]
---

![The search for meaning](/assets/images/explorer.png)

Over the past year, I’ve had over 1,300 conversations with ChatGPT — covering everything from local government and AI ethics to neurodivergence, coding, and digital tools.

Before OpenAI introduced the search feature I was getting frustrated with not being able to find some of the cool conversations I recalled having. Having given ChatGPT the classic "tell me something you know about me that I might not know about myself" prompt I was also curious about what the overall content of the corpus was and what insights I could glean from it.

So I built something. Or rather we, ChatGPT and I, did, before anyone was talking about 'vibe coding' let alone 'lego coding'



## 🛠 What we Built

Two Python scripts:

1. **`main.py`** — finds semantic similarity between markdown files and links them together with Obsidian-style `[[wikilinks]]`.
2. **`tagger.py`** — assigns smart tags to each file based on similarity to a predefined list of thematic tags.

The goal? Build a **self-organising knowledge graph** out of exported ChatGPT markdown files.

---

## 💡 How It Works

- Uses [Sentence Transformers](https://www.sbert.net/) to generate embeddings
- Caches embeddings for performance
- Calculates pairwise cosine similarity
- Adds Obsidian-style `[[links]]` to the bottom of each file
- Uses YAML frontmatter for tags (via `tagger.py`)
- Runs locally with GPU support (tested on RTX 4070 in a Lenovo Legion Slim 5)

---

## 📸 Here's the Result

![Obsidian graph view](/assets/images/metisem1.png)

^ This is a visualisation of my Obsidian vault after running the script — showing clusters of related notes linked by meaning, not keywords.

---

## ⚙️ Example Usage

```bash
python main.py vault_path \
  --clusters 40 \
  --similarity 0.6 \
  --title-weight 0.4 \
  --content-weight 0.6 \
  --batch-size 32 \
  --min-links 1 \
  --max-links 9 \
  --delete-links \
  --apply-links \
  --force-embeddings \
  --model gtr-x5-l
```

```bash
python tagger.py vault_path \
  --tags-file tags.txt \
  --apply-tags \
  --force-embeddings
```

---

## 🧪 What's Next

- Visual overlays of cluster topics in the graph
- GPT-generated summaries or categories
- Time-aware linking (chronological progression of ideas)
- Interface it with Obsidian Canvas

---

I’m thinking of turning this into a packaged tool — maybe even a plugin. If that sounds useful, let me know.

→ [View it on GitHub](#) _(coming soon)_

---

## 🔖 Bonus: Tags I Use

My `tags.txt` includes things like:

- `ai_and_automation`
- `neurodivergence`
- `ethics_and_policy`
- `education`
- `arts_and_cognition`
- `system_design`

Each one maps to a description and is matched semantically — not by string matching — which feels like the future of note organisation.

---

Let me know if you're trying to tame a similar pile of markdown chaos.
