---
layout: post
title: "Yatzy Scoreboard Tracker: Automating the Fun with AI"
title-up: "Yatzy Scoreboard Tracker:"
title-down: "Automating the Fun with AI"
intro: "Yatzy is a classic dice game, often played in social settings where players try to achieve various combinations with five dice"
date: 2025-03-06
categories: [coding]
image: /assets/images/dices.png
---

Yatzy is a classic dice game, often played in social settings where players try to achieve various combinations with five dice. Each round, players score points based on different categories, such as "Full House" or "Yahtzee," and at the end of the game, the scores are tallied to determine the winner. My girlfriend and I usually enjoy a few rounds every Sunday morning, and after a while, I thought it would be great to store our scores in a digital format to track our stats over time.

<div class="subtitle-separator">The Problem</div>

<hr>

That's when I realized I needed a system to automatically extract the scores from the images of our scorecards and save them to a CSV file for easy analysis. Here's how I tackled this project.


<div class="subtitle-separator">The Exploration Phase</div>

<hr>


I started by exploring different ways to extract text from images. I knew Optical Character Recognition (OCR) would be the key, but I quickly ran into some challenges.

1. Google AI Vision and OCR Tools
At first, I considered using Google's AI Vision tool, but it felt too heavy for this small-scale project. Next, I tried building an OCR system using Tesseract and PyTesseract. Unfortunately, after spending a few days configuring it, I couldn't achieve the accuracy I wanted, and the system was too slow for my needs.

2. Agentic Document Extraction
I then stumbled upon a post by Andrew Hew about the Agentic document extraction tool. I gave their API a shot, but I struggled with parsing the results. It seemed like a powerful tool, but my use case felt too lightweight for it. I still plan to investigate this further.

3. Back to the Drawing Board with LLMs
Realizing that I needed a more flexible solution, I went back to my initial idea: leveraging Large Language Models (LLMs) like ChatGPT. At the time, I was experimenting with different models, including ChatGPT, Claude 3.5, and DeepSeek via chat interfaces. I found that ChatGPT gave the best results with simple prompting. This is where the project started to gain traction.

4. Google AI Studio and Gemini Models
I was using Google AI Studio for coding assistance, and their reasoning models helped me quickly implement parts of the code. I decided to try Gemini 1.5 and 2.0 for extracting the scores, and it worked pretty well. This was the turning point in the project.

5. Building the System
With the help of Google AI Studio's reasoning models, I was able to quickly build a data parsing system. I implemented an image handler that monitors a folder where I drop images. I also had to install some packages to convert images from HEIC (since I use an iPhone) to PNG format, as Gemini handled them better this way. Lastly, I wrote a function to output the results to a CSV file.

6. Handling Categories and Language Mapping
At first, I asked Gemini to only return the scores, not the categories, but since I play with Finnish scorecards, the categories were in Nordic languages. This didn't work well, as Gemini skipped them. After modifying the prompt to include categories, I ran into another issue: translation. Instead of manually mapping the categories (Finnish -> English, Norwegian -> English), I let Gemini handle the translation. That worked much better.

7. Validation Logic
To ensure the accuracy of the scores, I added simple validation logic that checks if the upper score and the total match. If they don't, the system will prompt for confirmation. This added a layer of security against mistakes.

8. Fine-Tuning Image Handling
I wrote a short script to analyze the scores and automatically process every scoreboard image. However, Gemini struggled more with images that had empty spaces around the scoreboard, so I had to crop the images manually before adding them to the monitored folder. Eliminating this step is one of my next goals.

9. Dealing with Calculation Mistakes
Sometimes the system misinterpreted scores, especially when a number like "52" was misread as "5." In those cases, I had to edit the results manually, but most of the time, it was due to a miscalculation on our part.

What's Next?
The current version of the system works well, but there's still room for improvement. The next steps involve deploying the code somewhere so that it runs continuously without requiring manual intervention. I'd also like to add a simple user interface (UI) to make it more user-friendly.
