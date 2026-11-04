---
layout: post
date: 2026-11-04 07:59:00-0400
title: Code for our method <b>&#34;$$Counterfactual-Guided Diversified Path Integration for Transferable Neuron Attribution Attacks&#34;</b> is released!
inline: false
related_posts: false
---

### <b>Counterfactual-Guided Diversified Path Integration for Transferable Neuron Attribution Attacks</b>

***

<b> Di Ming, Renqing Yang, Yuanchengzhi Liu, Peng Ren, Pengzhan Zhou, Yunlong Wang, and Xin Feng&#42;</b>&#59; 34th ACM International Conference on Multimedia (ACM MM), 2026.

***

#### <b>Abstract</b>

Transferable adversarial attacks pose significant security threats to neural networks due to their strong black-box effectiveness against real-world models. While neuron attribution-based attacks have shown promise in enhancing transferability, existing methods are often constrained by integration paths that accumulate noise or lack structural diversity. Moreover, they typically rely on single layer neuron attribution, failing to exploit multi-layer information. To address these limitations, we propose COunterfactual-Guided Diversified Path Integration Neuron Attribution Attack, termed COPIA. Specifically, we incorporate counterfactual-guided paths into the neuron attribution framework, to effectively mitigate noise accumulation in integration trajectories and enable model-adaptive construction. Building on this, we diversify path update mechanisms and counterfactual samples to enhance path diversity and improve adversarial transferability. Furthermore, to capture the complementary semantics across different layers, we design a Cross-layer Attribution (CA) mechanism that progressively aggregates attribution information from deeper layers into the target attack layer via attribution flow. Extensive experiments on the ImageNet dataset across normally trained models, adversarially trained CNNs, ViTs, and various defense models demonstrate that COPIA consistently outperforms state-of-the-art methods in black-box attack settings. In addition, the proposed CA mechanism is highly generalizable and effectively improves the black-box transferability of existing single layer neuron attribution attacks. Code and supplementary materials
are available at https&#58;&#47;&#47;github&#46;com&#47;AdvML-Group&#47;COPIA.

***

#### <b>Related Material</b>

&#91;<a href="https://github.com/AdvML-Group/COPIA">html<a>&#93;      &#91;<a href="https://github.com/AdvML-Group/COPIA">paper<a>&#93;      &#91;<a href="https://github.com/AdvML-Group/COPIA/blob/main/COPIA_Full.pdf">supp<a>&#93; &#91;<a href="https://github.com/AdvML-Group/COPIA">code<a>&#93;      &#91;<a href="ttps://github.com/AdvML-Group/COPIA/blob/main/COPIA_Poster.pdf">poster<a>&#93;


***

#### <b>Citation</b>
```
@InProceedings{MM26_COPIA,
    author    = {Ming, Di and Yang, Renqing and Liu, Yuanchengzhi and Ren, Peng and Zhou, Pengzhan and Wang, Yunlong and Feng, Xin},
    title     = {Counterfactual-Guided Diversified Path Integration for Transferable Neuron Attribution Attacks},
    booktitle = {34th ACM International Conference on Multimedia (MM ’26)},
    month     = {November},
    year      = {2026},
    pages     = {}
}
```

***

&#42;Corresponding Author&#58; Xin Feng
