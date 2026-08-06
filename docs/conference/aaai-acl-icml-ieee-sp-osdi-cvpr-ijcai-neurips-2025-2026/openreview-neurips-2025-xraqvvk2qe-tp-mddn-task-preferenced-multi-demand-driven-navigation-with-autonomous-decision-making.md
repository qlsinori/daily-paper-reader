---
title: "TP-MDDN: Task-Preferenced Multi-Demand-Driven Navigation with Autonomous Decision-Making"
title_zh: TP-MDDN：任务偏好的多需求驱动导航与自主决策
authors: "Shanshan Li, Da Huang, Yu He, Yanwei Fu, Yu-Gang Jiang, Xiangyang Xue"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=xrAqVVk2qe"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 空间寻物; 多需求导航; 空间记忆; 具身AI
tldr: 现实中的移动往往是带着个人偏好去寻找多种所需物品，传统需求驱动导航一次只处理一个目标。为弥补这一差距，本文提出任务偏好的多需求驱动导航基准TP-MDDN，并构建自主决策系统AWMSystem，通过BreakLLM指令分解、LocateLLM目标选择和StatusMLLM任务监控完成长时导航，同时设计MASMap空间记忆来支持目标定位，提升了具身导航处理复杂多目标任务的能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 日常导航常需同时寻找多个符合需求的物体，传统单一需求导航无法反映真实任务的复杂性。
method: 提出AWMSystem，由指令分解、目标选择、任务监控三个LLM模块构成，并配合MASMap空间记忆实现多目标长时导航。
result: 构建了TP-MDDN基准和自主决策系统，能够处理带显式任务偏好的多子需求导航任务，扩展了物体目标导航的能力。
conclusion: 强调多需求与个人偏好在具身导航中的重要性，为未来复杂目标导航研究提供了新基准和方法。
---

## Abstract
In daily life, people often move through spaces to find objects that meet their needs, posing a key challenge in embodied AI. Traditional Demand-Driven Navigation (DDN) handles one need at a time but does not reflect the complexity of real-world tasks involving multiple needs and personal choices. To bridge this gap, we introduce Task-Preferenced Multi-Demand-Driven Navigation (TP-MDDN), a new benchmark for long-horizon navigation involving multiple sub-demands with explicit task preferences. To solve TP-MDDN, we propose AWMSystem, an autonomous decision-making system composed of three key modules: BreakLLM (instruction decomposition), LocateLLM (goal selection), and StatusMLLM (task monitoring). For spatial memory, we design MASMap, which combines 3D point cloud accumulation with 2D semantic mapping for accurate and efficient environmental understanding. Our Dual-Tempo action generation framework integrates zero-shot planning with policy-based fine control, and is further supported by an Adaptive Error Corrector that handles failure cases in real time. Experiments demonstrate that our approach outperforms state-of-the-art baselines in both perception accuracy and navigation robustness.

---

## 论文详细总结（自动生成）

# TP-MDDN：任务偏好的多需求驱动导航与自主决策 — 论文总结

## 1. 核心问题与整体含义
- **研究背景**：日常生活中，人们经常需要在空间中同时寻找多个符合个人需求的物体，这是具身智能的关键挑战之一。
- **传统方法不足**：传统 Demand-Driven Navigation（DDN）一次只处理一个需求，难以反映真实任务中“多需求 + 个人偏好”的复杂性。
- **本文目标**：提出 **TP-MDDN**（Task-Preferenced Multi-Demand-Driven Navigation）新基准，并构建自主决策系统 **AWMSystem**，将具身导航从单一目标扩展到带显式偏好的多子需求长时导航。

## 2. 提出的方法论
- **核心思想**：将复杂导航任务分解为“理解指令 → 选择目标 → 监控进度”等多个可独立处理的环节，并利用大语言模型/多模态大模型赋予系统自主决策能力。
- **AWMSystem 三大模块**：
  - **BreakLLM**：负责指令分解，将高层任务拆解为多个带偏好的子需求。
  - **LocateLLM**：负责目标选择，根据当前任务和空间记忆决定下一步要导航的目标。
  - **StatusMLLM**：负责任务监控，判断当前子目标是否完成、是否出错以及整体任务进度。
- **空间记忆 — MASMap**：
  - 结合 **3D 点云累积** 与 **2D 语义映射**，构建准确且高效的环境表示。
  - 用于支持目标定位与长期导航中的空间推理。
- **动作生成框架 — Dual-Tempo**：
  - 融合 **零样本规划**（全局、高层决策）与 **基于策略的精细控制**（局部、低层执行）。
- **自适应错误校正器（Adaptive Error Corrector）**：
  - 实时处理导航过程中的失败情况，提高系统鲁棒性。
- **算法流程（文字描述）**：
  1. 接收包含任务偏好的自然语言指令。
  2. BreakLLM 将指令分解为多个子需求。
  3. LocateLLM 结合 MASMap 中的空间记忆选择最优下一个目标。
  4. 通过 Dual-Tempo 框架执行动作，StatusMLLM 持续监控状态。
  5. 若发生错误或异常，自适应错误校正器介入修正。
  6. 重复 3–5 直到所有子需求完成。

## 3. 实验设计
- **基准（Benchmark）**：本文提出了 **TP-MDDN** 基准，专门用于评估带任务偏好的多需求长时导航。
- **评估维度**：摘要中提到比较了 **感知准确性** 和 **导航鲁棒性** 两个重要方面。
- **对比方法**：与 **state-of-the-art 基线** 进行了对比，但提供的文本未列出具体基线名称。
- **数据集/场景**：文本未明确说明使用的具体模拟环境或真实场景数据集（例如 Habitat、Matterport3D 等未提及），仅从标签可推测涉及“空间寻物、多需求导航、具身AI”。

## 4. 资源与算力
- **未明确说明**：提供的文本（标题、元数据、摘要）中完全没有提及 GPU 型号、数量、训练时长等计算资源信息。
- 因此，无法对本文的算力需求进行任何定量总结。

## 5. 实验数量与充分性
- **实验数量**：摘要仅指出“实验表明本方法在感知准确性和导航鲁棒性上优于 SOTA 基线”，但**没有说明具体做了多少组实验**（如不同场景对比、消融研究、参数敏感性等）。
- **充分性评估**：由于缺乏细节，无法判断实验是否充分、客观、公平。但从元数据来看，该论文被 NeurIPS 2025 接收，说明其研究质量得到认可，理想情况下应包含完整的实验章节，只是本提取文本未覆盖。

## 6. 主要结论
- **多需求与个人偏好** 是具身导航中不可忽视的现实特性，传统单需求范式不够充分。
- 提出的 **TP-MDDN 基准** 和 **AWMSystem 自主决策系统** 能够有效处理带显式任务偏好的多子需求导航任务。
- 系统在感知准确性和导航鲁棒性方面**超越现有最先进方法**，扩展了物体目标导航的边界。

## 7. 优点
- **问题新颖**：从“单需求导航”扩展到“多需求 + 任务偏好”的长时导航，更贴近实际应用。
- **模块化设计**：BreakLLM、LocateLLM、StatusMLLM 分工明确，结合空间记忆与动作生成，系统可解释性强、易于扩展。
- **空间记忆设计**：3D 点云 + 2D 语义映射的 MASMap，兼顾几何精细度和语义理解效率。
- **鲁棒性机制**：自适应错误校正器为长时间任务提供了实时容错能力。
- **基准贡献**：提供了 TP-MDDN 新基准，有利于后续研究者在统一标准下开展相关工作。

## 8. 不足与局限
- **信息局限**：本总结仅基于论文摘要和元数据，缺少方法细节、实验数据和可视化结果，无法做全面技术评价。
- **潜在风险**：
  - 系统高度依赖 LLM/MLLM 的分解与定位能力，在罕见场景或模糊偏好下可能表现不稳定。
  - MASMap 的长期记忆累积可能面临漂移或存储开销问题，文本未讨论该问题。
  - 自适应错误校正器的实时性、计算成本以及失效边界未在摘要中说明。
- **实验覆盖不足**：未明确说明测试环境的多样性、基线选择、消融实验等，因此难以评估其泛化能力。
- **应用限制**：从任务描述来看，主要面向室内物体寻物场景；对室外大范围、动态环境或多智能体协作等场景的适用性未提及。

（完）
