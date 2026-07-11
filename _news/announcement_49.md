---
layout: post
date: 2026-07-06 07:59:00-0400
title: Code for our method <b>&#34;Low-Rank and Sparsity Are All You Need&#58; Exploring Robust Hierarchical Latent Subspaces for Transferable Adversarial Attack&#34;</b> is released!
inline: false
related_posts: false
---

### <b>Low-Rank and Sparsity Are All You Need&#58; Exploring Robust Hierarchical Latent Subspaces for Transferable Adversarial Attack</b>

***

<b> Shuangshuang Pu, Wen Yang, Min Li, Guodong Liu, Chris Ding, Di Ming&#42;</b>&#59; Forty-third International Conference on Machine Learning (ICML), 2026.

***

#### <b>Abstract</b>

Adversarial examples pose serious threats to deep neural networks, exposing fundamental vulnerabilities in model robustness. However, most existing adversarial attacks directly manipulate dense and redundant feature representations, often leading to overfitting on surrogate models and poor black-box transferability. Recent SVD-based attack attempts to exploit low-rank feature subspaces, yet its reliance on single-layer optimization and single-gradient pathway neglects structural redundancy in feature representations and hierarchical heterogeneity across layers. To address these limitations, we propose LRS-Attack, a low-rank and sparse decomposition attack that explicitly models robust hierarchical subspaces in latent feature spaces. Specifically, the low-rank component captures dominant semantic directions, while the sparse component captures localized and discriminative patterns. To efficiently extract low-rank structure while preserving subspace fidelity, we develop a warm-started alternating low-rank approximation algorithm. Moreover, we introduce a hierarchical mixture of robust experts that leverages depth-dependent feature characteristics and guides gradient optimization toward more transferable adversarial directions. Extensive experiments on ImageNet show that LRS-Attack consistently improves black-box transferability over state-of-the-art methods across diverse CNN/ViT architectures and defense settings. Code is available at https&#58;&#47;&#47;github&#46;com&#47;AdvML-Group&#47;LRS-Attack.

***

#### <b>Related Material</b>

&#91;<a href="https://openreview.net/forum?id=EE7rcB8vxv">html<a>&#93;      &#91;<a href="https://openreview.net/pdf?id=EE7rcB8vxv">paper<a>&#93;      &#91;<a href="https://openreview.net/pdf?id=EE7rcB8vxv">supp<a>&#93; &#91;<a href="https://github.com/AdvML-Group/LRS-Attack">code<a>&#93;      &#91;<a href="https://icml.cc/virtual/2026/poster/65377">poster<a>&#93;      &#91;<a href="https://www.youtube.com/watch?v=pPuX0XHzsLs">video<a>&#93;


***

#### <b>Citation</b>
```
@InProceedings{ICML26_LRS_Attack,
    author    = {Pu, Shuangshuang and Yang, Wen and Li, Min and Liu, Guodong and Ding, Chris and Ming, Di},
    title     = {Low-Rank and Sparsity Are All You Need: Exploring Robust Hierarchical Latent Subspaces for Transferable Adversarial Attack},
    booktitle = {Forty-third International Conference on Machine Learning (ICML 2026)},
    month     = {July},
    year      = {2026},
    pages     = {}
}
```

***

&#42;Corresponding Author&#58; Di Ming
