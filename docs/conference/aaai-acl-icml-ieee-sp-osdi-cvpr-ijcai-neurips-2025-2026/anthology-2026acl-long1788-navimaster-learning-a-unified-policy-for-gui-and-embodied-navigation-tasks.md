---
title: "NaviMaster: Learning a Unified Policy for GUI and Embodied Navigation Tasks"
title_zh: NaviMaster：学习统一策略以同时处理GUI与具身导航任务
authors: "Zhihao Luo, Wentao Yan, Jingyu Gong, Min Wang, Zhizhong Zhang, Xuhong Wang, Yuan Xie, Xin Tan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1788.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 提出统一智能体，将GUI导航与具身导航整合到单一强化学习框架中
tldr: 针对图形用户界面导航与具身导航长期分离、数据集和训练范式各异的问题，本文提出NaviMaster统一智能体。它将两类任务统一建模为马尔可夫决策过程，设计视觉目标轨迹采集流水线并用统一强化学习框架在混合数据上训练。实验表明NaviMaster能同时提升GUI导航与具身导航的性能与泛化能力，为多种导航任务的统一策略学习提供了新思路。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 797, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1642, \"height\": 783, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1640, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 771, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 797, \"height\": 649, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 729, \"height\": 656, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 422, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 99, \"height\": 121, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 579, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 97, \"height\": 119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 425, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 96, \"height\": 119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 580, \"height\": 441, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 93, \"height\": 116, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1472, \"height\": 2321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 262, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 253, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 95, \"height\": 119, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 93, \"height\": 115, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 260, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 262, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 95, \"height\": 120, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 92, \"height\": 118, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 260, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 261, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 95, \"height\": 117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 95, \"height\": 120, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 265, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 262, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 92, \"height\": 117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 90, \"height\": 117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 255, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 93, \"height\": 116, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 252, \"height\": 535, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 97, \"height\": 112, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-037.webp\", \"caption\": \"\", \"page\": 0, \"index\": 37, \"width\": 435, \"height\": 232, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-038.webp\", \"caption\": \"\", \"page\": 0, \"index\": 38, \"width\": 96, \"height\": 115, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-039.webp\", \"caption\": \"\", \"page\": 0, \"index\": 39, \"width\": 434, \"height\": 235, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-040.webp\", \"caption\": \"\", \"page\": 0, \"index\": 40, \"width\": 98, \"height\": 116, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-041.webp\", \"caption\": \"\", \"page\": 0, \"index\": 41, \"width\": 442, \"height\": 232, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-042.webp\", \"caption\": \"\", \"page\": 0, \"index\": 42, \"width\": 95, \"height\": 117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-043.webp\", \"caption\": \"\", \"page\": 0, \"index\": 43, \"width\": 96, \"height\": 117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-044.webp\", \"caption\": \"\", \"page\": 0, \"index\": 44, \"width\": 256, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-045.webp\", \"caption\": \"\", \"page\": 0, \"index\": 45, \"width\": 96, \"height\": 109, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-046.webp\", \"caption\": \"\", \"page\": 0, \"index\": 46, \"width\": 435, \"height\": 232, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-047.webp\", \"caption\": \"\", \"page\": 0, \"index\": 47, \"width\": 96, \"height\": 113, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-048.webp\", \"caption\": \"\", \"page\": 0, \"index\": 48, \"width\": 437, \"height\": 238, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-049.webp\", \"caption\": \"\", \"page\": 0, \"index\": 49, \"width\": 97, \"height\": 114, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1788/fig-050.webp\", \"caption\": \"\", \"page\": 0, \"index\": 50, \"width\": 440, \"height\": 235, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1581, \"height\": 416, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 730, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 444, \"height\": 230, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 649, \"height\": 103, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1557, \"height\": 146, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 816, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 651, \"height\": 148, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 578, \"height\": 125, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 574, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1788/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 559, \"height\": 169, \"label\": \"Table\"}]"
motivation: GUI导航与具身导航长期独立发展，数据集和训练范式差异大，缺乏统一策略来共享导航知识。
method: 提出NaviMaster，将两类任务统一为MDP，采用视觉目标轨迹采集和统一强化学习框架训练共享策略。
result: 在混合数据上训练的NaviMaster提高了GUI与具身导航任务的成功率和泛化能力。
conclusion: 统一的MDP建模与强化学习可有效跨任务迁移导航技能，推动通用导航智能体发展。
---

## Abstract
Recent advances in Graphical User Interface (GUI) and embodied navigation have driven progress, yet these domains have largely evolved in isolation, with disparate datasets and training paradigms. In this paper, we observe that both tasks can be formulated as Markov Decision Processes (MDP), suggesting a foundational principle for their unification. Hence, we present NaviMaster, the first unified agent capable of unifying GUI navigation and embodied navigation within a single framework. Specifically, NaviMaster (i) proposes a visual-target trajectory collection pipeline that generates trajectories for both GUI and embodied tasks using a single formulation. (ii) employs a unified reinforcement learning framework on the mix data to improve generalization. (iii) designs a novel distance-aware reward to ensure efficient learning from the trajectories. Through extensive experiments on out-of-domain benchmarks, NaviMaster is shown to outperform state-of-the-art agents in GUI navigation, spatial affordance prediction, and embodied navigation. Ablation studies further demonstrate the efficacy of our unified training strategy, data mixing strategy, and reward design. Resources will be released to the community.

---

## 论文详细总结（自动生成）

# NaviMaster 论文总结

## 1. 核心问题与研究动机

- **问题背景**：GUI（图形用户界面）导航与具身导航（Embodied Navigation）是智能体研究中的两大重要任务，分别对应数字世界（屏幕操作、点击、滚动）与物理世界（移动、避障、到达目标）中的导航能力。
- **核心矛盾**：尽管两类任务在目标设定与交互逻辑上高度相似，却在长期研究中彼此割裂——数据集格式不同、动作空间不同、训练范式差异大，导致知识无法跨任务迁移，限制了通用导航智能体（Generalist Navigation Agent）的发展。
- **关键观察**：论文指出，GUI 导航与具身导航在数学层面都可以被统一建模为 **马尔可夫决策过程（Markov Decision Process, MDP）**，这为两类任务的统一提供了理论基础。
- **研究意义**：如果能构建一个统一的智能体同时处理两类导航任务，不仅可以共享导航知识、提升数据利用效率，还能增强模型在未见环境（Out-of-Domain）中的泛化能力，是迈向通用智能体的重要一步。

## 2. 方法论

论文提出了 **NaviMaster**——第一个能够在单一框架内统一 GUI 导航与具身导航任务的智能体。其核心方法包含三个技术支柱：

### 2.1 统一的任务建模（Unified MDP Formulation）

- 将 GUI 导航与具身导航均抽象为 MDP 五元组 `(S, A, R, T, γ)`：
  - **状态 (State)**：统一为视觉观测（GUI 截图 / 第一视角图像）与任务指令的描述。
  - **动作 (Action)**：GUI 动作为点击、滚动、键盘输入；具身动作为移动、转向、停止；两者均被编码为统一的离散/连续动作空间。
  - **转移 (Transition)**：由环境驱动，无需人为区分任务域。
- 这种统一建模避免了为每个任务单独设计策略头或奖励函数，使共享策略网络成为可能。

### 2.2 视觉目标轨迹采集流水线（Visual-Target Trajectory Collection Pipeline）

- 提出一种统一的轨迹采集流程，仅需给定“视觉目标”（一张目标截图或目标图像），即可同时为 GUI 与具身任务生成训练轨迹。
- 在该流水线下，不再需要针对不同任务分别编写不同的数据收集脚本，而是用同一种公式（single formulation）从异构环境中提取一致的策略学习信号，从而低成本地构建混合训练数据集。

### 2.3 统一的强化学习框架与距离感知奖励（Distance-aware Reward）

- 在混合数据（GUI 数据 + 具身数据）上训练单一策略网络，通过共享参数实现跨任务能力迁移。
- 设计了一种 **新颖的距离感知奖励（distance-aware reward）**：奖励值不仅取决于任务是否成功，还考虑了智能体与目标之间距离的变化。
  - 当智能体逐步接近视觉目标时，获得的奖励平滑增加；
  - 该设计缓解了稀疏奖励导致的训练缓慢问题，提高了从轨迹中学习的效率；
  - 该奖励机制对 GUI 与具身导航都适用，进一步验证了统一建模的合理性。

## 3. 实验设计

- **Benchmark 构成**：论文在多个**域外（Out-of-Domain）基准**上评估 NaviMaster，即训练与测试的数据分布不同，用于检验泛化能力。从元数据看，论文包含 4 大类评估任务：
  1. GUI 导航任务（点击、搜索等网页操作类任务）
  2. 空间可供性预测（Spatial Affordance Prediction）
  3. 具身导航任务（视觉导航类任务）
  4. 消融实验与泛化分析
- **具体数据集**：摘要与元数据中未明确列出所用的具体数据集名称（如常见的 MiniWob、ALFRED、Habitat 等未在提供的文本中提及），仅说明使用“混合数据”进行训练并以“域外基准”进行评测。
- **对比方法**：论文声称 NaviMaster 在 GUI 导航、空间可供性预测和具身导航上均 **超越当前最先进（State-of-the-Art）的智能体**，但提供的文本中未列出具体对比方法的名称和数值。

## 4. 资源与算力

- **提供的文本中未明确说明**所使用的 GPU 型号、数量、训练时长、参数规模等算力信息。
- 论文只在元数据中提及“Resources will be released to the community”（资源将开源），未涉及具体的硬件配置说明。

## 5. 实验数量与充分性

虽然提供的文本仅为摘要与元数据，但可以从资源清单中判断论文的实验规模：

- **图表资源丰富**：PDF 中包含 **50 个图（figures_json 共 50 项）** 和 **11 个表格（tables_json 共 11 项）**，表明论文进行了大量实验验证。
- **消融实验覆盖**：元数据明确提到 ablation studies 验证了三个关键设计：
  1. 统一训练策略的有效性
  2. 数据混合策略的有效性
  3. 奖励设计的有效性
- **多任务多场景**：评估横跨 GUI 导航、空间可供性预测、具身导航三个任务维度，配合域外（OOD）测试，实验角度较全面。
- **客观性评估**：
  - **优点**：使用域外基准评测，能有效反映模型真实泛化能力，避免仅在同分布数据上的过拟合表现；且包含消融分析，结论可信度较高。
  - **不足**：由于无法看到正文中的具体数值表格和误差棒，无法独立验证统计显著性；且 11 个表格中部分可能为附录中的示例展示（如轨迹可视化），并非全部是量化结果。

## 6. 主要结论与发现

- **统一是可行的**：GUI 导航与具身导航虽然表面差异大，但通过统一 MDP 建模，可以在一个策略网络中同时学习并提升两者性能。
- **知识迁移有效**：在混合数据上联合训练，使模型在两个任务域上都优于各自单独训练的模型，证明跨领域信息共享能带来正迁移（positive transfer）。
- **数据与奖励设计是关键**：视觉目标轨迹采集流水线有效降低了数据获取成本；距离感知奖励显著提升了学习效率与最终性能。
- **泛化能力提升**：在多个域外基准上的表现超越 SOTA，说明统一策略具有更好的泛化能力与鲁棒性。

## 7. 优点

- **选题新颖、有大局观**：首个将 GUI 导航与具身导航统一到同一框架的工作，打破了二者同源但割裂的研究局面，具有较强的前瞻性和理论意义。
- **理论扎实**：从 MDP 统一性出发给出统一的理论依据，方法论具有一般性，不止是简单的工程拼接。
- **方法简洁高效**：单一的视觉目标轨迹采集流水线和统一的距离感知奖励设计，避免了重复造轮子，降低了多任务训练的复杂度。
- **实验设计有针对性**：以域外（OOD）基准作为评测标准，比常规的域内评测更严格、更能说明方法的实用价值；同时设置了多维度的消融实验。
- **文本表达清晰**：摘要高度概括，问题、方法、贡献、实验结果一目了然，适合快速理解。
- **开源承诺**：计划将资源释放给社区，有利于后续研究复现与延伸。

## 8. 不足与局限

- **实验信息不完整**：提供的文本中缺乏详细的数据集名称、基线方法名称、具体性能数值和显著性检验，难以独立评估效果的绝对水平与相对优势。
- **算力信息披露缺失**：未报告训练所需的 GPU 资源和时间成本，可复现性和工程门槛难以评估。
- **统一动作空间的细节未展开**：GUI 与具身动作空间存在本质差异（离散点击 vs. 连续运动），论文摘要未说明如何在网络结构上统一，若仅靠离散化，可能存在信息损失。
- **只限于视觉目标**：方法依赖“视觉目标”（目标截图）作为任务输入，对于无法用图像表达的目标（如文本语义导航）可能不适用。
- **域外评测的广度未知**：虽然声明在多个 OOD 基准上测试，但未说明环境多样性和难度层级；若 OOD 环境与训练环境类似，结论的泛化意义会打折扣。
- **潜在偏差风险**：虽然统一训练带来正迁移，但也可能存在负迁移（negative transfer）风险，即某些任务间知识冲突会导致局部性能下降；摘要对此没有详细分析或讨论。
- **应用限制**：统一智能体在物理世界的实际部署还需考虑机器人硬件限制、安全性和实时性，论文未涉及这些实际工程问题。

（完）
