---
title: Video World Models with Long-term Spatial Memory
title_zh: 带长期空间记忆的视频世界模型
authors: "Tong Wu, Shuai Yang, Ryan Po, Yinghao Xu, Ziwei Liu, Dahua Lin, Gordon Wetzstein"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=HbTxc6U1fO"
tags: ["query:semantic-map"]
score: 9.0
evidence: 几何约束的长期空间记忆；三维记忆存储与检索；世界模型
tldr: 针对视频世界模型因上下文窗口有限而在重访场景中出现严重遗忘的问题，受人类记忆机制启发，提出几何约束的长期空间记忆框架。该框架包含显式的三维记忆存储与检索机制，并构建定制数据集进行训练和评测。实验表明该方法能改善生成视频的一致性和连贯性，为世界模型的长时空间记忆提供了可行方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视频世界模型因时间上下文窗口有限，重访场景时难以维持一致性，容易遗忘已生成的环境。
method: 引入几何约束的长期空间记忆，支持三维记忆的显式存储与检索，并构建专门数据集训练测评。
result: 评测显示生成视频的质量和一致性得到提升，减少了场景遗忘。
conclusion: 显式三维长期空间记忆能够显著提高世界模型在长时生成中的场景保持能力。
---

## Abstract
Emerging world models autoregressively generate video frames in response to actions, such as camera movements and text prompts, among other control signals. Due to limited temporal context window sizes, these models often struggle to maintain scene consistency during revisits, leading to severe forgetting of previously generated environments. Inspired by the mechanisms of human memory, we introduce a novel framework to enhancing long-term consistency of video world models through a geometry-grounded long-term spatial memory. Our framework includes mechanisms to store and retrieve information from the long-term spatial memory and we curate custom datasets to train and evaluate world models with explicitly stored 3D memory mechanisms. Our evaluations show improved quality, consistency, and context length compared to relevant baselines, paving the way towards long-term consistent world generation.

---

## 论文详细总结（自动生成）

# 论文总结：《Video World Models with Long-term Spatial Memory》

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：视频世界模型（Video World Models）能够根据动作、相机移动、文本提示等控制信号自回归地生成视频帧，在交互式环境模拟、具身智能等领域具有重要前景。
- **核心问题**：由于时间上下文窗口大小有限，现有视频世界模型在长时生成过程中，尤其是当模型“重访”之前已经生成过的场景区域时，难以维持场景一致性，会出现对先前生成环境的严重遗忘（severe forgetting）。
- **整体含义**：场景保持能力不足是制约世界模型走向长期一致生成的关键瓶颈。论文从人类记忆机制中获取灵感，探索将长期空间记忆显式地引入视频世界模型，以突破上下文窗口的限制。

## 2. 提出的方法论

- **核心思想**：受人类记忆机制启发，构建一个**几何约束的长期空间记忆（geometry-grounded long-term spatial memory）** 框架，让模型拥有独立于时间上下文窗口的“记忆模块”，从而在长时生成中维持对场景的稳定表征。
- **关键机制**：
  - **存储机制**：将生成过程中获取的场景信息以显式的三维空间记忆形式进行存储，而不是依赖隐式的时序上下文。
  - **检索机制**：在生成新帧时，模型能够从长期空间记忆中主动检索与当前视角、位置相关的信息，辅助当前帧的生成。
  - **几何约束**：记忆的存储与检索均以三维几何为锚点（geometry-grounded），保证记忆内容与真实场景的空间结构一致，增强泛化和一致性。
- **公式或算法流程**：原文摘要未给出具体的数学公式或算法流程细节。从摘要可得的基本流程为：场景生成 → 提取/更新三维空间记忆 → 在后续帧生成时检索相关记忆 → 融合记忆与当前上下文进行自回归生成。训练与推理均引入显式三维记忆通路。

## 3. 实验设计

- **数据集/场景**：论文提及了**自定义数据集（custom datasets）** 的构建，专门用于训练和评估带显式三维长期记忆机制的世界模型，但具体数据集名称、场景类别及规模在摘要中未列出。
- **Benchmark**：自定义的评测体系，用于衡量长期生成中的一致性、连贯性和质量；具体评测指标未在摘要中说明。
- **对比方法**：摘要指出与“相关基线（relevant baselines）”进行了比较，但未列出具体基线方法名称。
- **缺失信息**：由于仅有摘要可用，具体的训练/测试场景划分、评测指标细节、基线方法配置等实验细节暂无法获取。

## 4. 资源与算力

- 原文（摘要及元数据）**未明确说明**训练所用 GPU 型号、数量、训练时长、参数量等计算资源信息。
- 如需了解算力需求，需要查阅论文正文的实验设置部分。

## 5. 实验数量与充分性

- **实验数量**：摘要仅概述了评测结果（质量、一致性、上下文长度均优于基线），未列出具体实验组数，如跨多少个场景、多少种动作序列、进行了哪些消融研究等。
- **充分性判断**：从现有摘要信息来看，很难对实验的充分性、客观性和公平性做出完整评估。论文宣称构建了自定义数据集并对比了基线，说明作者已考虑了评测的可控性，但由于缺少具体评测指标、基线设置和消融实验细节，无法断定实验是否全面覆盖了不同场景复杂度、不同记忆长度等关键变量。
- **潜在风险**：仅使用自定义数据集可能存在评测偏置风险，且缺少与标准视频生成/世界模型公共基准的对比。

## 6. 主要结论与发现

- 显式三维长期空间记忆机制能够**显著改进视频世界模型在长时生成中的场景保持能力**，减少重访场景时的遗忘现象。
- 评测结果显示，该框架在**生成质量、一致性、可支持的上下文长度**三方面均优于相关基线。
- 论文的工作为长时一致的视频世界生成提供了一条可行路径，验证了“显式记忆”相对于“隐式上下文”的优越性。

## 7. 优点（方法与实验亮点）

- **问题选得好**：精准命中视频世界模型实际应用中的关键痛点——长时一致性遗忘，具有很高的应用价值。
- **思路有启发性**：将人类记忆机制（存储-检索）引入世界模型设计，做显式的三维空间记忆而非纯粹扩大上下文窗口，角度新颖。
- **设计整体性强**：同时提出了记忆存储、记忆检索、几何约束三个核心机制，并配套构建了定制数据集用于训练和评测，形成闭环。
- **记忆与几何绑定**：利用三维几何约束使记忆具备空间一致性，理论上比单纯的特征记忆更容易应对视角变化和场景重访。

## 8. 不足与局限

- **信息可见性限制**：本文输入仅为摘要+元数据，实验细节、算法公式、模型架构等均无法深入考察。
- **实验覆盖度存疑**：基于自定义数据集，缺少在公开标准数据集（如 Matterport3D、Habitat 或常见视频生成基准）上的验证，泛化性待考。
- **基线对比不透明**：摘要未明确对比的基线方法是什么（是无记忆的强基线？还是 RNN 式隐状态模型？），公平性难以评判。
- **几何记忆的适用边界**：几何约束的三维记忆对单目生成、动态场景或大规模开放世界是否仍然有效，论文摘要未做出讨论。
- **算力成本未说明**：显式三维记忆的存储与检索可能带来额外的计算与内存开销，但文中未提供相关成本分析。
- **缺乏消融研究**：从摘要看，未体现对“几何约束”“记忆存储”“记忆检索”等各组件的消融分析，无法确认各模块的独立贡献。

---

（完）
