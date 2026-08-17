---
title: "PhysVLM-AVR: Active Visual Reasoning for Multimodal Large Language Models in Physical Environments"
title_zh: 物理环境中的多模态大语言模型主动视觉推理
authors: "Weijie Zhou, Xuantang Xiong, Yi Peng, Manli Tao, Chaoyang Zhao, Honghui Dong, Ming Tang, Jinqiao Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=AYDMNzpJPv"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 在部分可观察环境中进行具身交互与主动探索
tldr: 针对多模态大语言模型在静态被动场景中视觉推理能力有限的问题，提出主动视觉推理（AVR）任务，将推理扩展为部分可观察物理环境下的具身交互范式。模型可通过移动、观察和操作等闭环过程主动收集信息，整合感知、推理与行动。该工作为具身智能体的主动感知与推理研究提供了新的任务设定和评测视角，有助于推动机器人导航等下游应用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态大模型视觉推理局限于静态场景，难以应对物理世界中的遮挡和有限视野。
method: 提出主动视觉推理任务，将具身探索与感知-推理-行动闭环结合。
result: 在部分可观察环境下验证了主动交互对推理精度的提升。
conclusion: 为具身智能体在复杂环境中进行视觉推理提供新范式。
---

## Abstract
Visual reasoning in multimodal large language models (MLLMs) has primarily been studied in passive, static settings, limiting their effectiveness in real-world physical environments where an embodied agent must contend with incomplete information due to occlusion or a limited field of view. Humans, in contrast, leverage their embodiment to actively explore and interact with their environment—moving, examining, and manipulating objects—to gather information through a closed-loop process integrating perception, reasoning, and action. Inspired by this capability, we introduce the Active Visual Reasoning (AVR) task, extending visual reasoning to a paradigm of embodied interaction in partially observable environments. AVR necessitates embodied agents to: (1) actively acquire information via sequential physical actions, (2) integrate observations across multiple steps for coherent reasoning, and (3) dynamically adjust decisions based on evolving visual feedback. To rigorously evaluate AVR, we introduce CLEVR-AVR, a simulation benchmark featuring multi-round interactive environments designed to assess both reasoning correctness and information-gathering efficiency. We present AVR-152k, a large-scale dataset that offers rich Chain-of-Thought (CoT) annotations detailing iterative reasoning for uncertainty identification, action-conditioned information gain prediction, and information-maximizing action selection, crucial for training agents in a higher-order Markov Decision Process. Building on this, we develop PhysVLM-AVR, an embodied MLLM achieving state-of-the-art performance on CLEVR-AVR, embodied reasoning (OpenEQA, RoboVQA), and passive visual reasoning (GeoMath, Geometry30K). Our analysis also reveals that current embodied MLLMs, despite detecting information incompleteness, struggle to actively acquire and integrate new information through interaction, highlighting a fundamental gap in active reasoning capabilities.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：现有MLLMs的视觉推理主要在被动的、静态的图像或视频场景中评估。然而，在真实物理世界中，智能体需要面对遮挡、视野有限等问题，导致信息不完整（部分可观察环境）。这种被动推理范式限制了模型在机器人导航、操作等下游具身任务中的实用性。
- **核心问题**：如何让多模态大语言模型像人类一样，通过主动探索（移动、观察、操作）在部分可观察环境中主动收集信息，并通过“感知—推理—行动”的闭环过程完成视觉推理？
- **整体含义**：本文提出Active Visual Reasoning (AVR)任务，将被动视觉推理拓展为具身交互范式，并为该任务构建了仿真基准（CLEVR-AVR）、大规模训练数据（AVR-152k）和专用模型（PhysVLM-AVR）。该工作为具身智能体的主动感知与推理提供了新的任务设定与评测视角，对下游具身导航、交互推理等应用具有推动意义。

## 2. 论文提出的方法论

- **核心思想**：将视觉推理从静态单步观察拓展为多步、交互式的具身决策过程。智能体不是一次性读取完整场景，而是根据当前不完整观测，主动选择下一步物理动作（如移动、旋转、靠近、操作），以获取更多信息，然后不断更新推理结果。
- **AVR任务需满足的三个关键能力**：
  1. **主动信息获取**：通过序列化的物理动作主动探索环境，而不是被动接收图像；
  2. **多步观测整合**：在不同时间步上将来自不同视角/位置的观测信息进行融合，形成连贯的推理；
  3. **动态决策调整**：根据不断变化的视觉反馈实时更新判断与下一步行动，即在高阶马尔可夫决策过程（higher-order MDP）中做决策。
- **训练数据构建（AVR-152k）**：大规模数据集，包含丰富的思维链（Chain-of-Thought, CoT）标注，具体覆盖三类推理过程：
  - 不确定性识别（identifying where and why current observation is insufficient）；
  - 动作条件下的信息增益预测（predicting how much new information an action would bring）；
  - 信息最大化动作选择（selecting the action that maximizes information gain）。
- **模型设计（PhysVLM-AVR）**：基于MLLM构建的具身体模型，输入多步/多视角视觉观测与历史动作轨迹，输出推理中间步骤与下一步动作决策。该模型在一个统一的框架内完成感知、推理与行动选择。

## 3. 实验设计

- **核心基准（CLEVR-AVR）**：基于CLEVR风格场景构建的多轮交互仿真环境，专门用于评测AVR任务。评测指标同时关注：
  - **推理正确性**（答案是否正确）；
  - **信息收集效率**（是否用最少的动作获得足够信息）。
- **其他评测基准**（用于验证模型的通用性和迁移能力）：
  - **具身推理基准**：OpenEQA、RoboVQA；
  - **被动视觉推理基准**：GeoMath、Geometry30K。
- **对比方法**：与现有具身多模态模型及被动视觉推理模型进行对比，PhysVLM-AVR在这三类基准上均取得了领先结果（state-of-the-art）。

## 4. 资源与算力

- 论文摘要与提供的元数据中**未明确说明**训练所用GPU型号、数量、训练时长、显存开销等具体算力信息。
- 若需了解具体的算力配置与训练成本，需要查阅论文正文或附录中的实现细节。

## 5. 实验数量与充分性

- **实验数量**：论文覆盖了四类评测（CLEVR-AVR、OpenEQA、RoboVQA、GeoMath/Geometry30K），涵盖具身主动推理、通用具身问答、被动几何推理等多个维度，能够较全面地展示模型在不同任务类型上的能力。
- **充分性分析**：
  - 跨三种不同性质的基准（主动具身、被动视觉、问答）进行评测，增强了结论的普适性；
  - 摘要中未明确提及针对AVR核心模块（如CoT标注设计、动作选择策略、观测融合模型等）的消融实验细节，因此关于各组件贡献的分析需要以论文正文为准；
  - 评测指标同时考虑正确性和效率，比单纯准确率更能刻画主动推理能力，设计较客观。

## 6. 论文的主要结论与发现

- PhysVLM-AVR在CLEVR-AVR、OpenEQA、RoboVQA、GeoMath、Geometry30K上均达到当前最优性能，表明主动推理框架不会损害被动推理能力，同时显著提升了具身交互场景下的表现。
- 关键发现：现有具身MLLMs尽管能**识别**出观测信息的不完整（即知道“看不见”），但往往**不能通过交互动作主动获取并整合新信息**来弥补认知缺口。这一“识别但不行动”的差距揭示了当前模型在主动推理能力上的根本性不足。

## 7. 优点

- **任务定义有创新性**：将视觉推理从静态范式拓展到部分可观察环境下的主动交互范式，提出“主动视觉推理（AVR）”这一新任务，弥补了现有MLLM评测中缺乏具身主动性的空白。
- **框架完整**：新任务 + 仿真基准（CLEVR-AVR）+ 大规模训练集（AVR-152k）+ 专用模型（PhysVLM-AVR），形成了从数据到评测再到模型的完整闭环。
- **训练数据设计细致**：CoT注释显式建模不确定性识别、信息增益预测和动作选择过程，使模型能够学习高阶决策中的推理逻辑，而非简单模仿动作。
- **评测指标兼顾正确性与效率**：不仅衡量最终答案的对错，还衡量获取信息所需的动作步数，更符合真实具身场景中对效率的要求。

## 8. 不足与局限

- **环境为仿真场景**：CLEVR-AVR属于合成环境，视觉风格和物理规律相对简单，与真实世界的复杂光照、动态物体、噪声感知存在差距，真实场景泛化能力有待验证。
- **训练数据依赖密集标注**：AVR-152k的CoT标注构建成本较高，依赖人工或半自动化的推理链标注，扩展到更大规模或开放域场景时存在瓶颈。
- **算力信息缺失**：论文未提供训练所需的GPU资源与时间信息，难以评估其在资源受限场景下的可复现性和实用性。
- **模型能力边界有待深入分析**：摘要中指出现有具身MLLMs“识别信息不完整但不采取行动”，但对PhysVLM-AVR为何能克服这一问题、其内部机制如何运作，缺乏更深入的分析。
- **下游应用验证有限**：虽然提及对机器人导航等应用有推动意义，但未在真实机器人平台上进行验证，缺少物理世界部署层面的证据。

（完）
