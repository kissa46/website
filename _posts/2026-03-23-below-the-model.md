---
layout: post
title: "Below the Model"
title-up: "Below the Model"
title-down: "You can't model your way out of bad data"
intro: "Identity, ingestion, and why the corpus is the product — not the LLM."
date: 2026-03-23
image: /assets/images/sphere2.png
---

I wanted a simple way to follow specific AI researchers — not a feed, not an aggregator. Something that tracks what they publish, surfaces the papers worth reading, and lets me have a real conversation with them. Not a chatbot on top of an abstract. Something that downloads the full PDF, processes it locally, and reasons about it before answering.

Building it turned out to be mostly a data problem.

The first instinct when building with LLMs is to think about the LLMs. Which model, which retrieval strategy, how to structure the prompt. That's where the interesting decisions seem to live. It's also the wrong place to start.

<div class="post-inline-image-container">
  <img src="{{ '/assets/images/explainer-1bg.png' | relative_url }}" alt="Explainer's paper view" class="post-image">
</div>

My first attempt at ingestion went directly at ArXiv. Query by lab or institution, pull the relevant papers. The problem is that ArXiv doesn't have reliable affiliation fields. Searching for "OpenAI" returns every paper that mentions OpenAI anywhere in the text — not papers by OpenAI researchers. The signal is completely polluted. I built a scoring layer on top, trying to infer authorship from extracted metadata. When that wasn't enough, I added an LLM filtering pass. It didn't work either. And at scale it would have been expensive. I was trying to model my way out of a data problem. That doesn't work.

So I turned to Semantic Scholar and OpenAlex. Rich metadata, open APIs, broad coverage. The problem wasn't the APIs — it was what I was using them for. I needed a reliable answer to one question: which papers did this person write? That query was unreliable on both. Semantic Scholar's author search returned multiple IDs for 91% of the researchers I was tracking. The pipeline looked like it was working. It wasn't.

The issue wasn't execution. It was that I had misunderstood the problem. Author identity and paper enrichment are fundamentally different jobs — and I'd been using the same tool for both.

DBLP is hand-curated. Each researcher gets one profile, publications linked persistently across institutional changes and name variations. It lags behind recent work — that's the tradeoff — but the linkage is reliable. DBLP for identity, Semantic Scholar for enrichment. The moment I separated those two jobs, the pipeline held.

<div class="post-inline-image-container">
  <img src="{{ '/assets/images/diagram.png' | relative_url }}" alt="Data flow" class="post-image">
</div>

Then I found the next gap. Hundreds of papers arrived without abstracts. Not fringe papers — Chain-of-Thought Prompting, Vision Transformer, Whisper. The most foundational AI research of the last five years clustered at exactly this gap. No abstract meant the recommendation engine treated them as invisible. The system wasn't just imperfect — it was systematically blind to the most important work. That problem is still open.

<div class="post-inline-image-container">
  <img src="{{ '/assets/images/explainer-front-bg.png' | relative_url }}" alt="Explainer frontpage" class="post-image">
</div>

The corpus, the identity layer, the ingestion pipeline — that's the product. The LLM is just the interface. Swap the model out tomorrow and nothing breaks. Lose the data and there's nothing left.
