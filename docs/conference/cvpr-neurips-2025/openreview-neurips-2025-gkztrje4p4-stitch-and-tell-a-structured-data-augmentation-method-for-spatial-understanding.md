---
title: "Stitch and Tell: A Structured Data Augmentation Method for Spatial Understanding"
title_zh: Stitch and Tell：一种面向空间理解的结构化数据增强方法
authors: "Hang Yin, Xiaomin He, Peiwen Yuan, Yiwei Li, Jiayi Shi, Wenxiao Fan, Shaoxiong Feng, Kan Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=GkztRjE4P4"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 面向空间理解的结构化数据增强，与视觉语言导航相关
tldr: 视觉语言模型在描述物体相对位置时经常产生空间幻觉，主要原因是图文数据的不对称性。本文提出Stitch and Tell（SiTe），通过沿空间轴拼接图像并生成空间感知的标题或问答对，向多模态数据注入结构化空间监督。该方法无需人工标注或昂贵模型，即插即用，可显著提升模型的空间理解能力，对视觉语言导航等空间推理任务具有重要价值。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视觉语言模型常有空间幻觉，因图文数据不对称而缺乏结构化空间监督。
method: 通过拼接图像并生成空间感知标题/QA对，注入结构化空间监督，实现无需标注的数据增强。
result: 实验表明SiTe显著增强VLMs的空间位置理解，缓解空间幻觉。
conclusion: 该即插即用的数据增强方法可广泛提升空间推理相关任务（如导航）的性能。
---

## Abstract
Existing vision-language models often suffer from spatial hallucinations, i.e., generating incorrect descriptions about the relative positions of objects in an image. We argue that this problem mainly stems from the asymmetric properties between images and text. To enrich the spatial understanding ability of vision-language models, we propose a simple, annotation-free, plug-and-play method named Stitch and Tell (abbreviated as SiTe), which injects structured spatial supervision into multimodal data. It constructs stitched image–text pairs by stitching images along a spatial axis and generating spatially-aware captions or question answer pairs based on the layout of stitched image, without relying on costly advanced models or human involvement. We evaluate SiTe across three architectures including LLaVA-v1.5-7B, LLaVA-Qwen2-1.5B and HALVA-7B, two training datasets, and thirteen benchmarks. Experiments show that SiTe improves spatial understanding tasks such as $\text{MME}_{\text{Position}}$ (+5.50\%) and Spatial-MM (+4.19\%), while maintaining or improving performance on general vision-language benchmarks. Our findings suggest that explicitly injecting spatially-aware structure into training data offers an effective way to mitigate spatial hallucinations and improve spatial understanding, while preserving general vision-language capabilities.

---

## 论文详细总结（自动生成）

# Stitch and Tell：面向空间理解的结构化数据增强方法（中文总结）

## 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：现有视觉语言模型（VLMs）在描述图像中物体的相对位置时经常产生**空间幻觉（spatial hallucination）**，即生成与图像真实空间布局不符的描述。
- **根本原因**：作者认为，这一问题主要源于**图像与文本之间的不对称性（asymmetric properties）**——图像天然包含丰富的空间位置信息，但文本描述往往关注语义内容而忽略结构化空间关系，导致多模态训练数据中缺乏明确的空间监督信号。
- **研究意义**：空间理解能力是视觉语言模型完成具身导航（embodied navigation）、空间推理等任务的基础，缓解空间幻觉对提升模型在真实世界中的可靠性至关重要。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **方法名称**：Stitch and Tell，缩写为 **SiTe**。
- **核心思想**：通过**沿空间轴拼接（stitch）图像**，并基于拼接后的布局生成**空间感知的标题或问答对**，从而向多模态训练数据中**显式注入结构化空间监督**。
- **技术流程（文字说明）**：
  1. **图像拼接**：从训练数据中选择图像，沿水平或垂直等空间轴将两张或多张图像拼接为一张合成图像，使不同物体形成明确的左右/上下/前后空间关系。
  2. **布局感知标注生成**：基于拼接图像中各子图的相对位置布局，自动生成空间感知的文本描述，包括说明物体相对位置的图文对（caption）或问答对（QA pairs）。
  3. **数据混合训练**：将生成的拼接图像-文本对与原始训练数据混合，用于微调视觉语言模型。
- **关键优势**：
  - **无需人工标注**（annotation-free）：完全自动化生成训练样本。
  - **不依赖昂贵模型**：无需使用高级视觉模型或大语言模型进行生成，成本低。
  - **即插即用**：作为数据增强模块，可直接集成到现有训练流程中，无需修改模型架构。

## 3. 实验设计

- **模型架构**：在三种不同规模/架构上验证：
  - LLaVA-v1.5-7B
  - LLaVA-Qwen2-1.5B
  - HALVA-7B
- **训练数据集**：使用了**两个训练数据集**（原文未明确说明具体数据集名称，推测为常用的视觉语言指令微调数据集）。
- **评测基准**：覆盖**十三个基准测试**，包括：
  - 空间理解专项基准：`MME_Position`、`Spatial-MM` 等
  - 通用视觉语言基准：用于检测方法是否影响通用能力
- **对比方法**：原文摘要中未明确列出具体对比方法，主要采用**有/无 SiTe 增强的对照实验**（即在同一模型和数据集上，比较是否加入 SiTe 数据的性能差异）。

## 4. 资源与算力

- 原文摘要与元数据中**未明确说明**使用的 GPU 型号、数量、训练时长等具体算力信息。
- 仅可知实验涉及三种 7B/1.5B 规模的模型在多个数据集上的训练，推断需要一定的多卡 GPU 资源支持，但具体配置不可知。

## 5. 实验数量与充分性

- **实验数量**：
  - 3 种模型架构 × 2 个训练数据集 × 13 个基准测试，构成较为全面的实验矩阵。
  - 空间专项任务上有明确性能提升，同时验证了通用基准不下降甚至提升。
- **充分性评价**：
  - **优点**：覆盖多种规模/架构、多个训练数据环境、多类评测基准，且验证了“空间能力提升”与“通用能力保持”两个维度，实验设计较为全面。
  - **不足**：原文未清晰交代是否包含消融实验（如拼接方式、拼接数量、空间轴方向、生成文本格式等），也未明确与既有数据增强方法的对比，因此在“方法优越性”论证上略显不足。

## 6. 论文的主要结论与发现

- **结论一**：SiTe 能显著提升视觉语言模型的空间理解能力——`MME_Position` 提升 **+5.50%**，`Spatial-MM` 提升 **+4.19%**。
- **结论二**：在通用视觉语言基准上，SiTe 能维持或改善模型整体性能，说明其不会以牺牲通用能力为代价换取空间能力的提升。
- **总体发现**：**显式地向训练数据中注入空间感知结构**（通过图像拼接生成空间标注）是一种有效缓解空间幻觉、提升空间理解的方法，为后续研究提供了低成本、可扩展的新方向。

## 7. 优点

- **方法简洁高效**：不依赖人工、不依赖昂贵模型，仅通过图像拼接这一简单操作即可构造大量空间监督数据，工程门槛低。
- **即插即用**：无需修改模型结构，可轻松适配任意视觉语言模型，实用性高。
- **验证充分且客观**：覆盖多种模型规模、多个训练集和十三项基准，并同时报告空间任务与通用任务结果，有效证明了方法带来的增益是“空间专项”的，而非通用能力的简单变化。
- **动机清晰**：从图文数据不对称性这一角度切入，解释了空间幻觉的根源，逻辑链条完整。

## 8. 不足与局限

- **算力细节缺失**：未报告 GPU 类型、数量、训练时长等资源信息，影响复现成本评估。
- **消融分析可能不足**：摘要中未提及对拼接方向（水平/垂直）、拼接图像数量、文本生成策略等因素的消融实验，方法的最优配置不明确。
- **对比基线有限**：未明确与其他空间数据增强或反幻觉方法进行直接对比，方法的相对优势有待进一步验证。
- **空间关系覆盖**：拼接技术主要构造“左右/上下”这类相对位置关系，对深度、遮挡、远近等更复杂的 3D 空间关系可能覆盖不足。
- **数据集描述不完整**：两个训练数据集的具体构成、规模、领域未在摘要中说明，影响对方法适用范围（如是否适用于导航类数据）的判断。

（完）
