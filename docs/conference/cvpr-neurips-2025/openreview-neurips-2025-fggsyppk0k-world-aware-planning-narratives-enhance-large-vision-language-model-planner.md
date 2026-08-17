---
title: World-aware Planning Narratives Enhance Large Vision-Language Model Planner
title_zh: 世界感知规划叙事增强大型视觉语言模型规划器
authors: "Junhao Shi, Zhaoye Fei, Siyin Wang, Qipeng Guo, Jingjing Gong, Xipeng Qiu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=fggSyPPk0K"
tags: ["query:embodied-nav"]
score: 7.0
evidence: WAP为具身规划注入环境感知与空间推理，适用于模拟环境中的具身导航
tldr: 大型视觉语言模型在具身规划中常因缺乏环境感知而难以处理陌生环境与多步目标。本文提出世界感知规划叙事增强（WAP）框架，通过视觉外观建模、空间推理、功能抽象和语法接地四种认知能力为模型注入环境理解，使其能结合视觉推理执行长程交互。实验证明该方法显著提升复杂具身规划任务的性能，为智能体在模拟环境中自主决策提供支撑。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LVLM规划器依赖与情境无关的模仿学习，难以在陌生环境和多步目标下结合视觉推理进行决策。
method: 提出WAP框架，通过视觉外观建模、空间推理、功能抽象与语法接地四种能力，将环境知识注入规划器。
result: 在具身规划实验中，WAP增强了模型对上下文相关指令的理解，显著提升了长程任务的规划成功率。
conclusion: 表明环境感知的规划叙事可显著增强LVLM在模拟环境中处理复杂目标的能力，有助于机器人导航等应用。
---

## Abstract
Large Vision-Language Models (LVLMs) show promise for embodied planning tasks but struggle with complex scenarios involving unfamiliar environments and multi-step goals. 
Current approaches rely on environment-agnostic imitation learning that disconnects instructions from environmental contexts, causing models to struggle with context-sensitive instructions and rely on supplementary cues rather than visual reasoning during long-horizon interactions.
In this work, we propose World-Aware Planning Narrative Enhancement (WAP), a framework that infuses LVLMs with comprehensive environmental understanding through four cognitive capabilities (visual appearance modeling, spatial reasoning, functional abstraction, and syntactic grounding) while developing and evaluating models using only raw visual observations through curriculum learning.
Evaluations on the EB-ALFRED benchmark demonstrate substantial improvements, with Qwen2.5-VL achieving a 60.7 absolute improvement in task success rates—particularly in commonsense reasoning (+60.0) and long-horizon planning (+70.0). Notably, our enhanced open-source models outperform proprietary systems like GPT-4o and Claude-3.5-Sonnet by a large margin.

---

## 论文详细总结（自动生成）

好的，以下是对该论文的详细中文总结。

## 论文总结：世界感知规划叙事增强大型视觉语言模型规划器

### 1. 核心问题与整体含义（研究动机和背景）
- **核心问题**：大型视觉语言模型（LVLM）在具身规划任务中展现出潜力，但在应对涉及**陌生环境**和**多步目标**的复杂场景时表现不佳。
- **现有方法的缺陷**：当前主流方法依赖于与情境无关（environment-agnostic）的模仿学习，导致指令与视觉环境上下文脱节。这使得模型在面对依赖于环境上下文的指令时难以理解，并在长程交互中更依赖附加的提示线索（如物体检测框）而非自身的视觉推理能力。
- **整体含义**：本研究旨在解决LVLM在具身规划中“缺乏环境感知”的瓶颈，通过注入环境知识来提升其在复杂动态场景下的自主决策能力，从而推动具身智能在机器人导航等领域的应用。

### 2. 方法论（WAP框架）
- **核心思想**：提出**世界感知规划叙事增强（World-Aware Planning Narrative Enhancement, WAP）**框架，旨在为LVLM注入全面的环境理解，而非仅仅模仿规划轨迹。
- **四种认知能力**：WAP框架通过构建规划叙事，系统性地增强模型的四种环境认知能力：
  - **视觉外观建模**：让模型理解环境中物体和场景的外观特征。
  - **空间推理**：增强模型对物体间空间关系、布局和可达性的判断能力。
  - **功能抽象**：使模型理解物体和区域的潜在功能（如可用于烹饪、可用于放置物品）。
  - **语法接地**：将语言指令与具体的视觉实体和空间状态进行对齐和绑定。
- **训练策略**：采用**课程学习（Curriculum Learning）**，仅使用**原始视觉观察**作为输入来开发和评估模型，避免了对外部辅助信号的依赖，确保模型必须真正理解视觉环境。
- **技术流程**：整个流程强调环境信息的结构化注入，通过生成的叙述性文本作为中间桥梁，促使LVLM将视觉信息与任务指令结合进行推理，从而生成上下文相关的行动计划。

### 3. 实验设计
- **基准与数据集**：使用 **EB-ALFRED** 基准进行评估。该基准侧重于需要环境感知和常识推理的具身导航与操作任务。
- **对比方法**：
  - **基线模型**：未增强的Qwen2.5-VL模型（自对比）。
  - **专有系统**：OpenAI的 **GPT-4o** 和 Anthropic的 **Claude-3.5-Sonnet**。
- **评估指标**：主要指标为**任务成功率（Task Success Rate）**，并针对**常识推理**和**长程规划**等子任务类型进行细分评测。

### 4. 资源与算力
- **未明确说明**：提供的论文元数据与摘要中**未提及**任何关于GPU型号、数量、训练时长或具体算力开销的细节。
- **注意**：由于原始PDF文本未能获取，该项信息缺失，无法对训练成本进行评估。

### 5. 实验数量与充分性
- **实验数量**：基于现有信息，实验主要围绕EB-ALFRED基准展开，核心实验包括：
  - 主实验：WAP增强后的Qwen2.5-VL对比其基线版本。
  - 跨模型对比：与专有模型（GPT-4o, Claude-3.5-Sonnet）的横向对比。
- **充分性和客观性评估**：
  - **优势**：在同一基准下与当前最强的专有闭源模型进行对比，且开源模型大幅胜出，具有较强的说服力。
  - **局限性**：由于无法查看完整论文，**未确认是否存在系统性的消融实验**（如单独验证每种认知能力的贡献）。因此，关于各模块有效性的证据尚不明确。实验场景局限于**模拟环境**（EB-ALFRED），缺乏真实世界物理环境的验证。

### 6. 主要结论与发现
- **显著性提升**：WAP框架带来了显著的性能提升。在EB-ALFRED基准上，Qwen2.5-VL在任务成功率上获得了 **+60.7** 的绝对提升。
- **子任务改善**：在**常识推理**方面提升 +60.0，在**长程规划**方面提升 +70.0，表明该方法对复杂指令理解有显著促进作用。
- **开源超越闭源**：经WAP增强后的开源模型，在任务成功率上**大幅超越**了GPT-4o和Claude-3.5-Sonnet等专有系统，证明了该方法的卓越有效性。
- **核心贡献**：环境感知的规划叙事能有效增强LVLM在模拟环境中处理复杂目标的能力，为该领域提供了一种新的范式。

### 7. 优点（方法与实验亮点）
- **针对性强**：准确点出当前LVLM规划的痛点，即缺乏环境理解能力。
- **创新性框架**：提出的WAP框架概念清晰，通过四种认知能力系统性地构建环境知识，为知识注入提供了结构化路径。
- **实用性与泛化性**：仅依赖原始视觉观察，无需额外的传感器数据或手工标注，提升了方法在真实场景中的应用潜力。
- **实验成果突出**：量化结果非常亮眼（+60.7成功率），且在与顶级专有模型的对比中取得压倒性胜利，验证了所提方法的显著优势。

### 8. 不足与局限
- **实验场景受限**：目前仅在EB-ALFRED等模拟环境中验证，未在真实物理世界或更复杂的开放环境中进行测试。模拟环境中的视觉多样性、动态性及传感器噪声与真实世界有差距，存在**泛化风险**。
- **依赖基准偏差**：性能高度依赖于EB-ALFRED基准的数据分布。若基准本身存在特定偏差（如任务类型单一），可能会高估模型在实际应用中的能力。
- **计算成本未知**：由于未提及训练算力，无法判断该方法是否高效。如果训练成本过高，可能会限制其在资源受限场景中的应用。
- **消融研究缺失**：现有信息无法确认是否对不同认知能力模块进行了详细的消融实验，导致对每种能力（如空间推理、功能抽象）具体贡献的评估不够透明。模型内部是否真的获得了这些认知能力，或是通过其他隐藏模式获得了性能提升，尚需进一步验证。

（完）
