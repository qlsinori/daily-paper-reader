---
title: "PhysVLM-AVR: Active Visual Reasoning for Multimodal Large Language Models in Physical Environments"
title_zh: PhysVLM-AVR：物理环境中多模态大语言模型的主动视觉推理
authors: "Weijie Zhou, Xuantang Xiong, Yi Peng, Manli Tao, Chaoyang Zhao, Honghui Dong, Ming Tang, Jinqiao Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=AYDMNzpJPv"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 在具身环境中通过主动探索和闭环感知-行动进行推理，与具身导航智能体相关
tldr: 多模态大语言模型通常在静态被动设置中进行视觉推理，难以应对遮挡或视野受限的真实环境。本文提出主动视觉推理（AVR）任务，让智能体通过移动、观察和操作在部分可观察环境中闭环感知-推理-行动，主动获取信息。该任务为具身智能体的空间理解与决策提供了新范式，对导航、物体寻找等应用具有重要意义。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有视觉推理多限于被动静态场景，具身智能体需在信息不完整的世界中主动探索。
method: 提出主动视觉推理（AVR）任务，将推理与具身交互闭环结合，要求智能体在部分可观察环境中主动感知和行动。
result: 通过AVR基准与模型训练，展示了具身主动探索对提升视觉推理性能的有效性。
conclusion: 为多模态模型在真实物理环境中的具身智能研究提供了新的任务设置与评估方式。
---

## Abstract
Visual reasoning in multimodal large language models (MLLMs) has primarily been studied in passive, static settings, limiting their effectiveness in real-world physical environments where an embodied agent must contend with incomplete information due to occlusion or a limited field of view. Humans, in contrast, leverage their embodiment to actively explore and interact with their environment—moving, examining, and manipulating objects—to gather information through a closed-loop process integrating perception, reasoning, and action. Inspired by this capability, we introduce the Active Visual Reasoning (AVR) task, extending visual reasoning to a paradigm of embodied interaction in partially observable environments. AVR necessitates embodied agents to: (1) actively acquire information via sequential physical actions, (2) integrate observations across multiple steps for coherent reasoning, and (3) dynamically adjust decisions based on evolving visual feedback. To rigorously evaluate AVR, we introduce CLEVR-AVR, a simulation benchmark featuring multi-round interactive environments designed to assess both reasoning correctness and information-gathering efficiency. We present AVR-152k, a large-scale dataset that offers rich Chain-of-Thought (CoT) annotations detailing iterative reasoning for uncertainty identification, action-conditioned information gain prediction, and information-maximizing action selection, crucial for training agents in a higher-order Markov Decision Process. Building on this, we develop PhysVLM-AVR, an embodied MLLM achieving state-of-the-art performance on CLEVR-AVR, embodied reasoning (OpenEQA, RoboVQA), and passive visual reasoning (GeoMath, Geometry30K). Our analysis also reveals that current embodied MLLMs, despite detecting information incompleteness, struggle to actively acquire and integrate new information through interaction, highlighting a fundamental gap in active reasoning capabilities.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

- 现有视觉推理研究大多集中在**被动、静态**设定上：模型只能基于给定的一张或若干张图像进行推理，无法主动改变视角或获取新信息。
- 在真实物理环境中，具身智能体常常面临**遮挡、视线受限、信息不完整**等问题，此时被动推理会严重影响判断与决策。
- 人类在类似情境中会利用身体能力主动探索环境——移动、观察、操作物体，并通过“感知—推理—行动”的闭环不断获取新信息。
- 本文由此提出**主动视觉推理（Active Visual Reasoning, AVR）**任务，将视觉推理从静态感知拓展到**部分可观察环境下的具身交互范式**，填补了多模态大语言模型（MLLM）在主动信息获取与闭环推理方面的空白。

## 2. 方法论

- **核心思想**：AVR 不再要求模型“一次看图、一次作答”，而是要求智能体在部分可观察环境中，通过多步动作主动获取信息，并随观察结果动态调整推理决策。
- **任务形式**：
  1. 智能体通过**连续物理动作**主动采集信息；
  2. 跨多个步骤**整合观察结果**，形成连贯推理；
  3. 根据不断变化的视觉反馈**动态调整后续决策**。
- **建模层面**：该问题被刻画为**高阶马尔可夫决策过程（higher-order Markov Decision Process）**，动作选择需要考虑历史上下文。
- **训练数据**：构建了大规模数据集 **AVR-152k**，包含丰富的 **Chain-of-Thought (CoT) 注释**，详细记录：
  - 不确定性识别；
  - 动作条件下的信息增益预测；
  - 信息最大化动作选择。
  这些注释用于训练智能体的迭代推理能力。
- **模型**：提出 **PhysVLM-AVR**，一个具身多模态大语言模型，能够基于多轮交互观察进行端到端的主动推理与决策。

## 3. 实验设计

- **基准测试**：提出 **CLEVR-AVR**，一个多轮交互式仿真环境，专门用于评估 AVR 任务。
- **评估维度**：
  - 推理正确性（reasoning correctness）；
  - 信息收集效率（information-gathering efficiency）。
- **对比任务与数据集**：
  - 主动视觉推理：CLEVR-AVR；
  - 具身推理：OpenEQA、RoboVQA；
  - 被动视觉推理：GeoMath、Geometry30K。
- **对比对象**：虽然摘要中未逐一列出基线模型名称，但论文明确表示 PhysVLM-AVR 在上述四个基准上均达到**当前最优（state-of-the-art）**性能。
- **额外分析实验**：论文还考察了已有具身 MLLM 在 AVR 任务上的表现，发现它们虽然能识别信息不完整的情况，但难以通过交互主动获取并整合新信息，说明主动推理能力仍是当前模型的明显短板。

## 4. 资源与算力

- 论文提供的摘要和元数据中**没有说明**所使用的 GPU 型号、数量、训练时长等算力信息。
- 由于仅有摘要级文本，无法获知训练规模、硬件配置或计算成本等细节。

## 5. 实验数量与充分性

- 从现有信息看，实验覆盖面较广，至少包含：
  - 一个自建 AVR 基准（CLEVR-AVR）；
  - 两个具身推理基准（OpenEQA、RoboVQA）；
  - 两个被动视觉推理基准（GeoMath、Geometry30K）；
  - 针对现有具身模型的诊断性分析。
- **充分性与客观性评估**：
  - 积极方面：同时覆盖主动推理、具身推理和被动推理三类任务，能较好体现模型在多种设定下的泛化能力；评估同时关注正确性与效率，比较全面。
  - 局限性：由于只能看到摘要，**无法确认是否进行了消融实验**（如 CoT 注释的作用、动作选择模块的贡献、数据规模的影响等），也无法核对基线选择的公平性和统计显著性检验。
  - 结论的稳健性还需要更多细节支撑，例如各基准上的数值差距、误差棒、跨多次随机种子的结果等。

## 6. 主要结论与发现

- 提出并验证了 AVR 任务：将视觉推理从被动静态转为具身主动交互，能够有效应对真实环境中的信息不完整问题。
- 构建的 CLEVR-AVR 基准和 AVR-152k 数据集，能够系统评估智能体的推理能力与信息获取效率，并提供用于训练的高质量 CoT 监督。
- 提出的 PhysVLM-AVR 在主动视觉推理、具身推理和被动视觉推理上均达到 SOTA，证明主动探索与闭环推理能够同时提升多类视觉推理任务的表现。
- 现有具身 MLLM 虽然具备“知道信息不够”的判断能力，但**缺乏通过动作主动补全信息并将其融入决策的能力**，反映出当前模型在主动推理上的结构性不足。

## 7. 优点

- 问题定义新颖：将视觉推理从“看图答题”拓展为“边做边想”，更贴近真实机器人应用。
- 数据集设计有针对性：AVR-152k 的动作条件信息增益预测、信息最大化动作选择等注释，为训练主动探索策略提供了强监督信号。
- 评估体系完整：既衡量推理正确性，也衡量信息获取效率，兼顾“答得对”和“动作高效”。
- 实验验证范围广：从主动推理到具身推理再到被动推理均有评测，增强结果的可信度和推广性。
- 诊断性分析有价值：明确指出当前具身 MLLM 在“主动信息获取”上的缺陷，为后续研究指明方向。

## 8. 不足与局限

- 实验环境依赖仿真（如 CLEVR-AVR），**尚未体现真实物理环境中的噪声、动态干扰和物理操作不确定性**，与真实机器人部署仍有差距。
- 摘要中未提供具体数值结果、消融实验和与代表性基线方法的定量对比细节，难以全面评估该方法的实际增益。
- 未说明计算资源、训练开销与推理速度，对于具身智能体而言，实时性是实际部署的重要约束。
- AVR 任务本身依赖较大的动作空间和交互轮次，可能存在**训练数据标注成本高、注释一致性难保证**的问题。
- 结论的泛化性有限：CLEVR-AVR 属于合成环境，在复杂真实场景（如家居、户外）中的迁移能力尚需验证。
- 对高阶马尔可夫决策过程的具体建模方式、CoT 在训练和推理中的具体使用方式，均未在摘要中展开，技术可复现性难以评估。

（完）
