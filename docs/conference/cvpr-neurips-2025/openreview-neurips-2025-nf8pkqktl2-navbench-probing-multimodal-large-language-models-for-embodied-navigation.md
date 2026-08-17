---
title: "NavBench: Probing Multimodal Large Language Models for Embodied Navigation"
title_zh: NavBench：探测多模态大语言模型的具身导航能力
authors: "Yanyuan Qiao, Haodong Hong, Wenqi Lyu, Dong An, Siqi Zhang, Yutong Xie, Xinyu Wang, Qi Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=nf8PKQKtl2"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 在模拟室内场景中评测MLLM具身导航能力的基准
tldr: NavBench旨在评估多模态大语言模型在零样本设定下的具身导航能力，填补了该方向缺乏系统性测评的空白。基准包含导航理解与逐步执行两部分，前者覆盖全局指令对齐、时间进度估计和局部观察-行动推理三类任务，后者在72个室内场景的432个回合中分层评估空间、认知与执行复杂度。实验揭示了当前模型在不同复杂度层面的能力边界，为具身导航模型评测与改进提供了标准化参考。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态大语言模型在视觉语言任务上表现强劲，但其具身环境的理解与行动能力仍缺乏系统性评估，构建专门基准成为必要。
method: 提出NavBench基准，设计导航理解问答与逐步执行两类测评，覆盖多类复杂度分层和室内场景。
result: 通过3200个问答对和432个场景回合评估，揭示零样本MLLM在具身导航中的能力边界与不足。
conclusion: 该基准为MLLM具身导航提供标准化评测框架，可指导后续模型设计与真实部署。
---

## Abstract
Multimodal Large Language Models (MLLMs) have demonstrated strong generalization in vision-language tasks, yet their ability to understand and act within embodied environments remains underexplored. We present NavBench, a benchmark to evaluate the embodied navigation capabilities of MLLMs under zero-shot settings. NavBench consists of two components: (1) navigation comprehension, assessed through three cognitively grounded tasks including global instruction alignment, temporal progress estimation, and local observation-action reasoning, covering 3,200 question-answer pairs; and (2) step-by-step execution in 432 episodes across 72 indoor scenes, stratified by spatial, cognitive, and execution complexity. To support real-world deployment, we introduce a pipeline that converts MLLMs' outputs into robotic actions. We evaluate both proprietary and open-source models, finding that GPT-4o performs well across tasks, while lighter open-source models succeed in simpler cases. Results also show that models with higher comprehension scores tend to achieve better execution performance. Providing map-based context improves decision accuracy, especially in medium-difficulty scenarios. However, most models struggle with temporal understanding, particularly in estimating progress during navigation, which may pose a key challenge.

---

## 论文详细总结（自动生成）

## NavBench：探测多模态大语言模型的具身导航能力——详细总结

### 1. 论文的核心问题与整体含义

- **研究动机**：多模态大语言模型（MLLMs）在视觉-语言任务上表现出了极强的泛化能力，但其在具身环境中的理解和行动能力仍缺乏系统性评估。现有基准多聚焦于静态视觉问答或纯语言推理，难以反映模型在真实交互环境中的感知-决策-执行闭环能力。
- **核心问题**：当前 MLLMs 在**零样本设定**下，能否完成具身导航中的**环境理解**与**逐步行动执行**？其能力边界在哪里？
- **整体意义**：论文提出 NavBench，填补了 MLLM 具身导航能力系统性测评的空白，为后续模型设计、评测标准化和真实部署提供了参考框架，是该领域首个覆盖双层能力（理解+执行）的基准。

### 2. 论文提出的方法论

NavBench 由两大核心组件构成：

- **导航理解测评（Navigation Comprehension）** ：基于认知科学理论，设计三类任务，共 3,200 个问答对。
  - *全局指令对齐（Global Instruction Alignment）*：评估模型将自然语言导航指令与全局路径/拓扑信息对齐的能力。
  - *时间进度估计（Temporal Progress Estimation）*：给定导航过程中的部分观察，评估模型估算当前已完成进度（时间/距离比例）的能力。
  - *局部观察-行动推理（Local Observation-Action Reasoning）*：给定第一视角局部观察，评估模型推理下一步行动（转向、前进等）的能力。
- **逐步执行测评（Step-by-Step Execution）**：
  - 在 72 个室内场景中进行 432 个回合的导航执行任务。
  - 回合按**空间复杂度**（场景拓扑复杂度）、**认知复杂度**（指令歧义性与推理需求）和**执行复杂度**（动作序列长度与容错要求）进行分层设计。
  - 提出一条将 MLLM 输出转换为机器人动作的**后处理管道（Pipeline）**，以支持真实/模拟环境中的部署执行。

### 3. 实验设计

- **基准构成**：
  - 理解部分：3,200 个问答对，覆盖三类认知任务。
  - 执行部分：432 个回合，分布在 72 个室内场景中。
- **评测模型**：包含**闭源模型**（如 GPT-4o）与**开源模型**（轻量级开源 MLLMs）。
- **对比方式**：跨模型对比（闭源 vs. 开源；大规模 vs. 轻量级），以及跨任务/跨复杂度层的性能分解。
- **附加分析**：探究了“理解分数”与“执行表现”的相关性，以及**地图上下文（map-based context）** 注入对决策准确性的影响（分低/中/高难度场景分别考察）。

### 4. 资源与算力

- 论文原文**未明确说明**具体的 GPU 型号、数量、训练/评测时长等算力信息。
- 唯一可推断的是：评测涉及多轮问答与多回合执行，且包含闭源 API 调用（GPT-4o），推理成本显著，但具体数值未披露。

### 5. 实验数量与充分性

- **实验数量**：
  - 理解测评：3,200 个问答对。
  - 执行测评：432 个回合 × 多模型对比。
  - 附加分析：包含“理解-执行相关性分析”和“地图上下文消融对比”（分难度层级），属于消融性质的分析。
- **充分性与客观性**：
  - **优点**：问答对与回合数量规模较大，复杂度分层设计合理，且同时评测闭源与开源模型，覆盖面广。
  - **不足**：
    - 未提供执行回合的**逐模型成功率详细分解表**，信息粒度较粗；
    - 缺乏对提示词敏感性的分析——MLLM 对提示词措辞高度敏感，未做多提示词变体对照会影响结论稳健性；
    - 地图上下文注入实验仅分析了 3 个难度层级，未进一步按“场景类型”或“指令类型”细分；
    - 未报告执行回合中“碰撞”或“非法动作”等安全性指标。

### 6. 论文的主要结论与发现

- **GPT-4o** 在各类任务中表现领先，而轻量级开源模型仅在简单场景中表现良好。
- **理解与执行正相关**：在导航理解测评中得分更高的模型，往往在执行任务中表现更好，支持“理解是执行的前提”这一直觉。
- **地图上下文有效**：提供地图信息能明显提升决策准确率，尤其在**中等难度**场景中增益最大；但在极低难度下增益有限，极高难度下仍然不足。
- **时间理解是共同短板**：大多数模型在**时间进度估计**任务上表现不佳，是当前 MLLM 具身导航能力的关键瓶颈之一，也是未来改进的重要方向。

### 7. 优点

- **首创性**：首个系统性地将 MLLM 零样本具身导航能力拆解为“理解”+“执行”两层并分别测评的基准。
- **认知驱动设计**：三类理解任务均有认知科学依据，任务设计具备理论支撑效度。
- **复杂度分层**：执行任务按空间、认知、执行三个维度分层，能精确定位模型能力边界。
- **部署导向**：提出 MLLM 输出到机器人动作的转换管道，促成“评测-部署”闭环。
- **分析深度**：除排行榜外，还做了“理解-执行相关性”与“地图上下文增益”等机制性分析，超越简单打分。

### 8. 不足与局限

- **信息缺失**：未报告算力消耗，影响实验可复现性与成本估计。
- **评测场景类型局限**：仅覆盖室内场景，未涉及室外、动态障碍物、多智能体等更复杂环境；对真实世界部署的代表性有限。
- **静态度量**：执行回合评估可能未充分考虑动作选择的累积误差——早期一步错误对后续效果的级联影响未明确讨论。
- **模型代表性有限**：开源模型多为轻量级，未包含 70B 级别以上高性能开源模型（如 Llama-3-70B 系 MLLM）的对比，对社区开源生态的反映不够完整。
- **偏差风险**：3,200 个问答对由自动或人工生成，可能存在生成偏差；且未披露问答对生成流程中的人工审核细节。
- **应用限制**：零样本设定排除了微调带来的性能增益，因此无法评估模型在具身导航任务上的“上限”，只反映预训练知识的零样本迁移能力。

（完）
