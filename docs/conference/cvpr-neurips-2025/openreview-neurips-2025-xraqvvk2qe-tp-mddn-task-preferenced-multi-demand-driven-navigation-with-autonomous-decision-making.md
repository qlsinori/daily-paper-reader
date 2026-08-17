---
title: "TP-MDDN: Task-Preferenced Multi-Demand-Driven Navigation with Autonomous Decision-Making"
title_zh: TP-MDDN：具有自主决策的任务偏好多需求驱动导航
authors: "Shanshan Li, Da Huang, Yu He, Yanwei Fu, Yu-Gang Jiang, Xiangyang Xue"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=xrAqVVk2qe"
tags: ["query:embodied-nav"]
score: 9.0
evidence: TP-MDDN面向物体目标导航，使用LLM指令分解与空间记忆实现多需求物体寻找
tldr: 日常生活中人们常需移动空间寻找满足需求的物体，现有需求驱动导航只能处理单一需求。本文提出任务偏好多需求驱动导航（TP-MDDN）基准，并设计AWMSystem自主决策系统，包含指令分解（BreakLLM）、目标选择（LocateLLM）和任务监控（StatusMLLM）模块，同时提出MASMap空间记忆表示。该系统能结合任务偏好对多子需求进行长期导航决策，显著提升了复杂室内场景下多目标物体寻找任务的效率，为具身导航提供了新范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 真实导航任务常涉及多个子需求和个性化选择，传统需求驱动导航只能处理单一需求。
method: 提出TP-MDDN基准与AWMSystem系统，包含LLM指令分解、目标选择、任务监控和MASMap空间记忆。
result: 实验表明AWMSystem在长期多需求导航中有效提升物体寻找与任务完成表现。
conclusion: 为具身智能体在复杂室内环境下的多目标导航提供了自主决策与空间记忆的综合解决方案。
---

## Abstract
In daily life, people often move through spaces to find objects that meet their needs, posing a key challenge in embodied AI. Traditional Demand-Driven Navigation (DDN) handles one need at a time but does not reflect the complexity of real-world tasks involving multiple needs and personal choices. To bridge this gap, we introduce Task-Preferenced Multi-Demand-Driven Navigation (TP-MDDN), a new benchmark for long-horizon navigation involving multiple sub-demands with explicit task preferences. To solve TP-MDDN, we propose AWMSystem, an autonomous decision-making system composed of three key modules: BreakLLM (instruction decomposition), LocateLLM (goal selection), and StatusMLLM (task monitoring). For spatial memory, we design MASMap, which combines 3D point cloud accumulation with 2D semantic mapping for accurate and efficient environmental understanding. Our Dual-Tempo action generation framework integrates zero-shot planning with policy-based fine control, and is further supported by an Adaptive Error Corrector that handles failure cases in real time. Experiments demonstrate that our approach outperforms state-of-the-art baselines in both perception accuracy and navigation robustness.

---

## 论文详细总结（自动生成）

# TP-MDDN：具有自主决策的任务偏好多需求驱动导航

## 1. 核心问题与整体含义
- **研究背景**：日常生活中，人们常需在空间中移动以寻找满足特定需求的物体，这是具身智能（Embodied AI）的关键挑战。
- **现有不足**：传统需求驱动导航（Demand-Driven Navigation, DDN）一次仅处理一个需求，无法反映真实任务中多需求、个性化选择等复杂情况。
- **本文贡献**：提出任务偏好多需求驱动导航（Task-Preferenced Multi-Demand-Driven Navigation, TP-MDDN）基准，用于长时程导航，其中包含多个子需求和明确的**任务偏好**，使具身智能体能更贴近真实场景地完成多目标物体寻找。

## 2. 方法论
- **总体框架**：提出 **AWMSystem**，一个自主决策系统，由三个关键模块组成：
  - **BreakLLM**：负责指令分解，将复杂任务拆分为多个子需求。
  - **LocateLLM**：负责目标选择，根据任务偏好确定下一步要寻找的物体。
  - **StatusMLLM**：负责任务监控，判断当前子任务是否完成、是否需要调整计划。
- **空间记忆**：设计 **MASMap**，融合三维点云累积与二维语义映射，实现精确且高效的环境理解与空间表征。
- **动作生成**：提出 **Dual-Tempo**（双节奏）动作生成框架，结合零样本规划（zero-shot planning）与基于策略的精细控制（policy-based fine control），兼顾全局决策和局部避障。
- **错误纠正**：配套 **Adaptive Error Corrector**，在实时导航中处理失败情况（如目标不可达、误检测等），增强系统鲁棒性。

## 3. 实验设计
- **基准**：论文提出新基准 **TP-MDDN**，包含多子需求与任务偏好的长时程导航任务。
- **对比方法**：与当前最先进的（State-of-the-Art）基线方法进行比较。
- **评估指标**：主要关注**感知准确性**和**导航鲁棒性**。
- **数据集/场景**：摘要中未明确列出具体的数据集名称或仿真平台，因此无法进一步说明场景细节。

## 4. 资源与算力
- 论文摘要和提供的元数据中**未提及**所使用的GPU型号、数量、训练时长、参数量等算力信息。
- 如需了解训练成本，需查阅论文全文的实验部分或附录。

## 5. 实验数量与充分性
- 摘要仅报告了“优于SOTA基线”的总体结论，**未给出**具体的实验数量、不同场景的对比、消融实验（例如对BreakLLM、LocateLLM、StatusMLLM、MASMap、Dual-Tempo、Adaptive Error Corrector等组件的单独验证）等细节。
- 因此，仅从摘要难以评估实验的充分性和公平性；但从系统设计的模块化程度来看，可以推测全文可能包含较丰富的消融研究和多场景对比。

## 6. 主要结论与发现
- AWMSystem在长期、多需求导航任务中能够有效提升物体寻找效率与任务完成表现。
- 在感知准确性和导航鲁棒性方面均优于现有最先进方法。
- 验证了将**任务偏好**纳入多需求导航的可行性，为具身导航提供了新范式。

## 7. 优点
- **问题新颖**：首次明确提出“任务偏好多需求驱动导航”，比单一需求DDN更贴近真实生活。
- **系统完整**：集成了LLM指令分解、目标选择、任务监控、多模态空间记忆、双节奏动作生成和自适应纠错，形成end-to-end的自主决策闭环。
- **空间记忆设计巧妙**：MASMap结合3D点云积累和2D语义图，兼顾几何精度和语义丰富度。
- **鲁棒性强**：Adaptive Error Corrector可实时应对导航失败案例，适合复杂室内环境。
- **基准价值**：提出的TP-MDDN基准可推动后续研究，填补该方向空白。

## 8. 不足与局限
- **信息不完整**：由于仅提供摘要，缺少具体实验结果、数据集细节、基线列表和量化指标，无法充分评估方法的实际性能和泛化能力。
- **算力未知**：未报告训练资源，可能影响复现性和实用性的判断。
- **对LLM的依赖**：BreakLLM、LocateLLM、StatusMLLM均基于大语言模型，可能带来推理延迟和计算开销，部署到实体机器人时存在挑战。
- **场景覆盖未知**：摘要未说明是否在真实场景或多种仿真环境中验证，仿真到真实的泛化问题尚待解决。
- **决策稳定性**：多模块级联可能产生误差累积，需要更多分析来验证在极端情况下的可靠性。

（完）
