---
title: "ThinkAct: Vision-Language-Action Reasoning via Reinforced Visual Latent Planning"
title_zh: ThinkAct：基于强化视觉潜在规划的视觉-语言-动作推理
authors: "Chi-Pin Huang, Yueh-Hua Wu, Min-Hung Chen, Yu-Chiang Frank Wang, Fu-En Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=72UR53jN7T"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 基于强化视觉潜在规划的具身指令跟随，可迁移至导航任务
tldr: 端到端视觉-语言-动作（VLA）模型缺乏显式推理，难以进行多步规划与适应复杂任务变化。本文提出ThinkAct双系统框架，通过强化视觉潜在规划训练多模态LLM生成具身推理计划，并以目标完成度和轨迹一致性作为奖励。该方法在长时程指令跟随与复杂任务适应上表现更好，为VLA推理提供了一条显式规划路径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 端到端VLA模型直接映射输入到动作，缺乏显式推理，导致长时程规划能力弱。
method: 提出双系统框架ThinkAct，训练多模态LLM生成推理计划，并用目标完成和轨迹一致性奖励强化。
result: 实验表明ThinkAct在长时程指令跟随和复杂任务适应性上优于端到端基线。
conclusion: 显式推理规划可显著提升VLA模型在多步任务中的表现与泛化能力。
---

## Abstract
Vision-language-action (VLA) reasoning tasks require agents to interpret multimodal instructions, perform long-horizon planning, and act adaptively in dynamic environments. Existing approaches typically train VLA models in an end-to-end fashion, directly mapping inputs to actions without explicit reasoning, which hinders their ability to plan over multiple steps or adapt to complex task variations. In this paper, we propose ThinkAct, a dual-system framework that bridges high-level reasoning with low-level action execution via reinforced visual latent planning. ThinkAct trains a multimodal LLM to generate embodied reasoning plans guided by reinforcing action-aligned visual rewards based on goal completion and trajectory consistency. These reasoning plans are compressed into a visual plan latent that conditions a downstream action model for robust action execution on target environments. Extensive experiments on embodied reasoning and robot manipulation benchmarks demonstrate that ThinkAct enables few-shot adaptation, long-horizon planning, and self-correction behaviors in complex embodied AI tasks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：端到端视觉-语言-动作（VLA）模型直接将多模态输入映射为动作，缺乏显式推理能力，导致在多步长时程规划、环境动态变化和复杂任务变体下表现不佳。
- **核心问题**：如何为VLA模型注入显式的高层推理能力，同时保持低层动作执行的高效性和鲁棒性。
- **整体含义**：该工作提出将“推理”与“执行”解耦的双系统框架，探索了一条通过可学习视觉潜在规划连接高层推理与低层控制的路径，为具身智能体的可解释性和泛化性提供了新思路。

## 2. 方法论

- **核心思想**：提出 **ThinkAct**，一种双系统框架，由“推理系统”（多模态大语言模型）和“执行系统”（下游动作模型）组成。推理系统生成“具身推理计划”，执行系统将其转化为实际动作。
- **关键技术细节**：
  - 使用**强化视觉潜在规划**训练多模态LLM生成推理计划。
  - 奖励函数基于两个信号：**目标完成度**（任务是否达成）和**轨迹一致性**（计划执行轨迹与推理计划是否一致）。
  - 推理计划被压缩为**视觉计划潜在变量（visual plan latent）**，用于条件化下游动作模型，确保推理信息有效传递给控制层。
- **算法流程（文字说明）**：
  1. 输入多模态指令与观测。
  2. 多模态LLM生成高层推理计划（自然语言或结构化的中间表示）。
  3. 将计划编码为视觉潜在变量。
  4. 下游动作模型以该潜在变量为条件，输出具体动作序列。
  5. 通过强化学习优化推理模型，奖励来自任务成功率和执行一致性。

## 3. 实验设计

- **Benchmark / 场景**：
  - **具身推理任务**（embodied reasoning）和**机器人操作任务**（robot manipulation）。
  - 具体数据集名称在提供内容中未详述，但从摘要可知涵盖长时程、多步指令跟随场景。
- **对比方法**：
  - 主要与**端到端VLA基线**进行比较，验证显式推理机制的有效性。
- **评估指标**：
  - 任务完成率、少样本适应能力、长时程规划成功率、自我纠正行为出现频率等。

## 4. 资源与算力

- 论文提供的元数据与摘要中**未明确说明**所使用的GPU型号、数量、训练时长或总计算量。
- 无法从现有信息中推断训练开销的具体数值。

## 5. 实验数量与充分性

- 摘要提到在“大量实验”中验证了方法，但**具体实验组数、消融设置、统计显著性检验等细节未提供**。
- 从可获取的信息看，实验覆盖了至少两个主要场景（具身推理和机器人操作），展示了少样本适应、长时程规划与自我纠正等能力，但**无法全面评估其完整性、公平性和统计可靠性**。
- 总体判断：方法的验证方向明确，但证据细节呈现不足。

## 6. 主要结论与发现

- 显式推理规划（ThinkAct）显著提升了VLA模型在长时程指令跟随和复杂任务适应性上的表现。
- 推理计划通过视觉潜在变量传递，有助于下游动作模型在不同目标环境中的鲁棒执行。
- 该方法展现出**少样本适应**、**长时程规划**和**自我纠正**能力，这些是关键的实际部署能力。
- 与端到端基线相比，ThinkAct在复杂任务上具有明确优势。

## 7. 优点

- **双系统解耦设计**：将“思考”和“行动”分离，兼具可解释性与执行效率。
- **强化学习引导推理**：直接优化任务目标而非仅仅模仿语言输出，推理计划更具任务对齐性。
- **视觉潜在计划压缩**：将高层推理与低层控制连接起来，减少信息传递损失。
- **方法通用性**：适用于多种具身智能任务，具备跨任务迁移潜力。

## 8. 不足与局限

- **实验细节信息不充分**：缺少数据集来源、任务数量、消融实验设计等详细描述，影响客观评估。
- **算力信息缺失**：未说明训练所需的计算资源，难以评估可复现性。
- **应用限制**：推理过程依赖多模态LLM，可能存在延迟开销，实时性难以保证。
- **评估偏差风险**：如果仅与端到端基线对比，可能无法体现与已有具身规划方法（如RAP、SayCan等）的相对优势。
- **实际部署中鲁棒性未充分验证**：环境动态变化下的行为安全性和泛化边界尚不清楚。

（完）
