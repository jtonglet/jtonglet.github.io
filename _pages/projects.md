---
layout: archive
title: "Projects"
permalink: /projects/
author_profile: true
---

## Image contextualization

<p align="center">
  <img width="120%" src="../images/5Pils_examples.png" alt="5pils_examples" />
</p>

Most research in multimodal automated fact-checking has focused on veracity prediction of multimodal claims. This usually takes the form of a classification task with true/false labels for multimodal (image+text, video+text, video+audio, ...) claims. However, in real-world fact-checking practices, a particular attention is also given to identifying the accurate context information about the multimodal content. For example,  identifying the true location and date of the image or video, i.e., geolocation and chronolocation. 

In this project, we assemble datasets and propose methods that focus on predicting true context of multimodal misinformation content.
We have introduced a first resource, [5Pils](https://github.com/UKPLab/5pils) which contains context data about the true source, date, location, and motivation of an image verified by professional fact-checkers. The task is to predict this context data using the image and evidence gathered from the web. In a follow-up [work](https://arxiv.org/abs/2502.01194), we show providing an in-depth context summary about an image is beneficial for detecting false captions afterwards, both for AI models and humans.



