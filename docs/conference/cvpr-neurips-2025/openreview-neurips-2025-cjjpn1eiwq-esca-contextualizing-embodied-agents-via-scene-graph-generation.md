---
title: "ESCA: Contextualizing Embodied Agents via Scene-Graph Generation"
title_zh: ESCA：通过场景图生成为具身智能体提供上下文感知
authors: "Jiani Huang, Amish Sethi, Matthew Kuo, Mayank Keoliya, Neelay Velingker, JungHo Jung, Ser-Nam Lim, Ziyang Li, Mayur Naik"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=cjjPn1EIwq"
tags: ["query:semantic-map"]
score: 8.0
evidence: 面向具身智能体的场景图生成，与语义地图/场景图导航相关
tldr: 多模态大模型在具身智能体中难以捕捉低层视觉特征与高层文本语义之间的细粒度关联，导致感知与接地不佳。本文提出ESCA框架，通过生成空间-时间场景图为具身智能体提供感知上下文，并训练开放域可提示的场景图生成模型SGCLIP。SGCLIP在8.7万+开放域视频上训练，无需人工标注即可对齐场景描述与场景图，为场景图驱动的导航等下游任务提供有力支撑。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有多模态大模型难以捕捉视觉与文本之间的细粒度关联，导致具身智能体感知接地能力弱。
method: 提出ESCA框架，用SGCLIP模型生成空间-时间场景图，以神经符号流程实现自动对齐与训练。
result: SGCLIP在开放域视频上训练后可生成高质量场景图，增强具身智能体的感知与上下文。
conclusion: 场景图生成可显著提升具身智能体的接地感知，并支持语义地图与场景图导航等应用。
---

## Abstract
Multi-modal large language models (MLLMs) are making rapid progress toward general-purpose embodied agents. However, existing MLLMs do not reliably capture fine-grained links between low-level visual features and high-level textual semantics, leading to weak grounding and inaccurate perception. To overcome this challenge, we propose ESCA, a framework that contextualizes embodied agents by grounding their perception in spatial-temporal scene graphs. At its core is SGCLIP, a novel, open-domain, promptable foundation model for generating scene graphs that is based on CLIP.  SGCLIP is trained on 87K+ open-domain videos using a neurosymbolic pipeline that aligns automatically generated captions with scene graphs produced by the model itself, eliminating the need for human-labeled annotations. We demonstrate that SGCLIP excels in both prompt-based inference and task-specific fine-tuning, achieving state-of-the-art results on scene graph generation and action localization benchmarks. ESCA with SGCLIP improves perception for embodied agents based on both open-source and commercial MLLMs, achieving state of-the-art performance across two embodied environments. Notably, ESCA significantly reduces agent perception errors and enables open-source models to surpass proprietary baselines. We release the source code for SGCLIP model training at https://github.com/video-fm/LASER and for the embodied agent at https://github.com/video-fm/ESCA.

---

## 论文详细总结（自动生成）

# 论文总结：ESCA：通过场景图生成为具身智能体提供上下文感知

## 1. 核心问题与整体含义（研究动机和背景）

- **背景**：多模态大语言模型（MLLMs）正快速发展，有望成为通用具身智能体的基础。然而，现有 MLLMs 难以可靠地捕捉低层视觉特征与高层文本语义之间的细粒度关联，导致智能体感知接地（grounding）能力薄弱、感知结果不准确。
- **核心问题**：如何增强具身智能体对环境的理解能力，使其能够将视觉输入与文本/语义描述精确对齐，从而提升在复杂环境中的感知与决策质量。
- **整体含义**：本文提出一种通过生成**空间-时间场景图**来为具身智能体提供感知上下文的框架 ESCA，旨在解决 MLLMs 在具身场景下的接地不足问题，并推动开放域场景图生成在机器人/具身智能领域的应用。

## 2. 方法论

- **核心思想**：将感知过程显式建模为**空间-时间场景图**，以此作为连接视觉与文本的中间表示，为具身智能体提供结构化的上下文信息。
- **关键组件**：
  - **SGCLIP**：一种新颖的、开放域的、可提示（promptable）的场景图生成基础模型，基于 CLIP 架构。
  - **神经符号训练流程（NeuroSymbolic Pipeline）**：利用自动生成的视频描述与模型自身生成的场景图进行对齐，完全不需要人工标注。该流程自动将视频字幕与场景图结构进行配对，生成训练数据。
- **训练数据**：在 **87K+ 个开放域视频**上训练 SGCLIP，覆盖广泛场景和实体关系。
- **推理与微调**：SGCLIP 既支持基于提示的推理（prompt-based inference），也支持针对特定任务的微调（task-specific fine-tuning）。

## 3. 实验设计

- **基准测试**：
  - **场景图生成**（Scene Graph Generation）基准
  - **动作定位**（Action Localization）基准
- **对比方法**：未在摘要中逐一列出，但强调 SGCLIP 在这两项基准上取得了**最先进（SOTA）结果**。
- **具身环境**：在两个不同的具身环境（embodied environments）中评估 ESCA（结合 SGCLIP）对 MLLMs 感知能力的提升效果。
- **对比对象**：
  - 基于开源 MLLM 的具身智能体
  - 基于商业 MLLM 的具身智能体（作为基线）
- **核心结果**：
  - ESCA 显著减少了智能体的感知错误。
  - 使开源模型在感知上**超越商业模型基线**。

## 4. 资源与算力

- **论文摘要中未明确说明**使用的 GPU 型号、数量、训练时长或具体算力规模。
- 仅提及训练数据量为 87K+ 视频，但未披露训练硬件与时间成本。

## 5. 实验数量与充分性

- **实验数量**：摘要中提及两组下游基准（场景图生成、动作定位）和两组具身环境评估，但未详细列出消融实验或具体实验次数。
- **充分性**：
  - 优点：覆盖了从模型能力（场景图生成、动作定位）到端到端具身感知的多个层面，并同时评估了开源与商业 MLLM，对比维度较完整。
  - 局限性：摘要未提供消融实验细节、统计显著性检验、不同场景下的方差等，因此无法从摘要层面判断实验的完整公平性；需阅读全文确认。

## 6. 主要结论与发现

- SGCLIP 在开放域视频上训练后，能够生成高质量的场景图，并在场景图生成和动作定位任务上达到 SOTA。
- ESCA 框架通过注入空间-时间场景图上下文，能够显著增强基于开源和商业 MLLM 的具身智能体的感知能力。
- 特别重要的是：**开源模型在 ESCA 辅助下可以超越专有模型基线**，表明结构化场景图上下文是缩小开源/闭源模型差距的有效手段。

## 7. 优点

- **创新性**：提出场景图生成作为具身智能体感知上下文的中间表示，区别于直接使用原始视觉特征或纯文本描述。
- **免标注训练**：利用神经符号流程自动生成训练数据，消除了对人工标注场景图的依赖，可扩展性强。
- **开放域与可提示性**：SGCLIP 基于 CLIP，支持开放域概念和提示交互，适应多样化下游任务。
- **实证价值**：在多个基准和具身环境中验证了有效性，并展示了开源模型超越商业模型的实用意义。
- **可复现性**：开源了模型训练代码（LASER）和具身智能体代码（ESCA），便于社区复现和进一步研究。

## 8. 不足与局限

- **算力信息缺失**：未提供训练和推理的算力消耗，不利于评估实际工程成本。
- **实验细节有限**：摘要未给出消融实验、失败案例、场景图质量分析等细粒度评估，需依赖全文补充。
- **数据集覆盖偏差风险**：87K+ 开放域视频虽规模可观，但可能仍存在长尾关系、稀有物体或复杂交互的覆盖不足，影响开放域泛化能力。
- **应用限制**：场景图生成的质量直接决定上下文信息的可靠性，若场景图出现结构错误或漏检，可能引入噪声并误导后续决策。
- **对比公平性**：虽然提及超越商业基线，但未明确说明基线的具体配置、是否经过同等微调或使用相同提示策略，潜在的比较优势可能受实现细节影响。

（完）
