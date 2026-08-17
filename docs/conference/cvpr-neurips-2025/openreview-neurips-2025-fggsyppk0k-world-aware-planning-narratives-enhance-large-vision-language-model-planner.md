---
title: World-aware Planning Narratives Enhance Large Vision-Language Model Planner
title_zh: 世界感知规划叙事增强大型视觉语言模型规划器
authors: "Junhao Shi, Zhaoye Fei, Siyin Wang, Qipeng Guo, Jingjing Gong, Xipeng Qiu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=fggSyPPk0K"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 面向LVLM具身规划的世界感知增强，可应用于仿真环境导航
tldr: 大型视觉语言模型在具身规划任务中面对陌生环境和多步目标时表现不佳，现有方法常与环境无关地模仿学习，导致指令与上下文脱节。本文提出世界感知规划叙事增强（WAP），通过视觉外观建模、空间推理、功能抽象和句法接地四种认知能力，将环境理解注入LVLM规划器。该方法帮助模型在长程交互中依靠视觉推理而非外部线索完成任务，改善了复杂具身规划的成功率。该工作为具身导航等规划任务的环境感知推理提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: LVLM在陌生环境和多步目标下的具身规划能力受限于环境无关的模仿学习，无法有效利用视觉上下文。
method: 提出WAP框架，注入视觉外观、空间推理、功能抽象和句法接地四种环境认知能力，增强LVLM的长程规划。
result: 在复杂具身规划任务上提升了成功率，减少了对外部线索的依赖，改善了长程交互中的视觉推理。
conclusion: 验证了环境感知叙事增强对LVLM具身规划的有效性，适用于导航等具身智能任务。
---

## Abstract
Large Vision-Language Models (LVLMs) show promise for embodied planning tasks but struggle with complex scenarios involving unfamiliar environments and multi-step goals. 
Current approaches rely on environment-agnostic imitation learning that disconnects instructions from environmental contexts, causing models to struggle with context-sensitive instructions and rely on supplementary cues rather than visual reasoning during long-horizon interactions.
In this work, we propose World-Aware Planning Narrative Enhancement (WAP), a framework that infuses LVLMs with comprehensive environmental understanding through four cognitive capabilities (visual appearance modeling, spatial reasoning, functional abstraction, and syntactic grounding) while developing and evaluating models using only raw visual observations through curriculum learning.
Evaluations on the EB-ALFRED benchmark demonstrate substantial improvements, with Qwen2.5-VL achieving a 60.7 absolute improvement in task success rates—particularly in commonsense reasoning (+60.0) and long-horizon planning (+70.0). Notably, our enhanced open-source models outperform proprietary systems like GPT-4o and Claude-3.5-Sonnet by a large margin.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

大型视觉语言模型（LVLM）在具身规划任务中展现出潜力，但面对**陌生环境**和**多步目标**时表现不佳。现有方法采用与环境无关的模仿学习，导致模型：
- 无法将指令与环境上下文有效关联；
- 在长程交互中依赖外部辅助线索，而非自身视觉推理。

该研究旨在解决这一关键缺口，提升 LVLM 在复杂具身场景中的规划能力，进而推动具身智能在真实环境中的部署与应用。

---

### 2. 论文提出的方法论：世界感知规划叙事增强（WAP）

**核心思想：** 通过注入对环境的结构化理解，将“环境感知”嵌入 LVLM 规划器的决策过程，使模型能够基于视觉上下文进行推理，而非机械模仿。

**四种认知能力注入：**
1. **视觉外观建模**：捕捉环境中物体、区域的视觉特征；
2. **空间推理**：理解物体间的位置关系与可达性；
3. **功能抽象**：推断环境中各元素的功能与用途；
4. **句法接地**：将自然语言指令与视觉/空间信息进行对齐绑定。

**训练机制：** 仅使用**原始视觉观测**，采用**课程学习**方式逐步训练模型，从简单任务过渡到复杂长程任务，使模型在规划过程中逐步提升环境理解与推理能力。

> 论文未给出具体的数学公式或算法伪代码，其核心流程可概括为：环境视觉输入 → 四种认知能力建模 → 叙事增强提示 → LVLM 规划输出 → 行动执行。

---

### 3. 实验设计

- **基准数据集：** EB-ALFRED（具身规划 benchmark，基于 ALFRED 的扩展版本）。
- **评测任务类型：** 包括常识推理、长视野（long-horizon）规划等具身导航与操作任务。
- **对比方法：**
  - 基线 LVLM 模型；
  - 闭源商业系统：GPT-4o、Claude-3.5-Sonnet；
  - 开源增强模型：Qwen2.5-VL（WAP 增强版）。
- **评估指标：** 任务成功率（success rate）。

---

### 4. 资源与算力

论文元数据中**未明确说明**训练所用的 GPU 型号、数量及训练时长。从方法设计推断，WAP 仅依赖原始视觉观测和课程学习，**无需额外人工标注数据**，训练开销可能较同类具身规划方法更低。但具体算力需求需查阅论文原文细节，当前信息不足以给出确切数字。

---

### 5. 实验数量与充分性

从摘要和元数据可见：

- 主实验：在 EB-ALFRED 上对比了多种 LVLM 模型与商业系统；
- 类别消融：分别报告了常识推理（+60.0）和长视野规划（+70.0）的绝对提升；
- 交叉对比：开源模型 vs. 闭源模型（GPT-4o、Claude-3.5-Sonnet）。

**充分性评价：** 实验覆盖了核心 benchmark 和代表性对比对象，但元数据未展示多数据集交叉验证、不同模型规模的扩展实验或详细的消融设计。整体可视为“初步充分”，若在更多场景（如真实机器人平台）和更多基座模型上验证，将更具说服力。

---

### 6. 论文的主要结论与发现

- WAP 框架能显著提升 LVLM 在复杂具身规划中的任务成功率；
- **Qwen2.5-VL** 增强后取得 **60.7 个百分点的绝对成功率提升**，其中：
  - 常识推理任务提升 +60.0；
  - 长视野规划任务提升 +70.0；
- 增强后的开源模型大幅**超越**商业闭源系统（GPT-4o、Claude-3.5-Sonnet）；
- 模型在长程交互中**减少对外部线索的依赖**，更多依赖视觉推理完成目标。

---

### 7. 优点

- **创新性强**：将环境感知分解为四种认知能力，概念清晰、系统化；
- **数据效率高**：仅需原始视觉观测，无需额外标注，降低了数据成本；
- **效果显著**：在 benchmark 上取得大幅提升，且开源模型超越商业闭源模型，具有很高的实用价值；
- **训练策略合理**：课程学习符合具身任务由简到繁的认知规律；
- **研究价值突出**：为“环境感知叙事”这一方向提供了可复现框架，对未来具身导航、操作等任务具有借鉴意义。

---

### 8. 不足与局限

- **benchmark 覆盖面有限**：仅在 EB-ALFRED 一个基准上评测，缺少对更多具身环境（如 Habitat、Matterport3D、真实机器人）的验证；
- **应用场景受限**：面向仿真导航环境，真实世界中的动态变化、传感器噪声等因素未涉及；
- **消融与分析细节不足**：元数据中未给出四种认知能力各自的独立贡献分析，缺乏可解释性说明；
- **算力与复现成本未知**：未提及模型训练的计算资源、时间成本，影响复现与推广；
- **商业模型对比公平性存疑**：闭源模型的提示策略、微调机制等细节未知，可能存在对比不完全公平的情况；
- **泛化能力待验证**：对陌生环境类别（超出训练分布）的适应能力、跨领域迁移能力未展示。

---

（完）
