---
layout: post
title:  "Building a Semantic Knowledge Graph from ChatGPT Conversations in Obsidian"
date:   2025-04-14 10:00:00 +0000
categories: [obsidian, ai, python]
---

![The search for meaning](/assets/images/explorer.png)

Over the 2 years I’ve had over 1,300 conversations with ChatGPT covering everything from local government and AI ethics to neurodivergence, coding, and digital tools.

Before OpenAI introduced the search feature I was getting frustrated with not being able to find some of the more interesting and useful conversations. Having given ChatGPT the classic "tell me something you know about me that I might not know about myself" prompt I was also curious about the overall content of the corpus and what insights I could glean from it.

So I built something. Or rather we, ChatGPT and I, did. This has been around a while but I finally got it dusted off and updated the repo.



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

![Obsidian graph view](/assets/images/metisem2.png)

^ This is a visualisation of my Obsidian vault after running the script — showing clusters of related notes linked by meaning, not keywords.

![Chat focus view](/assets/images/GPTethics.png)

^ And this is the first conversation I had on 9 Feb 2023, one of the more connected nodes.

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

## 🧪 What might come next

- Visual overlays of cluster topics in the graph
- GPT-generated summaries
- Semantically discovered hierearchical categories
- Time-aware linking (chronological progression of ideas)
- Interface it with Obsidian Canvas

---

I’m thinking of turning this into an Obsidian plugin. If you think that sounds useful, let me know.

→ [View it on GitHub](https://github.com/PFunnell/metisem)

---

Let me know if you're trying to tame a similar pile of markdown chaos.
