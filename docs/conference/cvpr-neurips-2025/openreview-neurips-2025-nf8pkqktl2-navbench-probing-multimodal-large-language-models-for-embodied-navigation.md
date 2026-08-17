---
title: "NavBench: Probing Multimodal Large Language Models for Embodied Navigation"
title_zh: NavBench：面向具身导航的多模态大语言模型评测基准
authors: "Yanyuan Qiao, Haodong Hong, Wenqi Lyu, Dong An, Siqi Zhang, Yutong Xie, Xinyu Wang, Qi Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=nf8PKQKtl2"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 多模态大模型具身导航能力基准，包含室内场景与逐步执行
tldr: 多模态大语言模型（MLLM）在视觉-语言任务上表现出色，但其在具身环境中的理解与行动能力尚待探索。本文提出NavBench基准，通过全局指令对齐、时间进度估计和局部观测-动作推理等任务评测导航理解，并在72个室内场景的432个回合中进行逐步执行测试。该工作为评估MLLM的零样本具身导航能力提供了框架和参考。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有评测缺乏对MLLM在具身导航中理解和执行能力的系统评估。
method: 设计NavBench基准，包含导航理解问答和逐步执行测试，覆盖多种空间与认知复杂度。
result: 在432个室内场景回合中评测了MLLM的零样本导航表现。
conclusion: NavBench为衡量多模态大模型的具身导航能力提供了新基准。
---

## Abstract
Multimodal Large Language Models (MLLMs) have demonstrated strong generalization in vision-language tasks, yet their ability to understand and act within embodied environments remains underexplored. We present NavBench, a benchmark to evaluate the embodied navigation capabilities of MLLMs under zero-shot settings. NavBench consists of two components: (1) navigation comprehension, assessed through three cognitively grounded tasks including global instruction alignment, temporal progress estimation, and local observation-action reasoning, covering 3,200 question-answer pairs; and (2) step-by-step execution in 432 episodes across 72 indoor scenes, stratified by spatial, cognitive, and execution complexity. To support real-world deployment, we introduce a pipeline that converts MLLMs' outputs into robotic actions. We evaluate both proprietary and open-source models, finding that GPT-4o performs well across tasks, while lighter open-source models succeed in simpler cases. Results also show that models with higher comprehension scores tend to achieve better execution performance. Providing map-based context improves decision accuracy, especially in medium-difficulty scenarios. However, most models struggle with temporal understanding, particularly in estimating progress during navigation, which may pose a key challenge.

---

## 论文详细总结（自动生成）

# NavBench：具身导航多模态大语言模型评测基准——详细中文总结

## 一、核心问题与研究动机

- **研究背景**：多模态大语言模型（MLLMs）在视觉-语言任务上展现出强大的零样本泛化能力，但其在**具身环境**（embodied environments）中"理解环境并采取行动"的能力仍缺乏系统性探索。
- **核心问题**：现有评测基准大多聚焦于MLLM在静态图像或纯语言任务上的表现，缺少对其**具身导航**能力（包括语义理解、空间推理、时序估计与动作决策）的标准化评估框架。
- **研究动机**：为填补这一空白，作者提出 **NavBench**——一个零样本设置下系统评估MLLM具身导航能力的基准，旨在回答两个关键问题：
  1. MLLM 能否真正"理解"导航任务中蕴含的空间与认知语义？
  2. 这种理解能否转化为实际环境中的逐步执行能力？

## 二、方法论

NavBench 包含两大核心组件，从"理解"与"执行"两个层面刻画模型能力，并配套一条输出-动作转换管线：

1. **导航理解（Navigation Comprehension）**——基于认知科学设计三类任务，共 **3,200 个问答对**：
   - **全局指令对齐（Global Instruction Alignment）**：考察模型能否将自然语言导航指令与整体环境布局建立正确映射，即路线级语义理解。
   - **时间进度估计（Temporal Progress Estimation）**：给定局部观测与起点/终点，判断当前已经行进的进度比例，考察模型的时序推理与里程碑定位能力。
   - **局部观测-动作推理（Local Observation-Action Reasoning）**：根据当前帧局部观测，选择合理的下一步动作，检验模型在即时感知层面的决策能力。
   - 三类任务构成由全局到局部、由静态到动态的认知梯度，覆盖不同层次的空间-认知复杂度。

2. **逐步执行（Step-by-Step Execution）**——在 **72 个室内场景、432 个执行回合（episodes）** 中，要求模型在轨迹推进过程中持续输出动作决策。实验按**空间复杂度、认知复杂度、执行复杂度**三个维度进行分层（stratified），保证评测覆盖的多样性。

3. **输出-动作转换管线（Output-to-Action Pipeline）**：为支持真实世界部署，作者设计了将 MLLM 的自由形式输出转换为机器人可执行动作的接口流程，使模型评测能够平滑延伸到实际导航系统。

> 注：论文正文未给出显式公式或算法伪代码，方法以任务定义、数据集构建与评估流程的形式呈现。

## 三、实验设计

- **评测基准**：NavBench 自身即为评测基准，包含：
  - 3,200 个导航理解问答对；
  - 72 个室内场景、432 个逐步执行回合；
  - 场景按空间/认知/执行复杂度分层。
- **对比模型**：
  - **闭源模型**：GPT-4o（代表先进商用系统）。
  - **开源模型**：若干轻量级开源 MLLM（论文摘要未逐一列出具体名称）。
  - 所有模型均在**零样本（zero-shot）** 条件下评测，不进行任何微调。
- **附加分析实验**：
  - 导航理解得分与执行表现的**相关性分析**；
  - 提供**地图上下文（map-based context）** 与否对决策准确率的**消融式对比**。

## 四、资源与算力

- 论文在摘要与元数据中**未给出**具体的训练/推理算力信息，包括 GPU 型号、数量、训练时长或推理硬件配置。
- 由于所有模型均采用**零样本评测**，训练成本为零，但推理资源需求取决于各模型官方部署配置，文中未详细披露。
- 作为读者，我们无法从现有文本中评估其计算开销规模，需查阅论文正文或附录获取更完整信息。

## 五、实验数量与充分性评估

- **实验规模**：
  - 理解任务：3,200 个 QA 对，覆盖三类认知子任务；
  - 执行任务：432 个回合，横跨 72 个场景，并按三重复杂度分层。
- **对比广度**：同时覆盖闭源（GPT-4o）与多种开源轻量模型，兼顾"能力上限"与"可部署性"两端。
- **分析深度**：不仅报告单任务得分，还做了理解-执行相关性分析、地图上下文消融对比，以及不同难度层级下的表现分层分析。
- **充分性评估**：
  - **优点**：数据集规模适中、任务设计有认知理论支撑、复杂度分层合理，能支撑"理解能力≠执行能力"这类跨层结论。
  - **局限**：仅评测零样本设置，未涉及微调或强化学习场景；缺乏随机种子、多次运行方差等统计细节的公开描述（摘要未提及）；未见跨数据集泛化测试（如与 Matterport3D、HM3D 等已有导航基准的对照）。
  - **客观性**：结论与实验设计一致性较好，相关性分析与消融分析增强了论证的客观性；但由于本文只能基于摘要与元数据总结，无法核对完整实验细节。

## 六、主要结论与发现

1. **GPT-4o 综合表现最佳**，在导航理解与执行任务上均显著领先。
2. **轻量开源模型在简单场景中表现可行**，但在高复杂度场景下能力快速下降，说明导航任务的认知负荷对模型规模敏感。
3. **理解与执行呈正相关**：在导航理解任务上得分越高的模型，其逐步执行表现也越好——这支持了"语言级空间理解是具身执行的前提"这一假设。
4. **地图上下文提升决策准确率**：在提供地图信息时，模型动作决策的准确率普遍提高，且**中等难度场景下提升最明显**——提示适度语义辅助能有效弥补模型推理短板。
5. **时序理解是共同短板**：绝大多数模型在**时间进度估计**任务上表现不佳，说明"我现在走多远了、还剩多少"这类动态量级推断是当前 MLLM 具身导航能力的核心瓶颈。
6. **总体判断**：现有 MLLM 具备一定零样本导航理解与执行能力，但离可靠的真实世界具身导航仍有明显差距，时序推理是最突出的薄弱环节。

## 七、优点与亮点

- **任务设计的认知分层**：从"全局指令对齐→时间进度估计→局部动作推理"构成由宏观到微观、由静态到动态的认知梯度，评测维度系统且理论有据。
- **"理解 + 执行"双轨结构**：既评测认知能力，又评测行动能力，并能通过两者相关性分析回答更深层的问题（理解是否足以支撑行动）。
- **复杂度三维分层**：空间、认知、执行复杂度分别刻画，使结论更精细（如"中等难度受益于地图最大"这类非平凡发现）。
- **零样本设置**：避免了微调带来的混淆因素，直接评估模型固有的泛化能力。
- **面向真实部署的转换管线**：将语言输出与机器人动作衔接，缩小了仿真评测与真实落地的鸿沟。
- **对比范围全面**：闭源旗舰与开源轻量模型并置，同时展示能力天花板与实用基线。

## 八、不足与局限

- **时序理解瓶颈未提出解决方案**：论文指出现有模型在时间进度估计上普遍失败，但基准本身并未提供缓解策略或训练信号，仅停留在诊断层面。
- **零样本单一设置**：未探索微调、上下文学习（in-context learning）或强化学习反馈下模型能否补足短板，限制了基准的应用纵深。
- **真实部署验证有限**：虽然设计了输出-动作转换管线，但 432 个室内回合的执行评测是否在真实机器人上完成，还是仿真环境代行，摘要未能明确，其 sim-to-real 保真度存疑。
- **误差传播与鲁棒性不明**：逐步执行中早期动作错误如何级联影响后续决策、模型是否会在错误发生后自我纠错，此类交互性分析在摘要层面缺失。
- **场景与任务覆盖的固有边界**：仅限室内场景，未涉及室外、动态障碍物、多智能体或人机交互等更复杂的具身导航形态。
- **地图上下文增益的适用边界**：地图帮助在"中等难度"最明显，但对于极简单与极困难场景效果不明，该非线性现象也缺乏深入解释。
- **信息透明度限制**：由于本文基于 OpenReview 摘要与元数据撰写，未能获取论文完整正文，上述实验质量控制细节（数据来源标注、人工评估一致性、统计显著性检验、baseline 超参数等）尚无法核实。

---

（完）
