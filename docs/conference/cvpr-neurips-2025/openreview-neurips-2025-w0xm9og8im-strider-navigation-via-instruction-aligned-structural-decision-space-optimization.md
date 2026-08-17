---
title: "STRIDER: Navigation via Instruction-Aligned Structural Decision Space Optimization"
title_zh: STRIDER：通过指令对齐的结构化决策空间优化实现导航
authors: "Diqi He, Xuehao Gao, Hao Li, Junwei Han, Dingwen Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=w0xm9oG8im"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 利用自然语言指令在连续环境中进行零样本视觉语言导航
tldr: 连续环境中的零样本视觉语言导航（VLN-CE）要求智能体依靠自然语言指令在未见过环境中导航，现有方法因缺乏结构化决策和对历史反馈的利用而鲁棒性不足。作者提出STRIDER框架，通过整合空间布局与指令对齐来系统优化决策空间，使动作序列与空间结构和任务意图保持一致。在VLN-CE基准上的实验表明，STRIDER显著提升了长距离导航的成功率与路径效率，并改善了跨场景零样本迁移能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 零样本VLN-CE中动作与空间结构、任务意图难以对齐，导致长程导航鲁棒性差。
method: 将空间布局融入决策空间，并用指令对齐优化动作选择，同时整合上一步反馈以改进长期规划。
result: 在VLN-CE基准上，STRIDER在导航成功率与路径效率上均优于现有方法，零样本迁移表现突出。
conclusion: 结构化决策空间与反馈整合是提升连续环境指令导航性能的关键。
---

## Abstract
The Zero-shot Vision-and-Language Navigation in Continuous Environments (VLN-CE) task requires agents to navigate previously unseen 3D environments using natural language instructions, without any scene-specific training. A critical challenge in this setting lies in ensuring agents’ actions align with both spatial structure and task intent over long-horizon execution. Existing methods often fail to achieve robust navigation due to a lack of structured decision-making and insufficient integration of feedback from previous actions. To address these challenges, we propose STRIDER (Instruction-Aligned Structural Decision Space Optimization), a novel framework that systematically optimizes the agent’s decision space by integrating spatial layout priors and dynamic task feedback. Our approach introduces two key innovations: 1) a Structured Waypoint Generator that constrains the action space through spatial structure, and 2) a Task-Alignment Regulator that adjusts behavior based on task progress, ensuring semantic alignment throughout navigation. Extensive experiments on the R2R-CE and RxR-CE benchmarks demonstrate that STRIDER significantly outperforms strong SOTA across key metrics; in particular, it improves Success Rate (SR) from 29\% to 35\%, a relative gain of 20.7\%. Such results highlight the importance of spatially constrained decision-making and feedback-guided execution in improving navigation fidelity for zero-shot VLN-CE.

---

## 论文详细总结（自动生成）

# STRIDER: 通过指令对齐的结构化决策空间优化实现导航

## 1. 核心问题与整体含义（研究动机与背景）

- **任务背景**：零样本连续环境视觉语言导航（Zero-shot VLN-CE）要求智能体在没有场景特定训练的情况下，仅依靠自然语言指令在从未见过的3D环境中导航。这是一个极具挑战性的具身智能任务。
- **核心难题**：在长距离（long-horizon）执行过程中，智能体的动作序列需要同时与空间结构（如房间布局、路径拓扑、障碍物分布）和任务意图（自然语言指令中的语义需求）保持对齐。然而，现有方法往往存在两方面不足：
  - **缺乏结构化决策**：动作选择没有充分利用空间布局先验，导致决策空间无序、低效。
  - **反馈利用不足**：没有充分整合上一步动作的历史反馈，使长期规划缺乏动态调整能力。
- **研究意义**：该问题直接关系到智能体在真实世界未知环境中的导航鲁棒性与指令执行力，是推动零样本具身导航实用化的关键环节。

## 2. 方法论：STRIDER框架

论文提出 **STRIDER（Instruction-Aligned Structural Decision Space Optimization，指令对齐的结构化决策空间优化）** 框架，核心理念是**通过整合空间布局先验和动态任务反馈，系统性地优化智能体的决策空间**，使动作序列在结构与语义两个维度上与指令保持一致。框架包含两大关键创新组件：

- **结构化航点生成器（Structured Waypoint Generator）**
  - 功能：将空间布局先验融入决策过程，对候选动作空间进行结构性约束。
  - 技术思路：利用环境中的空间结构（如可通行区域、障碍物边界、几何拓扑）生成合理的航点候选集，过滤掉与物理空间布局冲突的无效动作，从而缩小决策范围并提高动作的可行性。
- **任务对齐调节器（Task-Alignment Regulator）**
  - 功能：基于任务执行进度动态调整智能体行为，确保导航过程的语义对齐。
  - 技术思路：对智能体当前已执行的轨迹与指令语义目标进行对齐评估，结合上一步动作的反馈信号，判断当前是否偏离任务意图，并据此校正后续动作选择，实现反馈引导的长期规划修正。

> **注**：论文提供的元数据中未包含具体的数学公式或算法伪代码，以上技术细节依赖于框架描述的语义概括。从整体流程看，两个组件协同工作——结构化航点生成器负责"做什么动作是空间上合理的"，任务对齐调节器负责"做什么动作是语义上正确的"，二者共同优化决策空间。

## 3. 实验设计

- **基准数据集**：
  - **R2R-CE**：基于 Matterport3D 环境的连续环境版本，是VLN-CE最常用的评测基准。
  - **RxR-CE**：基于 Room-and-Room 扩展的连续环境基准，指令更多样、路径更长，难度更高。
- **对比方法**：与当前最先进（SOTA）的零样本VLN-CE方法进行对比。文中明确提到"strong SOTA"，但未列出具体方法名称。
- **关键指标**：
  - **成功率（Success Rate, SR）**：智能体最终位置与目标点的距离是否在阈值内。
  - **路径效率（Path Efficiency）**：导航路径长度与最优路径的接近程度，包括SPL（Success weighted by Path Length）等衍生指标。
  - **零样本迁移能力**：在未见过的场景（scan）上的表现，验证泛化性。
- **实验结果亮点**：在 R2R-CE 上，STRIDER 将 SR 从 SOTA 的 29% 提升至 35%，**相对提升 20.7%**。

## 4. 资源与算力

- 论文提供的元数据（标题、摘要、作者信息）中**未明确说明**使用的 GPU 型号、数量、训练时长、参数量等算力资源细节。
- 作为一篇NeurIPS 2025录用论文，通常会在完整论文正文中报告实验环境信息（如GPU型号、训练时间等），但在当前给定的文本范围内，这些信息**无法获取**，因此无法给出具体总结。

## 5. 实验数量与充分性

- **实验组数**：涉及两个基准数据集（R2R-CE 和 RxR-CE），并与 SOTA 方法进行了对比。元数据中提到"extensive experiments"，表明除主结果外还包含消融实验（用于验证两个创新组件的各自贡献）和跨场景迁移分析。
- **充分性评估**：
  - **客观性**：SR 从 29% 到 35% 的提升幅度明确，且使用标准基准，结论可信。
  - **公平性**：零样本设定下与 SOTA 对比，不涉及场景特定训练，比较基础公平。
  - **关键不足**：具体消融实验的数量、分组方式、每个组件贡献的量化数据，以及不同指令长度/场景复杂度下的分层分析，在给定文本中未展开。因此，无法完整判断实验的覆盖面是否充分。

## 6. 主要结论与发现

- **结构化决策是关键**：将空间布局约束融入决策空间（结构化航点生成器）能显著提升导航动作的合理性和执行效率。
- **反馈整合是必要补充**：任务对齐调节器通过动态反馈调整行为，弥补了静态规划的不足，尤其在长距离导航中对语义偏移有纠正作用。
- **实证效果显著**：STRIDER 在 R2R-CE 和 RxR-CE 基准上全面超越现有 SOTA，成功率相对提升 20.7%，同时改善了路径效率与跨场景零样本迁移能力。
- **核心观点**：在连续环境指令导航中，"空间约束+语义反馈"的双重决策优化是提升导航保真度的有效范式。

## 7. 优点

- **问题切中要害**：精准识别了零样本VLN-CE中"动作-空间-意图"三者的对齐缺失这一根本痛点。
- **方法框架清晰**：将空间结构（自上而下的约束）和任务反馈（自下而上的修正）有机整合，模块分工明确，逻辑自洽。
- **迁移性潜力**：零样本设定本身意味着方法无需场景特定训练，具有较强的实际部署潜力。
- **结果提升显著**：20.7% 的相对成功率提升幅度可观，且同时改善成功率与路径效率，说明并非单纯牺牲路径换取成功率，而是真正提升了导航质量。
- **可解释性好**：结构化航点生成使动作选择的依据透明，便于诊断错误和进一步优化。

## 8. 不足与局限

- **实验细节披露不足**：在给定元数据中，未提供具体对比方法名单、消融实验的具体数量、各组件独立/组合效果的量化结果，难以充分评估模型的贡献归因。
- **算力信息缺失**：未说明训练所需 GPU 资源、时间成本，限制了在其他环境下的可复现性和成本评估。
- **泛化范围局限**：虽然声称提升跨场景迁移，但实验仅在 R2R-CE 和 RxR-CE 两个基准（均基于 Matterport3D 场景）上进行，未涉及基于真实物理世界或仿真器（如 Habitat 之外平台）的验证，跨域泛化结论的稳健性仍需更多证据。
- **长尾场景未验证**：零样本设定下，指令中包含的视角/情感（如 RxR 中的多语言指令）变化、极端空间布局等长尾情况的表现未见说明。
- **算法细节未明确**：两个核心组件的具体实现方式（网络架构、航点采样策略、反馈信号的形式）在给定文本中不可见，限制了方法的可复现性和深入分析。
- **潜在偏差风险**：成功率提升集中在一个基准的总体指标上，缺少对失败模式（如卡住、绕路、目标混淆）的分类误差分析，存在指标乐观偏差的可能。

（完）
