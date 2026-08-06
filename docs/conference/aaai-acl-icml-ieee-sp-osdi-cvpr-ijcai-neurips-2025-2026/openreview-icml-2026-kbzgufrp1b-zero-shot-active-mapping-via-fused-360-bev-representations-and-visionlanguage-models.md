---
title: Zero-shot Active Mapping via Fused 360-BEV Representations and Vision–Language Models
title_zh: 基于融合360度BEV表征与视觉-语言模型的零样本主动建图
authors: "Yuanze Wang, Dianxi Shi, Yuetian Wang, Shiming Song, Haikuo Peng, Chunping Qiu, Mengzhu Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/660b962b7ae442fb719f019905c65f1e4bbc6a74.pdf"
tags: ["query:semantic-map"]
score: 8.0
evidence: 主动建图、360度BEV、视觉-语言模型、面向具身的语义地图
tldr: 针对现有主动建图方法难以零样本泛化到大规模场景且缺乏语言指令支持的问题，该文提出基于视觉-语言模型的主动建图方法。方法引入360-BEV表征融合全方位语义与几何结构，并设计候选路点生成策略，使智能体能在图像空间选择信息丰富的路点并反投影为可执行的三维动作。该方法实现了零样本语义地图构建并支持语言驱动的人机交互，为具身导航提供了可扩展的建图方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 主动建图需要智能体理解未知环境，但现有方法大场景泛化弱且不支持语言指令。
method: 提出360-BEV表征融合语义与几何，用视觉-语言模型生成候选路点并反投影为三维动作完成建图。
result: 在未见环境中实现零样本主动建图，并支持语言驱动的人机交互。
conclusion: 视觉-语言模型与BEV表征相结合能显著增强智能体的主动建图与交互能力。
---

## Abstract
Active mapping enables embodied agents to understand and interact in previously unseen environments. However, most methods struggle to achieve zero-shot generalization to large-scale scenes and lack support for language instructions. We propose a VLM-based active mapping method that achieves zero-shot mapping while facilitating language-driven human–agent interaction. First, we introduce a 360-BEV representation that integrates omnidirectional semantics with BEV-aligned geometric structure to enhance scene understanding. Second, we develop a candidate waypoint generation strategy that allows the VLM-driven agent to select informative 2D waypoints in image space and back-project them into executable metric actions in 3D space, enabling the VLM to plan in its strongest modality. Third, we design a VLM-based depth-first exploration agent that decomposes the scenes into explorable regions, selects informative waypoints within each region, and organizes them into a topological tree. The agent follows the depth-first exploration policy to achieve thorough coverage of large-scale scenes. Without task-specific training, our method outperforms the strongest baseline, improving coverage and AUC by approximately 13.25\% and 14.00\%, respectively, while enabling language-conditioned interaction.

---

## 论文详细总结（自动生成）

# 中文总结：基于融合360度BEV表征与视觉-语言模型的零样本主动建图

## 1. 核心问题与研究动机
- **背景**：主动建图（Active Mapping）旨在让具身智能体在未知环境中通过自主探索构建语义地图，从而支撑后续的导航与交互任务。
- **核心问题**：
  - 现有方法在**大规模未知场景**中的零样本泛化能力较弱；
  - 缺乏对**自然语言指令**的支持，难以实现人机交互；
  - 智能体往往依赖任务特定训练，在新环境中部署成本高。
- **研究目标**：提出一种基于视觉-语言模型（VLM）的主动建图方法，实现**零样本主动建图**，并同时支持**语言驱动的人机交互**。

## 2. 方法论
论文提出的方法主要由三个关键技术组成：

- **360-BEV 表征融合**
  - 将**全方位语义信息**与**与BEV对齐的几何结构**相融合；
  - 提升智能体对大规模未知环境的整体场景理解能力；
  - 统一了语义与几何两种模态，为后续路径规划提供基础。

- **候选路点生成策略**
  - 智能体在**二维图像空间**中由VLM选择信息量丰富的候选路点；
  - 再将二维路点**反投影（back-project）**为三维空间中可执行的度量动作；
  - 核心优势：让VLM在其最强的**图像理解模态**中进行规划，避免直接生成三维动作的困难。

- **基于VLM的深度优先探索智能体**
  - 将场景分解为多个可探索区域；
  - 在每个区域内选择信息丰富的路点；
  - 将这些路点组织成**拓扑树**结构；
  - 智能体遵循**深度优先探索策略**，逐步遍历这些区域，从而实现对大规模场景的全面覆盖。

整体算法流程可概括为：**场景感知 → 360-BEV融合表征 → 图像空间候选路点生成 → 反投影为三维动作 → 深度优先拓扑树探索 → 完成零样本主动建图**。

## 3. 实验设计
- **测试环境**：论文声称在“未见环境”（unseen environments）中进行测试，以验证零样本泛化能力，但当前摘要中未给出具体数据集或仿真场景名称。
- **基准与指标**：
  - 对比了现有最强基线方法（strongest baseline）；
  - 主要评价指标为**覆盖率（Coverage）**和**AUC**（Area Under the Curve）。
- **定量结果**：
  - 覆盖率比最强基线提升约 **13.25%**；
  - AUC 提升约 **14.00%**。
- **额外能力验证**：论文还展示了语言条件交互的研究目标，但摘要中未提供详细的交互评测细节。

## 4. 资源与算力
- **论文摘要和元数据中均未明确说明**使用的GPU型号、数量、训练时长或推理成本等算力信息。
- 由于该方法宣称“无需任务特定训练”，其训练算力可能较低，但具体数值无法从当前文本中确认。

## 5. 实验数量与充分性
- **已公开的实验信息有限**：当前可见文本仅提供了在未见环境中的一个整体性能对比结果。
- **未提及的细节**：
  - 未列出具体数据集/仿真器；
  - 未报告消融实验；
  - 未给出多次运行的标准差或统计显著性检验；
  - 未展示语言交互任务的定量评估。
- **总体评价**：从摘要层面看，实验初步验证了方法有效性，但**充分性和客观性无法完全判断**，需要论文全文的更多实验细节（如多个场景、多组基线、消融分析）来支撑。

## 6. 主要结论与发现
- 将**视觉-语言模型**与**360-BEV融合表征**相结合，可以显著增强智能体的主动建图能力。
- 该方法在**零样本**条件下，超越现有最强基线，并在覆盖率与AUC上取得显著提升。
- 方法天然支持**语言驱动的人机交互**，为具身导航和语义建图提供了可扩展的新方案。

## 7. 主要优点
- **零样本能力**：无需任务特定训练，具备较强的泛化能力。
- **表征设计新颖**：360-BEV融合语义和几何结构，较好地解决了全方位感知与BEV对齐问题。
- **规划模态匹配**：在图像空间选择路点再反投影为三维动作，降低VLM生成三维动作的难度，设计思路合理。
- **交互友好**：支持自然语言指令，扩展了主动建图的应用范围。
- **探索策略完备**：利用深度优先策略和拓扑树组织区域，理论上能较好覆盖大规模场景。

## 8. 不足与局限
- **信息不完整**：当前可见文本缺少详细实验设置、数据集描述、基线与消融实验，难以全面评估方法的可复现性和泛化边界。
- **算力成本未说明**：未报告运行资源消耗，实际部署成本和实时性未知。
- **依赖VLM能力**：性能可能受VLM的视觉理解、幻觉问题影响，尤其在复杂或感知退化的环境中，路点选择可靠性有待验证。
- **覆盖率与AUC提升的具体来源**：缺少消融实验来区分360-BEV表征、路点生成策略和深度优先探索三部分各自的贡献。
- **语言交互评测缺失**：摘要中仅提及支持语言驱动交互，但没有给出具体交互成功率或用户评测结果。

（完）
