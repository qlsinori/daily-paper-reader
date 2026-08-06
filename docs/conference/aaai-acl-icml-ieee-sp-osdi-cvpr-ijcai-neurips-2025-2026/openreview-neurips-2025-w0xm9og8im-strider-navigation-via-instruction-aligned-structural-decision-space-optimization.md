---
title: "STRIDER: Navigation via Instruction-Aligned Structural Decision Space Optimization"
title_zh: STRIDER：通过指令对齐的结构化决策空间优化进行导航
authors: "Diqi He, Xuehao Gao, Hao Li, Junwei Han, Dingwen Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=w0xm9oG8im"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 连续环境下的零样本视觉语言导航
tldr: 论文针对零样本连续环境视觉语言导航中动作与空间结构及任务意图难以对齐的问题，提出STRIDER框架，系统优化智能体的决策空间，融合空间布局与历史动作反馈。方法在未见过的3D环境中无需场景特定训练即可提升导航稳定性，有效的长时程指令跟随能力。实验结果验证了结构化决策空间优化对零样本VLN-CE的显著改进，为连续环境导航提供新方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 零样本VLN-CE中动作与空间结构及任务意图难以对齐，现有方法缺乏结构化决策。
method: 提出STRIDER框架，通过整合空间布局和先前动作反馈优化智能体决策空间。
result: 在未见环境上提升长时程导航稳定性和指令跟随能力。
conclusion: 证明了结构化决策空间优化对零样本连续环境导航的有效性。
---

## Abstract
The Zero-shot Vision-and-Language Navigation in Continuous Environments (VLN-CE) task requires agents to navigate previously unseen 3D environments using natural language instructions, without any scene-specific training. A critical challenge in this setting lies in ensuring agents’ actions align with both spatial structure and task intent over long-horizon execution. Existing methods often fail to achieve robust navigation due to a lack of structured decision-making and insufficient integration of feedback from previous actions. To address these challenges, we propose STRIDER (Instruction-Aligned Structural Decision Space Optimization), a novel framework that systematically optimizes the agent’s decision space by integrating spatial layout priors and dynamic task feedback. Our approach introduces two key innovations: 1) a Structured Waypoint Generator that constrains the action space through spatial structure, and 2) a Task-Alignment Regulator that adjusts behavior based on task progress, ensuring semantic alignment throughout navigation. Extensive experiments on the R2R-CE and RxR-CE benchmarks demonstrate that STRIDER significantly outperforms strong SOTA across key metrics; in particular, it improves Success Rate (SR) from 29\% to 35\%, a relative gain of 20.7\%. Such results highlight the importance of spatially constrained decision-making and feedback-guided execution in improving navigation fidelity for zero-shot VLN-CE.

---

## 论文详细总结（自动生成）

## STRIDER：通过指令对齐的结构化决策空间优化进行导航（论文总结）

### 1. 核心问题与研究动机

- **任务背景**：零样本连续环境视觉语言导航（Zero-shot VLN-CE）要求智能体仅依靠自然语言指令，在**从未见过的3D环境**中导航，且**不能进行任何场景特定的训练**。
- **核心挑战**：在长时程执行过程中，智能体的动作难以同时与**空间结构**（如墙体、障碍物、可行区域）和**任务意图**（指令语义要求）保持对齐。
- **现有方法不足**：已有方法因缺乏**结构化决策机制**，以及对**先前动作反馈**的整合不足，导致导航鲁棒性差、长时程指令跟随容易偏差。
- **研究意义**：解决零样本VLN-CE中的动作-空间-意图对齐问题，是推进连续环境具身导航实用化的重要一步。

### 2. 方法论述

STRIDER 的整体思想是：**通过整合空间布局先验和动态任务反馈，系统地优化智能体的决策空间**，使每一步动作既符合物理空间约束，又贴近指令语义意图。框架由两个关键组件构成：

- **结构化路标生成器（Structured Waypoint Generator）**：
  - 作用：利用空间布局先验（如深度、可行区域、障碍物分布）对候选动作进行约束和筛选，将原始动作空间压缩为结构化、语义上有意义的路标序列。
  - 思想：通过显式引入空间结构约束，避免智能体在无意义或不可行方向上产生动作，从源头上提升动作空间质量。
- **任务对齐调节器（Task-Alignment Regulator）**：
  - 作用：根据任务执行进度动态调整智能体行为，通过持续整合来自先前动作的反馈，校正当前动作与指令意图的偏差。
  - 思想：在长时程导航中加入反馈引导机制，确保每个时间步的决策与整体任务目标保持语义对齐。

在算法流程层面，STRIDER 按如下方式运作：
1. 接收视觉观测、深度信息和自然语言指令，解析出导航相关的结构化信息；
2. 由结构化路标生成器从空间结构约束中生成候选路标（可能的下一步目标点）；
3. 由任务对齐调节器结合历史动作反馈、任务进度状态，评估和筛选最符合指令语义的路标；
4. 智能体执行选定的路标动作，更新任务进度并循环上述过程，直至完成指令任务或到达终止条件。

### 3. 实验设计

- **数据集 / Benchmark**：
  - **R2R-CE**：基于 Matterport3D 连续环境的视觉语言导航基准，是该领域最常用的标准评测集。
  - **RxR-CE**：R2R-CE 的扩展版本，指令更多样、更长，且包含多语种指令，评测更严格。
- **对比方法**：与当前强基线（Strong SOTA）方法对比，报告了 VLN-CE 的标准核心指标。
- **核心指标**：主要报告 **成功率（Success Rate, SR）**，此外还涉及导航误差等连续环境导航常用指标。

### 4. 资源与算力

- 原文（提取到的摘要与元数据）**未明确提及**使用的 GPU 型号、数量、训练时长或其他算力资源。
- 需要指出：由于该论文为 NeurIPS-2025 接收论文，且方法涉及视觉-语言多模态推理，通常需要较高级别 GPU 资源，但在本文公开材料中并未给出具体信息。

### 5. 实验数量与充分性

- **公开信息可考的实验**：在 R2R-CE 和 RxR-CE 两个 benchmark 上进行了评测，SR 从 29% 提升至 35%，相对提升 20.7%。
- **实验充分性评估**：
  - 优势：在两个不同的基准上验证，且与 SOTA 对比，核心指标提升显著，能初步证明方法有效性。
  - 局限：由于仅公开了摘要级信息，**未见逐项消融实验**（如单独移除结构化路标生成器或任务对齐调节器的效果）、**未见分场景/分复杂度的细化分析**、**未见失败案例与误差模式分析**。
  - 公平性：从摘要看，对比的是"strong SOTA"，但没有展示同设置、同预算下的随机种子、重复实验等细节，无法完全评估统计显著性和稳定性。

### 6. 主要结论与发现

- **结构化的决策空间优化能显著提升零样本 VLN-CE 性能**：在未见过的环境中，仅靠空间约束与反馈引导，就能带来 20.7% 的相对 SR 提升。
- **空间约束与反馈引导缺一不可**：动作空间结构化（限制在可行路径上）和任务语义对齐（持续校准意图偏差）共同构成了鲁棒导航的核心。
- **长时程指令跟随能力增强**：方法在更长、更复杂的指令（RxR-CE）上也表现出稳定的导航保真度。
- **零样本设置下的可推广性**：无需场景特定微调即可适应新环境，具有实际部署价值。

### 7. 方法优点

- **概念清晰、动机明确**："动作与空间结构和任务意图对齐"这一切入点准确而具体。
- **双组件解耦设计**：结构化路标生成器和任务对齐调节器各司其职（空间约束 vs. 语义反馈），便于理解、复现和后续扩展。
- **零样本泛化能力强**：不依赖场景微调，在未见环境上即有大幅性能增益，应用前景广。
- **提升幅度显著**：SR 从 29% 到 35%，在成熟基准上属可观提升。
- **覆盖标准多基准**：在 R2R-CE 和 RxR-CE 两个主流 benchmark 上验证，增加了结论的可信度。

### 8. 不足与局限

- **实验细节不透明**：摘要中缺少消融实验、超参数敏感性、各环境类型（如房间 vs. 走廊）的表现差异等关键信息，难以全面评估方法各组成部分的实际贡献。
- **算力开销未知**：未披露模型规模、推理速度、是否依赖预训练视觉-语言大模型等，实际部署成本不明。
- **基准覆盖面有限**：仅在 VLN-CE 两个基准上评估，未在更传统的离散环境 VLN、或真实机器人平台上测试，跨域迁移能力未知。
- **零样本下的极端场景未知**：未见对长指令、高度复杂空间、光照变化等极端条件下的性能边界分析。
- **对比公平性存疑**：未展示与 SOTA 在同种子、同框架下的配对复现结果，无法确认收益来源是否完全来自方法本身。
- **方法局限性**：若空间先验（如深度/障碍信息）质量下降，或指令与空间格局高度冲突，结构化约束可能反而限制决策灵活性。

（完）
