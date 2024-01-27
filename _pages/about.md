---
layout: about
title: about
permalink: /

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  address: 

news: true  # includes a list of news items
selected_papers: true # includes a list of papers marked as "selected={true}"
social: false  # includes social icons at the bottom of the page
---

Hi! My name is David Bick and I work in Applied ML at Cerebras Systems, the leading deep learning hardware accelerator startup. Previously I spent six years at Carnegie Mellon: I first earned a Bachelors in Statistics and Machine Learning, and then published three papers under Prof. Bhiksha Raj durng a Research Masters in the Language Technologies Institute of the School of Computer Science.  

My work and interests are generally in natural language processing and speech processing. My research followed a line of work on improving the perceptual quality of machine-generated speech. I have also worked on a number of projects at Cerebras and CMU using LLMs, including multi-modal QA, instruction-fine-tuning, etc.  

**Research Details:**

To improve perceptual quality, we created deep learning estimators of fine-grained speech characteristics, whose importance we identified from the acoustic-phonetics literature. A useful analogy is that they are a "fingerprint" of natural speech. Our work has focused on different ways to optimize networks to produce speech that has this same "fingerprint". 

These characteristics were previously calculated using traditional _non-differentiable_ signal processing techniques. Our neural estimators are differentiable and thus open up their application in optimizing other networks. In the last year we have presented this work in 3 papers across 2 conferences, and at an invited talk to Meta Reality Labs Research Audio.

