---
title: "REMI: Reconstructing Episodic Memory During Internally Driven Path Planning"
title_zh: REMI：在内部驱动路径规划中重建情景记忆
authors: "Zhaoze Wang, Genela Morris, Dori Derdikman, Pratik Chaudhari, Vijay Balasubramanian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=LPWzV8zrgj"
tags: ["query:vln-memory"]
score: 7.0
evidence: 空间记忆与路径规划的神经机制理论
tldr: 网格细胞与位置细胞分别形成空间表征，但它们如何支持内部驱动的路径规划仍不清楚。本文提出MEC-海马连接的系统理论，认为位置细胞将感觉输入与网格细胞模式关联，从而允许线索触发目标检索、规划路径并重建沿线感觉体验。该理论为空间长期记忆在导航中的计算角色提供新解释，对未来类脑导航智能体设计具有启发。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 网格细胞与位置细胞的交互如何支撑内部驱动的路径规划和记忆重建缺乏计算框架。
method: 构建MEC-海马连接理论模型，用模式关联实现线索触发目标检索和路径体验重建。
result: 理论模型解释了路径规划中的记忆重建机制，可启发仿生导航算法。
conclusion: 该工作为空间长期记忆机制提供神经层面的理论支持，有助于发展认知启发的导航系统。
---

## Abstract
Grid cells in the medial entorhinal cortex (MEC) and place cells in the hippocampus (HC) both form spatial representations. Grid cells fire in triangular grid patterns, while place cells fire at specific locations and respond to contextual cues. How do these interacting systems support not only spatial encoding but also internally driven path planning, such as navigating to locations recalled from cues? Here, we propose a system-level theory of MEC-HC wiring that explains how grid and place cell patterns could be connected to enable cue-triggered goal retrieval, path planning, and reconstruction of sensory experience along planned routes. We suggest that place cells autoassociate sensory inputs with grid cell patterns, allowing sensory cues to trigger recall of goal-location grid patterns. We show analytically that grid-based planning permits shortcuts through unvisited locations and generalizes local transitions to long-range paths. During planning, intermediate grid states trigger place cell pattern completion, reconstructing sensory experiences along the route. Using a single-layer RNN modeling the HC-MEC loop with a planning subnetwork, we demonstrate these effects in both biologically grounded navigation simulations using RatatouGym and visually realistic navigation tasks using Habitat Sim.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：内嗅皮层（MEC）中的网格细胞与海马体（HC）中的位置细胞都被认为参与空间表征——网格细胞以规则的三角形网格模式放电，位置细胞则在特定位置放电并对情境线索做出响应。然而，这两类系统如何协同工作，以支持**内部驱动的路径规划**（例如，根据某个线索回忆目标位置并导航过去），在计算机制上仍不清楚。
- **核心问题**：网格细胞和位置细胞之间的连接模式能否解释“线索触发目标检索 → 路径规划 → 沿规划路径重建感觉体验”这一完整过程？
- **整体含义**：论文提出一个系统级理论（MEC-HC 连接理论），为空间长期记忆在导航中的计算角色提供了新的神经机制解释，并可能启发未来类脑导航智能体的设计。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：位置细胞将感觉输入与网格细胞模式进行**自联想（autoassociative）**关联，从而允许感觉线索触发目标位置对应的网格模式回忆。
- **关键机制**：
  1. **线索触发目标检索**：感觉线索（如视觉、嗅觉等）通过位置细胞的自联想网络，激活与目标地点对应的网格细胞放电模式。
  2. **网格细胞驱动的路径规划**：在网格细胞表征空间中进行规划。论文分析证明，基于网格的规划能够：
     - 生成经过**未访问位置**的捷径；
     - 将局部的转移模式推广到长距离路径。
  3. **重建沿途感觉体验**：在规划过程中，中间网格状态会触发位置细胞的**模式补全（pattern completion）**，从而重建规划路径上的感觉体验（如沿途看到的地标、场景等）。
- **模型实现**：使用一个**单层 RNN** 模拟 HC-MEC 环路，并包含一个“规划子网络（planning subnetwork）”，用于在上述理论框架下实现路径规划和记忆重建。
- **数学/算法层面**：论文以文字分析的方式证明网格表征的几何性质（三角形网格）有利于路径推广和捷径生成；具体公式未在摘要中展示。

## 3. 实验设计：使用了哪些数据集 / 场景、benchmark、对比方法

- **实验场景**（摘要中明确指出两个）：
  - **RatatouGym**：一个生物合理（biologically grounded）的导航仿真环境，用于模拟大鼠在简单环境中的空间导航。
  - **Habitat Sim**：一个视觉上更真实的导航任务平台，用于评估模型在视觉复杂环境中的表现。
- **Benchmark**：未在摘要中给出具体基准任务名称（如是否与经典 RL 导航基线比较、是否有标准成功率/路径长度指标等）。
- **对比方法**：摘要中未提及与哪些现有方法（如其他认知地图模型、深度学习导航方法）进行了对比。

## 4. 资源与算力

- 论文提供的内容（摘要）中**未明确说明**使用的 GPU 型号、数量、训练时长、显存等算力信息。
- 由于内容来自论文摘要部分，完整实验设置（包括硬件环境）可能出现在论文正文中，但当前文本无法获取。

## 5. 实验数量与充分性

- **实验数量**：摘录中仅提到两个主要实验环境（RatatouGym 和 Habitat Sim），未列出具体实验组数、消融实验数量或统计结果。
- **充分性评估**：
  - 从摘要看，实验覆盖了“生物仿真”和“视觉真实”两类场景，具有一定代表性。
  - 但缺少消融实验（例如去除网格细胞规划子网络、去除模式补全机制等）的描述。
  - 由于缺少对比方法和定量结果，无法从现有信息判断实验的客观性和公平性。需要查看完整论文才能评估。

## 6. 论文的主要结论与发现

- 位置细胞与网格细胞之间的自联想连接可支持线索触发的目标位置记忆回忆。
- 网格细胞表征的规则性允许路径规划时进行长距离推广和未访问位置的捷径生成。
- 规划过程中网格状态的激活能够引导位置细胞模式补全，从而重建沿线感觉体验。
- 上述机制在 RatatouGym 和 Habitat Sim 中均得到验证，表明该理论可解释生物导航中的记忆重建，并对类脑导航算法具有启发意义。

## 7. 优点

- 提出了一个**系统级且可计算**的 MEC-HC 连接理论，弥补了网格细胞/位置细胞交互在路径规划中的计算框架空白。
- 理论分析（捷径、泛化）与仿真实验相结合，易于为后续研究提供验证基础。
- 使用两个不同粒度的仿真平台（生物仿真 vs. 视觉真实），兼顾神经合理性与应用场景。
- 用 RNN 建模环路，模型简洁可扩展，与类脑计算方向契合。

## 8. 不足与局限

- **实验覆盖有限**：仅从摘要看，缺少大规模量化实验（如成功率、路径长度、效率指标）以及对不同环境复杂度/干扰的鲁棒性分析。
- **消融与对比不充分**：未提及消融实验和与现有导航模型的对比，难以判断该机制的独特贡献和相对优势。
- **缺乏真实神经数据验证**：论文属于理论+仿真模型，未使用真实神经记录数据（如大鼠 MEC/HC 电生理数据）验证预测。
- **应用限制**：模型基于网格细胞周期性的假设，可能难以直接迁移到无规则/非欧几里得空间或动态变化的环境中。
- **算力与复现信息缺失**：没有报告训练细节，影响可复现性。

（完）
