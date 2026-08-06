---
title: "NavBench: Probing Multimodal Large Language Models for Embodied Navigation"
title_zh: NavBench：探测多模态大语言模型的具身导航能力
authors: "Yanyuan Qiao, Haodong Hong, Wenqi Lyu, Dong An, Siqi Zhang, Yutong Xie, Xinyu Wang, Qi Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=nf8PKQKtl2"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向多模态大模型在室内场景具身导航能力的评测基准
tldr: 该论文提出NavBench基准，用于零样本评估多模态大语言模型在具身导航任务中的能力。基准包含导航理解（3200道问答）和逐步执行（432个室内场景回合）两部分，并按空间、认知和执行复杂度分层。实验揭示了MLLM在全局指令对齐与局部行动推理上的表现差异，为具身导航模型评测提供了标准化工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态大语言模型在视觉语言任务上表现强，但其具身理解与行动能力缺乏系统评测。
method: 构建NavBench基准，包含导航理解问答与432回合室内场景逐步执行两大评测组件。
result: 评测揭示了MLLM在导航理解和执行中的强项与薄弱环节，支持跨模型对比。
conclusion: NavBench为具身导航场景下的多模态模型能力诊断提供了可复用的基准平台。
---

## Abstract
Multimodal Large Language Models (MLLMs) have demonstrated strong generalization in vision-language tasks, yet their ability to understand and act within embodied environments remains underexplored. We present NavBench, a benchmark to evaluate the embodied navigation capabilities of MLLMs under zero-shot settings. NavBench consists of two components: (1) navigation comprehension, assessed through three cognitively grounded tasks including global instruction alignment, temporal progress estimation, and local observation-action reasoning, covering 3,200 question-answer pairs; and (2) step-by-step execution in 432 episodes across 72 indoor scenes, stratified by spatial, cognitive, and execution complexity. To support real-world deployment, we introduce a pipeline that converts MLLMs' outputs into robotic actions. We evaluate both proprietary and open-source models, finding that GPT-4o performs well across tasks, while lighter open-source models succeed in simpler cases. Results also show that models with higher comprehension scores tend to achieve better execution performance. Providing map-based context improves decision accuracy, especially in medium-difficulty scenarios. However, most models struggle with temporal understanding, particularly in estimating progress during navigation, which may pose a key challenge.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- 多模态大语言模型（MLLMs）在视觉-语言任务上表现出很强的泛化能力，但其在具体物理/仿真环境中的“具身理解”与“行动决策”能力尚未被系统评估。
- 现有评测多集中在静态图片问答或纯语言推理，缺少对“感知-理解-规划-执行”这一完整导航链路的标准化测试。
- 论文提出 **NavBench**，旨在零样本（zero-shot）条件下衡量 MLLMs 的具身导航能力，为模型诊断、对比和落地提供统一基准。

## 2. 论文提出的方法论

- **核心思想**：将导航能力拆解为“理解”与“执行”两个层次，分别设计评测任务，并建立从自然语言输出到机器人动作的转换管道。
- **导航理解组件**：包含三类认知任务：
  - **全局指令对齐**：检验模型能否将高层指令与场景/路径信息正确关联；
  - **时间进度估计**：检验模型对导航过程中已走路径/剩余进度的时序判断能力；
  - **局部观测-动作推理**：检验模型基于当前局部观察选择下一步动作的能力。
  - 共涵盖 **3,200 个问答对**。
- **逐步执行组件**：在 **72 个室内场景**中设置 **432 个回合（episodes）**，要求 MLLMs 进行逐步决策，并按空间复杂度、认知复杂度和执行复杂度分层设计，以区分不同难度下的表现。
- **动作转换管道**：将 MLLMs 输出的文本/推理结果解析为可执行的机器人动作指令，支撑真实或仿真环境中的部署。

## 3. 实验设计

- **基准内容**：NavBench 本身即为评测基准，包含理解测试集与执行测试集。
- **数据集/场景**：72 个室内场景，432 个导航回合，3,200 个理解问答对。
- **对比方法**：评估了专有模型（如 GPT-4o）与开源模型（较轻量的开源模型）的表现。
- **其他实验分析**：
  - 对比不同模型在理解分数与执行成功率之间的关系；
  - 分析是否提供地图上下文对决策准确率的影响（尤其在中等难度场景下）；
  - 检验模型在时间进度估计任务上的薄弱情况。

## 4. 资源与算力

- 原文摘要和元数据中 **未明确说明** 使用的 GPU 型号、数量或训练/推理时长。
- 推测其作为评测基准，主要消耗在模型推理（inference）上，而非训练；但具体算力细节缺失。

## 5. 实验数量与充分性

- **实验数量**：理解任务 3,200 个问答对，执行任务 432 个回合，覆盖 72 个室内场景，样本量较为可观。
- **充分性评估**：
  - 从任务分层看，实验考虑了空间、认知、执行多维复杂度，设计较全面；
  - 对比了专有和开源两类模型，覆盖不同规模；
  - 但摘要中未提及消融实验、不同提示策略或动作管道变体的对比，因此对于“管道设计有效性”“任务分层合理性”等维度的验证有待补充。
- **客观公平**：基准公开（OpenReview 可获取），任务定义分层清晰，支持跨模型复现，整体设计具备公平比较的基础。

## 6. 论文的主要结论与发现

- **GPT-4o** 在各类任务上表现较好，而较轻盈的开源模型只在简单情形下表现良好。
- 模型在导航理解上的得分越高，其执行成功率也越高——理解能力与执行能力呈正相关。
- **提供地图上下文**能显著提升决策准确率，尤其对中等难度场景帮助最大。
- 多数模型在**时间进度估计**上存在显著短板，即对“导航过程中已走多远/还剩多少”这类时序推理能力不足，是当前 MLLMs 的共性难题。

## 7. 优点

- **两方面评测结合**：同时覆盖静态理解与动态执行，更贴近真实导航任务。
- **认知分层设计**：按空间、认知、执行复杂度分层，便于定位模型的具体能力边界。
- **零样本设置**：免去任务微调，直接评测模型的泛化能力，具有实际参考价值。
- **落地导向**：提供从 MLLM 输出到机器人动作的转换管道，有利于应用到具身智能系统。
- **标准化基准**：提供了可复现的评测工具，推动后续模型对比和改进。

## 8. 不足与局限

- **算力信息缺失**：未报告推理/训练所需的硬件资源与时长，影响复现成本评估。
- **实验覆盖有限**：仅涉及室内场景，未覆盖室外、动态障碍物、多智能体等复杂环境。
- **时间进度估计能力普遍较差**：但对这一短板的原因分析（如是否因训练数据缺乏时序知识、评测任务设计不当等）并未在摘要中体现。
- **地图上下文的引入方式**：如何提供地图、是否与模型输入兼容等问题尚未详细说明。
- **未报告消融与敏感性分析**：例如动作转换管道的误差、任务分层阈值的设置依据，以及不同提示模板对结果的影响。
- **模型范围**：虽然对比了专有和开源模型，但开源模型的种类和规模代表性有限，难以全面反映开源社区最新水平。

（完）
