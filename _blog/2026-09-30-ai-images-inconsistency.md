---
title: "This looks real, but is it true? What AI-generated images get wrong about the world"
date: 2026-09-30
permalink: /blog/this_looks_real_but_is_it_true/
excerpt: "Practical tips to detect AI-generated images using your knowledge of the world."
header:
  teaser: "mic_2.png"
tags:
  - multimodal
  - misinformation
  - fact-checking
---

<p align="center">
  <img width="70%" src="/images/mic_2.png" alt="Practical tips to detect AI-generated news images" />
</p>

Like me, you may have come across an AI-generated news image on Facebook or Instagram that, at first glance, looked real. AI-generated images are becoming increasingly realistic and can be misused to misrepresent real-world events. A few years ago, we could spot the gross physical distortions introduced by GenAI models: hands with four fingers, a third arm, distorted faces, and so on. As GenAI models improve, these obvious clues are becoming scarcer, making it increasingly difficult to determine whether an image is AI-generated from its appearance alone. But instead of asking only whether an image looks real, we can ask another question: is it consistent with the real-world event that it claims to depict? This blog post discusses a simple but useful strategy for answering that question: use your knowledge of the world.

### This may be a traffic jam, but it ain't a Belgian one

Take the illustration above. The robot is skeptical about the image currently displayed on the TV screen. Sure, it looks real (in a cartoon universe). But could this really represent a traffic jam in Belgium? Nope, and any local would immediately spot two problems. First, the Belgian flag is black-yellow-red, not black-red-yellow as shown on the TV. Second, cars in Belgium drive on the right, while the TV screen shows cars driving on the left. The inconsistency on the driving side tells us that something is wrong. However, it does not prove that the image is AI-generated. The image might be real, but taken in England, for example. The fictional Belgian flag provides an additional clue: it depicts something that should simply not exist. In both cases, we leveraged our world knowledge, in this case, about national flags and driving rules around the world. 

### From visual artifacts to inconsistencies with world knowledge

This verification strategy relies on a simple observation: while GenAI models are becoming increasingly good at producing well-formed objects and realistic-looking scenes, they can make mistakes in the subtle contextual details that tie an image to a particular event. Depicting a specific news event requires getting many details right: the flags, police or military uniforms, vegetation, architectural styles, road signs, license plates,  and much more. For a much more comprehensive list of such clues, I recommend Henk van Ess's detailed guide to detecting AI-generated content [1]. These cues help us verify, at the very least, that an image does not accurately depict the event it claims to show. In some cases, we may get lucky and find an even stronger clue that the image is AI-generated, e.g., when it shows a flag that does not exist.

Professional fact-checkers regularly use this verification strategy. The image below was investigated by the fact-checking organization Dubawa [2]. It claimed to show Muslims praying on a road in Abuja, Nigeria, interrupting traffic. Here again, something does not fit the claimed context. Vehicles in Nigeria drive on the right, while the cars in the image drive on the left. For sure, this image does not show Abuja.

<p align="center">
  <img width="80%" src="/images/mic/abuja.png" alt="An AI-generated image of Abuja roads." />
</p>


### Fighting fire with fire: AI can help

Checking whether an image is consistent with its claimed context is nothing new. Long before generative AI became capable of producing convincing visual misinformation, misleading posts often reused real but unrelated images to illustrate an event. For example, a real photograph from the Syrian civil war might be reposted years later with a caption claiming that it shows the conflict in Yemen. These are what we call "out-of-context" images: the image itself is authentic; the claimed context might be real or not, but it is definitely not consistent with the image. AI-generated images can be more challenging. In many cases, they will be entirely consistent with the claimed context, except for a small detail: a flag, a police badge, a road sign, or a license plate.  Finding these consistencies may require very local knowledge. Would this tree species grow in this city? What uniform do the local firemen wear? Checking all these details manually is time-consuming and requires extensive world knowledge. This is where I believe AI can help.

In our recent paper "MIC: Explaining Image-Claim Inconsistencies in AI-Generated Multimodal Misinformation" [3], Ruihong Zeng, Preslav Nakov, Iryna Gurevych, and I tackle this problem head-on. We ask the following question: Can multimodal LLMs detect inconsistencies between AI-generated images and their claimed context using their world knowledge? On our dataset, MICBench, we show that multimodal LLMs can be trained to detect nine types of inconsistencies, including flags, architecture, and uniforms, and explain why there is an inconsistency. Our paper and datasets are public; check them out!

In conclusion, an image does not exist in isolation: if it claims to depict a news event, it must make assumptions about the surrounding context. Flags, uniforms, traffic rules, vegetation, architecture, and many other small details can therefore serve as valuable cues for spotting errors made by GenAI models.
However, no human can know all these details about every place in the world. This is where AI can help by identifying which parts of an image do not fit the story it claims to tell.


{% capture takeaways %}
- AI-generated images are increasingly real-looking
- When an image is associated with a news event, it has to be consistent with its surrounding context. Checking for subtle inconsistencies can help detect visual misinformation, and in some cases, establish that the image is AI-generated
- AI models can help identify these subtle inconsistencies, using their comprehensive world knowledge
{% endcapture %}{% include takeaway.html content=takeaways %}




### References

[1] Henk van Ess. 2025. [Reporter’s Guide to Detecting AI-Generated Content](https://gijn.org/resource/guide-detecting-ai-generated-content/).

[2] Sunday Awosoro. 2026. [Photo of Muslims worshipping on Abuja road, AI-generated ](https://dubawa.org/photo-of-muslims-worshipping-on-abuja-road-ai-generated/).

[3] Ruihong Zeng, Jonathan Tonglet, Preslav Nakov, Iryna Gurevych. 2026. [MIC: Explaining Image-Claim Inconsistencies in AI-Generated Multimodal Misinformation](https://arxiv.org/abs/2609.33441).
