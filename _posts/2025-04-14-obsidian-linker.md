---
layout: post
title:  "Building a Semantic Knowledge Graph from ChatGPT Conversations in Obsidian"
date:   2025-04-14 10:00:00 +0000
categories: [obsidian, ai, python]
---

![The search for meaning](/assets/images/explorer.png)

I’ve been a ChatGPT plus customer for over two years and during that time I've had over 1,300 conversations with it covering everything from local government and AI ethics to neurodivergence, coding, and digital tools.

Before OpenAI introduced the search feature I was getting frustrated with not being able to find some of the more interesting and useful conversations that I knew were lurking in there somewhere. Having given ChatGPT the classic "tell me something you know about me that I might not know about myself" prompt I was also curious about the patterns in the corpus and what insights into my thinking and interests I could glean from it.

I'd also been dabbling with [Obsidian](https://obsidian.md/) for note taking and pondering [second brain learning theory](https://petermeglis.com/blog/unlock-your-brains-potential-a-beginners-guide-to-obsidian-and-building-a-second-brain/).

Then I discovered Superkikim's [Nexus AI Chat Importer](https://github.com/Superkikim/nexus-ai-chat-importer) plugin for Obsidian.

This worked great, but the graph of the imported chats looked like a dandelion seed, with everything connected to a central index but no interrelationships. I wasn't about to go through over 1000 chats and manually link them, surely there's a smarter way to do this?

So I built something. Or rather we, ChatGPT and I, did. 

I was trained in coding in the early 90s but never really put it into action, becoming an IT generalist early in my career. However, in the last few years I've had the privilige to lead a team of talented developers which has led me back into the deeper tech side of things, wrangling with devops and cloud architecture, and rekindled an interest in coding. I'll never be as good a coder as the rest of the team but using gen-AI and applying over 30 years of career knowledge I've got a few tricks up my sleeve. 

This project has been around a while but I finally got it dusted off and updated the repo, learning a few things about git, VScode, GitHub copilot and dipping a toe into a few other things like Jekyll static websites and Ruby in the process.



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
- Runs locally with CUDA support (tested on RTX 4060 in a Lenovo Legion Slim 5)

---

## 📸 Here's the Result

![Obsidian graph view](/assets/images/metisem2.png)

^ This is a visualisation, using Obsidian's in-built graph, of my vault after running the script, showing clusters of related notes linked by meaning, not keywords, and coloured by tags from a short high-level tag list that can be easily adjusted.

![Chat focus view](/assets/images/GPTethics.png)

^ And this is the first conversation I had with ChatGPT on 9 Feb 2023, one of the more connected nodes.

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

## 🧠 Why This Matters

This is about uncovering patterns in how we think. When ChatGPT helps us ideate or explain something, that output shouldn’t be stuck on OpenAI's servers or vanish into a markdown graveyard. It should become part of a living, evolving knowledge network.

By letting AI link our own AI-generated content, we turn our conversations into a map of our intellectual journeys.

And when visualised in Obsidian's graph view we get an intuitively explorable map of our AI-enhanced second brain.

This helps us find connections we would otherwise miss and to step up through layers of metacognition and cognitive offloading in a more productive and organised fashion.


---

## 🧪 What might come next

- Visual overlays of cluster topics in the graph
- GPT-generated summaries
- Semantically discovered hierearchical categories
- Time-aware linking (chronological progression of ideas)
- Interface it with Obsidian Canvas

---

I’m thinking of turning this into an Obsidian plugin. If that sounds useful let me know. Likewise, drop me a message if you have ideas about where we could take this or what you could apply it to.

---

## What's in a name?

We called this 'Metisem' a contraction of Metis, the pre-Olympian goddess of wisdom, counsel and deep thought and 'semantic'. A bit pretentious maybe but you've got to have a name. :blush: 

→ [View it on GitHub](https://github.com/PFunnell/metisem)

---


