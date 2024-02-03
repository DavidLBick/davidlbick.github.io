---
layout: post
title: "Tensor Programs"
date: 2024-01-27
excerpt: "An initial foray into understanding Greg Yang's Tensor Programs"
tags: [sample, intuition-building, tensor-programs]
---

## Motivation

The Tensor Programs series is really interesting because it seems like one of the first set of works that have developed theory on deep learning that actually resulted in large tangible benefits, specifically in the hyper-parameter transfer for large models. Perhaps I am overstating this, as there have been important works such as Gradient Noise Scale (GNS) from OpenAI, and the Neural Tangent Kernel (NTK) by Arthur Jacot (although I don't know of the practical impacts of this work as well), etc. But another engaging aspect of Tensor Programs series is that it unifies and explains some of the other theoretical ideas such as NTK, as well as others like the connection between neural networks and gaussian processes. 

On Greg Yang's [website](https://thegregyang.com), he suggests his paper on [A Spectral Condition for Feature Learning](https://arxiv.org/pdf/2310.17813.pdf) as the entrypoint to the series, so that is where I will begin here. 

## Introduction 

This paper seems to be primarily about two equations: the magnitude of activations (and their updates), and the magnitude of weights (and their updates): 

$$
\begin{align}
|| h_l(x) ||_2 = \Theta(\sqrt{n_l}), \; || \Delta h_l(x)||_2 = \Theta(\sqrt{n_l}) \\
|| W_l ||_{*} = \Theta(\sqrt{\frac{n_l}{n_{l-1}}}), \; || \Delta W_l ||_{*} = \Theta(\sqrt{\frac{n_l}{n_{l-1}}})
\end{align}
$$

There is an important step that is glossed over in the intro but will be crucial to the above properties -- gradient descent training induces alignment between the layer inputs and the top singular subspaces of the weight matrices. 

Assuming this alignment, the definitional forward pass
$$h_{l}(x) = W_{l} h_{l-1}(x)$$ 
entails that 
$$|| h_l(x) ||_2 = || W_l ||_{*} \cdot || h_{l-1}(x) ||_2$$
. This follows by the definition of spectral norm 
$$|| A ||_{*} = \max_{v \in \mathbb{R}^n \ \{0\}} \frac{||Av||_2}{||v||_2}$$, as substituting gives us
$$|| W ||_{*} = \frac{|| W_{l} h_{l-1}(x) ||_2}{|| h_{l-1}(x) ||_2} = \frac{|| h_{l}(x) ||_2}{|| h_{l-1}(x) ||_2}$$

So in this blog post I will seek to explain and build intuition on: 
1. Why should activations scale this way? 
2. Why should weights scale this way? 
4. How can you learn features when the updates are of this order?
3. Why does gradient descent induce the alignment between activations and singular subspaces of weights?


## Preliminaries 
Some sub-questions that might be useful to answer along the way include: 
1. What is the intuition behind the spectral norm? 
2. The spectral norm of a matrix is equal to the largest singular value. What is the intuition behind the singular vectors/values? 
3. What is the intuition behind the Frobenius norm? 

