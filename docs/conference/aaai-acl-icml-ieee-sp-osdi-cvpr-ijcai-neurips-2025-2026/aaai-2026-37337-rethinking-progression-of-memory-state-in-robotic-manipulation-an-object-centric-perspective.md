---
title: "Rethinking Progression of Memory State in Robotic Manipulation: An Object-Centric Perspective"
title_zh: 重新思考机器人操作中记忆状态的进展：基于对象中心的视角
authors: "Nhat Chung, Taisei Hanyu, Toan Nguyen, Huy Le, Frederick Bumgarner, Duy Minh Ho Nguyen, Khoa Vo, Kashu Yamazaki, Chase Rainwater, Tung Kieu, Anh Nguyen, Ngan Le"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37337/41299"
tags: ["query:semantic-map"]
score: 6.0
evidence: 机器人操作中的记忆状态；对象中心记忆；非马尔可夫任务
tldr: 针对具身智能体在非马尔可夫环境中需依赖物体历史交互来进行决策的问题，提出LIBERO-Mem任务套件，用于压力测试机器人操作中的对象级记忆能力。该套件结合短时与长时任务，暴露了无持久记忆的视觉运动策略会重复动作或遗漏已完成步骤。通过该基准可推动具身智能体长期记忆与推理研究，提升复杂操作任务的鲁棒性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37337/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1755, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37337/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1817, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37337/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1324, \"height\": 532, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37337/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 883, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37337/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 881, \"height\": 1340, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37337/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 884, \"height\": 595, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37337/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 841, \"height\": 595, \"label\": \"Table\"}]"
motivation: 在非马尔可夫操作任务中，若缺乏对物体历史交互的持久记忆，策略可能重复或遗漏动作。
method: 提出LIBERO-Mem非马尔可夫任务套件，包含短时和长时任务，通过部分可观测性压测对象级记忆。
result: 揭示了物体历史信息对操作成功的关键影响，表明记忆缺失会导致策略失败。
conclusion: 对象中心持久记忆是复杂操作任务中不可或缺的组成部分，为后续长期记忆研究提供基准。
---

## Abstract
As embodied agents operate in increasingly complex environments, the ability to perceive, track, and reason about individual object instances over time becomes essential, especially in tasks requiring sequenced interactions with visually similar objects. In non-Markovian settings, critical decision cues lie in object histories rather than the current scene. Without persistent memory of prior interactions (what was used, where it was placed, or how it changed), visuomotor policies may fail, repeat past actions, or overlook completed ones. To surface this challenge, we introduce LIBERO-Mem, a non-Markovian task suite for stress-testing robotic manipulation under object-level partial observability. It combines short- and long-horizon object tracking with temporally sequenced subgoals, requiring reasoning beyond the current frame. However, vision-language-action (VLA) models often struggle in such settings, with token scaling quickly becoming intractable even for tasks spanning just a few hundred frames. We propose Embodied-SlotSSM, a slot-centric VLA framework built for temporal scalability. It maintains spatio-temporally consistent slot identities and leverages them through two mechanisms: (1) slot-state-space modeling for reconstructing short-term history, and (2) a relational encoder to align the input tokens with action decoding. Together, these components enable temporally grounded, context-aware action prediction. Experiments show Embodied-SlotSSM's baseline performance on LIBERO-Mem and general tasks, offering a scalable solution for non-Markovian reasoning in object-centric policies.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：在非马尔可夫（non-Markovian）的机器人操作环境中，当前的视觉运动策略（visuomotor policy）仅依赖当前帧的观测来决定动作，无法利用物体层面的历史交互信息（如某物体是否已被操作过、被放置在哪里、状态如何变化）。这种仅依赖当前观测的马尔可夫假设，在面对重复步骤、视觉相似物体和长时间跨度任务时，容易导致动作重复、遗漏已完成步骤或错误操作。
- **理论背景**：研究者将问题建模为**对象中心的 POMDP**（部分可观测马尔可夫决策过程），其中最优决策不仅取决于当前场景，更取决于与特定物体相关的历史交互记录。这种设定比传统的全可观测马尔可夫任务更贴近真实世界。
- **整体含义**：要实现对真实世界的可靠操作，机器人必须拥有**持久、结构化、对象级别的记忆**，以完成长时序、多步骤的复杂任务。论文通过提出新基准（LIBERO-Mem）和新方法（Embodied-SlotSSM），推动了这一方向的研究。

## 2. 论文提出的方法论

### 2.1 核心思想

论文提出了 **Embodied-SlotSSM**，一个基于槽位（slot）的状态空间模型（SSM）框架，核心思路是将视觉输入分解为**离散、持久、对象中心**的槽表示（slot representations），通过状态空间模型建模对象的时序演化，从而为动作解码提供结构化记忆支持。

### 2.2 关键组成部分

- **槽注意力机制（Slot Attention）**：将稠密的视觉嵌入转换为 K 个对象中心化 token（论文默认为 K=16）。通过可学习的查询槽和迭代注意力更新，将视觉特征绑定到对象级表示。
  - 槽的初始化具有时间连续性：首帧随机初始化，后续帧用前一帧的最终槽状态初始化，从而保持对象身份的跨帧一致性。
- **时间对比损失（Temporal Contrastive Loss）**：约束同一物体在相邻帧中的槽表示保持一致，防止身份漂移。
- **基于槽的 SSM（SlotSSM）**：对每个槽分别应用状态空间模型，将对象历史编码为隐藏状态。其矩阵设计为块对角阵，每个块仅依赖相应槽的输入，实现模块化的对象级时序建模。SSM 输出一个时间窗口（p 帧过去、q 帧未来）的预测表示，支持短期对象运动建模和状态重建。
- **槽融合模块（Slot Fusion）**：将当前槽、预测的下一时刻槽以及（在 Naive 版本中）任务子目标文本嵌入融合，形成包含时序上下文的动作解码输入。
- **关系编码器（Relation Encoder）**：对槽隐状态与原始视觉特征做交叉注意力，生成关系 token，使动作解码可以综合感知与对象状态。
- **动作解码**：将关系 token、槽动态信息和语言指令嵌入送入冻结的 LLM 动作解码器，输出动作预测。

### 2.3 关键公式与算法流程

- **SSM 核心递推公式**：

  ht = A(et)ht−1 + B(et)et, yt = C(et)ht

  其中 A、B、C 为输入条件化矩阵，在网络中以块对角形式按槽分解。

- **槽注意力更新公式**：

  ai,j = (1/√D_enc) · qi·kjᵀ，经过 softmax 归一化后加权聚合特征，并通过 GRU 循环细化槽表示。

- **时间对比损失**：以同一对象相邻时间槽为正样本，以其他视频/位置的槽为负样本，计算 InfoNCE 风格损失，强制槽的时间一致性。

- **训练和推理流程**：视觉观测 → 预训练视觉编码器 → Slot Attention 分解 → SlotSSM 时序建模 → Slot Fusion → Relation Encoder → LLM 动作解码 → 输出动作。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **LIBERO-Goal**：通用机器人操作基准，用于评估一般场景下的任务表现。
- **LIBERO-Mem（本文新提出）**：非马尔可夫、对象级记忆压力测试基准，包含 10 个任务（T1–T10），覆盖 4 种记忆类型：
  - **对象运动（OM）**：需要记住上一次动作（如拿起或放下）。
  - **对象序列（OS）**：需要记住物体被操作的次数（如重复拿放 3 次、5 次、7 次）。
  - **对象关系（OR）**：需要跟踪物体在时间上的关系变化（如从左到右轮换碗）。
  - **对象遮挡（OO）**：被遮挡物体需要靠记忆推断目标。
- 每个任务包含 120 条轨迹（100 条训练、20 条验证），每条轨迹 200–700 帧，支持短时与长时评估。任务还提供**子目标级细粒度评估**机制和物体实例 ID 标注。

### 3.2 对比方法

- **OpenVLA**（预训练的 VLA 模型）
- **π0**（基于流的 VLA 基础模型，token 数 256）
- **SlotVLA**（基于槽注意力的对象中心 VLA，支持 h=1 和 h=8 的输入帧数）
- **Naive E-SlotSSM**（本文方法的带 oracle 子目标信息的实现，token 数 32）

### 3.3 评估指标

- **任务成功率**（LIBERO-Goal）与**子目标完成率**（LIBERO-Mem），均为 20 次独立随机种子实验的平均值。

## 4. 资源与算力

- **论文正文未明确说明所使用的 GPU 型号、数量、训练时长等算力资源信息**。文中仅在数据分析中提到了 token 数量对比（如 OpenVLA 使用 256 个 token，SlotVLA 使用 16/128 个，Embodied-SlotSSM 使用 32 个），用于说明方法的计算效率优势，但未提供实际训练资源的量化描述。

## 5. 实验数量与充分性

### 5.1 实验数量

- **两大 Benchmark**：LIBERO-Goal（10 类任务）和 LIBERO-Mem（10 个任务）。
- **对比方法**：4 类基线（π0、SlotVLA(h=1)、SlotVLA(h=8)、Naive E-SlotSSM）。
- **实验规模**：每项任务在 20 个随机种子下重复实验，报告成功率和子目标完成率。
- **定性可视化**：提供槽注意力对抓取物体（如碗、夹爪）在时间维度上的注意力可视化。
- **未进行消融实验**：论文没有对 Embodied-SlotSSM 的各个组件（如 SSM、对比损失、关系编码器、槽融合）进行系统的消融分析。

### 5.2 实验充分性与客观性分析

- **优点**：覆盖了通用任务与非马尔可夫特殊任务两类场景；对比了多种代表性子目标类型（OM/OS/OR/OO）；采用多随机种子平均以降低方差；提供了定性可视化证据。
- **不足**：
  - 实验**缺乏消融研究**，无法量化评估每个组件对最终效果的独立贡献。
  - 在 LIBERO-Mem 上的**绝对成功率较低**（平均 14.8%），且部分任务（如 T2、T4、T6–T8）完成率为 0%，表明方法的实际能力有限。
  - Naive E-SlotSSM 依赖 **oracle 子目标文本信息**，与直觉上应“自主发现子目标”的完整设定仍有距离，实验结果有“上限参考”性质，不能反映完全自主推理的性能。

## 6. 论文的主要结论与发现

- **现有 VLA 模型在非马尔可夫任务中表现极差**：π0 和 SlotVLA 在 LIBERO-Mem 上的平均子目标完成率仅 0%–5%，几乎无法处理需要对象级历史记忆的任务。
- **Embodied-SlotSSM 的有效性**：Naive E-SlotSSM 在 LIBERO-Goal 上取得 83.0% 的最高平均成功率，在 LIBERO-Mem 上取得 14.8% 的子目标完成率，均明显超过无记忆基线，说明槽级时序记忆对非马尔可夫推理有实质帮助。
- **槽表示的时序一致性**：可视化结果证实模型能够在时间轴上稳定追踪同一对象实例（包括运动与遮挡场景），这种对象持久性是长时推理的基础。
- **Token 效率**：与 OpenVLA（256 token）和 SlotVLA（128 token）相比，Embodied-SlotSSM 只用 32 个 token 即可达到更好的记忆推理效果，验证了对象中心表示在长时序扩展上的可扩展性。

## 7. 优点

- **问题定位准确且重要**：指出了现有 VLA 在非马尔可夫设定下因缺乏对象级记忆而失败的关键问题，并以形式化定义（POMDP 与马尔可夫假设违反）阐明其必要性和艰巨性。
- **基准设计有针对性**：LIBERO-Mem 通过对象身份歧义、重复计数、关系排序、遮挡场景等设计，系统性地覆盖了不同类型的对象记忆需求，弥补了现有基准只测“当前帧推理”的不足。
- **方法设计具有创新性**：将槽注意力与状态空间模型结合用于机器人操作，把记忆建模从“整帧历史”简化为“对象级模块化历史”，兼顾了结构性和计算效率。
- **记忆机制的生物学启发**：借鉴认知科学中物体持久性推理的理论，提出了与人类记忆方式一致的对象中心记忆架构，具有较强的可解释性。
- **评估体系比较精细**：引入子目标级评估和物体/子目标标注，能更细粒度地诊断模型在哪个阶段失败，优于仅看最终成功率的评估方式。

## 8. 不足与局限

- **仿真环境限制**：实验仅基于模拟器（LIBERO），未在真实物理环境中验证，基准和方法的实际应用价值需进一步评估。
- **对 oracle 信息的依赖**：Naive E-SlotSSM 依赖 oracle 提供的文本化子目标状态来推进推理，距离完全自主感知与推理的目标还有明显距离。论文也承认这是其“薄弱”之处。
- **绝对性能有限**：在 LIBERO-Mem 上平均子目标完成率仅 14.8%，且多个任务为 0%，表明方法的记忆能力对复杂场景仍显著不足。
- **缺乏消融实验**：未系统验证 SSM、对比损失、槽融合、关系编码器各组件的作用，无法确认各设计选择的边际贡献。
- **分析深度不足**：对失败模式（如为何 T2、T4 等任务完全失败）未做深入剖析，对部分成功任务的泛化性和稳定性也缺乏讨论。
- **潜在偏差风险**：LIBERO-Mem 中部分任务（如若干重复操作任务）高度同质化，可能不足以全面反映对象中心记忆的多样性，存在任务设计偏差的可能。

（完）
