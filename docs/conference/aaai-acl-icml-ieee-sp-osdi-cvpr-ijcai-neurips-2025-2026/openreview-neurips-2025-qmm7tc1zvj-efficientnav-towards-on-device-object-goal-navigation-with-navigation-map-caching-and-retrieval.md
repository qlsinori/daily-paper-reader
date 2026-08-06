---
title: "EfficientNav: Towards On-Device Object-Goal Navigation with Navigation Map Caching and Retrieval"
title_zh: EfficientNav：面向设备端目标导航的地图缓存与检索
authors: "Zebin Yang, Sunjian Zheng, Tong Xie, Tianshi Xu, Bo Yu, Fan Wang, Jie Tang, Shaoshan Liu, Meng Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qMm7tC1zvj"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 面向目标物体类别导航，结合导航地图缓存与检索的端侧具身智能方法
tldr: 针对现有零样本目标导航依赖云端大模型、小型本地模型理解复杂导航地图能力不足且延迟高的问题，本文提出EfficientNav。该方法通过导航地图的缓存与检索机制，压缩地图描述并辅助小型语言模型进行目标导向推理，使目标导航可在设备端高效运行。实验表明，在保持较高成功率的同时显著降低规划延迟，为机器人和边缘设备上的目标导航部署提供了可行方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有ObjNav智能体依赖GPT-4等云端大模型，小型模型处理复杂地图时成功率下降且提示过长导致延迟高。
method: 提出EfficientNav，利用导航地图缓存与检索，为小型LLM提供精简且相关的空间信息以支持零样本目标导航。
result: 在设备端环境中实现更快的规划速度和可比的导航成功率，优于直接使用小模型的基线。
conclusion: 地图缓存与检索能有效弥合小型模型与大型模型在目标导航任务上的差距，推动端侧部署。
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

## 论文总结：EfficientNav

### 1. 核心问题与整体含义
- **研究动机**：目标导航（Object-goal Navigation, ObjNav）要求智能体在未知环境中导航至特定物体位置。现有方法依赖云端大语言模型（如 GPT-4）配合在线构建的导航地图实现零样本导航，但在本地设备上部署存在两大障碍：
  - 小型 LLM（如 LLaMA3.2-11B）理解复杂导航地图的能力有限，直接切换会导致成功率显著下降；
  - 导航地图描述导致的超长提示（prompt）在本地推理时产生高延迟。
- **整体含义**：该论文旨在解决**端侧零样本目标导航**的效率与性能矛盾，推动具身智能在机器人等边缘设备上的实际部署。

### 2. 方法论
- **核心思想**：通过“导航地图缓存与检索”机制，为小型 LLM 提供精简且相关的空间信息，使其能够在设备端高效完成目标导向推理。
- **关键技术**：
  - **语义感知的记忆检索**：用于从导航地图中去除冗余信息，提取与目标最相关的空间内容，降低小型 LLM 的理解负担；
  - **离散记忆缓存**：通过离散化方式保存历史导航信息，便于后续快速复用；
  - **基于注意力的记忆聚类**：对缓存内容进行聚类组织，并有效保存与重用 KV 缓存，从而减少重复计算，降低规划延迟。
- **算法流程**：智能体在导航过程中持续构建地图 → 利用语义检索压缩地图描述 → 结合历史缓存与聚类后的记忆生成精简提示 → 由小型 LLM 进行目标定位与动作规划。

### 3. 实验设计
- **数据集与 benchmark**：在 **HM3D 基准**上进行评估。
- **对比方法**：
  - 基于 GPT-4 的规划器（云端大模型基线）；
  - 直接使用小型 LLM（如 LLaMA3.2-11B）的基线方法。
- **主要评测指标**：成功率（Success Rate）、实时延迟（real-time latency）、端到端延迟（end-to-end latency）。

### 4. 资源与算力
- **论文提供的元数据中未明确说明**使用的 GPU 型号、数量、训练时长等信息。
- 仅能得知系统面向设备端（on-device）部署，但具体算力配置未在摘要和元数据中披露。

### 5. 实验数量与充分性
- 摘要中仅给出了在 **HM3D 单一基准**上的实验结果，以及相较 GPT-4 基线的成功率提升和延迟降低数据。
- **未提及消融实验**、多场景或多数据集对比，也未详细描述重复实验次数和统计显著性检验。
- 因此，从现有信息来看，实验**覆盖范围有限**，公平性（例如是否控制相同地图、相同硬件条件等）尚无法完全确认，但对比基线类型合理（大模型 vs 小模型），能初步验证方法有效性。

### 6. 主要结论与发现
- EfficientNav 在 HM3D 基准上相比 GPT-4 基线实现了 **11.1% 的成功率提升**；
- 相比 GPT-4 规划器，实现了 **6.7× 的实时延迟降低**和 **4.7× 的端到端延迟降低**；
- 证明地图缓存与检索机制能有效弥合小型模型与大型模型在目标导航任务上的性能差距，为端侧部署提供了可行路径。

### 7. 优点
- **面向实际部署**：针对设备端限制提出系统性方案，具有较强应用价值；
- **创新性**：将 KV 缓存复用与语义检索结合，同时解决小模型理解能力不足和延迟高两个核心问题；
- **效率提升显著**：延迟降低幅度大，且成功率没有牺牲反而有所提高；
- **开源**：提供了代码仓库，便于复现和后续研究。

### 8. 不足与局限
- **实验验证有限**：仅在 HM3D 一个 benchmark 上报告结果，缺乏更多室内环境（如 Gibson、MP3D）或真实机器人平台的泛化验证；
- **缺乏消融分析**：未说明各模块（语义检索、离散缓存、注意力聚类）对最终性能的独立贡献；
- **计算资源未透明**：未提供训练或推理所需的具体硬件配置，影响可复现性和成本评估；
- **潜在偏差风险**：测试场景、地图构建方式、提示模板等细节未披露，可能引入实验结果偏差；
- **实际部署限制**：虽然面向设备端，但小型 LLM 推理仍需一定计算资源，对于微型嵌入式设备是否可运行尚未明确。

（完）
