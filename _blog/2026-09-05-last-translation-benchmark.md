---
title: "How I invited ChatGPT for breakfast, and it showed up for lunch"
date: 2026-09-05
permalink: /blog/ltb/
excerpt: "Lessons learned from contributing to the Last Translation Benchmark"
header:
  teaser: "ltb.png"
tags:
  - translation
  - belgium
---

<p align="center">
  <img width="40%" src="/images/ltb.png" alt="Last Translation Benchmark illustration" />
</p>



## How I invited ChatGPT for breakfast, and it showed up for lunch

> September 5th 2026


When someone in France invites you for a "déjeuner", they want to have lunch with you. Ask the same thing to a Belgian at 1 PM, though, and they might wonder why you are inviting them to breakfast so late. This is but one example of the many differences between the French language used in France and in Belgium. Growing up in Belgium, I experienced this firsthand and learned to adjust my vocabulary when crossing the border to France for vacation.

When ChatGPT came out in 2022, I remember being disappointed at its lack of adjustment to Belgian variations of the French language. Large language models (LLMs) have improved dramatically since then, to the point that it is tempting to think that language translation is a solved problem.  When I heard about the [Last Translation Benchmark](https://last-translation-benchmark.vilda.net/), a research project aiming to create a challenging translation benchmark for the latest large language models (LLMs) this summer 2026, I jumped at the opportunity to put LLMs to the test on some of my favorite Belgian French idioms and linguistic quirks. In this post, I provide a recap of my experiments from July and August 2026, illustrating when LLMs can and cannot translate (Belgian) French to English, or vice-versa, correctly. 

### 90 is 90, not 4x20+10 - What LLMs get right 

Let's start with the good news: today's LLMs can translate many Belgian French expressions correctly. This includes the famous "nonante" as a translation for "ninety", instead of "quatre-vingt-dix". To my great surprise, many LLMs could perfectly translate more obscure idioms such as "passer la nuit à l'amigo", a Brussels expression that does not mean spending the night with a friend but rather ending up in jail. Overall, for every example where an LLM failed, I found roughly two where it got the translation right.

### Mayo with the fries? No maybe! - What LLMs get wrong

So, where do LLMs fail then? I encountered three broad types of failures.

Belgian French is full of sarcasm and irony. A famous example is "Non peut-être!". This literally translates to "No maybe!", but if a Belgian tells you this, they probably mean "Yes of course (and it was pointless to ask the question to begin with)!". Picking up on that irony is challenging for many LLMs. 

Many words have a different meaning whether they are used in France or Belgium. This includes the "déjeuner" which means lunch in France but breakfast in Belgium. Even when the context provides a strong clue, such as "à 7h30" (7:30 AM), most LLMs still default to the French interpretation.

Some words of the Belgian French vocabulary are used only in narrow communities, such as student societies. While most students will know that a "pif-paf" consists of chugging two glasses, most LLMs ignore this community-specific vocabulary.

### When pain is not bread - LLMs can't talk like cool kids

Beyond the Belgian context, I encountered another category of challenging translations from French to English: idioms that entered youth slang in recent years. Languages evolve fast; that is a well-known fact. I believe this is one of the biggest challenges for LLMs: language is a constantly moving target. Youth slang is the perfect test case for this. I will conclude with this example. When a French teenager talks about their "pain", they don't mean their favorite type of bread but rather their crush. This expression comes from the Ivorian nouchi language and has made its way in recent years into youth slang in France and Belgium. Ask an LLM, though, and it is often just as confused as a parent trying to figure out what their teenager is saying.

### The Last Translation Benchmark needs you

These examples are part of a large project called the Last Translation Benchmark. A [preprint](https://arxiv.org/abs/2609.04173) recently came out, and the [dataset](https://huggingface.co/datasets/zouhar/last-translation-benchmark) can be found on HuggingFace. Check it out and join the project by contributing your own challenging translation pairs.






