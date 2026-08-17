---
title: Learning 3D Persistent Embodied World Models
title_zh: 学习持久化具身世界模型
authors: "Siyuan Zhou, Yilun Du, Yuncong Yang, Lei Han, Peihao Chen, Dit-Yan Yeung, Chuang Gan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=XTTbzC7O2T"
tags: ["query:vln-memory"]
score: 6.0
evidence: 持久化具身世界模型，具备显式场景记忆以支持长程规划
tldr: 针对现有视频世界模型缺乏对未观测场景的记忆、导致长程规划不一致的问题，论文提出持久化具身世界模型，在生成时显式记忆之前生成的内容。视频扩散模型根据记忆预测RGB-D视频，从而在复杂部分可观察环境中保持长期模拟一致性，为具身导航的记忆增强与规划提供潜在支持。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有视频世界模型缺乏场景记忆，难以在部分可观察环境中进行一致的长程模拟。
method: 构建显式记忆的持久化世界模型，通过视频扩散模型预测RGB-D视频。
result: 实验表明能生成更一致的长程模拟结果，支持长期规划。
conclusion: 为具身智能体的记忆增强与长时程规划提供了新的建模思路。
---

## Abstract
The ability to simulate the effects of future actions on the world is a crucial ability of intelligent embodied agents, enabling agents to anticipate the effects of their actions and make plans accordingly. While a large body of existing work has explored how to construct such world models using video models, they are often myopic in nature, without any memory of a scene not captured by currently observed images, preventing agents from making consistent long-horizon plans in complex environments where many parts of the scene are partially observed. We introduce a new persistent embodied world model with an explicit memory of previously generated content, enabling much more consistent long-horizon simulation. During generation time, our video diffusion model predicts RGB-D video of the future observations of the agent. This generation is then aggregated into a persistent 3D map of the environment. By conditioning the video model on this 3D spatial map, we illustrate how this enables video world models to faithfully simulate both seen and unseen parts of the world. Finally, we illustrate the efficacy of such a world model in downstream embodied applications, enabling effective planning and policy learning.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：现有视频世界模型（video world models）在模拟未来动作效果时存在"短视"（myopic）缺陷，即模型不具备对当前观测图像之外的场景的记忆能力，导致智能体在复杂部分可观察环境（partially observable environments）中无法进行一致的长程（long-horizon）规划与模拟。
- **研究动机**：具身智能体要做出有效规划，必须能够预测自身行动对未来世界状态的影响。视频世界模型虽有潜力，但由于缺乏显式的场景记忆，一旦场景部分区域未被当前视野覆盖，模型就无法持续保持一致的模拟结果，长时间步后容易产生"幻觉"或漂移。
- **整体含义**：该论文提出一种**持久化具身世界模型**（Persistent Embodied World Model），将显式记忆引入视频世界模型，使其能够同时模拟可见与不可见的场景区域，从而支撑更可靠的长程规划与策略学习，弥补了现有方法在记忆机制上的关键缺失。

---

## 2. 提出的方法论：核心思想、关键技术细节与算法流程

- **核心思想**：在生成过程中显式维护一个持久化的 3D 场景记忆，将视频扩散模型每次生成的新观测聚合到该记忆中，再以该 3D 空间记忆作为条件输入来指导后续视频生成，实现"边生成边记忆、以记忆指导生成"的闭环。
- **关键技术细节**：
  - 视频扩散模型预测的是 **RGB-D 视频**（彩色图像+深度图像），而非仅 RGB 视频，以便将观测反投影到三维空间。
  - 每次生成的新观测（RGB-D）会被聚合到一个 **持久化 3D 地图**（persistent 3D map）中，形成显式场景记忆。
  - 视频模型在预测下一步时，以当前这个 3D 空间地图为条件，从而在视角移动或物体被遮挡时仍能生成与历史记忆一致的未来观测。
- **算法流程（文字说明）**：
  1. 智能体在环境中执行动作，获得当前 RGB-D 观测；
  2. 该观测被用于更新/聚合到持久化 3D 地图中；
  3. 视频扩散模型以当前观测 + 3D 地图记忆 + 未来动作序列为条件，生成下一段 RGB-D 视频；
  4. 新生成的视频帧再次聚合到 3D 地图中，如此迭代推进；
  5. 最终形成的长程模拟结果既包含已见区域，也包含由记忆推断出的未见区域，可供规划器或策略学习使用。

---

## 3. 实验设计

- **摘要中提到的实验内容**：论文在“具身下游应用”中验证了该世界模型的有效性，支持**有效的规划**与**策略学习**。
- **数据集 / 场景 / Benchmark**：原文摘要**未明确提及**具体使用的数据集名称、仿真环境（如 Habitat、Matterport3D、AI2-THOR 等）或评估基准。这些细节需要查阅论文全文方可确认。
- **对比方法**：摘要中未列出具体对比基线，但根据问题设定，合理的对比对象应为：无记忆的基线视频世界模型、仅以当前帧为条件的视频预测模型等。

---

## 4. 资源与算力

- 论文提供的摘要与元数据中**未提及**任何算力相关信息，包括 GPU 型号、数量、训练时长、参数量、显存占用等。
- 如需了解训练资源与部署成本，只能以假设形式推测（例如视频扩散模型通常需要多卡大规模训练），但论文原文并未说明，应明确指出这一点。

---

## 5. 实验数量与充分性

- **实验数量**：摘要中只提到了下游规划与策略学习两类实验，未给出具体实验组数、消融实验数量或量化指标。
- **充分性评价**：由于缺乏具体数据集、指标数值、消融对比（如"有/无 3D 记忆"的对比）等信息，无法从现有提取文本中全面评估实验的充分性与公平性。需要阅读全文图表与实验章节后才能做出可靠判断。但从问题本身的重要性来看，该实验至少覆盖了"长程一致性模拟"和"下游任务有效性"两个关键维度，如果全文提供了定量对比，实验设计思路是合理的。

---

## 6. 论文的主要结论与发现

- 论文提出的持久化 3D 记忆机制能够显著提升视频世界模型在长程模拟中的**一致性**（consistent long-horizon simulation），使模型能同时忠实模拟**已见与未见**的世界部分。
- 这种带显式 3D 记忆的世界模型可有效支持下游具身应用，包括**规划**（planning）与**策略学习**（policy learning），展现出作为通用具身世界模型的潜力。

---

## 7. 优点

- **方法创新性**：提出"显式 3D 持久记忆 + 视频扩散模型"的组合，这是对现有"短视"视频世界模型的实质性改进，直接解决了部分可观察环境下的长程一致性问题。
- **生成与记忆的闭环设计**：将生成结果反哺到 3D 地图中，再以地图条件化生成，形成了一个自然且可扩展的循环架构。
- **使用 RGB-D 作为观测空间**：深度信息的使用使 3D 记忆的构建更加高效和准确，是一种具有实际意义的技术选型。
- **应用价值明确**：明确将世界模型用于导航类下游任务（结合元数据标签 query:vln-memory），说明方法面向真实具身需求，而不仅是视频生成质量的提升。

---

## 8. 不足与局限

- **实验信息不全**：从当前提取文本来看，论文未明确报告使用的数据集、基准和对比方法，这限制了对其实验严谨性的判断。
- **算力与可扩展性未说明**：视频扩散模型 + 3D 地图聚合的计算开销较大，论文未给出资源消耗信息，实际部署成本存疑。
- **场景泛化能力未知**：是否适用于不同尺度（室内/室外）、不同传感器配置（单目/双目）以及开放世界场景，摘要中未展示。
- **长期记忆的累积误差**：3D 地图的构建依赖于每步生成的深度信息，若生成结果存在误差，误差会随记忆累积而传播，该问题在摘要中未讨论。
- **应用边界**：虽然支持规划与策略学习，但仅限于具身导航类任务可能更为适配，是否对操作（manipulation）等其他具身任务有效仍属未知。

---

（完）
