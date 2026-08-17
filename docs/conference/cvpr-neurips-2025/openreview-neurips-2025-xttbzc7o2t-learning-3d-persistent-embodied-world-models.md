---
title: Learning 3D Persistent Embodied World Models
title_zh: 学习三维持久化具身世界模型
authors: "Siyuan Zhou, Yilun Du, Yuncong Yang, Lei Han, Peihao Chen, Dit-Yan Yeung, Chuang Gan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=XTTbzC7O2T"
tags: ["query:vln-memory"]
score: 8.0
evidence: 带显式场景记忆的持久化具身世界模型
tldr: 提出一种带显式记忆的持久化具身世界模型，以解决现有视频世界模型缺乏场景记忆、长时程仿真不一致的问题。模型利用视频扩散模型预测RGB-D视频，并显式存储先前生成的内容，从而在部分可观察的复杂环境中实现一致的长时程模拟。实验证明了该方法在长期模拟一致性上的显著提升，为智能体长期规划提供支持。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视频世界模型缺乏场景记忆，无法在部分可观察环境中进行长期一致仿真。
method: 设计持久化具身世界模型，在视频扩散中显式保存已生成内容。
result: 长期模拟一致性得到明显改善，支持长时程规划。
conclusion: 显式记忆机制提升世界模型在复杂场景中的预测能力。
---

## Abstract
The ability to simulate the effects of future actions on the world is a crucial ability of intelligent embodied agents, enabling agents to anticipate the effects of their actions and make plans accordingly. While a large body of existing work has explored how to construct such world models using video models, they are often myopic in nature, without any memory of a scene not captured by currently observed images, preventing agents from making consistent long-horizon plans in complex environments where many parts of the scene are partially observed. We introduce a new persistent embodied world model with an explicit memory of previously generated content, enabling much more consistent long-horizon simulation. During generation time, our video diffusion model predicts RGB-D video of the future observations of the agent. This generation is then aggregated into a persistent 3D map of the environment. By conditioning the video model on this 3D spatial map, we illustrate how this enables video world models to faithfully simulate both seen and unseen parts of the world. Finally, we illustrate the efficacy of such a world model in downstream embodied applications, enabling effective planning and policy learning.

---

## 论文详细总结（自动生成）

# 论文总结：Learning 3D Persistent Embodied World Models

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：智能具身体（embodied agents）需要具备对“未来动作如何影响世界”的预测能力，这是规划与决策的基础。近年来，大量研究尝试用视频生成模型构建世界模型（world models）。
- **核心问题**：现有视频世界模型本质上是**“近视”的（myopic）**——它们没有对场景的持久记忆，仅基于当前可观测的RGB图像进行预测，无法感知当前视野之外的世界。这导致在复杂、部分可观察的环境中，模型无法进行**一致的长时程（long-horizon）仿真**，从而限制了智能体的长期规划能力。
- **整体含义**：论文指出，要使世界模型真正支持长期规划，必须赋予其**显式的场景记忆**，使其能够在时间推移中构建并维护对环境的一致理解，而不是逐帧孤立地预测未来。

## 2. 方法论：核心思想、关键技术细节与算法流程

- **核心思想**：提出一种**持久化具身世界模型（Persistent Embodied World Model）**，在视频生成过程中显式存储已生成的内容，形成对环境的持久3D记忆，并以此作为后续生成的额外条件。
- **关键技术细节**：
  - 使用**视频扩散模型**作为生成骨干，预测智能体未来观察的**RGB-D视频**；
  - 将预测生成的RGB-D帧实时聚合为**持久化的3D场景地图（persistent 3D map）**；
  - 在生成下一段视频时，将当前3D地图作为**条件输入（conditioning）**注入视频扩散模型，使模型在预测时同时考虑历史记忆与当前观察；
  - 这种“生成→聚合→再条件化”的循环，使模型能够对**已见过和未见过**的世界部分进行一致仿真。
- **算法流程（文字描述）**：
  1. 智能体在当前状态采集RGB-D观测；
  2. 视频扩散模型根据当前观测 + 已有3D地图，预测未来若干步的RGB-D视频；
  3. 将预测的RGB-D帧通过空间变换聚合到3D地图中，更新场景记忆；
  4. 重复上述过程，实现长时程的一致仿真。

## 3. 实验设计：数据集、Benchmark 与对比方法

- **数据集/场景**：论文摘要中未明确列出具体数据集名称。
- **Benchmark**：摘要中未详细说明。
- **对比方法**：摘要中未明确列出对比基线，但从问题设定来看，对比对象应为**无记忆的经典视频世界模型**，例如基于视频扩散的逐帧/短视频预测模型。
- **下游应用评估**：论文在具身智能的下游任务上验证了模型的有效性，包括**长期规划（planning）**和**策略学习（policy learning）**。

> **说明**：由于原始文本仅包含摘要，缺少实验章节的细节。以上实验部分信息受限于可获取的文本范围。

## 4. 资源与算力

- **原文未明确说明**：在可获取的摘要部分，**没有提及**任何关于GPU型号、数量、训练时长、参数量等算力资源的信息。

## 5. 实验数量与充分性

- **已知实验**：从摘要可以确认的实验包括：
  - 长时程仿真一致性评估（核心实验）；
  - 对“已见/未见”世界部分的仿真能力评估；
  - 下游具身应用评估（规划与策略学习）。
- **充分性评估**：由于缺少实验章节的细节，无法判断是否有消融实验（如去掉3D记忆的变体）、不同场景泛化实验等。从摘要描述看，实验设计意图较完整，覆盖了**仿真质量**与**下游有效性**两个层面；但**具体实验数量、对比公平性、指标选择**等信息不足，需查阅全文才能评估。

## 6. 主要结论与发现

- 将**显式持久化3D记忆**引入视频世界模型，能够显著提升**长时程仿真的环境一致性**；
- 相比无记忆的myopic世界模型，该方法能够同时一致地仿真环境中**已观察**和**未观察**的部分；
- 该世界模型在**下游具身规划**和**策略学习**任务中表现出有效性，证明其具有实用价值。

## 7. 优点

- **问题定位精准**：直击视频世界模型缺乏持久记忆的痛点，动机清晰、问题重要；
- **方案简洁有效**：通过“生成→3D聚合→条件生成”的循环，以较小改动获得长期一致性的大幅提升；
- **任务覆盖面广**：从仿真质量到下游规划/策略学习，验证链条完整；
- **形式新颖**：将3D场景表示与视频扩散模型结合，符合具身智能中“空间智能”的发展趋势。

## 8. 不足与局限

- **信息完整性受限**：本次分析仅基于摘要，实验细节、消融设计、基线对比充分性无法完整评估；
- **可扩展性存疑**：RGB-D视频生成 + 3D地图聚合的计算开销较大，其**实时性**和**扩展到大规模场景**的能力有待验证；
- **依赖RGB-D观测**：方法需要深度信息作为输入，在无深度传感器的场景中应用受限；
- **长期累积误差**：虽然持久记忆缓解了一致性问题，但3D地图中累积的生成误差是否会随仿真时间增长而退化，仍需进一步分析；
- **评测基准不明确**：摘要未说明在哪些具体benchmark上测试，以及是否与SOTA方法做了全面对比，结论的泛化性需谨慎看待。

---

**（完）**
