---
title: "Aux-Think: Exploring Reasoning Strategies for Data-Efficient Vision-Language Navigation"
title_zh: Aux-Think：利用推理策略实现数据高效的视觉语言导航
authors: "Shuo Wang, Yongcai Wang, Wanting Li, Xudong Cai, Yucheng Wang, Maiyue Chen, kaihui.wang, Zhizhong Su, Deying Li, Zhaoxin Fan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=vNmWbINtwH"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 视觉语言导航，按自然语言指令导航
tldr: 论文针对视觉语言导航中推理策略未被充分探索的问题，首次系统评估了No-Think、Pre-Think等推理策略在动作中心的长时程导航任务中的作用。通过在大规模预训练模型上微调并对比不同推理方式，揭示了推理策略对指令跟随与泛化性能的影响。实验表明合适的推理策略能显著提升数据效率与导航效果，为VLN中的推理设计提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视觉语言导航对具身智能体至关重要，但推理策略在长时程导航任务中作用未被探索。
method: 首次系统评估多种推理策略如No-Think、Pre-Think，并在预训练模型上微调进行对比。
result: 发现不同的推理策略显著影响导航的性能和数据效率，合适的策略可提升泛化。
conclusion: 为视觉语言导航中的推理策略选择提供实证指导，推动数据高效导航研究。
---

## Abstract
Vision-Language Navigation is a critical task for developing embodied agents that can follow natural language instructions to navigate in complex real-world environments.  Recent advances by finetuning large pretrained models have significantly improved generalization and instruction grounding compared to traditional approaches. However, the role of reasoning strategies in navigation—an action-centric, long-horizon task—remains underexplored, despite Chain-of-Thought reasoning's demonstrated success in static tasks like question answering and visual reasoning. To address this gap, we conduct the first systematic evaluation of reasoning strategies for VLN, including No-Think (direct action prediction), Pre-Think (reason before action), and Post-Think (reason after action). Surprisingly, our findings reveal the Inference-time Reasoning Collaps issue, where inference-time reasoning degrades navigation accuracy, highlighting the challenges of integrating reasoning into VLN. Based on this insight, we propose Aux-Think, a framework that trains models to internalize structured reasoning patterns through CoT supervision during training, while preserving No-Think inference for efficient action prediction. To support this framework, we release R2R-CoT-320k, a large-scale Chain-of-Thought annotated dataset.  Empirically, Aux-Think significantly reduces training effort without compromising performance.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究任务**：视觉语言导航（Vision-Language Navigation, VLN），要求智能体依据自然语言指令在复杂真实环境中完成长时程动作决策与导航。
- **研究痛点**：尽管大规模预训练模型微调已提升导航的指令跟随与泛化能力，但**推理策略（reasoning strategies）在导航这一动作中心、长时程任务中的作用尚未被系统探索**。已有的 Chain-of-Thought（CoT）推理成功主要体现在问答、视觉推理等静态任务中。
- **核心问题**：能否以及如何将推理策略引入 VLN？不同的推理方式会如何影响导航性能和数据效率？
- **整体含义**：该论文是**首次系统评估 VLN 中多种推理策略**的工作，并提出了新的训练框架 Aux-Think，旨在在保持高效推理的同时，利用训练阶段的 CoT 监督提升数据效率，从而为 VLN 的推理设计提供实证指导。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：将推理过程与动作预测解耦——在训练时让模型学习结构化推理模式，而在推理（测试）时不显式生成推理链，以避免推理开销和潜在的精度下降。
- **系统评估的三种推理策略**：
  - **No-Think**：直接预测动作，无显式推理；
  - **Pre-Think**：在动作预测之前先进行推理；
  - **Post-Think**：先预测动作，再生成推理。
- **关键发现——推理时坍缩（Inference-time Reasoning Collapse）**：在推理阶段引入显式推理链反而会降低导航准确率，说明静态任务中有效的 CoT 推理并不能直接迁移到 VLN。
- **提出框架 Aux-Think**：
  - 训练阶段：通过 CoT 监督（可视为辅助任务）让模型内化结构化推理模式；
  - 推理阶段：采用 No-Think 方式直接输出动作，兼顾效率与效果。
- **支持数据**：发布了大规模 CoT 标注数据集 **R2R-CoT-320k**，为上述训练提供监督信号。

## 3. 实验设计

- **数据集**：论文发布并使用了 **R2R-CoT-320k**，这是一个基于 R2R 路线的大规模 CoT 标注数据集（约 32 万条），用于训练模型内化推理模式。
- **Benchmark**：依据摘要推断，评估基于 VLN 领域通用的 **R2R（Room-to-Room）** 基准，该基准涉及真实室内环境的指令跟随导航。
- **对比方法**：论文对比了不同推理策略配置，包括：
  - **No-Think（基线，直接动作预测）**；
  - **Pre-Think（先推理后动作）**；
  - **Post-Think（先动作后推理）**；
  - **Aux-Think（训练时有 CoT 监督，推理时无显式推理）**。
- **评估指标**：摘要中未明确提及具体指标，但 VLN 常用成功率（SR）、路径加权成功率（SPL）等；推测论文使用了此类标准指标，但需以原文为准。

## 4. 资源与算力

- 论文提供的材料中**未明确说明 GPU 型号、数量、训练时长、显存占用等算力信息**。
- 从“R2R-CoT-320k”的大规模数据集和“finetuning large pretrained models”的描述推断，训练需要较大的计算资源（如多卡高端 GPU），但原文未给出具体数值。
- 这一信息缺失可能因为提取文本不完整，建议查阅原文实验设置部分确认。

## 5. 实验数量与充分性

- 从现有信息看，实验覆盖了：
  - **三种基础推理策略的系统性对比**（No-Think、Pre-Think、Post-Think）；
  - **Aux-Think 与这些策略的对比**；
  - **在 R2R-CoT-320k 数据集上的训练与评估**。
- **充分性判断**：
  - 优点是首次对推理策略进行系统评估，且包含推理时坍缩现象的发现，能有效揭示 CoT 在 VLN 中的适用边界。
  - 但受限于摘要信息，**未看到消融实验、不同模型规模、不同导航环境（如未见过的场景）泛化实验的具体数量**。因此，实验是否覆盖了足够的模型变体和场景尚不明确，需依赖原文补充。
  - 公平性方面：对三种推理策略的对比设计较为直接，能够客观比较推理时序的影响；但若未控制推理长度、提示模板等变量，可能存在偏差。

## 6. 主要结论与发现

- **发现一：推理时坍缩（Inference-time Reasoning Collapse）**——在 VLN 的推理阶段使用显式推理链会**降低导航准确率**，这与 CoT 在静态任务中的正向作用相反。
- **发现二：合适的训练策略可提升数据效率**——Aux-Think 通过在训练时加入 CoT 监督、推理时去掉显式推理，能够**显著减少训练成本而不损害性能**。
- **整体结论**：推理策略的选择对 VLN 的性能和数据效率有显著影响；将推理作为训练中的辅助信号而非推理时的显式步骤，是更有效的设计思路，为后续 VLN 推理研究提供了实证基础。

## 7. 优点

- **研究视角新颖**：首次系统研究推理策略在 VLN 中的作用，填补了该领域空白。
- **实践导向强**：发现推理时坍缩并据此设计 Aux-Think，兼顾性能与效率，具有实际应用价值。
- **数据贡献大**：发布 R2R-CoT-320k 大规模 CoT 数据集，可支持后续研究。
- **结论清晰**：通过直接对比三种推理时序，直观揭示了推理在动作中心任务上的特殊性质。

## 8. 不足与局限

- **信息不完整**：当前提供的论文文本仅包含摘要和元数据，缺少方法细节、实验具体数值、算力配置等关键内容，无法进行完整复现评估。
- **数据集依赖**：R2R 数据集基于真实室内场景，但只有一种基准环境，缺乏对不同场景类型（如户外、多楼层）、不同指令风格和跨域泛化的验证。
- **推理时坍缩的普适性存疑**：该现象可能受模型容量、任务长度、指令复杂度影响，论文未说明是否在多种模型规模下均成立。
- **潜在偏差**：CoT 标注数据（R2R-CoT-320k）的生成方式、标注质量及对模型行为的引导可能引入系统性偏差，文中未提及质量控制细节。
- **应用限制**：推理时采用 No-Think 意味着显式推理的可解释性被牺牲，对于需要透明决策的导航场景可能不适用。

（完）
