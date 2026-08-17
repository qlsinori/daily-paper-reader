---
title: Fine-Grained Preference Optimization Improves Spatial Reasoning in VLMs
title_zh: 细粒度偏好优化提升视觉语言模型的空间推理能力
authors: "Yifan Shen, Yuanzhe Liu, Jingyuan Zhu, Xu Cao, Xiaofeng Zhang, Yixiao He, Wenming Ye, James Matthew Rehg, Ismini Lourentzou"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=L9vV3wVC72"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 提升视觉语言模型的细粒度空间推理，是视觉语言导航的基础能力
tldr: 视觉语言模型在处理多步逻辑与精细空间对齐的细粒度空间推理时仍存在困难。论文提出 SpatialReasoner-R1，使用多模型蒙特卡洛树搜索生成多样且逻辑一致的长思维链轨迹，并设计细粒度直接偏好优化，按片段进行描述性锚定与逻辑推理的偏好学习。空间奖励机制进一步权衡推理质量。实验表明该方法显著提升VLM的细粒度空间推理能力，可望为视觉语言导航等空间理解任务提供更强的推理基础。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLM在细粒度空间推理上表现不佳，尤其是需要多步逻辑与精确空间对齐的任务。
method: 用多模型MCTS生成LongCoT轨迹，并以细粒度直接偏好优化和空间奖励机制训练推理模型。
result: 显著提升VLM的细粒度空间推理能力，为空间理解任务提供更好的推理基础。
conclusion: 细粒度偏好优化是增强VLM空间推理能力的有效途径，对空间感知智能体具有借鉴价值。
---

## Abstract
Current Vision-Language Models (VLMs) struggle with fine-grained spatial reasoning, particularly when multi-step logic and precise spatial alignment are required. In this work, we introduce SpatialReasoner-R1, a vision-language reasoning model designed to address these limitations. To construct high-quality supervision for spatial reasoning, we design a Multi-Model Monte Carlo Tree Search (M3CTS) method that generates diverse, logically consistent Long Chain-of-Thought (LongCoT) reasoning trajectories. In addition, we propose a fine-grained Direct Preference Optimization (fDPO) method that introduces segment-specific preference granularity for descriptive grounding and logical reasoning, guided by a spatial reward mechanism that evaluates candidate responses based on visual consistency, spatial grounding, and logical coherence. Experimental results demonstrate that fDPO achieves relative performance gains of 4.1% and 9.0% over standard DPO on spatial qualitative and quantitative tasks, respectively. SpatialReasoner-R1, trained with fDPO, sets a new SoTA on SpatialRGPT-Bench, outperforming the strongest baseline by 9.4% in average accuracy, while maintaining competitive performance on general vision-language tasks.

---

## 论文详细总结（自动生成）

# 论文总结：Fine-Grained Preference Optimization Improves Spatial Reasoning in VLMs

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：当前视觉语言模型在处理**细粒度空间推理**任务时表现不佳，尤其是在需要**多步逻辑推理**与**精确空间对齐**的场景下（如空间关系、相对位置、路径理解等）。
- **研究动机**：空间感知是视觉语言导航（如 embodied navigation）等下游任务的基础能力。已有的 VLM 在粗粒度视觉问答上表现良好，但对精细空间关系的理解仍存在明显短板。论文旨在通过**高质量推理轨迹生成**与**细粒度偏好优化**，系统性提升 VLM 的空间推理能力。
- **整体意义**：该工作为提升 VLM 在空间理解方面的推理能力提供了一种新路径，有望为空间感知智能体的构建提供更坚实的推理基础。

## 2. 方法论：核心思想、关键技术细节与算法流程

论文提出了 **SpatialReasoner-R1**，其核心方法论包含三个关键组件：

- **多模型蒙特卡洛树搜索（M3CTS，Multi-Model Monte Carlo Tree Search）**
  - 核心思想：利用多个不同模型协同参与蒙特卡洛树搜索，生成**多样化、逻辑一致**的长思维链（LongCoT）推理轨迹。
  - 作用：M3CTS 保证了训练数据的多样性与逻辑流畅性，解决了传统单模型生成数据易于重复或存在逻辑断裂的问题。
- **细粒度直接偏好优化（fDPO，fine-grained Direct Preference Optimization）**
  - 核心思想：在传统 DPO 的基础上，引入**片段级（segment-specific）偏好粒度**，分别针对**描述性锚定（descriptive grounding）** 与**逻辑推理（logical reasoning）** 进行细粒度的偏好学习。
  - 与标准 DPO 的区别：标准 DPO 对整条回答作整体偏好判断，而 fDPO 能够定位到回答中的具体片段，识别哪些部分在视觉锚定或逻辑推理上更好，从而进行更精准的优化。
- **空间奖励机制（Spatial Reward Mechanism）**
  - 该机制从三个维度评估候选回答的质量：**视觉一致性、空间锚定、逻辑连贯性**，从而为偏好学习提供可靠的奖励信号。
  - 这一机制用于筛选和构建偏好对，是 fDPO 训练的关键支撑。

> 注：摘要中未提供具体的公式或详细算法步骤，以上为基于论文摘要对核心方法框架的文字性描述。

## 3. 实验设计

- **数据集 / 基准**：论文在 **SpatialRGPT-Bench** 上进行了评估，该基准专门用于测试 VLM 的空间推理能力。此外还涉及空间**定性任务（qualitative）** 与**定量任务（quantitative）** 的评估。
- **对比方法**：
  - 将 fDPO 与**标准 DPO** 进行对比，以验证细粒度偏好的有效性。
  - 在 SpatialRGPT-Bench 上与**最强基线模型**进行对比。
  - 同时在**通用视觉语言任务**上评估模型性能，以检测引入空间推理训练是否会影响通用能力。

## 4. 资源与算力

- 论文提供的材料中**未明确说明**所投入的算力资源，包括 GPU 型号、数量、训练时长、参数量等信息均未提及。
- 因此无法对该模型的训练成本进行具体评估。

## 5. 实验数量与充分性

- **实验数量**：从摘要信息来看，主要包含以下几组关键实验：
  1. fDPO vs. 标准 DPO 在空间定性任务上的对比（提升 4.1%）；
  2. fDPO vs. 标准 DPO 在空间定量任务上的对比（提升 9.0%）；
  3. SpatialReasoner-R1 vs. 最强基线在 SpatialRGPT-Bench 上的对比（平均准确率提升 9.4%）；
  4. 在通用视觉语言任务上的性能保持性评估。
- **充分性评估**：
  - 从摘要呈现的结果看，fDPO 在不同任务类型上均有一致的正向增益，且最终模型在专用基准上达到 SoTA，具有较强的说服力。
  - 然而，摘要中**未提及消融实验**（如去掉 M3CTS、去掉空间奖励机制等）、**跨多基准的泛化实验**，以及**误差分析**等细节，因此基于摘要信息，实验的完整性尚无法完全判定。
  - 总体上，核心实验设计合理且结果明确，但完整的充分性需要结合论文全文进行进一步审视。

## 6. 主要结论与发现

- **fDPO 优于标准 DPO**：在空间定性任务上相对提升 **4.1%**，定量任务上相对提升 **9.0%**，证明片段级偏好优化比整体偏好优化更适合空间推理任务。
- **SpatialReasoner-R1 达到新 SOTA**：在 SpatialRGPT-Bench 上以平均准确率超越最强基线 **9.4%**。
- **不牺牲通用性能**：模型在通用视觉语言任务上保持了具有竞争力的表现，说明空间推理能力的增强没有以牺牲通用能力为代价。
- **细粒度偏好优化是有效路径**：该工作验证了结合高质量轨迹生成与片段级偏好学习可有效增强 VLM 的空间推理能力。

## 7. 优点

- **方法创新性强**：将 MCTS 引入多模型协同生成空间推理轨迹，并创新性地提出片段级 fDPO，在偏好优化粒度上做出了有价值的改进。
- **问题导向明确**：针对细粒度空间推理这一薄弱环节进行专门建模，而非泛泛地提升 VLM 能力。
- **评估维度全面**：从视觉一致性、空间锚定、逻辑连贯性三个维度综合设计奖励机制，覆盖了空间推理的关键质量因素。
- **结果显著且稳健**：在多个对比维度上均有明显增益，且与标准 DPO 的对比直接验证了核心贡献的有效性。

## 8. 不足与局限

- **算力成本信息缺失**：未报告训练所需的 GPU 资源与时间成本，难以评估方法的实用性与可复现门槛。
- **实验覆盖有限**：摘要中仅提及一个专用基准（SpatialRGPT-Bench），未展示在更多空间推理基准上的泛化表现。
- **消融实验不明**：未在摘要中披露对 M3CTS、空间奖励机制等关键组件的消融分析，方法中各部分的独立贡献尚不清晰。
- **基线数量不清**：仅提到“最强基线”，未给出参与对比的基线模型列表与数量，难以判断提升幅度的全面性。
- **长度与稳定性风险**：LongCoT 轨迹的引入可能带来训练和推理效率开销，以及长回答中中间步骤出错的风险，摘要未对上述潜在问题进行讨论。
- **偏差风险**：偏好数据的生成与奖励机制的设计可能引入系统偏差（如对特定表达风格的偏好），需在真实下游任务中进一步验证。

（完）
