---
title: "EfficientNav: Towards On-Device Object-Goal Navigation with Navigation Map Caching and Retrieval"
title_zh: EfficientNav：面向设备端物体目标导航的导航图缓存与检索
authors: "Zebin Yang, Sunjian Zheng, Tong Xie, Tianshi Xu, Bo Yu, Fan Wang, Jie Tang, Shaoshan Liu, Meng Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qMm7tC1zvj"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 基于导航图缓存与检索的设备端物体目标导航
tldr: 现有物体目标导航依赖云端大语言模型理解导航地图，难以部署到本地设备。EfficientNav提出导航图缓存与检索机制，压缩地图提示并降低规划延迟，使小规模LLM也能高效完成零样本物体导航。实验表明该方法在保持较高成功率的同时显著降低计算开销，促进了物体目标导航在设备端的实际应用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有物体目标导航依赖云端大模型，小模型理解和规划能力不足且提示延迟高，难以设备端部署。
method: 提出导航图缓存与检索机制，将地图描述压缩缓存并快速检索，配合小语言模型实现轻量高效的物体目标导航。
result: 实验表明EfficientNav在设备端保持较高成功率的同时显著降低规划延迟。
conclusion: EfficientNav为物体目标导航的端侧部署提供了高效可行的方案。
---

## Abstract
Object-goal navigation (ObjNav) tasks an agent with navigating to the location of a specific object in an unseen environment. 
Embodied agents equipped with large language models (LLMs) and online constructed navigation maps can perform ObjNav in a zero-shot manner. However, existing agents heavily rely on giant LLMs on the cloud, e.g., GPT-4, while directly switching to small LLMs, e.g., LLaMA3.2-11b, suffer from significant success rate drops due to limited model capacity for understanding complex navigation maps, which prevents deploying ObjNav on local devices.
At the same time, the long prompt introduced by the navigation map description will cause high planning latency on local devices.
In this paper, we propose EfficientNav to enable on-device efficient LLM-based zero-shot ObjNav. To help the smaller LLMs better understand the environment, we propose semantics-aware memory retrieval to prune redundant information in navigation maps.
To reduce planning latency, we propose discrete memory caching and attention-based memory clustering to efficiently save and re-use the KV cache.
Extensive experimental results demonstrate that EfficientNav
achieves 11.1\% improvement in success rate on HM3D benchmark over GPT-4-based baselines, 
and demonstrates 6.7$\times$ real-time latency reduction and 4.7$\times$ end-to-end latency reduction over GPT-4 planner. Our code is available on https://github.com/PKU-SEC-Lab/EfficientNav.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：物体目标导航（Object-goal Navigation, ObjNav）要求智能体在未知环境中导航到特定物体的位置。现有基于大语言模型（LLM）的方法通过在线构建导航地图，实现了零样本（zero-shot）导航，但严重依赖云端巨型模型（如 GPT-4），难以部署到本地设备端。
- **设备端困境**：如果直接换用小型模型（如 LLaMA3.2-11b），由于模型容量有限，难以理解复杂的导航地图描述，会导致成功率显著下降；同时，长导航地图提示词也会带来较高的规划延迟。
- **整体含义**：本文旨在解决“零样本物体目标导航如何高效部署在本地设备上”这一关键问题，兼顾导航成功率与计算资源开销，推动具身智能体在资源受限场景中的实际应用。

## 2. 论文提出的方法论

- **核心思想**：通过“导航图缓存与检索”机制，让小型 LLM 也能高效执行零样本 ObjNav，同时降低规划延迟。
- **关键技术细节**：
  - **语义感知的记忆检索（Semantics-Aware Memory Retrieval）**：在导航地图中剪除冗余信息，仅保留与目标物体相关的语义关键区域，从而减轻小型模型的理解负担。
  - **离散记忆缓存（Discrete Memory Caching）**：将导航地图描述对应的 KV 缓存（Key-Value cache）进行压缩和保存，避免每次规划时重复处理长提示。
  - **基于注意力的记忆聚类（Attention-Based Memory Clustering）**：对缓存的历史记忆进行聚类管理，在需要时快速检索和复用相关的缓存片段，降低延迟并提升检索效率。
- **流程概述**：智能体在线构建导航地图 → 通过语义感知检索过滤冗余信息 → 将关键信息对应的 KV 缓存离散化保存 → 利用注意力聚类组织缓存 → 在规划时仅需加载和检索相关缓存，配合小型 LLM 快速生成导航决策，而无需重新编码完整的导航地图提示词。

## 3. 实验设计

- **数据集 / 基准**：使用了 HM3D（Habitat-Matterport 3D）基准，这是物体目标导航常用的室内场景数据集。
- **对比方法**：以 GPT-4 规划器为基线，对比了直接使用小型 LLM（如 LLaMA3.2-11b）的方案。
- **主要指标**：任务成功率（Success Rate）和规划延迟（包括实时延迟和端到端延迟）。
- **实验结果**：
  - 在 HM3D 上相比 GPT-4 基线，成功率提升了 **11.1%**。
  - 相比 GPT-4 规划器，实时延迟降低了 **6.7 倍**，端到端延迟降低了 **4.7 倍**。

## 4. 资源与算力

- 摘要和元数据中**没有明确说明**实验所使用的 GPU 型号、数量、训练时长或推理设备等具体算力信息。
- 仅能推断出目标场景是“设备端（on-device）”部署，且规划延迟显著低于 GPT-4 云端方案，意味着其计算开销远小于云端大模型，但具体的硬件规格尚未披露。

## 5. 实验数量与充分性

- 摘要中仅报告了在 **HM3D 单一基准**上的结果，未提及更多数据集或跨场景验证。
- 方法的两个核心组件（语义检索、KV 缓存与聚类）理论上应有消融实验，但摘要未明确说明是否进行了消融分析。
- 因此，从现有信息看，实验设计在“展示端测效率优势”方面是有效的，但**覆盖范围有限**：缺少多场景泛化测试、不同小模型家族的验证、以及更详细的消融和对参数敏感性的分析，客观性和公平性尚无法完全评估。

## 6. 论文的主要结论与发现

- 通过导航图缓存与检索机制，小型 LLM 可以替代云端巨型模型完成零样本物体目标导航，且**成功率不降反升**。
- 在保持甚至提升成功率的同时，规划延迟得到数量级级别（6.7×/4.7×）的降低，证明了该方法在设备端部署的可行性和高效性。
- EfficientNav 为资源受限的具身智能体提供了一种轻量化、低延迟的解决方案，推动了 ObjNav 从云端向本地设备的迁移。

## 7. 优点

- **问题导向强**：精准抓住设备端部署中“小模型理解力差”和“长提示延迟高”两个痛点，提出针对性解决方案。
- **方法创新**：将 KV 缓存技术引入导航地图处理，通过缓存与聚类避免重复编码长提示，是较新颖的轻量化思路。
- **效果显著**：相比 GPT-4 基线的成功率提升和延迟降低幅度较大，且代码开源，便于复现和应用。
- **实用性高**：面向真实设备端场景，具有较强的工程落地价值。

## 8. 不足与局限

- **信息完整性不足**：当前提供的文本只有摘要，缺乏算法细节、硬件信息、完整实验表格和可视化结果，无法进行深入评估。
- **实验覆盖单一**：仅基于 HM3D 进行验证，未涉及其他主流导航基准（如 MP3D、Gibson、多目标/动态场景等），泛化能力有待验证。
- **对比范围有限**：仅与 GPT-4 基线和若干小模型比较，未与更多前沿零样本导航方法（如其他轻量化方案、视觉-语言模型方法）进行系统对比。
- **潜在偏差风险**：成功率提升是否对所有物体类别和场景一致未知；KV 缓存与聚类的引入可能带来额外的内存占用和缓存维护开销，在长期导航任务中的累积效果需要进一步研究。
- **应用限制**：方法依赖导航地图的构建质量，若地图本身噪声大或目标物体语义复杂，检索与缓存的有效性可能下降；设备端小型模型的能力上限也可能限制其在极端场景下的规划能力。

（完）
