---
title: "BeliefMapNav: 3D Voxel-Based Belief Map for Zero-Shot Object Navigation"
title_zh: BeliefMapNav：用于零样本物体导航的三维体素信念图
authors: "Zibo Zhou, Yue Hu, Lingkai Zhang, Zonglin Li, Siheng Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=7AMriz7I3K"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 基于三维体素信念图的零样本物体目标导航
tldr: 零样本物体导航要求机器人在未知环境中依据自然语言描述寻找目标物体，但现有通用大模型常因缺乏全局环境理解而贪心选择目标。本文提出三维体素信念图，估计目标在各体素中的先验存在分布，并将语义推理与空间记忆结合以指导导航。实验表明该方法在零样本物体导航任务中性能更优，为具身智能体提供了更强的空间推理与长期记忆能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有零样本物体导航方法缺乏全局空间理解，无法有效估计目标位置分布。
method: 构建三维体素信念图表示目标先验分布，并融合语言与视觉语义进行导航决策。
result: 在零样本物体导航中优于已有方法，改善了空间推理与长期记忆能力。
conclusion: 验证了信念图表示对复杂物体导航任务的有效性，可迁移至其他具身任务。
---

## Abstract
Zero-shot object navigation (ZSON) allows robots to find target objects in unfamiliar environments using natural language instructions, without relying on pre-built maps or task-specific training. Recent general-purpose models, such as large language models (LLMs) and vision-language models (VLMs), equip agents with semantic reasoning abilities to estimate target object locations in a zero-shot manner. However, these models often greedily select the next goal without maintaining a global understanding of the environment and are fundamentally limited in the spatial reasoning necessary for effective navigation. To overcome these limitations, we propose a novel 3D voxel-based belief map that estimates the target’s prior presence distribution within a voxelized 3D space. This approach enables agents to integrate semantic priors from LLMs and visual embeddings with hierarchical spatial structure, alongside real-time observations, to build a comprehensive 3D global posterior belief of the target’s location. Building on this 3D voxel map, we introduce BeliefMapNav, an efficient navigation system with two key advantages: i) grounding LLM semantic reasoning within the 3D hierarchical semantics voxel space for precise target position estimation, and ii) integrating sequential path planning to enable efficient global navigation decisions. Experiments on HM3D and HSSD benchmarks show that BeliefMapNav achieves state-of-the-art (SOTA) Success Rate (SR) and Success weighted by Path Length (SPL), with a notable 9.7 SPL improvement over the previous best SR method, validating its effectiveness and efficiency.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：零样本物体导航（Zero-Shot Object Navigation, ZSON）要求机器人在完全陌生的环境中，仅依靠自然语言指令（如“找到厨房里的杯子”）定位并导航至目标物体，且不能依赖预先构建的地图或针对特定任务的训练。
- **核心问题**：现有借助大语言模型（LLM）和视觉语言模型（VLM）的方法虽然具备语义推理能力，能够“猜测”目标可能出现的位置，但普遍存在两个关键缺陷：
  - 缺乏对环境的全局理解，倾向于**贪心式**地选择下一个导航点，容易陷入局部最优；
  - 空间推理能力不足，难以将语义先验与三维空间结构有效结合，导致导航效率低下。
- **整体含义**：本文旨在解决“如何让具身智能体在未知环境中高效、准确地定位并导航到语言描述的目标物体”这一基础问题，通过引入三维体素信念图，将语义推理、空间记忆与实时观测统一起来，从而提升零样本物体导航的性能与效率。

## 2. 论文提出的方法论

- **核心思想**：构建一个**三维体素信念图（3D Voxel-Based Belief Map）**，在三维体素化空间中估计目标物体在各体素内的“先验存在概率分布”。该信念图融合了来自 LLM 的语义先验、来自 VLM 的视觉嵌入，以及环境的层级空间结构，并结合机器人实时观测，最终形成对目标位置的全居**后验信念**。
- **关键技术细节**：
  - **语义先验注入**：将 LLM 的语义推理结果“落地”到三维体素空间中，使每个体素携带与目标相关的语义概率。
  - **视觉嵌入融合**：利用视觉编码器将当前观测图像转换为视觉特征，与体素中的语义信息进行匹配和更新。
  - **层级空间结构**：在三维体素图中引入分层语义（如“房间—家具—物体”层级），增强空间推理能力。
  - **全局后验更新**：实时观测不断更新体素信念值，形成一个动态更新的全局目标位置概率分布。
- **导航策略**：
  - 在三维层级语义体素空间中，将 LLM 的语义推理结果“接地”（grounding），精确估计目标位置。
  - 引入**序列路径规划（sequential path planning）**，避免贪心决策，基于全局信念图进行高效导航决策。
- **算法流程**（文字概述）：
  1. 初始化三维体素地图，并利用 LLM/VLM 先验为各体素赋予目标存在的初始信念。
  2. 机器人移动过程中，实时采集 RGB-D 观测，提取视觉嵌入并更新对应体素的信念。
  3. 根据当前信念图，进行分层路径规划：先选取高信念区域，再规划到达该区域的路径。
  4. 重复观测—更新—规划过程，直至目标被找到或搜索空间被充分探索。

## 3. 实验设计

- **数据集 / 场景**：
  - **HM3D**（Habitat-Matterport 3D）：真实场景扫描的高质量三维重建数据集。
  - **HSSD**（Habitat Synthetic Scene Dataset）：合成场景数据集，包含多样化的室内布局。
- **Benchmark**：零样本物体导航（ZSON）标准评测协议，在 Habitat 仿真环境中进行，评估智能体能否根据语言指令在未见过的场景中找到目标物体。
- **对比方法**：与现有零样本物体导航方法进行对比，包括基于 LLM/VLM 的通用大模型方法（如使用语义猜测的典型方法）以及其他基于地图或学习的基线方法。论文报告了多种方法的成功率（SR）和路径加权成功率（SPL）。

## 4. 资源与算力

- 论文提供的文本中**未明确说明**具体的实验算力资源，如 GPU 型号、数量、训练时长等。
- 仅能推断实验基于 Habitat 仿真平台完成，训练和推理开销可能集中在视觉编码器与大模型的推理环节，但具体细节缺失。

## 5. 实验数量与充分性

- **实验组数**：至少包含两个标准数据集（HM3D 和 HSSD）上的对比实验，以及消融分析（由摘要中“两个关键优势”的验证推测存在针对信念图和后端规划策略的消融，但原文未完整列出具体消融数量）。
- **充分性评价**：
  - **积极面**：在两个不同来源（真实扫描与合成）的数据集上均验证了 SOTA 性能，并使用 SR 与 SPL 两个互补指标，能较好体现有效性与效率。
  - **不足**：论文提取内容有限，未能看到详细的消融实验设计、统计显著性检验、不同场景类别（如厨房、卧室）的分项结果，以及失败案例分析。因此实验的覆盖程度和公平性需要查看完整论文才能全面评估。

## 6. 论文的主要结论与发现

- BeliefMapNav 在 HM3D 和 HSSD 数据集上均取得 **SOTA 成功率（SR）** 和 **路径加权成功率（SPL）**。
- 相比此前“最佳 SR 方法”，BeliefMapNav 在 SPL 上提升了 **9.7 个点**，说明不仅找得到目标，而且路径更短、导航效率更高。
- 验证了三维体素信念图能够有效融合 LLM 语义先验与实时观测，显著增强智能体的空间推理和长期记忆能力，从而克服贪心局部决策问题。

## 7. 优点

- **创新性**：首次将“信念图”概念扩展到三维体素空间，并用于零样本物体导航，突破了以往仅用语言模型做“点选式”目标预测的局限。
- **端到端可解释**：信念图提供了可解释的空间概率分布，便于理解智能体“为什么去那里”。
- **鲁棒的语义接地**：将 LLM 的抽象语义先验具体化到体素坐标，避免了“模型会答但不会走”的脱节问题。
- **效率提升显著**：通过全局路径规划替代贪心策略，SPL 大幅提升，证明方法不仅效果更好，而且动作更经济。
- **通用潜力**：三维体素信念图作为一种空间记忆表示，可迁移到其他具身任务（如目标搜索、房间清洁等）。

## 8. 不足与局限

- **资源细节缺失**：未报告算力配置与运行时间，复现成本不明。
- **实验细节不完整**：提供的信息不足以评估所有消融的严格性；未见不同环境复杂度、目标类别难易度、感知噪声下的鲁棒性分析。
- **偏差风险**：
  - 语义先验可能引入语言模型自身的知识偏差（如对某些物体“常见位置”的刻板印象），在异常布局环境中可能误导导航。
  - 基准场景均为室内家居环境，对室外或动态场景的泛化能力未知。
- **应用限制**：
  - 方法依赖三维体素地图的实时构建与更新，在计算资源受限的机器人平台上可能成为瓶颈。
  - 视觉嵌入与语义先验的融合方式对传感器质量敏感，实际部署时可能面临域适应挑战。
- **样本规模**：未提及测试场景数量与目标实例数量，难以判断统计可靠性。

（完）
