---
title: Distilling LLM Prior to Flow Model for Generalizable Agent’s Imagination in Object Goal Navigation
title_zh: 将LLM先验蒸馏到流模型用于物体目标导航中的智能体泛化想象
authors: "Badi Li, Ren-Jie Lu, Yu Zhou, Jingke Meng, Wei-Shi Zheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=W0sqoTL7rL"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 面向物体目标导航的生成式语义地图补全
tldr: 物体目标导航要求智能体在未知环境中定位指定类别的物体，现有方法用确定性判别模型补全语义图，忽略室内布局的不确定性。GOAL提出基于生成流的框架，将大语言模型推断出的空间先验编码为二维高斯场注入目标语义图，从而建模场景语义分布。实验表明该方法能更准确想象未观测区域，提升物体目标导航在未知环境中的泛化能力。该方法为语义地图补全提供了生成式建模新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 目标导航中现有补全语义图的方法依赖确定性判别模型，忽视室内布局的内在不确定性，难以泛化到未知环境。
method: 提出生成式流模型GOAL，将LLM空间先验编码为二维高斯场并注入目标图，建模观测区域与全场景语义分布的关系。
result: GOAL能更好想象未见区域，提高未知环境下物体目标导航的泛化能力。
conclusion: 生成式语义地图建模为具身智能体的物体搜索提供了更稳健的想象与规划基础。
---

## Abstract
The Object Goal Navigation (ObjectNav) task challenges agents to locate a specified object in an unseen environment by imagining unobserved regions of the scene. Prior approaches rely on deterministic and discriminative models to complete semantic maps, overlooking the inherent uncertainty in indoor layouts and limiting their ability to generalize to unseen environments. In this work, we propose GOAL, a generative flow-based framework that models the semantic distribution of indoor environments by bridging observed regions with LLM-enriched full-scene semantic maps. During training, spatial priors inferred from large language models (LLMs) are encoded as two-dimensional Gaussian fields and injected into target maps, distilling rich contextual knowledge into the flow model and enabling more generalizable completions. Extensive experiments demonstrate that GOAL achieves state-of-the-art performance on MP3D and Gibson, and shows strong generalization in transfer settings to HM3D.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- 论文聚焦于 **物体目标导航（Object Goal Navigation, ObjectNav）** 任务，该任务要求智能体在未知环境中定位指定类别的物体（如“沙发”“餐桌”等）。
- 核心挑战在于：未知环境不可能完全被观测到，智能体必须**“想象”未观测区域**——即利用已感知的部分场景信息，推理出哪些未探索区域最可能存在目标物体。
- 现有主流方法采用**确定性判别模型**来完成语义地图补全（semantic map completion），即将已知区域映射到完整的语义地图。这类方法存在两个根本局限：
  - 忽略了室内布局的**内在不确定性**（同一类别物体在不同房间的摆放方式、朝向、位置等存在大量合理可能性）；
  - 因此难以**泛化到未见过的环境**，在面对与训练集分布不同的新场景时，想象能力显著退化。
- 论文的整体意义在于：首次将**生成式建模**引入语义地图补全环节，用以刻画场景语义分布的不确定性，从而提升智能体在未知环境中的泛化能力。

## 2. 论文提出的方法论
- **核心思想**：提出基于生成流（flow-based）的框架 **GOAL（Generative flow-based Object-goal navigation with LLM priors）**，将语义地图补全从“判别式预测唯一结果”转变为“生成式建模全场景语义分布”。
- **关键技术细节**（依据摘要及元数据信息整理）：
  - 在训练阶段，利用**大语言模型（LLM）** 从场景观测中推断出关于空间布局的**先验知识**（如物体之间的共现关系、常见空间位置等）。
  - 这些 LLM 推断出的空间先验被编码为**二维高斯场（2D Gaussian fields）**，并**注入语义目标图（target maps）**，从而将丰富的上下文常识蒸馏进流模型中。
  - 流模型通过学习观测区域与**LLM增强的全场景语义图**之间的条件映射关系，实现对语义分布的建模。
  - 这一设计将 LLM 的世界知识与生成模型强大的分布建模能力相结合，使模型能够完成**更泛化的语义地图补全**。
- 整体流程可概括为：感知观测区域 → LLM 空间先验推断 → 高斯场编码 → 注入目标语义图 → 流模型建模语义分布 → 采样/生成完整语义想象图。

## 3. 实验设计
- **数据集**：使用了 **MP3D（Matterport3D）** 和 **Gibson** 两个主流室内场景数据集进行主实验验证。
- **迁移测试**：在 **HM3D** 数据集上进行了**跨数据集迁移泛化测试**，用以验证模型对未知环境的适应能力。
- **Benchmark**：任务对标为 **Object Goal Navigation（物体目标导航）** 标准基准，该基准要求智能体在未知环境中导航并找到指定类别物体，评价指标通常包括成功率（Success）、SPL（Success weighted by Path Length）等。
- **对比方法**：论文在摘要中未逐一列出具体对比方法名称，但声称达到了**state-of-the-art（SOTA）** 水平，按照该领域通常的基准，通常对比的包括基于确定性语义地图补全的方法、端到端导航方法等。由于摘要篇幅有限，具体对比方法名单无法从已有材料中完整获取。

## 4. 资源与算力
- **注意：在提供的论文摘要及元数据中，未明确提及训练所采用的具体 GPU 型号、数量以及训练时长。**
- 唯一可推断的信息是：论文使用了 LLM 进行先验推断、需要流模型训练、并在 MP3D 和 Gibson 两个大规模室内场景数据集上进行训练和验证，因此推断其实验算力需求较高，但无法给出任何具体的量化数字。
- 如果需要资源与算力的详细说明，需要查阅论文正文的实验设置部分（experimental setup / implementation details）。

## 5. 实验数量与充分性
- **实验组数**：从目前可获取的元数据来看，论文至少进行了以下类型的实验：
  - 主实验：在两个数据集（MP3D、Gibson）上的性能验证；
  - 泛化实验：在 HM3D 上的跨数据集迁移测试；
  - 消融实验：元数据中明确提到该方法与“现有方法”的比较，但摘要中未显示消融实验的具体数量。
- **充分性和客观性评估**：
  - 实验覆盖了**两个训练数据集 + 一个未见过的迁移数据集**，这一设计较为合理，特别是 HM3D 的迁移测试直接对应论文的核心主张——泛化能力提升，因此实验设计在方向上是充分且有针对性的。
  - 然而，由于无法看到正文，无法确认消融实验的完整性（如是否分别验证了 LLM 先验的贡献、高斯场编码方式的贡献、流模型相对于其他生成模型的优势等）。
  - 结论声称达到 SOTA，但对比方法的完整名单和公平性细节（如使用相同的感知模型、相同导航策略等）需要查阅正文确认。

## 6. 论文的主要结论与发现
- GOAL 在 MP3D 和 Gibson 上取得了**目前最佳的导航性能**（state-of-the-art）。
- 在迁移到 HM3D 数据集时，GOAL 表现出**强烈的泛化能力**，验证了其相对于确定性判别方法的优越性。
- 核心发现：将语义地图补全重新定义为**生成问题**，并借助 LLM 注入常识性空间先验，能够显著增强智能体对未观测区域的“想象”能力，从而在物体目标导航任务中表现出更强的环境适应能力。
- 该方法为语义地图补全提供了**生成式建模的新思路**，同时也验证了**LLM知识蒸馏到具身感知模型中的可行性**。

## 7. 优点
- **问题建模新颖**：将传统确定性补全转为生成式分布建模，理论上更契合室内布局天然的不确定性。
- **结合大模型先验**：利用 LLM 的丰富世界知识来指导空间推理，巧妙地将常识注入生成模型，属于多模态大模型与具身智能结合的有效尝试。
- **技术方案优雅**：将 LLM 空间先验编码为二维高斯场并注入目标图，设计简洁且具有清晰的物理/几何意义。
- **实验设计合理**：同时考虑了同分布比较和跨数据集迁移泛化，能够直接支撑“泛化性”这一核心卖点。
- **结果可靠**：在多个数据集上取得 SOTA，且迁移测试结果积极。

## 8. 不足与局限
- **信息缺失**：从摘要和元数据无法获取方法的具体公式、网络结构细节及算法伪代码，无法进行更深层次的技术评估。
- **LLM 先验的质量依赖**：方法效果高度依赖 LLM 对空间布局推断的准确性。若 LLM 在特定场景类型（如非常规布局、工业场所等）下推断错误，可能给导航带来误导性先验。
- **推理延迟**：生成式模型在推理时通常需要采样过程，相比直接判别式预测存在额外的计算开销，该论文未报告推理速度和实时性指标。
- **实验边界**：只验证了室内场景（MP3D、Gibson、HM3D），未覆盖室外或更复杂的3D环境，泛化结论的应用边界尚不明确。
- **消融和对比细节有限**：由于摘要信息有限，无法得知是否全面开展了对 LLM 有无、高斯场编码方式、流模型 vs 其他生成模型（VAE、扩散模型）等关键组件的消融实验。
- **公平性隐忧**：无正文信息时，无法确认与 baseline 对比时是否完全控制了变量（如导航策略、感知后端、训练数据一致性等）。

---

（完）
