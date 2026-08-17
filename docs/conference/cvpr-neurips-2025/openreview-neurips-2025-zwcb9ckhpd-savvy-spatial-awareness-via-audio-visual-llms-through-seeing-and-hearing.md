---
title: "SAVVY: Spatial Awareness via Audio-Visual LLMs through Seeing and Hearing"
title_zh: SAVVY：通过视听大模型的看与听实现空间感知
authors: "Mingfei Chen, Zijun Cui, Xiulong Liu, Jinlin Xiang, Caleb Zheng, Jingyuan Li, Eli Shlizerman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=zwCb9cKHpd"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向音视频大模型的动态三维空间推理基准
tldr: 现有音视频大模型多聚焦静态或二维场景，缺乏动态三维空间推理能力评测。本文提出SAVVY-Bench，包含数千个关于静态与移动物体方向距离关系的问答对，并设计两阶段免训练推理流水线SAVVY，实现动态视听环境中的三维定位与时序对齐。基准与流水线为具身智能的空间感知提供了新的评测维度。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 动态三维空间推理是具身智能的关键，但现有视听模型与基准主要停留在静态二维场景。
method: 构建动态三维音视频问答基准，并设计两阶段免训练推理模型SAVVY处理任务。
result: SAVVY-Bench涵盖细粒度时空与多模态标注，评测了模型在动态场景中的三维空间推理能力。
conclusion: 为视听大模型在具身环境中的空间推理研究提供了基准与推理基线。
---

## Abstract
3D spatial reasoning in dynamic, audio-visual environments is a cornerstone of human cognition yet remains largely unexplored by existing Audio-Visual Large Language Models (AV-LLMs) and benchmarks, which predominantly focus on static or 2D scenes. We introduce SAVVY-Bench, the first benchmark for 3D spatial reasoning in dynamic scenes with synchronized spatial audio. SAVVY-Bench is comprised of thousands of carefully curated question–answer pairs probing both directional and distance relationships involving static and moving objects, and requires fine-grained temporal grounding, consistent 3D localization, and multi-modal annotation. To tackle this challenge, we propose SAVVY, a novel training-free reasoning pipeline that consists of two stages: (i) Egocentric Spatial Tracks Estimation, which leverages AV-LLMs as well as other audio-visual methods to track the trajectories of key objects related to the query using both visual and spatial audio cues, and (ii) Dynamic Global Map Construction, which aggregates multi-modal queried object trajectories and converts them into a unified global dynamic map. Using the constructed map, a final QA answer is obtained through a coordinate transformation that aligns the global map with the queried viewpoint. Empirical evaluation demonstrates that SAVVY substantially enhances performance of state-of-the-art AV-LLMs, setting a new standard and stage for approaching dynamic 3D spatial reasoning in AV-LLMs.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：在动态、视听同步的三维环境中进行空间推理，是人类认知的基础能力，但现有音频-视觉大语言模型（AV-LLMs）及其评测基准主要局限于静态或二维场景，尚未有效探索动态三维空间推理。
- **研究动机**：具身智能（如机器人导航、空间感知）需要模型在移动视角、多物体运动、空间音频并存的复杂环境中，理解物体的方向与距离关系，并实现时间对齐与三维定位。现有模型缺乏此类能力的系统评测与专用推理方法。
- **整体含义**：本文旨在填补这一空白，为AV-LLMs在动态三维视听环境中的空间推理提供首个基准与免训练推理基线，推动该方向的研究进展。

### 2. 方法论（核心思想、关键技术细节、算法流程）
论文提出 **SAVVY** —— 一种**免训练**（training-free）的两阶段推理流水线：
- **阶段一：自我中心空间轨迹估计（Egocentric Spatial Tracks Estimation）**
  - 利用 AV-LLMs 及其他音视频方法，结合视觉与空间音频线索，跟踪与查询问题相关的关键物体在自我中心视角下的运动轨迹。
  - 强调多模态线索（视觉+空间音频）的融合，以应对动态场景中的物体移动和视角变化。
- **阶段二：动态全局地图构建（Dynamic Global Map Construction）**
  - 将阶段一获得的多模态物体轨迹进行聚合，转换为统一的**全局动态地图**。
  - 该地图能够表达场景中多个物体随时间变化的空间关系。
- **最终问答**：
  - 在已构建的全局动态地图基础上，通过**坐标变换**（coordinate transformation），将全局地图对齐到查询视角（queried viewpoint），从而得出最终答案。
- **技术特点**：无需额外训练，即可增强现有AV-LLMs的动态三维空间推理能力；整个流程强调时间对齐与三维定位的一致性。

### 3. 实验设计
- **基准（Benchmark）**：提出 **SAVVY-Bench**，这是首个面向动态场景中三维空间推理的基准，包含同步空间音频。
- **数据内容**：
  - 包含**数千个精心策划的问答对**，涉及静态与移动物体的**方向**和**距离**关系。
  - 需要细粒度的时间定位、一致的三维定位以及多模态标注。
- **对比方法**：在实证评估中，将 SAVVY 应用于当前最先进的 AV-LLMs（state-of-the-art AV-LLMs）进行性能对比，验证其增强效果。具体模型名称、基线数量等信息在摘要中未详细列出。

### 4. 资源与算力
- 摘要和现有元数据中**未明确说明**所使用的GPU型号、数量、训练时长或推理计算量。
- 由于SAVVY是**免训练**流水线，可能仅需推理阶段的计算资源，但具体算力需求未披露。
- 建议读者查阅论文正文或附录获取详细资源信息。

### 5. 实验数量与充分性
- 摘要表明进行了“实证评估”（Empirical evaluation），并宣称SAVVY显著提升了当前最先进AV-LLMs的性能。
- 但**未提供具体实验数量**（如数据集子集数、消融实验数、模型数量等）。
- 基准包含数千个问答对，覆盖方向/距离、静态/动态物体，维度较为丰富。
- **充分性评估**：从现有信息看，实验设计具有明确目标（验证SAVVY对AV-LLMs的提升），但缺乏消融研究、跨模型对比细节、误差分析等证据，难以完全判断公平性与全面性。需依赖论文全文。

### 6. 主要结论与发现
- SAVVY-Bench 可作为动态三维视听空间推理的标准评测基准。
- SAVVY 免训练流水线（轨迹估计+全局地图构建+坐标变换）能显著增强现有AV-LLMs在动态三维空间推理任务上的表现。
- 论文为AV-LLMs在具身环境中的空间推理研究设立了“新标准和新舞台”。

### 7. 优点
- **问题新颖**：首次系统研究动态三维空间推理，突破静态/二维限制。
- **基准设计完整**：包含方向、距离、静态/移动物体、时间定位、三维一致性、多模态标注等细粒度维度。
- **方法创新性**：免训练两阶段流水线，不依赖额外训练数据或模型微调，易于推广到现有AV-LLMs。
- **多模态融合**：充分结合视觉和空间音频线索，符合人类多感官空间认知机制。
- **实用价值**：直接面向具身智能应用（如导航、交互），评测与推理基线具备现实意义。

### 8. 不足与局限（基于现有信息）
- **实验细节缺失**：摘要未提供具体数据划分、基线的超参数设置、评估指标（如准确率、F1等），以及对比模型的完整列表。
- **消融分析不足**：未展示各阶段（轨迹估计、地图构建、坐标变换）的单独贡献，缺乏可解释性验证。
- **泛化性存疑**：基准场景仅提及“动态，同步空间音频”，未说明是否覆盖室内/室外、不同声学环境、不同物体类别等，可能限制结论的通用性。
- **算力透明度低**：未报告任何资源/能耗信息，难以评估方法在实际部署中的成本。
- **主观性风险**：问答对“精心策划”但未说明是否经过人类验证或一致性检验，可能存在标注偏差。
- **应用限制**：免训练方法虽灵活，但可能受限于底层AV-LLMs本身的空间推理上限；对极端动态场景（快速运动、遮挡、噪音）的鲁棒性未知。

（完）
