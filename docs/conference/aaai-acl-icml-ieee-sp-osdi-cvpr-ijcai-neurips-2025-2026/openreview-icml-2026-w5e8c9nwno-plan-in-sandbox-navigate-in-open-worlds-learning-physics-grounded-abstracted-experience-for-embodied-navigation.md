---
title: "Plan in Sandbox, Navigate in Open Worlds: Learning Physics-Grounded Abstracted Experience for Embodied Navigation"
title_zh: 在沙盒中规划，在开放世界中导航：学习物理接地抽象经验用于具身导航
authors: "Zhixuan Shen, Jiawei Du, Ziyu Guo, Han Luo, Lilan Peng, Joey Tianyi Zhou, Haonan Luo, Tianrui Li"
date: 2026-04-30
pdf: "https://openreview.net/pdf/27299763732e881621b2b6f37e47e47722f2e575.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 提出在物理语义抽象中学习具身导航策略，提升开放世界迁移能力。
tldr: 具身导航智能体受限于视觉与控制数据稀缺，且照片级仿真训练的策略难以迁移到开放世界。该文提出SAGE框架，让智能体在基于物理的语义抽象环境中进行规划预演，借鉴人类心智模拟能力。在简化但物理一致的环境中学习抽象经验，可显著增强开放世界的导航泛化性能，为低成本获取可迁移导航策略提供新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 仿真到现实的迁移受限，需要更抽象、可迁移的训练环境。
method: 构建物理语义抽象的沙盒环境，让智能体在其中预演规划并学习经验。
result: 实验显示该方法在开放世界具身导航任务上提升策略泛化能力。
conclusion: 验证了基于物理抽象训练替代逼真仿真的可行性，拓展了具身导航学习范式。
---

## Abstract
Vision-Language Models (VLMs) have demonstrated exceptional general reasoning capabilities. However, their performance in embodied navigation remains hindered by a scarcity of aligned open-world vision and robot control data. Despite simulators providing a cost-effective alternative for data collection, the inherent reliance on photorealistic simulations often limits the transferability of learned policies. To this end, we propose ***S**andbox-**A**bstracted **G**rounded **E**xperience* (***SAGE***), a framework that enables agents to learn within a physics-grounded semantic abstraction rather than a photorealistic simulation, mimicking the human capacity for mental simulation where plans are rehearsed in simplified physics abstractions before execution. *SAGE* operates via three synergistic phases: (1) *Genesis*: constructing diverse, physics-constrained semantic environments to bootstrap experience; (2) *Evolution*: distilling experiences through Reinforcement Learning (RL), utilizing a novel asymmetric adaptive clipping mechanism to stabilize updates; (3) *Navigation*: bridging the abstract policy to open-world control. We demonstrate that *SAGE* significantly improves planner-assisted embodied navigation, achieving a 53.21% LLM-Match Success Rate on A-EQA (+9.7% over baseline), while showing encouraging transfer to physical indoor robot deployment. Project page is available at: <https://frankzxshen.github.io/SAGE>.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：视觉-语言模型（VLM）在通用推理任务中表现出色，但在具身导航任务中性能受限，主要原因在于**开放的视觉数据与机器人控制数据之间存在严重的稀缺性与对齐问题**。
- **现有方案困境**：仿真器虽然提供了低成本的数据采集途径，但主流方法依赖**照片级真实感仿真**，而这类仿真环境训练出的策略往往**难以迁移到开放世界**中，存在严重的Sim-to-Real泛化鸿沟。
- **研究动机**：人类在真实执行复杂动作之前，通常会在头脑中进行**心智模拟（mental simulation）**，即在简化的物理抽象中预演计划。该文受此启发，提出一个关键问题：**能否让具身智能体在简化的、物理一致的抽象环境中学习导航经验，而非依赖逼真仿真，从而获得更强的开放世界迁移能力？**

## 2. 方法论：SAGE框架

- **核心思想**：提出 **Sandbox-Abstracted Grounded Experience（SAGE）** 框架，让智能体在**物理接地（physics-grounded）的语义抽象环境**而非照片级仿真环境中学习导航策略。这一范式跳出了"仿真越逼真越好"的传统思路，转而模仿人类"在简化心智模型中预演计划"的认知机制。
- **三阶段协同流程**：
  - **阶段一：Genesis（环境生成）**：构建多样化、受物理约束的语义环境。该环境不追求视觉逼真度，而是保留物理规律（如碰撞、重力、可达性）和语义信息（如物体类别、空间关系），用于低成本地引导经验生成。
  - **阶段二：Evolution（经验蒸馏）**：利用强化学习（RL）在上述抽象环境中蒸馏导航经验，其中引入了一种**非对称自适应裁剪机制（asymmetric adaptive clipping mechanism）** 来稳定策略更新，避免训练震荡。
  - **阶段三：Navigation（策略迁移）**：将抽象环境中习得的策略桥接至开放世界的真实控制，实现从语义抽象到物理世界控制的迁移。

## 3. 实验设计

- **主要Benchmark**：使用了 **A-EQA**（具身问答导航任务）作为核心评测基准。
- **核心指标**：**LLM-Match Success Rate**（大语言模型匹配成功率），即导航结果与LLM给定正确答案之间的匹配程度。
- **主要结果**：SAGE在A-EQA上达到 **53.21%** 的LLM-Match成功率，相比基线提升 **+9.7%**。
- **迁移实验**：除仿真benchmark外，还进行了**物理室内机器人部署实验**，验证策略对真实环境的迁移能力。
- **对比方法**：从摘要推断，对比了基于照片级仿真训练的基线方法，以及可能的VLM具身导航基线。具体对比方法列表在元数据中未细化。

## 4. 资源与算力

- 原始论文中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。
- 仅能推断其核心训练开销来自：阶段二的强化学习（RL）策略训练以及VLM相关模块的推理/微调，但由于缺少具体配置说明，无法给出量化的算力估计。

## 5. 实验数量与充分性评估

- **已涵盖的实验维度**：
  1. A-EQA benchmark上与基线方法的性能对比（主实验）；
  2. 物理机器人真实部署实验（跨域迁移验证）；
  3. 框架本身包含三阶段设计，暗示存在对三阶段设计有效性的验证。
- **充分性判断**：从现有摘要信息来看，论文展示了**主实验和真实世界迁移实验**，但其公开内容未提及系统性的消融实验（如移除物理接地、移除自适应裁剪机制、不同抽象粒度的影响等）。如果正文中包含这些消融实验，会显著增强结论的可信度，但目前从提取文本中无法确认。整体而言，关键实验证据存在，但**实验充分性在元数据层面无法完全验证**。需要注意的是：
  - 主实验效果提升幅度明确（+9.7%）；
  - 物理部署实验是加分项；
  - 但缺少多场景、多任务维度的泛化验证细节。

## 6. 主要结论与发现

- **核心结论**：SAGE框架验证了**用物理语义抽象环境替代照片级仿真进行具身导航训练的可行性**，表明"抽象但物理一致"的训练环境能够有效提高策略的开放世界泛化能力。
- **关键发现**：
  1. 基于物理抽象的RL经验蒸馏可显著提升VLM具身导航的策略质量（+9.7%）；
  2. 学习到的抽象策略能够成功迁移到物理真实机器人上，而不仅仅是仿真环境中的数值提升；
  3. 该方法为具身导航学习提供了**低成本、高泛化**的新范式，拓宽了训练环境设计的可能性空间。

## 7. 方法亮点与优势

- **范式创新**：跳出"照片级真实感仿真"的传统框架，提出"沙盒抽象"式训练理念，与人类心智模拟机制对齐，思想新颖。
- **成本优势**：在简化环境中训练，数据采集与计算开销远低于构建照片级仿真环境，具有实际应用潜力。
- **三阶段设计清晰**：环境生成→经验蒸馏→策略迁移的拆解逻辑清晰，模块化程度高。
- **技术贡献**：非对称自适应裁剪机制作为RL更新策略的改进，在稳定训练方面提供了具体的技术增量。
- **验证完整度**：同时包含仿真benchmark和物理机器人部署验证，增强了可信度和说服力。

## 8. 不足与局限

- **实验细节公开不足**：从当前提取内容看，数据集的具体规模、环境类型多样性、对比方法的具体配置等细节未充分披露，难以全面复现。
- **消融实验不明确**：未明确展示各设计组件（如物理接地的作用、非对称裁剪机制的增益）的独立贡献。
- **泛化范围有限**：仅在一个A-EQA benchmark和一个物理部署场景上验证，结论向更广泛具身任务（如操作、人机交互）推广时需要更多证据支撑。
- **可靠性偏差风险**：LLM-Match指标的语义覆盖程度未说明，可能带来评测偏差；物理部署实验的具体场景复杂度、任务难度未知，可能带来评估乐观偏差。
- **算力信息缺失**：未报告训练成本，不利于同行评估方法的实际资源门槛和可复现性。

---

（完）
