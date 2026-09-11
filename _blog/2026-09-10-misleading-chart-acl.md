---
title: "28% of NLP papers have misleading charts. Is yours one of them?"
date: 2026-09-10
permalink: /blog/how-not-to-make-your-next-paper-results-charts/
excerpt: "An analysis of the bad chart design practices in ACL and EMNLP conference papers."
header:
  teaser: "misleading_chart_anthology.png"
tags:
  - multimodal
  - data visualization
  - misleading charts
---

<p align="center">
  <img width="60%" src="/images/misleading_chart_anthology.png" alt="How to not make your next paper's results charts" />
</p>

One of my research focuses is the development of AI methods to detect and counter misleading charts, i.e., charts with questionable design choices that can lead readers to misinterpret the data behind the chart. While the misleading charts I encounter in my research are usually published by sketchy companies, politicians, or social media accounts, I have always been curious whether flawed design practices also affect charts published at Natural Language Processing (NLP) research conferences. Equipped with Gemini-3.5-Flash and the taxonomy of misleaders that I used in my prior work [1], I investigated a random collection of 261 papers published at ACL and EMNLP, the two flagship NLP conferences. This blog post discusses the main insights.

> 📖 **Glossary**
> 
>  A **misleading chart** is a chart that contains design flaws that may lead readers to misunderstand the underlying data.
> Importantly, this does not mean that the chart will systematically be deceiving, but rather that one or more best design practices were broken.
> These design flaws are also called **misleaders** [1].

### 73 Papers. 91 Charts. More misleading than expected

**73**. That is the number of scientific papers in the collection that contained at least one misleading chart. That corresponds to a staggering 28% of the collection, way more than I ever expected. Of the 825 charts in the collection papers, 91 were labeled as misleading by Gemini 3.5 Flash and me. That's 11% of all charts. The types of misleaders affecting these charts are diverse. 

In total, we found 9 of the 12 misleaders in our taxonomy. These stats are not great. But there is good news, almost all of it comes down to two culprits: "inconsistent tick intervals" and "truncated axis", and they are both easy to address. Let's see how we can fix those charts with some examples.

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/distribution_misleader.png" alt="The distribution of misleaders in the collection of 91 misleading charts." />
</p>


###  The slippery slopes of inconsistent tick intervals

The most common misleader is the use of inconsistent intervals between numerical values on the x-axis of line charts. Let's take a fictional example where we evaluate the performance of three models, A, B, and C, at predicting whether a picture shows a Chihuahua or a muffin.

The following line chart shows the classification accuracy of the models across different numbers of few-shot demonstrations (i.e., examples) provided in their prompts. Now, a line chart consists of two things: dots that represent accuracy scores and lines that connect them. The slope of the line is useful to show the rate at which accuracy is increasing or decreasing. The problem with this chart is that the slope cannot be analyzed that way because the x-axis values do not have consistent intervals. If I were to ask you whether going from 2 to 5 demonstrations yielded a higher increase than going from 1 to 2, you would probably answer "Yes" because the slope is steeper between 2 and 5. However, there is a 3-unit increase between 2 and 5, so the slope should be divided by 3 to compare it with the increase between 1 and 2.

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/inconsistent_tick.png" alt="A chart with inconsistent tick intervals." />
</p>

A much better solution is to use consistent tick intervals, as in the chart displayed below. This ensures that the slope of the line chart remains meaningful. If I were to ask the same question again, the answer here would clearly be "No", as the slope is steeper between 1 and 2.


<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/inconsistent_tick_corrected.png" alt="The corrected chart." />
</p>

### Dude, don't be so dramatic and just start the axis at 0 

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/truncated.png" alt="A chart with a truncated y-axis." />
</p>


<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/truncated_corrected.png" alt="The corrected chart." />
</p>


### Two axes, one illusion

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/dual_axis.png" alt="A dual axes chart." />
</p>


<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/dual_axis_corrected.png" alt="The corrected chart." />
</p>

### To go further, return first to 1954

Misleading charts have only gained major interest recently in the wake of the COVID pandemic, due to their extensive use to propagate disinformation about the virus. However, they were already discussed in 1954 by Darrel Huff in his excellent book "How to Lie with Statistics" [2]. I highly recommend this short but great read to anyone interested in the topic. If you want to explore this growing research area further, you can also check out [the reading list](https://github.com/UKPLab/awesome-misleading-visualizations) that I regularly update on Github [3].


{% capture takeaways %}
- **Many charts in ACL and EMNLP contain design flaws** that can make them misleading.
- In a random sample of 261 papers, **~28%** contain at least one misleading chart. Out of a sample of 825 charts, **~11%** are misleading.
- The top three misleaders are: **inconsistent tick intervals**, **truncated axis**, **dual axes**.
- Avoiding misleading design flaws is essential to avoid misinterpretation of the results by readers.
{% endcapture %}{% include takeaway.html content=takeaways %}

> Disclaimer: The collection is only a small random sample (n=261) of the papers published at ACL and EMNLP.
> This blog post will be regularly updated to provide new results based on larger samples.

### Collection method

I scraped a random sample from the ACL Anthology for the ACL and EMNLP conferences of 2022-2025. 
I used pymupdf to extract figures from the papers. I conducted two rounds of automated labeling with Gemini 3.5 Flash. (1) Removing all figures that are not charts (e.g., prompts, methodology diagrams, ...). 
(2) Detecting whether the chart is misleading, and which misleaders affect it, using the taxonomy of 12 design misleaders from [1].
All charts flagged as misleading were manually validated afterward, yielding a final set of 261 papers containing 825 charts of which 91 are misleading. 

### References

[1] Jonathan Tonglet, Jan Zimny, Tinne Tuytelaars, and Iryna Gurevych. 2026. [Is this chart lying to me? Automating the detection of misleading visualizations](https://aclanthology.org/2026.acl-long.398/).

[2] Darrell Huff. 1954. [How to Lie with Statistics](https://en.wikipedia.org/wiki/How_to_Lie_with_Statistics).

[3] Jonathan Tonglet. 2025. [Awesome misleading visualizations (GitHub repo)](https://github.com/UKPLab/awesome-misleading-visualizations).
