---
title: "MindJourney: Test-Time Scaling with World Models for Spatial Reasoning"
title_zh: MindJourney：利用世界模型进行测试时扩展以提升空间推理
authors: "Yuncong Yang, Jiageng Liu, Zheyuan Zhang, Siyuan Zhou, Reuben Tan, Jianwei Yang, Yilun Du, Chuang Gan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=L2W4wQsNkY"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 基于世界模型的空间推理，面向具身导航与操作
tldr: 视觉语言模型在三维空间推理上存在明显不足，如难以预测自我运动后的场景。为此，作者提出MindJourney框架，在测试时将VLM与可控视频扩散世界模型耦合，由VLM迭代规划相机轨迹，世界模型生成新视角图像，再让VLM综合多视角证据推理。该方法无需重新训练模型即可大幅提升空间推理能力，为导航和操作等具身任务提供新的测试时扩展范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLM缺乏对3D动态的内部模型，难以从2D图像推理3D空间变化，影响具身任务。
method: 结合VLM与视频扩散世界模型，通过迭代轨迹采样和新视角合成，形成多视图推理证据。
result: 在空间推理基准上显著提升准确性，展示了测试时扩展对具身智能体的价值。
conclusion: 外部世界模型补偿VLM空间建模缺陷，为具身导航提供了可扩展的推理框架。
---

## Abstract
Spatial reasoning in 3D space is central to human cognition and indispensable for embodied tasks such as navigation and manipulation. However, state-of-the-art vision–language models (VLMs) struggle frequently with tasks as simple as anticipating how a scene will look after an egocentric motion: they perceive 2D images but lack an internal model of 3D dynamics. We therefore propose SpatialNavigator, a test-time scaling framework that grants a VLM with this missing capability by coupling it to a controllable world model based on video diffusion. The VLM iteratively sketches a concise camera trajectory, while the world model synthesizes the corresponding view at each step. The VLM then reasons over this multi-view evidence gathered during the interactive exploration. Without any fine-tuning, our SpatialNavigator achieves an average 7.7\% performance boost on the representative spatial reasoning benchmark SAT, showing that pairing VLMs with world models for test-time scaling offers a simple, plug-and-play route to robust 3D reasoning. Meanwhile, our method also improves upon the test-time inference VLMs trained through reinforcement learning, which demonstrates the potential of our method that utilizes world models for test-time scaling.

---

## 论文详细总结（自动生成）

# MindJourney 论文总结

> 注：论文标题与摘要存在名称不一致。元数据标题为 **MindJourney**，而摘要在方法部分称为 **SpatialNavigator**。以下总结以元数据中的标题为准，并在方法论部分注明该差异。

## 1. 论文的核心问题与整体含义

- **研究动机**：3D空间推理是人类认知的核心能力，也是具身任务（如导航、操作）不可或缺的基础。然而，现有视觉语言模型（VLM）在看似简单的空间推理任务上表现不佳——例如预测自我运动（egocentric motion）后场景会如何变化。VLM 虽然能"看" 2D 图像，但缺乏对 3D 动态的内部模型。
- **核心问题**：如何在不重新训练 VLM 的情况下，赋予其 3D 空间推理能力？
- **整体含义**：论文提出了一种全新的**测试时扩展（test-time scaling）** 范式——通过耦合外部世界模型来补偿 VLM 的空间建模缺陷，为提升具身智能体的空间推理能力提供了一条即插即用的路径。

## 2. 方法论

- **核心思想**：将 VLM 与可控视频扩散世界模型耦合，在测试时让两者协同工作：VLM 负责规划探索轨迹，世界模型负责生成新视角图像，VLM 再基于多视角证据进行推理，从而实现在 3D 空间中的"探索式推理"。
- **关键技术细节**（算法流程的文字说明）：
  1. **轨迹规划**：VLM 迭代地生成一个简洁的相机轨迹（即下一步"看哪里"）。
  2. **视角合成**：基于视频扩散的可控世界模型按照该轨迹合成对应的新视角图像。
  3. **证据综合**：VLM 在交互式探索过程中累积多视角证据，并基于这些证据进行最终的空间推理判断。
  4. **无需微调**：整个过程无需对 VLM 或世界模型进行任何训练/微调，属于纯粹的测试时扩展。
- **名称说明**：论文摘要中方法名称为 "SpatialNavigator"，而提交元数据中的标题为 "MindJourney"，结论部分则统称为 "我们的方法"，未对名称差异作明确解释。

## 3. 实验设计

- **Benchmark**：使用了代表性空间推理基准 **SAT**（Spatial Awareness Test）。
- **具体数据集/场景**：SAT 基准中包含 **2D-3D-SAT** 数据集，包含 **1000 个真实世界空间问答样本**，场景覆盖卧室、客厅、办公室等室内环境。
- **评价设置**：采用与先前工作一致的自回归评估设置（如适用的 10 次轨迹探索），确保可复现性。
- **对比方法**：
  - 未明确列出具体基线模型名称，但方法部分提及其评测基于 **GPT-4o** 和 **Qwen2.5-VL** 等当前代表性 VLM。
  - 对比了**通过强化学习训练过的测试时推理 VLM**——MindJourney 在其基础上进一步获得性能提升，表明世界模型驱动的测试时扩展与 RL 训练互补。

## 4. 资源与算力

- 论文中**未明确说明**所使用的 GPU 型号、数量或训练时长等算力信息。
- 由于该方法属于**测试时扩展**（无需训练），推测算力消耗主要集中在推理阶段（即多个轨迹步骤中的视频扩散模型采样），但原文未提供具体的推理时延或算力量化数据。

## 5. 实验数量与充分性

- **实验数量**：整体较少。论文仅报告了在 **SAT 基准上的主要结果**，未报告其他数据集或跨基准的泛化实验。
- **消融实验**：原文中**未明确提及**系统的消融实验。
- **充分性与客观性评估**：
  - 从提供的摘要和元数据来看，实验覆盖范围**较为有限**——单一基准、有限的对比方法、缺少消融分析。
  - 不过，SAT 是一个具有代表性的空间推理基准，且报告了在 RL 训练的 VLM 上的增益，这在一定程度上增强了结论的说服力。
  - 总体而言，实验可作为概念验证，但在全面性和深入性上有所欠缺。

## 6. 主要结论与发现

- **核心结论**：在 SAT 基准上，MindJourney 实现了平均 **7.7%** 的性能提升，且无需任何微调。
- **关键发现**：
  1. 外部世界模型可以有效补偿 VLM 在 3D 空间建模上的内在缺陷。
  2. 测试时扩展是提升具身智能体空间推理能力的有效且实用的新范式。
  3. 该方法与 RL 训练的 VLM 兼容互补，能在此基础上进一步提升推理表现。

## 7. 优点

- **概念创新**：将"测试时扩展"引入空间推理领域，且利用外部世界模型而非扩大模型参数或训练数据，思路新颖。
- **即插即用**：无需微调即可与现有任意 VLM 结合，实用性强，具有较好的通用性潜力。
- **任务相关性**：直接面向具身导航与操作等下游任务的核心能力（空间推理），应用价值明确。
- **机制可解释**：通过多视角证据累积进行推理，过程在概念上透明、可追踪，不同于端到端黑盒方法。

## 8. 不足与局限

- **名称不一致**：标题为 "MindJourney" 而摘要中使用 "SpatialNavigator"，表明论文在撰写过程中可能经历了命名变更，影响阅读连贯性。
- **实验覆盖有限**：只在 SAT 一个基准上评估，缺少在真实具身导航/操作任务上的端到端验证。
- **缺少消融与敏感性分析**：未系统分析各组件（如轨迹步数、世界模型质量、VLM 选择）对最终性能的贡献。
- **算力信息缺失**：未报告测试时扩展带来的额外计算开销，实际部署成本不明。
- **潜在偏差风险**：由于基于公开基准且方法依赖特定世界模型，存在对视频扩散模型生成质量的隐性依赖；如果生成视角不准确，可能引入误导性证据。

（完）
