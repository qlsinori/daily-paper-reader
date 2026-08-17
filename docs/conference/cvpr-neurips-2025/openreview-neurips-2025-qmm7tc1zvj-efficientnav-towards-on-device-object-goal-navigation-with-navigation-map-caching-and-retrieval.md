---
title: "EfficientNav: Towards On-Device Object-Goal Navigation with Navigation Map Caching and Retrieval"
title_zh: EfficientNav：面向设备端目标导航的导航地图缓存与检索
authors: "Zebin Yang, Sunjian Zheng, Tong Xie, Tianshi Xu, Bo Yu, Fan Wang, Jie Tang, Shaoshan Liu, Meng Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qMm7tC1zvj"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 直接针对物体目标导航任务，智能体需导航至特定物体位置
tldr: 针对小模型在零样本物体目标导航中因理解复杂导航地图能力不足而性能下降、且地图描述导致规划延迟高的问题，提出EfficientNav导航地图缓存与检索方法，让设备端小语言模型高效复用地图信息，在降低延迟的同时维持较高的导航成功率，推动导航智能体在本地设备上的实际部署。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有零样本物体目标导航依赖云端大语言模型，难以部署到本地设备，且小模型处理复杂地图时成功率大幅下降。
method: 提出导航地图缓存与检索机制，压缩地图描述并复用历史导航信息，辅助小语言模型进行规划。
result: 在保持较高成功率的同时显著降低规划延迟，实现设备端高效导航。
conclusion: 验证了面向设备端的高效目标导航可行性，为边缘部署提供新方案。
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

以下是基于给定论文信息生成的详细中文总结。

---

# EfficientNav：面向设备端目标导航的导航地图缓存与检索——论文解析

## 1. 核心问题与整体含义（研究动机与背景）

- **任务背景**：物体目标导航（Object-goal Navigation, ObjNav）要求智能体在未知环境中自主导航到特定物体的位置。现有的先进方案通常将大型语言模型（LLMs，如GPT-4）与在线构建的导航地图结合，以零样本（zero-shot）方式完成此任务。
- **核心痛点一：小模型能力不足**。当前系统高度依赖云端大模型（如GPT-4）。若直接切换为设备端可部署的小模型（如LLaMA3.2-11b），由于模型容量受限，无法充分理解复杂导航地图中的冗余信息，导致导航成功率显著下降。
- **核心痛点二：规划延迟高**。导航地图描述会引入超长提示词（long prompt），在本地设备上进行推理时会造成严重的规划延迟，阻碍了ObjNav在真实设备上的实时部署。
- **论文整体目标**：解决上述两大痛点，证明仅依靠设备端小语言模型即可实现高效的零样本物体目标导航，推动LLM驱动的导航智能体从云端下沉至边缘端本地设备。

## 2. 论文提出的方法论（EfficientNav）

EfficientNav的核心思想是**通过优化"输入压缩"和"计算复用"两条路径**，让小模型在设备端高效处理导航任务。

### 2.1 核心技术：双管齐下的轻量化策略

- **语义感知记忆检索（Semantics-Aware Memory Retrieval）**：
  - 针对小模型理解能力弱的问题，该机制在导航地图送入模型之前，对地图描述信息进行**剪枝**。
  - 通过语义相关性评估，主动剔除导航地图中的冗余、无关信息，只保留与当前目标物体方位、任务路径最相关的关键环境描述，从而降低小模型的理解负担。
- **离散记忆缓存与注意力记忆聚类（Discrete Memory Caching & Attention-based Memory Clustering）**：
  - 针对推理延迟高的问题，该方法引入了KV Cache（键值缓存）的保存与复用机制。
  - **离散记忆缓存**：将历史导航步骤产生的KV Cache高效存储，避免每次规划都从头计算整个导航地图的上下文。
  - **注意力记忆聚类**：通过基于注意力分数的聚类算法，将历史缓存中相似或相关的记忆进行分组整理，使得小模型在规划时能快速检索到所需的缓存片段，而无需扫描全部历史信息。
- **算法流转（文字描述）**：导航任务开始后 → 智能体实时构建导航地图 → 由语义感知检索模块压缩地图描述 → 结合基于聚类检索的历史KV Cache → 小语言模型进行动作规划（Plan）→ 动作执行并更新缓存 → 循环往复直至到达目标。

### 2.2 整体框架特征

该方法不修改小语言模型本身的结构，而是在模型**输入侧（地图剪枝）**与**推理侧（KV缓存复用）**做工程层面的算法优化，实现了即插即用式的设备端部署方案。

## 3. 实验设计

- **数据集/场景**：使用了**HM3D（Habitat-Matterport 3D）基准数据集**，这是具身智能领域广泛使用的室内真实场景扫描数据集。
- **基准（Benchmark）**：HM3D数据集上的标准零样本ObjNav评估协议。
- **对比方法**：
  - 主要基线：基于**GPT-4**（云端大模型）的规划器，作为强基线。
  - 对照对象：小模型（如LLaMA3.2-11b）直接进行规划的基线。
- **评测指标**：
  - 导航**成功率（Success Rate, SR）**。
  - **实时推理延迟（Real-time latency）** 及 **端到端延迟（End-to-end latency）**。
- **实验结果概览**：
  - 在HM3D上，相对GPT-4基线，成功率提升了**11.1%**。
  - 相对GPT-4规划器，**实时延迟降低6.7倍**，**端到端延迟降低4.7倍**。

## 4. 资源与算力

- 在提供的论文摘要与元数据中，**未明确说明**训练/运行所消耗的GPU型号、GPU数量或具体运行时长。
- 推测性分析：由于该方法主要服务于"设备端"（如边缘设备、机器人计算单元），且核心方法是推理侧的缓存与检索优化，而非重新训练大模型，因此对硬件的依赖主要在**推理侧**（单卡或边缘设备）而非训练集群。但具体配置在本文提供的内容中缺失。

## 5. 实验数量与充分性评估

- **已提及的实验深度**：论文在主流公认的HM3D基准上进行了验证，对比了云端大模型（GPT-4）与设备端小模型（LLaMA3.2-11b）两类关键对象，数据充分体现了方法在成功率和延迟两个维度的双重收益（分别为+11.1%成功率、6.7x/4.7x提速）。
- **客观性分析**：核心结果在公开基准上进行，结果相对客观可复现。
- **潜在不足（基于已知信息）**：材料中仅笼统提到"广泛实验"，**未明确交代消融实验的具体组数**（例如：仅验证剪枝策略？仅验证缓存策略？两者叠加效果？），也**未提及是否在多个不同布局风格的场景（如多户型、光照差异、物体类别概率差异）下分别测试**。因此实验的全面性（尤其是对泛化能力的证明）在当前材料中体现不充分——可能存在选择性展示最佳结果的偏差风险。

## 6. 主要结论与发现

- **核心结论**：验证了面向设备端的高效零样本目标导航的**可行性**。
- **具体发现**：
  1. 通过消除地图冗余信息，可以有效弥补小语言模型相对云大模型在语义理解上的短板（成功率反超GPT-4达11.1%）。
  2. 通过KV缓存的聚类与复用，大幅削减了规划延迟，证明了"延迟"并非不可逾越的技术阻碍。
  3. 为边缘部署（如机器人本地计算平台）提供了新的算法方案，打破了ObjNav依赖云端算力的思维定式。

## 7. 优点（方法与实验设计亮点）

- **定位准确、直击痛点**：精准抓住了ObjNav落地边缘端的两个核心瓶颈（小模型精度差、长提示词延迟高），针对性强。
- **技术选型新颖且高效**：巧妙利用KV Cache的重用思想——这是高效推理领域的常见手段，但创新性地将其应用于具身导航的"跨步骤"规划中，并引入**注意力聚类**缓解缓存膨胀问题，体现出极高的工程智慧。
- **显著的双重收益**：不是为了单纯提速而牺牲精度，做到了"更快且更准"，结果具有较强说服力。
- **部署友好**：保持模型结构不变，仅对外围系统做改动，便于产业界快速采纳。

## 8. 不足与局限

- **实验透明度的局限**：缺乏对消融实验设计的详细描述（如是否有逐步叠加的对照实验），也未提及不同小模型（如8B/1.5B等不同规格）的泛化测试，影响了对方法鲁棒性的全面判断。
- **算力信息缺失**：未披露具体实验硬件配置，包括边缘端设备的实际性能参数（如内存带宽、CPU/GPU型号），使得读者难以评估其在更差硬件上的可移植性。
- **适用场景假设限制**：方法基于"历史轨迹记忆具有复用价值"的假设。若环境动态变化剧烈（如家具移动或动态障碍物频繁干扰），缓存的历史信息可能反而引入误导性先验，这一潜在风险在已有摘要材料中未讨论。
- **对比基准范围有限**：主要对比了GPT-4系列和单一小模型，未提及与专为导航设计的其他端到端模型（如ViNG、SemExp等）或更高效紧凑的多模态模型（Qwen-VL、Gemini Nano等）的对比，对比广度有所欠缺。
- **端到端延迟构成未细分**：6.7x的实时推理延迟与4.7x的端到端延迟倍数差异表明存在未被优化的其他环节（如地图构建、传感器感知），论文未明确分解各部分延迟占比，可能掩盖了系统其他部分的瓶颈。

---

（完）
