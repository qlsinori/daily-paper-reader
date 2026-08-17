---
title: "ThinkAct: Vision-Language-Action Reasoning via Reinforced Visual Latent Planning"
title_zh: "ThinkAct: 通过强化视觉潜在规划进行视觉-语言-动作推理"
authors: "Chi-Pin Huang, Yueh-Hua Wu, Min-Hung Chen, Yu-Chiang Frank Wang, Fu-En Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=72UR53jN7T"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 多模态指令推理与长程规划，面向具身动作执行
tldr: 针对视觉-语言-动作模型端到端直接映射导致长程规划能力不足的问题，论文提出双系统框架ThinkAct，以强化视觉潜在规划连接高维推理与低层动作执行。该方法用目标完成度和轨迹一致性指导多模态大模型生成具身推理计划，实验表明在长程任务和复杂变化中表现更优，可迁移至指令导航等具身任务。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 端到端VLA模型缺乏显式推理，多步规划和任务泛化能力受限。
method: 提出双系统框架，利用强化视觉潜在规划训练多模态LLM生成推理计划。
result: 在长程与复杂任务上提升规划一致性和成功率。
conclusion: 为语言指导下的具身决策提供可泛化的推理-执行桥接方案。
---

## Abstract
Vision-language-action (VLA) reasoning tasks require agents to interpret multimodal instructions, perform long-horizon planning, and act adaptively in dynamic environments. Existing approaches typically train VLA models in an end-to-end fashion, directly mapping inputs to actions without explicit reasoning, which hinders their ability to plan over multiple steps or adapt to complex task variations. In this paper, we propose ThinkAct, a dual-system framework that bridges high-level reasoning with low-level action execution via reinforced visual latent planning. ThinkAct trains a multimodal LLM to generate embodied reasoning plans guided by reinforcing action-aligned visual rewards based on goal completion and trajectory consistency. These reasoning plans are compressed into a visual plan latent that conditions a downstream action model for robust action execution on target environments. Extensive experiments on embodied reasoning and robot manipulation benchmarks demonstrate that ThinkAct enables few-shot adaptation, long-horizon planning, and self-correction behaviors in complex embodied AI tasks.

---

## 论文详细总结（自动生成）

# 论文总结：ThinkAct: 通过强化视觉潜在规划进行视觉-语言-动作推理

## 1. 论文的核心问题与整体含义

- **研究动机**：视觉-语言-动作（VLA）推理任务要求智能体理解多模态指令、执行长时间跨度的规划，并在动态环境中自适应地采取行动。然而，现有VLA模型通常采用端到端训练方式，将输入直接映射为动作，缺乏显式推理过程，导致其在多步规划、复杂任务变体适应上能力受限。
- **核心问题**：如何在高维推理与底层动作执行之间建立有效桥梁，使VLA模型能够显式地进行规划推理，同时保持对动态环境的鲁棒执行能力。
- **整体含义**：该研究旨在为语言指导下的具身决策提供一种可泛化的“推理-执行”桥接方案，填补端到端VLA模型在显式推理能力上的空白。

## 2. 论文提出的方法论

- **核心思想**：提出双系统（dual-system）框架 **ThinkAct**，将高维推理与低层动作执行解耦，通过“强化视觉潜在规划”连接二者。
- **关键技术细节**：
  - 训练一个多模态大语言模型（multimodal LLM）生成具身推理计划。
  - 通过基于**目标完成度**与**轨迹一致性**的强化信号（action-aligned visual rewards）指导推理计划的生成，使其与可执行动作对齐。
  - 将生成的推理计划压缩为**视觉计划潜在变量（visual plan latent）**，作为下游动作模型的条件输入，从而在目标环境中实现鲁棒的动作执行。
- **算法流程（文字说明）**：
  1. 输入多模态指令与环境观测；
  2. 多模态LLM生成高层推理计划（语言/视觉形式）；
  3. 对计划施加强化奖励信号（评估目标完成度与轨迹一致性）；
  4. 计划被编码为视觉潜在变量；
  5. 下游动作模型以该潜在变量为条件，输出具体执行动作。

## 3. 实验设计

- **数据集与场景**：论文在**具身推理**与**机器人操作**基准（embodied reasoning and robot manipulation benchmarks）上进行实验。
- **Benchmark**：涉及长程任务、复杂任务变化、自纠错（self-correction）场景，以及指令导航等具身任务。
- **对比方法**：论文材料中未逐一列出对比的具体基线方法，但可推断其与标准端到端VLA模型进行对比，以验证显式推理带来的增益。

## 4. 资源与算力

- 论文材料中**未明确说明**使用的GPU型号、数量、训练时长等硬件与算力资源信息。
- 这一点属于信息缺失，无法从现有材料中评估训练成本或复现难度。

## 5. 实验数量与充分性

- 材料中概括性地报告了在多个具身任务上的实验结果，涵盖少样本适应、长程规划、自纠错行为等维度。
- 由于提供的材料仅为论文元数据与摘要，**未列出具体实验组数、消融研究细节或统计显著性检验**，因此无法完全评估实验的量化充分性。
- 从描述看，实验覆盖了多种复杂任务场景，但缺少对失败案例分析、超参数敏感性等更深入的实验细节。

## 6. 论文的主要结论与发现

- ThinkAct在**长程任务与复杂任务变化**中显著提升了规划一致性与任务成功率。
- 该方法支持**少样本适应**（few-shot adaptation）、**长程规划**（long-horizon planning）和**自纠错行为**（self-correction）。
- 推理计划与动作执行的解耦设计能够更好地泛化到指令导航等下游具身任务。
- 总体结论：为语言指导下的具身决策提供了一种可泛化的推理-执行桥接方案。

## 7. 优点

- **方法创新性**：首次将“强化视觉潜在规划”作为连接高层推理与底层动作的桥梁，设计新颖，逻辑自洽。
- **双系统设计**：符合认知科学中的双系统理论（快速直觉系统 vs. 慢速推理系统），在具身AI中具有理论深度。
- **强化信号对齐**：通过目标完成度与轨迹一致性作为奖励，确保推理计划与真实可执行动作对齐，具有工程实用性。
- **通用性与可迁移性**：方法在操作任务之外还可应用到指令导航等具身任务，表明其具有一定的跨任务泛化能力。

## 8. 不足与局限

- **实验细节不透明**：材料中未提供具体的数据集名称（如具体机器人操作基准名称）、基线方法列表、消融实验设计等，难以独立验证其声明。
- **算力信息缺失**：未报告训练所需GPU资源与时长，不利于研究者评估复现成本。
- **潜在偏差风险**：奖励信号仅依赖目标完成度和轨迹一致性，在极为复杂或开放性的任务中可能无法充分刻画推理质量；对失败模式的鲁棒性也未在材料中讨论。
- **应用限制**：方法依赖多模态LLM的推理能力与下游动作模型的匹配精度，在实际物理机器人系统中可能面临推理延迟、sim-to-real gap等工程挑战。
- **材料完整性限制**：本总结基于的仅为论文元数据与摘要，未包含全文实验细节，因此上述不足的某些方面可能是信息缺失而非论文实际缺陷。

---

（完）
