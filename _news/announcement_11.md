---
layout: post
date: 2023-9-28 07:59:00-0400
title: Code for the method <b>&#34;TRM-UAP&#58; Enhancing the Transferability of Data-Free Universal Adversarial Perturbation via Truncated Ratio Maximization (ICCV2023)&#34;</b> is released!
inline: false
related_posts: false
---

***

#### Abstract

Aiming at crafting a single universal adversarial perturbation (UAP) to fool CNN models for various data samples, universal attack enables a more efficient and accurate evaluation for the robustness of CNN models. Early universal attacks craft UAPs depending on data priors. For more practical applications, the data-free universal attacks that make UAPs from random noises have aroused much attention recently. However, existing data-free UAP methods perturb all the CNN feature layers equally via the maximization of the CNN activation, leading to poor transferability. In this paper, we propose a novel data-free universal attack without depending on any real data samples through truncated ratio maximization, which we term as TRM-UAP. Specifically, different from the maximization of the positive activation in convolution layers, we propose to optimize the UAP generation from the ratio of positive and negative activations. To further enhance the transferability of universal attack, TRM-UAP not only performs the ratio maximization merely on low-level generic features via the truncation strategy, but also incorporates a curriculum optimization algorithm that can effectively learn the diversity of artificial images. Extensive experiments on the ImageNet dataset verify that TRM-UAP achieves a state-of-the-art average fooling rate and excellent transferability on different CNN models as compared to other data-free UAP methods. Code is available at <a href="https://github.com/RandolphCarter0/TRMUAP">https&#58;&#47;&#47;github&#46;com&#47;RandolphCarter0&#47;TRMUAP</a>.
