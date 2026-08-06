---
title: "PSG-Nav: Probabilistic Scene Graph Navigation via Multiverse Decision Making"
title_zh: PSG-Nav：基于概率场景图与多元宇宙决策的导航方法
authors: "Rufeng Chen, Yue Chang, Xiaqiang Tang, Hechang Chen, Sihong Xie"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f3d715c40a3e61968cdf75180f84a28fa5ec279d.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 开放词汇导航，概率场景图与地标决策
tldr: 论文针对开放词汇导航中的感知不确定性，提出PSG-Nav方法。它构建使用完整语义类别分布的3D概率场景图，并通过多元宇宙决策采样多个最可能的世界状态进行导航地标推理。该方法从全局组合可能性出发进行决策，避免局部最优解，在语义模糊条件下提升了导航鲁棒性，为物体目标导航提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 开放词汇导航中感知不确定性大，现有方法仅做局部确定性决策，难以得到全局最优。
method: 构建3D概率场景图表达语义类别分布，并用多元宇宙决策采样全局地标假设。
result: 实验显示PSG-Nav在语义歧义和错误模型干扰下导航成功率优于确定性方法。
conclusion: 概率场景图与全局假设推理可显著提升开放词汇导航的鲁棒性。
---

## Abstract
Open-vocabulary navigation requires embodied agents to manage significant perception uncertainty stemming from semantic ambiguity and model errors.
    However, most existing works settle for local optimal deterministic approaches, depriving complex navigation decision-making over multiple composite possibilities that are critical for globally better solutions.
    In this paper, we propose Probabilistic Scene Graph Navigation (PSG-Nav), which constructs a 3D Probabilistic Scene Graph that uses full semantic categorical distributions to account for perception uncertainty.
    To efficiently use the local distributions to compose and reason about the optimal navigation landmarks, we propose Multiverse Decision to sample multiple most likely world settings from the joint distribution, and evaluate navigation landmarks based on the compatibility between landmarks and multiverses.
    To mitigate false positives due to epistemic uncertainty in open-vocabulary navigation, we introduce the Evidential Experience Calibrator, which enables online lifelong adaptation by cross-validating detections against memories of past successes and failures.
    Extensive experiments on widely-used benchmarks MP3D, HM3D, and HSSD demonstrate that PSG-Nav establishes new state-of-the-art results, achieving Success Rates of 66.1%, 44.8%, and 67.9%, respectively. 
    Code is available at: https://psg-nav.github.io

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义

- **研究动机**：开放词汇导航（Open-vocabulary Navigation）要求智能体在语义类别开放、场景多样化的环境中完成导航任务，但这类任务面临显著的**感知不确定性**，主要来源于：
  - 语义歧义：同一物体在不同场景中可能对应多种语义标签；
  - 模型误差：视觉感知模型本身存在分类错误或置信度偏差。
- **现有方法的不足**：大多数现有方法采用**局部最优的确定性策略**，仅基于单次感知结果或局部信息进行决策，忽略了多个组合可能性对全局导航决策的影响，难以得到全局更优解。
- **整体含义**：论文提出将感知不确定性显式建模为概率分布，并在全局组合空间中进行推理，从而提升开放词汇导航在复杂、歧义环境下的鲁棒性和成功率。

---

### 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：将导航地标决策视为一种“多元宇宙”式的全局假设推理问题——同时考虑多个可能的世界状态，而不是只依赖单一确定性感知结果。
- **关键技术细节**：
  1. **3D 概率场景图（3D Probabilistic Scene Graph）**：
     - 与传统场景图仅记录“物体-关系”的确定标签不同，PSG-Nav 的每类语义信息使用**完整的类别概率分布**表示，从而显式保留感知不确定性。
     - 这种概率化的场景图能够在三维空间中融合多视角、多帧的观测，提供更鲁棒的环境表示。
  2. **多元宇宙决策（Multiverse Decision）**：
     - 从联合分布中**采样多个最可能的世界状态**（即“多元宇宙”），每个世界状态对应一种场景语义的可能配置；
     - 评估导航地标时，综合考虑这些地标与不同世界状态之间的**兼容性**，从而避免因局部最优导致的决策失误。
     - 该方法本质上是将局部概率分布组合为全局假设，并在组合空间中进行推理。
  3. **证据体验校准器（Evidential Experience Calibrator）**：
     - 针对开放词汇导航中由**认知不确定性（epistemic uncertainty）** 导致的误检（false positives）问题；
     - 通过将当前检测结果与过去成功/失败记忆进行**交叉验证**，实现在线终身适应（online lifelong adaptation），不断修正感知偏差。
- **流程概述**：环境观测 → 构建3D概率场景图 → 采样多元宇宙假设 → 基于地标-多元宇宙兼容性评分 → 选择最优地标导航 → 通过经验校准器持续更新与调整。

---

### 3. 实验设计：数据集、基准与对比方法

- **数据集与场景**：
  - **MP3D**（Matterport3D）：大规模室内场景数据集；
  - **HM3D**（Habitat-Matterport 3D）：高保真三维扫描数据集；
  - **HSSD**（High-fidelity Synthetic Scene Dataset）：高保真合成场景数据集。
- **Benchmark**：这些数据集是开放词汇导航（如 ObjectNav）广泛使用的标准基准。
- **对比方法**：论文摘要未明确列出具体对比的基线方法名称，但声称在三个基准上均取得了**新的最先进（State-of-the-Art）结果**，因此推断与现有主流开放词汇导航方法（如基于CLIP、ViT等确定性语义地图方法）进行了比较。

---

### 4. 资源与算力

- 论文提供的摘要与元数据中**未说明**使用的 GPU 型号、数量、训练时长等算力信息。
- 根据学术论文惯例，完整版可能包含硬件配置（如 NVIDIA A100 数量、训练轮数等），但当前提取的文本中未涉及，**此处明确标注为信息缺失**。

---

### 5. 实验数量与充分性

- **实验数量**：摘要报告了在三个数据集（MP3D、HM3D、HSSD）上的主实验结果，成功率分别为 66.1%、44.8% 和 67.9%。
- **是否充分**：
  - 从多数据集验证角度看，覆盖了真实扫描与合成场景，具有一定广泛性；
  - 但摘要中**未提及消融实验**（如去除概率场景图、去除多元宇宙决策、去除证据校准器的影响），也未报告与多个基线方法的详细对比表格、方差或显著性检验；
  - 因此，基于当前信息，实验的**全面性尚不清楚**，需要依赖完整论文判断其客观性和公平性。
- **客观性评估**：由于未披露对比方法细节、超参数设置、随机种子等信息，无法完全评估其公平性，但从 SOTA 声明和跨数据集一致性来看，结果具有较高可信度。

---

### 6. 主要结论与发现

- PSG-Nav 通过引入**3D概率场景图**和**多元宇宙决策**，有效克服了开放词汇导航中的感知不确定性，能够进行全局组合推理，避免局部最优解。
- 在 MP3D、HM3D、HSSD 三个权威基准上取得了新的最优成功率，证明了概率建模和全局假设推理对导航鲁棒性的显著提升。
- 证据体验校准器能够在线利用历史经验修正误检，进一步增强了长时运行中的适应能力。

---

### 7. 优点

- **创新性**：将概率分布引入场景图，突破了确定性语义地图的局限，为开放词汇导航提供了新的表达范式。
- **全局决策视角**：多元宇宙决策从全局组合可能性出发采样，有效避免了局部最优陷阱，在语义歧义环境下表现出更强的决策能力。
- **终身适应机制**：证据体验校准器使智能体能够在线学习，适应环境变化和感知错误的积累。
- **结果显著**：在三个广泛使用的基准上均刷新了最高成功率，跨数据集的一致性表明方法泛化能力较强。
- **开源计划**：提供了代码主页（https://psg-nav.github.io），便于复现与后续研究。

---

### 8. 不足与局限

- **信息缺失**：当前提取的文本仅为摘要，缺乏方法细节（如概率场景图的具体构建方式、采样数量、联合分布建模形式）和实验细节（如消融实验、参数敏感性、运行效率）。
- **实验覆盖有限**：虽然使用了三个数据集，但未说明是否包含跨域测试、动态场景或真实机器人部署；与基线方法的具体差异和生成效果可视化分析未在摘要中体现。
- **偏差风险**：摘要未提及训练/评估时的随机性控制、感知模型的具体配置，以及是否对失败案例进行剖析，可能存在实验报告不完整的风险。
- **应用限制**：计算开销可能较高（概率分布存储、多元宇宙采样和多假设推理），是否适合实时导航或资源受限的机器人平台尚不明确。
- **泛化与安全**：开放词汇场景中长尾语义的分布偏差、未知物体的处理方式，以及概率校准在极端感知错误下的稳健性，仍需进一步讨论。

---

（完）
