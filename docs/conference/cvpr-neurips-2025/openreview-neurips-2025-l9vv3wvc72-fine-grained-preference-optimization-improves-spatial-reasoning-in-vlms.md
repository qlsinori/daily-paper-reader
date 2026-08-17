---
title: Fine-Grained Preference Optimization Improves Spatial Reasoning in VLMs
title_zh: 细粒度偏好优化提升视觉语言模型的空间推理能力
authors: "Yifan Shen, Yuanzhe Liu, Jingyuan Zhu, Xu Cao, Xiaofeng Zhang, Yixiao He, Wenming Ye, James Matthew Rehg, Ismini Lourentzou"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=L9vV3wVC72"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 提升视觉语言模型的空间推理能力
tldr: 当前视觉语言模型在精细空间推理上存在不足，尤其是在多步逻辑与精确空间对齐方面。本文提出SpatialReasoner-R1，利用多模型蒙特卡洛树搜索生成多样且逻辑一致的长思维链推理轨迹，并通过细粒度直接偏好优化结合空间奖励机制提升推理质量。实验表明该方法显著增强了VLM的空间推理能力，为具身智能中的空间理解提供了可迁移的优化手段。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 面向具身智能的空间理解需要精细的视觉语言推理，现有VLM难以完成多步空间逻辑。
method: 用多模型MCTS生成长思维链轨迹，并用细粒度DPO与空间奖励机制优化空间推理。
result: 在空间推理基准上显著提升VLM性能，验证了偏好优化的有效性。
conclusion: 为视觉语言模型的空间推理能力提升提供了新训练方法，可支持后续导航任务。
---

## Abstract
Current Vision-Language Models (VLMs) struggle with fine-grained spatial reasoning, particularly when multi-step logic and precise spatial alignment are required. In this work, we introduce SpatialReasoner-R1, a vision-language reasoning model designed to address these limitations. To construct high-quality supervision for spatial reasoning, we design a Multi-Model Monte Carlo Tree Search (M3CTS) method that generates diverse, logically consistent Long Chain-of-Thought (LongCoT) reasoning trajectories. In addition, we propose a fine-grained Direct Preference Optimization (fDPO) method that introduces segment-specific preference granularity for descriptive grounding and logical reasoning, guided by a spatial reward mechanism that evaluates candidate responses based on visual consistency, spatial grounding, and logical coherence. Experimental results demonstrate that fDPO achieves relative performance gains of 4.1% and 9.0% over standard DPO on spatial qualitative and quantitative tasks, respectively. SpatialReasoner-R1, trained with fDPO, sets a new SoTA on SpatialRGPT-Bench, outperforming the strongest baseline by 9.4% in average accuracy, while maintaining competitive performance on general vision-language tasks.

---

## 论文详细总结（自动生成）

# 论文总结：细粒度偏好优化提升视觉语言模型的空间推理能力

## 1. 核心问题与整体含义

- **研究背景**：当前视觉语言模型（VLM）虽然在通用视觉理解任务上表现出色，但在**细粒度空间推理**方面仍然存在显著不足，尤其当任务需要**多步逻辑推断**与**精确空间对齐**（如物体间的相对位置、方向、几何关系）时，VLM 的表现明显薄弱。
- **核心动机**：面向具身智能（如机器人导航、操作）的空间理解，要求模型具备精细的视觉语言推理能力，而现有 VLM 难以胜任这类高精度、多步骤的空间逻辑任务。因此，提升 VLM 的空间推理能力具有重要的研究价值和实际应用意义。
- **整体含义**：本文提出了一个完整的训练方案，包括高质量推理轨迹的生成方法、细粒度的偏好优化算法以及空间专用的奖励机制，为增强 VLM 的空间推理能力提供了一条可行且有效的技术路径。

## 2. 方法论

论文提出的方法包含三大核心组件：

- **多模型蒙特卡洛树搜索（M3CTS）**：
  - 核心思想是利用多个不同 VLM 作为树搜索中的策略/价值评估器，通过蒙特卡洛树搜索（MCTS）对推理路径进行探索和评估。
  - 生成的推理轨迹具有**多样性**（多个模型产生多种思路）和**逻辑一致性**（MCTS 的奖励信号引导路径朝正确逻辑前进）。
  - 最终生成高质量的 **长思维链（LongCoT）** 推理轨迹，作为后续偏好优化的监督数据。

- **细粒度直接偏好优化（fDPO）**：
  - 相比标准 DPO 在整条回复层面进行偏好优化，fDPO 将偏好粒度细化到**片段（segment）级别**。
  - 针对空间推理中两个关键子能力分别设计偏好评判：**描述性空间锚定（Descriptive Grounding）** 和**逻辑推理（Logical Reasoning）**。
  - 通过分段级别的选择与优化，模型能够更精准地学习哪些中间推理步骤是可靠的、哪些是错误的。

- **空间奖励机制（Spatial Reward Mechanism）**：
  - 用于评估候选回复质量的奖励函数，从三个维度进行评判：
    1. **视觉一致性（Visual Consistency）**：回复是否与输入图像的视觉内容一致；
    2. **空间锚定（Spatial Grounding）**：回复中的空间关系描述是否准确锚定到图像中的物体；
    3. **逻辑连贯性（Logical Coherence）**：多步空间推理逻辑是否自洽。
  - 该奖励信号同时用于 MCTS 的路径评估和 fDPO 中偏好对的筛选。

## 3. 实验设计

- **基准数据集**：主要在 **SpatialRGPT-Bench** 空间推理基准上进行评估，该基准涵盖空间定性任务（如空间关系判断）与空间定量任务（如距离/尺寸估计）等多类空间推理能力测试。
- **对比方法**：
  - 基线模型：未经过空间专项优化的通用 VLM；
  - 标准 DPO：整条回复级别的直接偏好优化；
  - 论文提出的 **fDPO**：分段级别的细粒度偏好优化；
  - 最强基线（SpatialRGPT-Bench 上的已有最优模型）。
- **评估维度**：
  - 空间定性任务上的准确率；
  - 空间定量任务上的准确率；
  - 平均准确率；
  - 通用视觉语言任务上的性能保持情况（用于检验是否发生灾难性遗忘）。

## 4. 资源与算力

- 论文提供的摘要和元数据中**未明确说明**训练所用的 GPU 型号、数量、训练时长、参数量等算力信息。
- 仅仅可以推断训练涉及多个 VLM 的推理（用于 M3CTS）和一个目标模型的偏好优化，整体计算开销预计高于普通 SFT + DPO 流程，但具体数值无从得知。

## 5. 实验数量与充分性

- **已报告的实验结果**：
  - 在空间定性任务上，fDPO 相比标准 DPO 取得 **4.1%** 的相对性能提升；
  - 在空间定量任务上，相对提升达到 **9.0%**；
  - SpatialReasoner-R1 在 SpatialRGPT-Bench 上平均准确率超过最强基线 **9.4%**；
  - 在通用视觉语言任务上保持了竞争性表现。
- **充分性评价**：
  - 实验覆盖了空间推理的核心场景（定性与定量），并与标准 DPO 和最强基线进行了对比，验证了方法的有效性。
  - 但摘要中未提及详细的消融实验（如单独去除 M3CTS、fDPO 或空间奖励机制各自的影响），也未展示在不同 VLM 主干上的泛化实验。实验数量和信息在论文正文中可能更为丰富，但仅凭摘要而言，**消融和泛化性验证略显不足**。

## 6. 主要结论与发现

- **fDPO 显著优于标准 DPO**：细粒度的片段级偏好优化更契合空间推理中"部分步骤正确/部分错误"的特点，比整条回复的粗粒度优化更有效。
- **空间奖励机制有效**：将视觉一致性、空间锚定和逻辑连贯性纳入奖励评估，能够有效筛选高质量推理轨迹并指导偏好学习。
- **M3CTS 能生成高质量监督数据**：通过多模型协作与树搜索，生成的 LongCoT 轨迹兼具多样性和逻辑正确性，为训练提供了关键的监督信号。
- **SpatialReasoner-R1 刷新 SoTA**：在 SpatialRGPT-Bench 上大幅超越既有最优模型，且未显著牺牲通用任务性能，表明空间推理能力可以针对性地增强而不产生严重的灾难性遗忘。

## 7. 优点

- **问题切入精准**：聚焦"细粒度空间推理"这一具身智能的关键瓶颈，选题具有明确的实际应用价值。
- **方法链路完整**：从数据生成（M3CTS）到偏好优化（fDPO）再到奖励设计（空间奖励机制），形成了一套端到端的训练方案，各组件之间逻辑自洽。
- **粒度创新合理**：将 DPO 的偏好粒度从回复级细化到片段级，更符合空间推理中"部分正确、部分错误"的客观情况，是方法上的一个亮点。
- **多模型协作的 MCTS**：利用多个 VLM 共同生成推理轨迹，降低了单一模型的偏见风险，提升了数据多样性。
- **多维度奖励设计**：空间奖励机制同时考虑视觉一致性、空间锚定和逻辑连贯性，覆盖面较全面。

## 8. 不足与局限

- **算力信息缺失**：未报告训练所需的计算资源（GPU 类型/数量/时长），不利于他人复现时评估成本和可行性。
- **消融实验未见**：摘要未展示各组件（M3CTS  vs. 简单采样、fDPO vs. DPO、奖励机制的不同消融变体）的贡献分解，难以判断每个设计选择的确切增益来源。
- **基准覆盖有限**：仅在 SpatialRGPT-Bench 上评估空间推理，未提及在其他空间/导航基准（如 ScanQA、R2R 等）或真实机器人场景中的验证。
- **泛化性验证不足**：未报告方法在不同规模/不同系列的 VLM 主干上的适用性，其迁移能力尚不明确。
- **通用任务评估篇幅有限**：虽然提到"在通用视觉语言任务上保持竞争性表现"，但未给出具体的数据集和数字，抗遗忘的证据不够充分。
- **潜在偏差风险**：M3CTS 中多个模型可能共享相似训练数据分布的偏见，且空间奖励机制中三个维度的权重设置可能引入主观性，论文摘要未讨论这些偏差的处理。

（完）
