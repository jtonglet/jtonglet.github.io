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
  <img width="70%" src="/images/misleading_chart_anthology.png" alt="How to not make your next paper's results charts" />
</p>

One of my research focuses is developing AI methods to detect and counter misleading charts, i.e., charts with questionable design choices that can lead readers to misinterpret the data behind the chart. While the misleading charts I encounter in my research are usually published by sketchy companies, politicians, or social media accounts, I have always been curious whether flawed design practices also affect charts published at Natural Language Processing (NLP) research conferences. Equipped with Gemini 3.5 Flash and the taxonomy of misleaders that I used in my prior work [1], I investigated a random collection of 261 papers published at ACL and EMNLP, the two flagship NLP conferences. This blog post discusses the main insights.

> 📖 **Glossary**
> 
>  A **misleading chart** is a chart that contains design flaws that may lead readers to misunderstand the underlying data.
> Importantly, this does not mean that the chart will systematically be deceiving, but rather that one or more best design practices were broken.
> These design flaws are also called **misleaders** [1].

### 73 Papers. 91 Charts. More misleading than expected

**73**. That is the number of scientific papers in the collection that contained at least one misleading chart. That corresponds to a staggering 28% of the collection, way more than I ever expected. Of the 825 charts in the collection, 91 were labeled as misleading by Gemini 3.5 Flash and me. That's 11% of all charts. The types of misleaders affecting these charts are diverse. 

In total, we found 9 of the 12 misleaders in our taxonomy. These stats are not great. But there is good news; almost all of it comes down to two culprits: "inconsistent tick intervals" and "truncated axis", and they are both easy to address. Let's see how we can fix those charts with some examples.

> All the examples below are fictional but directly based on the real-world cases that I observed in the collection.

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/distribution_misleader.png" alt="The distribution of misleaders in the collection of 91 misleading charts." />
</p>


###  The slippery slopes of inconsistent tick intervals

The most common misleader is the use of inconsistent intervals between numerical values on the x-axis of line charts. Let's take a fictional example in which we evaluate the performance of three models, A, B, and C, at predicting whether a picture shows a chihuahua or a muffin.

The following line chart shows the classification accuracy of the models across different numbers of few-shot demonstrations (i.e., examples) provided in their prompts. Now, a line chart consists of two things: dots representing accuracy scores and lines connecting them. The slope of the line is useful to show the rate at which accuracy is increasing or decreasing. The problem with this chart is that the slope cannot be analyzed that way because the x-axis values do not have consistent intervals. 

If I were to ask you whether going from 2 to 5 demonstrations yielded a higher increase than going from 1 to 2, you would probably answer "Yes" because the slope is steeper between 2 and 5. However, there is a 3-unit increase from 2 to 5, so the slope should be divided by 3 to compare it with the increase from 1 to 2. This is a typical example of how charts can be misleading: a visual artifact, here the slope, could lead you to conclusions that are not supported by the actual data.

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/inconsistent_tick.png" alt="A chart with inconsistent tick intervals." />
</p>

A much better solution is to use consistent tick intervals, as in the chart displayed below. This ensures that the slope of the line chart remains meaningful. If I were to ask the same question again, the answer here would clearly be "No", as the slope is steeper between 1 and 2. It is worth noting that many papers in the collection adopt this better design practice for drawing their line charts.


<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/inconsistent_tick_corrected.png" alt="The corrected chart." />
</p>

### Don't be so dramatic and just start the axis at 0 

Let's stay with our chihuahuas and muffins for a little longer. The following chart shows the accuracy of all three models on the classification task. The main purpose of a bar chart like this one is to compare the models based on the height of their bars. So, model A's accuracy is three times better than model B. Right? No, wait. Based on the y-axis ticks, the accuracy of model A is 80, and that of model B is 40. That's twice as good, not three times. 

So what happened here? The little culprit lies in the bottom-left corner. The y-axis starts at 20. This is called a truncation. Implicitly, the human mind assumes that the bars start at 0, but a quarter of the bars are actually hidden. Again, we got deceived by analyzing the visual signal, here, the height of the bar.

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/truncated.png" alt="A chart with a truncated y-axis." />
</p>

The fix is quite simple: start the y-axis at 0. But you might argue that doing so makes the bars too long and the gaps in accuracy harder to see. If that bothers you, I have two suggestions: (1) use another metric, (2) report the accuracy in a table instead of using a chart. Using a truncated bar chart is the least recommended option, because even if you specify the accuracy scores on top of the bars, there will always be readers who will remember that the blue bar was three times bigger than the orange one, and as time passes, this will transform into remembering that model A was three times better than model B.


<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/truncated_corrected.png" alt="The corrected chart." />
</p>


### Two axes, one illusion

Let's explore one more example of the third most-represented misleader: dual axis. Here, we compare the three models against human accuracy on three NLP tasks. This is a bar chart, so let's see which bar is the tallest. Damn, model A looks really strong, beating the human accuracy on all tasks!

<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/dual_axis.png" alt="A dual axes chart." />
</p>

Of course, there is a trick. Look to your left, look to your right; there is not one but two numerical axes. The left one is a standard 0-100 axis used to report model accuracy. The one on the right is truncated at 80% (!) and reports the human accuracy. In this setting, it's simply impossible to fairly compare model A's performance with human performance. This chart needs an urgent fix.





The chart below is much better. It uses a single axis. Now it is clear that model A never beats human performance in practice. Takeaway: dual axes are misleading in almost all scenarios; avoid using them.


<p align="center">
  <img width="50%" src="/images/misleading_chart_acl/dual_axis_corrected.png" alt="The corrected chart." />
</p>

> This example is inspired by a real dual-axis AI-vs-human comparison published at ACL/EMNLP.

### To go further, return first to 1954

Misleading charts have only gained major interest recently in the wake of the COVID pandemic, due to their extensive use to propagate disinformation about the virus. However, they were already discussed in 1954 by Darrel Huff in his excellent book "How to Lie with Statistics" [2]. I highly recommend this short but great read to anyone interested in the topic. If you want to explore this growing research area further, you can also check out [the reading list](https://github.com/UKPLab/awesome-misleading-visualizations) that I regularly update on GitHub [3].


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
All charts flagged as misleading were manually validated afterward, yielding a final set of 261 papers containing 825 charts, of which 91 are misleading. 

### References

[1] Jonathan Tonglet, Jan Zimny, Tinne Tuytelaars, and Iryna Gurevych. 2026. [Is this chart lying to me? Automating the detection of misleading visualizations](https://aclanthology.org/2026.acl-long.398/).

[2] Darrell Huff. 1954. [How to Lie with Statistics](https://en.wikipedia.org/wiki/How_to_Lie_with_Statistics).

[3] Jonathan Tonglet. 2025. [Awesome misleading visualizations (GitHub repo)](https://github.com/UKPLab/awesome-misleading-visualizations).
