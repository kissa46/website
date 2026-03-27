---
layout: post
title: "When the Map Runs Out"
title-up: "When the Map Runs Out"
title-down: "On confident models and unknown terrain"
intro: "A satellite classifier failed spectacularly on Finnish permafrost."
date: 2025-01-15
image: /assets/images/maps.png
---


As part of an AI course at Sorbonne University, I trained a CNN on a plant pathology dataset — the kind of Kaggle staple where the task is classifying healthy versus diseased leaves. I got curious about other image recognition use cases, so I took it further and fine-tuned EfficientNetB0 on EuroSAT, a satellite imagery dataset covering ten land cover classes across Europe. The model hit around 81% validation accuracy, which for a side experiment felt solid enough to start poking at.

I started testing it with screenshots from Google Earth. In general it held up — forests looked like forests, residential areas came back as residential. Then I fed it an image from north of Finland. Patterned ground shaped by permafrost, polygonal soils from frost-heaving, boulder fields where almost nothing grows. The model returned Residential Buildings at 82% confidence.


The model just picked the nearest pattern it knew and committed. EuroSAT is drawn almost entirely from Central Europe. The model learned "European landscape" and had no way to represent where that map ended.

<div class="post-inline-image-container">
  <img src="{{ '/assets/images/lapland-result-bg.png' | relative_url }}" alt="Lapland classification result" class="post-image">
</div>

At least in this case I knew the dataset. I could trace the blind spot back to a concrete gap in the training distribution. It made me think about LLMs and the same class of problem at a different scale — except there, the training data is opaque, the worldview harder to audit, and the failure modes far less legible.

The standard response to model unreliability is human feedback — flag the errors, reinforce the right behavior. But a [2023 paper from UCL and Cohere](https://arxiv.org/abs/2309.16349) made me skeptical of that logic. Humans consistently rate confident, well-structured answers as more accurate, even when they're wrong. We don't evaluate truth. We evaluate the performance of truth. The reward signal being used to correct the model is built on the same bias the model is expressing — leading to sycophancy, length bias, confidence over accuracy.


Classifiers already make automated decisions at scale — credit scoring, fraud detection, content moderation. The permafrost image was visible to me because it was my experiment. In production systems, most of these outputs never surface to a human at all.

Agentic workflows extend this further. An agent managing customer renewals doesn't make a single classification call — it decides who to contact, when, with what offer, and acts on the response. It chains decisions across multiple systems over time. You can put a human in the loop for one agent. You can't put a human in the loop for a hundred running simultaneously across an organization.

The current response here is evals — build tests, measure known failure modes, iterate. But evals only cover the failure modes you already thought of. The model will pass every eval you designed and still fail confidently on the next thing it hasn't seen.

The deeper issue is that the model doesn't understand what it predicts. It has no priors to draw from, no way to represent the boundary of its own knowledge. The Finland image wasn't just a data gap — it was a calibration failure too. The model had no mechanism to signal uncertainty. It was as confident on terrain it had never seen as on terrain it knew well. RLHF, evals, guardrails — these are patches on that foundation. Useful patches, but patches. Until models are grounded in something closer to understanding, we're not solving the problem. We're managing it, one workaround at a time, while the systems get more autonomous.
