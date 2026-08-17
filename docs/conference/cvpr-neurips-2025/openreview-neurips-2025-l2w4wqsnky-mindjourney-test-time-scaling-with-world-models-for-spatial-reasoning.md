---
title: "MindJourney: Test-Time Scaling with World Models for Spatial Reasoning"
title_zh: MindJourney：基于世界模型的测试时扩展空间推理
authors: "Yuncong Yang, Jiageng Liu, Zheyuan Zhang, Siyuan Zhou, Reuben Tan, Jianwei Yang, Yilun Du, Chuang Gan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=L2W4wQsNkY"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 面向具身任务的空间推理框架，将VLM与可控世界模型耦合，用于导航相关推理
tldr: 现有视觉语言模型缺乏对3D动态场景的内在建模，难以预测视角变化后的场景。论文提出MindJourney测试时扩展框架，将VLM与基于视频扩散的可控世界模型耦合：VLM迭代规划相机轨迹，世界模型生成对应视角图像，VLM综合多视角证据进行推理。该方法在空间推理和具身任务基准上显著提升精度，展示了扩展计算时间而非模型规模来增强空间能力的新范式，可服务于导航等任务。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视觉语言模型缺乏3D动态建模能力，在空间推理任务中表现不佳。
method: 在测试时将VLM与可控视频扩散世界模型耦合，通过迭代轨迹规划与多视角证据收集进行推理。
result: 在空间推理与具身基准上取得准确率提升。
conclusion: 验证了测试时扩展可弥补VLM空间能力缺陷，为导航等具身智能提供重要方法。
---

## Abstract
Spatial reasoning in 3D space is central to human cognition and indispensable for embodied tasks such as navigation and manipulation. However, state-of-the-art vision–language models (VLMs) struggle frequently with tasks as simple as anticipating how a scene will look after an egocentric motion: they perceive 2D images but lack an internal model of 3D dynamics. We therefore propose SpatialNavigator, a test-time scaling framework that grants a VLM with this missing capability by coupling it to a controllable world model based on video diffusion. The VLM iteratively sketches a concise camera trajectory, while the world model synthesizes the corresponding view at each step. The VLM then reasons over this multi-view evidence gathered during the interactive exploration. Without any fine-tuning, our SpatialNavigator achieves an average 7.7\% performance boost on the representative spatial reasoning benchmark SAT, showing that pairing VLMs with world models for test-time scaling offers a simple, plug-and-play route to robust 3D reasoning. Meanwhile, our method also improves upon the test-time inference VLMs trained through reinforcement learning, which demonstrates the potential of our method that utilizes world models for test-time scaling.

---

## 论文详细总结（自动生成）

# 论文总结：MindJourney（摘要中方法名写作 SpatialNavigator）

## 1. 核心问题与整体含义
- **研究动机**：空间推理是具身智能（如导航、操作）的核心能力，但现有视觉语言模型（VLM）本质上只能感知 2D 图像，缺乏对 3D 动态场景的内在建模能力。
- **核心问题**：VLM 难以完成“预测第一人称视角移动后场景如何变化”这类基础空间推理任务，导致其在具身任务中表现不佳。
- **整体含义**：论文提出一种测试时扩展（test-time scaling）的新范式——不通过扩大模型规模或微调，而是通过引入外部世界模型，在推理阶段弥补 VLM 的 3D 动态建模缺陷，从而提升空间推理能力。这对导航等具身智能任务具有重要意义。

## 2. 方法论
- **核心思想**：将 VLM 与一个基于视频扩散的可控世界模型（controllable world model）耦合，形成一个测试时扩展框架。
- **算法流程（文字说明）**：
  1. VLM 根据当前观测，迭代地规划一段简洁的相机轨迹（camera trajectory）。
  2. 可控世界模型根据该轨迹合成对应的新视角图像。
  3. 世界模型生成的多视角图像作为“多视角证据”返回给 VLM。
  4. VLM 基于这些收集到的证据进行综合推理，得出更可靠的空间判断。
- **关键技术特点**：
  - 无需对 VLM 进行任何微调。
  - 属于即插即用（plug-and-play）式的推理增强方法。

## 3. 实验设计
- **使用的数据集 / 基准**：论文提到使用代表性空间推理基准 **SAT** 进行评估。
- **对比方法**：
  - 对比了基线 VLM。
  - 还对比了通过强化学习（RL）训练的测试时推理 VLM。
- **主要结果**：在 SAT 基准上平均获得 **7.7% 的性能提升**；同时优于 RL 训练过的测试时推理 VLM，展示了方法的互补潜力。

## 4. 资源与算力
- **未明确说明**：所提供的论文内容（摘要与元数据）中未提及 GPU 型号、数量、训练时长或推理算力开销。若要评估实际成本，需查阅论文全文。

## 5. 实验数量与充分性
- **实验数量**：从现有信息看，仅提及一个基准（SAT）和两组对比（基线 VLM、RL 训练的 VLM），未列出消融实验、多数据集验证或不同世界模型变体实验。
- **充分性评价**：信息不足以充分验证方法的泛化能力。缺少消融分析（如轨迹规划策略、证据数量、世界模型类型等对性能的影响），也未展示在真实具身环境（如导航模拟器）中的验证。因此实验覆盖度偏有限，客观性和公平性需要全文补充。

## 6. 主要结论与发现
- 将 VLM 与视频扩散世界模型结合进行测试时扩展，可以显著提升 3D 空间推理能力。
- 无需微调即可获得性能收益，说明该方法是一种简单有效的“即插即用”路线。
- 即便对于已经用强化学习增强过的测试时推理 VLM，世界模型方法仍能带来额外提升，表明该范式具有独立价值与互补性。

## 7. 优点
- **新范式**：将“测试时扩展”引入空间推理，不同于传统“扩大模型”的思路，开创性较强。
- **即插即用**：无需重新训练 VLM，易于集成到现有系统中。
- **可解释性/可控性**：通过显式规划相机轨迹和世界模型生成多视角，推理过程具有可观测、可干预的中间步骤。
- **应用价值**：直接面向导航等具身智能任务，实践意义明显。

## 8. 不足与局限
- **信息不一致**：元数据标题为 *MindJourney*，但摘要中方法名写为 *SpatialNavigator*，存在命名不一致的问题。
- **实验覆盖不足**：仅报告单一基准，缺少多数据集、多任务、多模型基线的系统评估。
- **缺乏消融与细节**：未公开轨迹规划策略、世界模型具体架构、迭代步数等关键细节，难以复现。
- **算力开销未披露**：视频扩散世界模型在推理时本身计算代价高，论文未讨论效率问题，实际部署可能受限。
- **泛化风险**：仅在 SAT 上的提升不足以证明其在真实复杂 3D 场景中的可靠性；对 RL 类 VLM 的对比也缺少具体模型与训练细节，存在公平性疑问。
- **偏差风险**：摘要中“平均 7.7% 提升”是否覆盖所有难度层级或是否在特定子集上更高，目前信息不明，可能存在选择性报告风险。

（完）
