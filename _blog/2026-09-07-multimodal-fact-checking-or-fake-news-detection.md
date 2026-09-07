---
title: "Multimodal fact-checking or multimodal fake news detection: two communities, one goal"
date: 2026-09-07
permalink: /blog/mfmfd/
excerpt: "An analysis of the two communities conducting research on countering multimodal misinformation and a call to unite our efforts."
header:
  teaser: "mfc_mfd_2.png"
tags:
  - multimodal
  - misinformation
  - fact-checking
---

<p align="center">
  <img width="60%" src="/images/mfc_mfd_2.png" alt="Multimodal fact-checking and fake news detection, two communities but one goal" />
</p>

How much can a difference in terminology lead researchers working on the same real-world problem to form separate communities, with their own methods and datasets? I have been working for the last three years on developing AI methods to assist professional fact-checkers in detecting misinformation that combines text and multimedia content, primarily images. While conducting literature searches or reviewing papers, I realized that several synonyms exist for this task: multimodal fact-checking, multimodal misinformation/fake news/rumor detection, ... In practice, these terms describe the same thing. "Fact-checking" refers to the nature of the task, while other terms refer to the object of study. Some terms are preferable to others. For example, the UN recommend using "misinformation" (or "disinformation" when the act is intentional) rather than the more generic and easily misused "fake news" [1]. As we will see later, "fake news" is still sadly the most popular term in research papers. Some terms are more specific. For example, "out-of-context misinformation" (OOC) focuses on authentic images that are presented with misleading captions.

I started to notice that papers using different names for the task also tended to use different benchmarks and baselines, with surprisingly little overlap between the two groups. Over the years, I became increasingly concerned that our field was splitting into separate communities. To see whether this impression was more than an anecdotal observation, I used the [Semantic Scholar API](https://www.semanticscholar.org/) to collect all papers citing a curated list of major datasets and analyzed them. I discuss below the main insights.

### Tell me your task name, I'll tell you your benchmarks


<p align="center">
  <img width="100%" src="/images/mafc_analysis/dataset_keyword.png" alt="Most task names map to specific benchmarks" />
</p>

Our initial intuition seems to be correct: different task names are  associated with different benchmarks. If one uses the terms "fake news" or "rumor", there is a good chance that they will report results on the Weibo, Twitter, or Pheme datasets. But if you wrote "fact-checking" or "OOC" in the title, you are likely using NewsCLIPpings or VERITE. Only the term "misinformation" lies in between what appears to be two partially separated communities, one centered around fake news and rumor detection and the other around fact-checking and OOC detection.

<p align="center">
  <img width="100%" src="/images/mafc_analysis/datasets_used_together.png" alt="There are two separate clusters of datasets used in combination" />
</p>

Analyzing which benchmarks are used in combination further supports the presence of two communities.  On the one hand, Weibo, Twitter, Fakenewsnest, and Pheme form a cluster. On the other, NewsCLIPpings, VERITE, and the more recent MMFakeBench form another.  Only Fakeddit acts as a thin bridge between the two..

<p align="center">
  <img width="100%" src="/images/mafc_analysis/citing_versus_using.png" alt="Citing the benchmark of one community often means using the benchmarks of that community solely" />
</p>


Let's zoom in on the main datasets from each community, NewsCLIPpings and Weibo. When a paper cites them, do they use datasets from the other community as benchmarks? The answer is no. We found no paper in our corpus that cites Weibo and then uses datasets of the fact-checking/OOC community. The same holds for papers that cite NewsCLIPpings, they very rarely use Weibo or Twitter.

### Fake news detection is winning the terminology race, for now


<p align="center">
  <img width="100%" src="/images/mafc_analysis/task_name_time.png" alt="Paper count by task name in title over time" />
</p>

The papers calling the task "multimodal fake news detection" have had a much higher volume of submissions, particularly in recent years. This means that datasets such as Weibo (which exists in several variants released over the years) and Twitter are among the most cited and used as benchmarks. This is unfortunate for three reasons. First, the term "fake news", discouraged by organizations such as UNESCO, the WHO, and the EU, continues to be used extensively. Second, some of the corresponding benchmarks, such as Weibo, are now old and largely saturated, with reported accuracies above 95%. Their evaluation setups also do not follow recent best practices, such as temporally ordering claims between training and test sets. Third, many methods in the "multimodal fake news detection" community focus on binary classification: is the content true or fake? They often do not provide explanations grounded in external evidence, even though such output is more useful to professional fact-checkers than a simple binary verdict [2].

In contrast, the "multimodal fact-checking" community is better aligned with real-world use cases of professional fact-checkers. In this community, leveraging external information to ground and justify verdicts is standard practice, and reference datasets are regularly updated and improved to avoid shortcuts and data leakage within LLM pretraining corpora. At the same time, many methods proposed within the "multimodal fake news detection" community achieve high detection performance across benchmarks and deserve to be evaluated on more recent benchmarks from the other community. After all, the next state-of-the-art might emerge from an encounter between the methods of both communities.

<p align="center">
  <img width="100%" src="/images/mafc_analysis/usage_time.png" alt="Number of papers using a benchmark over time" />
</p>

### Time to build some bridges

In summary, researchers trying to automatically detect multimodal misinformation are currently split across two main communities, with separate benchmarks and partially overlapping methods. Building more bridges between these communities in the coming years could benefit both and, perhaps, eventually bring them entirely together. The "fake news" community would benefit from evaluating its methods on more recent, less saturated, and more robust benchmarks developed by "multimodal fact-checking" researchers, such as AVerImaTeC, M4FC, or VERITAS. Conversely, researchers working on fact-checking could benefit from testing their evidence-based approaches against the sophisticated multimodal architectures developed for fake news detection. 


> Disclaimer: A corpus of around 200 papers was collected from the Semantic Scholar API and manually reviewed for the purpose of this post. The corpus was constructed by following citations to a curated list of major datasets, so it should not be considered a systematic literature review. The analysis is intended to illustrate broad trends rather than provide a comprehensive picture of the field.

### References

[1] Cherilyn Ireton and Julie Posetti. 2018. [Journalism,
fake news & disinformation: handbook for journalism education and training](https://www.unesco.org/en/articles/journalism-fake-news-disinformation). Unesco Publishing.

[2] Preslav Nakov, David Corney, Maram Hasanain, Firoj Alam, Tamer Elsayed, Alberto Barrón-Cedeño, Paolo Papotti, Shaden Shaar, Giovanni Da San Martino. 2021. Automated Fact-Checking for Assisting Human Fact-Checkers. IJCAI 2021 Survey Track. Pages 4551-4558. https://doi.org/10.24963/ijcai.2021/619


