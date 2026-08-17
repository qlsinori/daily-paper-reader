---
title: "BeliefMapNav: 3D Voxel-Based Belief Map for Zero-Shot Object Navigation"
title_zh: "BeliefMapNav: 用于零样本目标导航的3D体素信念地图"
authors: "Zibo Zhou, Yue Hu, Lingkai Zhang, Zonglin Li, Siheng Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=7AMriz7I3K"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 零样本目标导航，利用语言指令与3D体素信念地图进行空间推理
tldr: 针对零样本目标导航中智能体缺乏全局环境理解、仅贪婪选点导致空间推理不足的问题，论文提出基于3D体素的目标存在信念地图，将大语言模型与视觉语言模型的语义推理能力融入导航过程。该方法在未知环境中估计目标的先验分布，从而支持更全局的导航决策。实验表明该方法在零样本目标导航任务上显著提升成功率，展示了显式空间信念表达对具身导航的价值。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有零样本目标导航智能体依赖大模型语义推理，却缺少全局环境理解，空间推理能力有限。
method: 提出一种3D体素信念地图，估计目标在空间中的先验存在分布，辅助导航决策。
result: 在零样本目标导航基准上取得显著成功率提升，验证了显式全局信念图的有效性。
conclusion: 利用3D信念地图弥补大模型空间推理短板，为零样本具身目标导航提供新思路。
---

## Abstract
Zero-shot object navigation (ZSON) allows robots to find target objects in unfamiliar environments using natural language instructions, without relying on pre-built maps or task-specific training. Recent general-purpose models, such as large language models (LLMs) and vision-language models (VLMs), equip agents with semantic reasoning abilities to estimate target object locations in a zero-shot manner. However, these models often greedily select the next goal without maintaining a global understanding of the environment and are fundamentally limited in the spatial reasoning necessary for effective navigation. To overcome these limitations, we propose a novel 3D voxel-based belief map that estimates the target’s prior presence distribution within a voxelized 3D space. This approach enables agents to integrate semantic priors from LLMs and visual embeddings with hierarchical spatial structure, alongside real-time observations, to build a comprehensive 3D global posterior belief of the target’s location. Building on this 3D voxel map, we introduce BeliefMapNav, an efficient navigation system with two key advantages: i) grounding LLM semantic reasoning within the 3D hierarchical semantics voxel space for precise target position estimation, and ii) integrating sequential path planning to enable efficient global navigation decisions. Experiments on HM3D and HSSD benchmarks show that BeliefMapNav achieves state-of-the-art (SOTA) Success Rate (SR) and Success weighted by Path Length (SPL), with a notable 9.7 SPL improvement over the previous best SR method, validating its effectiveness and efficiency.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 目标：解决**零样本目标导航（Zero-shot Object Navigation, ZSON）**问题，即让机器人在完全陌生的环境中，仅凭借自然语言指令找到目标物体，且不依赖预建地图或任务专属训练。
- 现有方法的不足：
  - 通用大模型（LLM/VLM）虽然具备语义推理能力，能零样本估计目标物体的大致位置，但往往只做**贪心式选点**，缺乏对环境的全局理解。
  - 这类模型在**空间推理**上存在根本性短板，难以支持长时间、多步的导航决策。
- 核心意义：论文提出用**显式3D体素信念地图**来弥补大模型在空间推理上的缺陷，将语义先验与实时观测融合为全局后验信念，为具身智能体的零样本导航提供了一种新范式。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- 核心思想：构建一个**3D体素化的目标存在信念地图**，估计目标在空间中每个体素内的“先验存在概率分布”，并在导航过程中通过实时观测更新为“后验信念”，从而指导全局导航决策。
- 关键技术细节：
  1. **3D体素信念地图**：将环境体素化为3D网格，每个体素携带目标存在的概率信念。
  2. **层级语义空间结构**：将LLM提供的语义先验与VLM的视觉嵌入，映射到3D体素空间中，形成分层的语义表示。
  3. **实时观测融合**：将当前传感器观测与先验信念结合，构建全局后验信念地图。
  4. **路径规划集成**：基于信念地图执行**序列化路径规划**，实现全局而非局部贪心的导航决策。
- 算法流程（文字说明）：
  1. 初始化3D体素地图，输入自然语言目标描述。
  2. 利用LLM/VLM获取目标语义先验，散布到相应体素上。
  3. 智能体在环境中移动，实时更新体素信念（融合观测到的视觉信息）。
  4. 在每个决策步，根据当前信念地图选择通往目标概率最高的全局路径点。
  5. 重复更新与规划，直至找到目标或判定失败。

> 注：原文摘要中未提供具体数学公式，因此这里仅基于描述性内容概括。

## 3. 实验设计：数据集、benchmark、对比方法

- 数据集/场景：
  - **HM3D**（Habitat Matterport 3D）基准。
  - **HSSD**（Habitat Synthetic Scene Dataset）基准。
- Benchmark：使用零样本目标导航的标准评价指标：
  - **Success Rate (SR)**：能找到目标的成功率。
  - **Success weighted by Path Length (SPL)**：按路径长度加权的成功率，反映导航效率。
- 对比方法：与现有零样本目标导航方法比较，特别是与“此前SR最高的方法”进行对比，并指出在SPL上实现了**9.7的提升**。
- 结果：BeliefMapNav在HM3D和HSSD上均达到**SOTA的SR和SPL**。

## 4. 资源与算力

- 论文摘要和元数据中**未明确说明**使用的GPU型号、数量、训练时长等资源细节。
- 由于该方法属于零样本导航方案，可能无需大规模任务专属训练，但具体算力投入未知，需查阅论文全文或附录才能获知。

## 5. 实验数量与充分性

- 已知实验覆盖两个数据集（HM3D、HSSD），并报告了SR和SPL两个核心指标。
- 摘要中**未详细列出消融实验**，例如：
  - 是否分别验证3D体素信念地图、层级语义集成、序列规划各自的贡献？
  - 是否与其他类型的信念表达（如2D地图）对比？
  - 是否在不同场景复杂度下进行鲁棒性测试？
- 整体来看，实验结果提到了SOTA的提升，但**实验的全面性在摘要中无法完全判断**；就公开信息而言，覆盖了两个主流基准，但缺乏详细消融和统计显著性描述，充分性有待全文验证。

## 6. 论文的主要结论与发现

- 提出并验证了**3D体素信念地图**能显著提升零样本目标导航的成功率和路径效率。
- 通过将LLM/VLM的语义推理**落地到结构化3D空间**，有效弥补了大模型空间推理不足的问题。
- 在HM3D和HSSD基准上取得SOTA成绩，尤其SPL比此前最优SR方法提升9.7，说明方法不仅更准，而且路径更高效。
- 验证了显式空间信念表达对具身导航任务的重要价值。

## 7. 优点：方法或实验设计上的亮点

- **创新性强**：将大模型的语义先验转化为可更新的3D体素信念，是一种优雅的“知识-空间”融合方案。
- **全局视角**：区别于贪心选点，通过全局后验信念进行序列路径规划，理论上能避免陷入局部最优。
- **零样本能力**：无需任务专属训练，适用于未知环境，符合具身智能实际部署需求。
- **性能显著**：在两个标准benchmark上均达到SOTA，SPL提升明显说明效率改善突出。
- **结构清晰**：方法模块化（语义映射、信念更新、路径规划），便于复现和扩展。

## 8. 不足与局限

- **算力信息缺失**：未报告资源消耗，难以评估实际部署成本。
- **实验细节不足**：摘要中未提供消融实验、不同组件贡献分析、失败案例等，无法全面判断方法的鲁棒性。
- **依赖预训练模型**：方法底层依赖LLM/VLM的质量，若模型语义先验有偏，可能影响最终效果。
- **体素分辨率与计算复杂度**：3D体素地图的构建和更新可能带来较高的内存和时间开销，摘要中未讨论实时性问题。
- **评估场景范围**：目前只提到HM3D和HSSD，未涉及更开放、动态或更大尺度的环境，泛化能力有待进一步验证。
- **未讨论边界情况**：如目标完全不可见、语义模糊/歧义、环境噪声等场景下的表现未知。

（完）
