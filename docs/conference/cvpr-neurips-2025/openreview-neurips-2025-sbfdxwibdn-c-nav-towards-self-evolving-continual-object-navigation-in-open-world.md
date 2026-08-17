---
title: "C-NAV: Towards Self-Evolving Continual Object Navigation in Open World"
title_zh: C-NAV：面向开放世界自演进的持续物体导航
authors: "MingMing Yu, Fei Zhu, wenzhuo liu, Yirong Yang, Qunbo Wang, wenjun wu, Jing Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=SbfdxWibDn"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 开放世界环境中的持续物体目标导航
tldr: 现有物体导航方法在训练时依赖静态轨迹和固定物体类别，难以适应动态开放世界的持续变化。本文提出持续物体导航基准，要求智能体在学习新类别目标的同时不遗忘旧知识。为应对该挑战，C-Nav采用包含特征蒸馏和双路径抗遗忘机制的持续视觉导航框架，在多模态特征层面统一新旧知识。实验证明C-Nav能有效缓解灾难性遗忘，持续提升开放世界中物体导航能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 真实开放世界中物体导航需要持续适应新类别，现有方法在固定类别上训练，忽视持续学习和防遗忘需求。
method: 提出C-Nav框架，引入双路径抗遗忘机制和特征蒸馏，对齐多模态特征来持续学习新物体类别。
result: 在提出的持续物体导航基准上，C-Nav在获取新技能的同时减轻了对旧知识的灾难性遗忘。
conclusion: 展示了持续物体导航的可行性，为开放世界具身导航提供了新基准和训练范式。
---

## Abstract
Embodied agents are expected to perform object navigation in dynamic, open-world environments. However, existing approaches typically rely on static trajectories and a fixed set of object categories during training, overlooking the real-world requirement for continual adaptation to evolving scenarios. To facilitate related studies, we introduce the continual object navigation benchmark, which requires agents to acquire navigation skills for new object categories while avoiding catastrophic forgetting of previously learned knowledge. To tackle this challenge, we propose C-Nav, a continual visual navigation framework that integrates two key innovations: (1) A dual-path anti-forgetting mechanism, which comprises feature distillation that aligns multi-modal inputs into a consistent representation space to ensure representation consistency, and feature replay that retains temporal features within the action decoder to ensure policy consistency. (2) An adaptive sampling strategy that selects diverse and informative experiences, thereby reducing redundancy and minimizing memory overhead. Extensive experiments across multiple model architectures demonstrate that C-Nav consistently outperforms existing approaches, achieving superior performance even compared to baselines with full trajectory retention, while significantly lowering memory requirements. 
The code will be publicly available at \url{https://bigtree765.github.io/C-Nav-project}.

---

## 论文详细总结（自动生成）

## 论文总结：C-NAV：面向开放世界自演进的持续物体导航

### 1. 核心问题与研究动机

- **背景**：具身智能体（Embodied Agents）被期望在动态、开放的世界环境中执行物体目标导航任务。然而，现有物体导航方法通常在**固定的物体类别集合**上训练，且依赖**静态轨迹数据**，这不符合真实世界不断出现新类别、场景持续演化的客观规律。
- **核心问题**：当智能体需要学习新类别的导航技能时，会遭遇**灾难性遗忘（Catastrophic Forgetting）**，即在学习新知识的同时丢失之前学到的导航能力。解决“如何持续学习新类别而不遗忘旧知识”是该论文关注的核心科学问题。
- **推动力**：现有导航领域缺乏针对“持续学习”设定的评估基准与训练范式，难以支撑相关研究的发展。为此论文引入**持续物体导航（Continual Object Navigation）**新基准，推动该方向的研究。

### 2. 方法论：C-Nav 框架

论文提出 **C-Nav**（Continual Visual Navigation Framework），其核心思想是在多模态特征层面统一新旧知识的表达，通过“抗遗忘机制 + 自适应采样”实现在开放世界中持续学习。关键技术创新包括：

- **双路径抗遗忘机制（Dual-path Anti-forgetting Mechanism）**：
  - **特征蒸馏（Feature Distillation）路径**：将多模态输入（视觉、语义、动作指令等）对齐到一致的表示空间，确保在持续学习过程中新旧类别所对应的特征表示保持一致性，从而缓解表示层面的遗忘。
  - **特征回放（Feature Replay）路径**：在动作解码器（Action Decoder）中保留时序特征，通过“回放”过去任务中关键的时间序列信息，确保**策略**层面的连续性，防止导航策略在参数更新时发生漂移。
- **自适应采样策略（Adaptive Sampling Strategy）**：
  - 用于从历史经验中选择**多样化、信息量大**的样本存入回放缓冲区，降低冗余存储，减小内存开销。这与传统“无差别保留全部历史轨迹”的做法形成对比。
- **整体流程**（文字说明）：
  1. 智能体在多模态环境中接收新类别的导航目标指令与视觉观测；
  2. 提取多模态特征后，特征蒸馏路径将其对齐到与旧知识一致的表示空间；
  3. 特征回放路径在动作解码阶段结合历史时序特征，生成导航动作；
  4. 在新任务学习过程中，自适应采样策略筛选有代表性的旧任务经验参与重放；
  5. 联合优化新任务损失与抗遗忘损失，使模型在适应新类别的同时保持旧类别的导航能力。

### 3. 实验设计

- **Benchmark**：论文提出了**持续物体导航基准（Continual Object Navigation Benchmark）**，该基准要求智能体在连续任务序列中学习新物体类别的导航技能，同时保持对旧类别的导航性能。
- **场景**：基于具身导航仿真环境构建（具体仿真平台如AI2-THOR、Habitat等信息，当前摘要与元数据中未明确说明）。
- **对比方法**：
  - 与现有导航方法进行比较（如经典的目标导航基线方法，具体名称文摘未列出）；
  - 特别与**保留完整轨迹（Full Trajectory Retention）**的基线进行对比，以验证 C-Nav 在显著降低内存需求的同时是否能取得更优性能。
- **模型架构**：实验在**多种模型架构**上进行，以验证方法的通用性。

### 4. 资源与算力

- 当前提供的论文摘要与元数据中**未明确披露**训练所用 GPU 型号、数量、训练时长等算力信息。
- 需要注意：由于原始 PDF 提取受限（经 OpenReview 验证页面获取），完整的实验设置、超参数与硬件细节有待查阅全文版本。

### 5. 实验数量与充分性分析

- **已披露的实验内容**：跨多种模型架构的对比实验、与全轨迹保留基线的对比实验，且实验覆盖“持续学习效果 + 内存开销”两个维度，表明作者有意识地评估“性能-资源”权衡。
- **充分性判断**：
  - 从摘要反映的结论看，实验设计能支撑“C-Nav 优于现有方法、且超越全轨迹保留基线”的核心结论，初步具备说服力；
  - 但当前信息不足以评估消融实验的完整度（如是否逐一验证双路径机制各自贡献、采样策略不同设计选择的影响）、以及跨不同数据集与仿真环境的泛化验证情况；
  - 若全文包含消融、不同任务序列长度、不同类别增量规模等实验，则充分性更强；该部分有待以全文信息为准。

### 6. 主要结论与发现

- C-Nav 在持续物体导航基准上显著优于现有方法，能有效**缓解灾难性遗忘**，使智能体在学习新类别技能的同时保持旧类别的导航能力。
- 即使在**只保留少量经验样本（而非全部历史轨迹）**的情况下，C-Nav 仍能取得优于全轨迹保留基线的性能，同时**大幅降低内存占用**。
- 结论表明：持续物体导航在开放世界中是可行的，C-Nav 为开放世界具身导航提供了新的基准与训练范式。

### 7. 方法亮点与优势

- **问题设定新颖**：率先将“持续学习/防遗忘”引入物体目标导航，提出持续性导航基准，填补了该方向空白。
- **双重抗遗忘设计**：同时从“特征表示一致性”和“动作策略连续性”两个层面防止遗忘，针对导航任务特点（感知+决策）做了专门设计，思路清晰。
- **兼顾性能与资源**：通过自适应采样策略有效控制内存开销，在低资源占用下超越全量回放基线，实用性强。
- **跨架构泛化验证**：在多种模型架构上验证通用性，增强结论的可信度。

### 8. 不足与局限

- **信息完整度受限**：当前基于论文摘要撰写的总结未能获取完整的实验参数、详细方法公式与实现细节，无法做更深层技术评估。
- **基准覆盖范围**：若基准仅基于单一仿真环境，则对真实世界复杂场景（光照变化、物体外观多样、动态障碍物等）的迁移效果尚未可知；具体验证环境待全文确认。
- **类别增量设定**：持续物体导航的难度受类别序列顺序、相似度分布影响，文中未展示对多种序列顺序的敏感性分析（基于现有信息判断）。
- **长期持续性**：若任务序列很长，遗忘累积效应如何、回放缓冲区上限如何设定等问题，尚待全文详细说明。
- **未见算力对比**：论文未比较训练/推理开销与其他方法的具体差异，实际部署效率未能完整评估。
- **应用限制**：导航策略的学习依赖仿真训练环境与预定义的动作空间，直接迁移到真实机器人系统仍需克服 sim-to-real 差距。

---

（完）
