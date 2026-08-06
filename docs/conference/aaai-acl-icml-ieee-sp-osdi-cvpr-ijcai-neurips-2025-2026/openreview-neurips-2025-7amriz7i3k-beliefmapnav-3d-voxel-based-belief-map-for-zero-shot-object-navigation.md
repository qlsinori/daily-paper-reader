---
title: "BeliefMapNav: 3D Voxel-Based Belief Map for Zero-Shot Object Navigation"
title_zh: 信念地图导航：用于零样本物体导航的三维体素信念地图
authors: "Zibo Zhou, Yue Hu, Lingkai Zhang, Zonglin Li, Siheng Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=7AMriz7I3K"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 零样本物体导航；三维体素信念地图；语言引导目标搜索
tldr: 针对现有零样本物体导航模型缺乏全局环境感知与空间推理、仅做贪婪目标选择的问题，提出一种新颖的三维体素信念地图，用以估计目标在空间中出现的先验分布。该方法结合视觉语言模型的语义推理，在无预建地图和任务训练条件下引导机器人搜索。实验表明其能有效提升陌生环境中的目标导航性能，为具身智能导航提供了更具全局性和可扩展性的表示方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有大模型在零样本物体导航中仅贪婪选择下一步，缺乏全局环境理解和空间推理能力。
method: 提出三维体素信念地图，将目标先验分布存储于体素中，用于引导零样本导航决策。
result: 在陌生环境中展示了更有效的目标搜索能力，减少了对预建地图和任务训练的依赖。
conclusion: 三维信念地图可显著提升零样本物体导航的空间推理性能，为具身导航提供新的表示方式。
---

## Abstract
Zero-shot object navigation (ZSON) allows robots to find target objects in unfamiliar environments using natural language instructions, without relying on pre-built maps or task-specific training. Recent general-purpose models, such as large language models (LLMs) and vision-language models (VLMs), equip agents with semantic reasoning abilities to estimate target object locations in a zero-shot manner. However, these models often greedily select the next goal without maintaining a global understanding of the environment and are fundamentally limited in the spatial reasoning necessary for effective navigation. To overcome these limitations, we propose a novel 3D voxel-based belief map that estimates the target’s prior presence distribution within a voxelized 3D space. This approach enables agents to integrate semantic priors from LLMs and visual embeddings with hierarchical spatial structure, alongside real-time observations, to build a comprehensive 3D global posterior belief of the target’s location. Building on this 3D voxel map, we introduce BeliefMapNav, an efficient navigation system with two key advantages: i) grounding LLM semantic reasoning within the 3D hierarchical semantics voxel space for precise target position estimation, and ii) integrating sequential path planning to enable efficient global navigation decisions. Experiments on HM3D and HSSD benchmarks show that BeliefMapNav achieves state-of-the-art (SOTA) Success Rate (SR) and Success weighted by Path Length (SPL), with a notable 9.7 SPL improvement over the previous best SR method, validating its effectiveness and efficiency.

---

## 论文详细总结（自动生成）

# 论文总结：BeliefMapNav——用于零样本物体导航的三维体素信念地图

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：零样本物体导航（Zero-shot Object Navigation, ZSON）要求机器人仅根据自然语言指令在陌生环境中找到目标物体，并且不能依赖预建地图或任务专用训练。
- **现有方法局限**：近期研究使用大语言模型（LLM）和视觉语言模型（VLM）为智能体提供语义推理能力，从而零样本地估计目标位置。但这些模型通常只是**贪婪地选择下一步目标**，缺乏对环境的全局理解，其空间推理能力从根本上限制了导航效率。
- **研究动机**：构建一种能够整合语义先验、视觉嵌入与实时观测的**全局空间表示**，使智能体在导航过程中具备更强的空间推理和全局决策能力，从而提升零样本物体导航的成功率与路径效率。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：提出一种新颖的**三维体素化信念地图（3D voxel-based belief map）**，用于估计目标物体在三维空间中的先验出现分布，并在此基础上构建全局后验信念。
- **关键技术细节**：
  - 将环境空间划分为**层次化的三维体素（hierarchical voxel）结构**，每个体素存储目标存在的信念值。
  - 融合两类信息源：① LLM 提供的**语义先验**（如“杯子通常在厨房台面上”）；② 视觉编码器提供的**视觉嵌入**，结合实时观测来更新体素信念。
  - 通过三维层次语义体素空间，将 LLM 的语义推理**落地**到具体空间位置，实现精确的目标位置估计。
  - 引入**序贯路径规划（sequential path planning）** 模块，基于体素信念地图做出全局导航决策，避免贪婪局部选择。
- **算法流程（文字描述）**：
  1. 接收自然语言指令，提取目标物体语义；
  2. 初始化三维体素信念地图，注入 LLM 语义先验；
  3. 机器人实时感知环境，生成视觉嵌入并更新对应体素的信念值；
  4. 根据当前全局信念地图，规划一条高效路径；
  5. 逐步执行路径，持续更新信念地图，直到找到目标或遍历完高信念区域。

## 3. 实验设计

- **数据集/场景**：使用 **HM3D** 和 **HSSD** 两个具身导航基准数据集。
- **Benchmark 指标**：主要评估 **成功率（SR, Success Rate）** 和**路径加权成功率（SPL, Success weighted by Path Length）**。
- **对比方法**：与当前最先进的（SOTA）零样本物体导航方法进行对比，尤其强调了与“此前 SR 最优方法”的对比。

## 4. 资源与算力

- 论文提供的内容（摘要与元数据）中**未明确说明**所使用的 GPU 型号、数量、训练时长或推理计算资源等详细信息。
- 因此无法评估其算力成本与可复现所需的硬件要求。

## 5. 实验数量与充分性

- **实验组数**：摘要中仅明确报告了在 HM3D 和 HSSD 两个基准上的主实验，以及一次与“先前最佳 SR 方法”的对比结果。未详细列出消融实验或更多变体实验。
- **充分性评估**：从已提供的信息看，实验覆盖了两个主流具身导航基准，且报告了 SOTA 的 SR 和 SPL，表明方法在多个环境下具有一定泛化性。但由于摘要内容有限，无法判断是否进行了充分的消融实验（如体素分辨率、语义先验来源、路径规划策略等敏感度分析），因此不能完全确认实验的完整性与公平性。

## 6. 主要结论与发现

- BeliefMapNav 在两个基准（HM3D、HSSD）上均取得了 **SOTA 的 SR 和 SPL**。
- 相比“此前 SR 最优方法”，SPL 提升了 **9.7 个百分点**，说明其不仅在成功率上表现优异，在**路径效率**上也有显著优势。
- 结论表明，三维信念地图能够有效增强零样本物体导航中的空间推理能力，为具身导航提供了一种新的全局表示范式。

## 7. 优点

- **全局性**：首次在零样本导航中引入三维体素信念地图，克服了贪婪局部决策的局限，实现了全局环境感知与推理。
- **高效结合语义与空间**：巧妙地将 LLM 语义先验与视觉嵌入融合到层次化三维空间中，使语言推理具有空间锚点。
- **即插即用**：无需预建地图、无需任务训练，具有较强的通用性与可扩展性。
- **显著性能提升**：在标准基准上同时提升 SR 和 SPL，尤其在路径效率上提升明显，具备实际应用潜力。

## 8. 不足与局限

- **信息缺失**：由于提供内容仅为摘要，方法中的体素分辨率、先验来源、更新公式、规划算法等细节未展开，无法深入评估其技术完整性与复现性。
- **实验覆盖有限**：仅在仿真数据集（HM3D、HSSD）上验证，未提及真实机器人实验、动态障碍物、多目标或更复杂语言指令场景。
- **计算与存储开销**：三维体素地图在大型环境中可能产生较高的内存与计算开销，摘要中未讨论资源效率问题。
- **潜在偏差**：LLM 先验可能存在环境或文化偏差，可能导致在非典型场景中的导航失败；摘要未讨论此类鲁棒性分析。
- **公平性存疑**：未提供与其他方法在相同计算资源条件下的详细对比，也没有消融实验来验证各组件（如语义先验 vs. 视觉嵌入 vs. 路径规划）的独立贡献。

（完）
