---
title: "TANGO: Training-free Embodied AI Agents for Open-world Tasks"
title_zh: TANGO：面向开放世界任务的无训练具身AI智能体
authors: "Ziliotto, Filippo, Campari, Tommaso, Serafini, Luciano, Ballan, Lamberto"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ziliotto_TANGO_Training-free_Embodied_AI_Agents_for_Open-world_Tasks_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 使用点目标导航与基于记忆的探索作为开放世界具身任务的基础原语
tldr: 针对多任务具身智能体需要重新训练的问题，论文提出TANGO框架，将简单的PointGoal导航模型与记忆式探索策略作为原语，由LLM在上下文中组合这些原语来执行具体任务。TANGO无需额外训练即可完成多种具身任务，展示了LLM编排基础导航能力的高效性。该工作验证了记忆化探索与点目标导航相结合在开放世界任务中的通用性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 840, \"height\": 887}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1723, \"height\": 1124}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 874, \"height\": 255}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 802}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 422}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 820, \"height\": 542}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 655, \"height\": 485}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 898, \"height\": 384}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 443}]"
motivation: 现有具身智能体依赖任务专属训练，难以泛化到开放世界多种任务且成本高。
method: 将PointGoal导航模型与记忆探索策略封装为基础原语，由LLM组合原语解决新任务，无需训练。
result: 在多种开放世界任务上验证了单个模型不训练即可适用不同任务的能力。
conclusion: 展示了利用LLM组合已有导航原语实现通用具身智能体的潜力，并为后续研究提供范例。
---

## Abstract
Large Language Models (LLMs) have demonstrated excellent capabilities in composing various modules together to create programs that can perform complex reasoning tasks on images. In this paper, we propose TANGO, an approach that extends the program composition via LLMs already observed for images, aiming to integrate those capabilities into embodied agents capable of observing and acting in the world. Specifically, by employing a simple PointGoal Navigation model combined with a memory-based exploration policy as a foundational primitive for guiding an agent through the world, we show how a single model can address diverse tasks without additional training. We task an LLM with composing the provided primitives to solve a specific task, using only a few in-context examples in the prompt. We evaluate our approach on three key Embodied AI tasks: Open-Set ObjectGoal Navigation, Multi-Modal Lifelong Navigation, and Open Embodied Question Answering, achieving state-of-the-art results without any specific fine-tuning in challenging zero-shot scenarios.

---

## 论文详细总结（自动生成）

# TANGO：面向开放世界任务的无训练具身AI智能体（CVPR 2025）

## 1. 核心问题与整体含义（研究动机）

- **背景**：LLM（大语言模型）已在视觉任务中展现出强大的程序组合能力（如 VisProg、ViperGPT），能以少量上下文示例生成组合式程序，无需任务特化训练。
- **核心问题**：这一范式能否拓展到**具身智能（Embodied AI）**领域？即让智能体不仅"看图"还能"在环境中行动"——自主导航、探索、感知并完成开放世界任务。
- **现有局限**：
  - 端到端方法（如 PointGoal 导航）需要海量训练（如 25 亿步），且无法跨任务复用；
  - 模块化方法虽共享探索/导航组件，但切换到新任务时仍需要手动调整模块结构；
  - LLM 导航方法（如 NavGPT）多为单任务优化，缺乏组合式、可扩展的系统架构。
- **TANGO 的定位**：以简单的**PointGoal 导航模型** + **记忆增强的探索策略**为底层原语，由 LLM 在上层组合这些原语，构建一个**无需额外训练**即可应对多种具身任务的通用框架。

## 2. 方法论

### 2.1 核心思想

- 受 VisProg 启发，用 LLM 作为**规划器**，将用户自然语言指令转换为**可执行的伪代码程序**。
- 每个程序由若干**模块/原语（primitives）**构成（如 `detect`、`navigate_to`、`explore_scene`、`answer`、`match` 等），这些模块要么调用预训练视觉模型，要么是简单 Python 子函数。
- 框架内无需任何任务专属微调，仅通过 15 个固定"上下文示例"引导 LLM 为不同任务生成正确的程序组合。

### 2.2 关键模块与工作机制

- **Program Interpreter（程序解释器）**：
  - 按行解析 LLM 生成的程序；
  - 提取每个模块的参数名、参数值及输出变量名；
  - 在环境中逐步执行模块，更新程序状态，并支持输出监控与解释性分析。

- **导航模块（Navigation Module）**：
  - 基于预训练的 PointGoal 导航策略（约 99% 成功率、亚秒级前向推理）；
  - 输入仅为**深度图像** + 相对目标点的距离/朝向；
  - 起始时执行 360° 旋转以初始化探索边界。

- **探索策略（Exploration Policy）**：
  - 借鉴 VLFM [55] 的**语言接地价值图（language-grounded value map）**方法；
  - 基于深度观测构建占据图，结合 BLIP2 生成视觉-语言价值图，引导智能体高效寻找目标；
  - **拓展之处**：引入**记忆机制**——将价值图每个像素编码为特征向量并逐步更新形成"记忆特征图"；当新目标出现（文本或图像形式）时，通过余弦相似度重新评分记忆图，若高分像素超过阈值则直接导航至记忆中的目标位置，实现终身（lifelong）多目标导航。

### 2.3 任务适配

- **开放词汇目标导航（OVON）**：使用 Owlv2（开放类别）或 DETR（COCO 类别）检测目标，随后导航至检测框中心（结合深度计算方位）。
- **GOAT-Bench（多模态终身导航）**：目标可通过类别名、描述文本或图像指定；图像目标用 BLIP2 提取语义 + SuperGlue 做实例匹配，记忆机制在顺序目标切换时复用已有空间记忆。
- **开放具身问答（OpenEQA）**：LLM 将问题分解为"先去哪、看什么、答什么"，最终由 BLIP2 基于观测生成自然语言回答。

## 3. 实验设计

| 任务 | 数据集 / Benchmark | 评估指标 | 对比方法 |
|---|---|---|---|
| 开放词汇目标导航 | HM3D-OVON（val unseen，379 类别、15k+ 对象） | SR、SPL | RL、BCRL、DAgRL、VLFM、DAgRL+OD |
| 多模态终身导航 | GOAT-Bench（val unseen，312 类别、5~10 个序列目标） | SR、SPL | SenseAct-NN Skill Chain / Monolithic、Modular GOAT、Modular Clip on Wheels |
| 开放具身问答 | OpenEQA（A-EQA 子集，1600+ 问答对，180+ 场景） | LLM-Match Score（1~5 分制归一化）、Answer Accuracy | Human Agent、Blind LLMs、Socratic LLMs（Frame / Scene-Graph Captions） |

- **环境设置**：所有实验均在 Habitat 模拟器中完成；各任务沿用对应 benchmark 的标准智能体配置（传感器高度、RGB 分辨率、步长、转角等）。
- **零样本设定**：除 PointGoal 导航模型在 HM3D 训练集上预训练外（测试场景均未在训练中出现），所有视觉模块均为预训练现成模型，无任何任务专属微调。

## 4. 资源与算力

- **论文未明确披露** GPU 型号、数量或总训练/评估时长等具体算力信息。
- 仅间接提及：
  - PointGoal 基础导航模型为预训练模型（参考 DD-PPO 等文献）；
  - 所有模块均为开源预训练模型（Owlv2、BLIP2、CLIP、SuperGlue、DETR），无需从头训练；
  - 作者感谢 University of Padova 提供计算资源，但未给出硬件细节。

## 5. 实验数量与充分性

- **覆盖广度较好**：3 个不同性质的任务（开放词汇检测导航、序列多模态导航、开放问答），涵盖探索、记忆复用、语义理解、实例匹配等核心具身能力。
- **对比公平性**：均为零样本/无微调设定下的同类方法对比，OBJNAV 和 GOAT 使用标准 SR/SPL 指标，EQA 采用 LLM 评分协议，与既有文献保持一致。
- **可能不足**：
  - OVON 与 GOAT 任务**缺少消融实验**（如记忆机制有/无、不同检测器对比等）；
  - EQA 仅报告 Score 指标，Answer Accuracy 放在补充材料中，未独立分析各问题类别（空间推理 vs. 属性识别）的分项表现；
  - 失败分析仅在 EQA 上进行，未覆盖其他任务。

## 6. 主要结论与发现

- TANGO 在**三个零样本任务**上达到或接近 SOTA：OVON SR 35.5%、GOAT SR 32.1%（优于 SOTA +2.6%）、OpenEQA Score 37.2%（距最佳方法仅差 <1%）。
- 证明了"**简单 PointGoal 导航原语 + LLM 组合规划**"足以应对多种开放世界具身任务，无需任务特化训练，极大降低了具身导航的开发成本。
- 记忆机制显著提升了终身导航任务表现；但记忆错误会导致路径效率显著下降。
- 失败分析显示：主要错误源于**检测模块**（停在错误目标或漏检，占比最高），LLM 程序生成错误仅占约 11.2%，说明探索策略本身较稳健。

## 7. 优点

- **真正的零训练框架**：全部依赖预训练模块 + LLM 上下文学习，规避了端到端方法的巨额训练成本。
- **模块化、可扩展、可解释**：模块可即插即用（可替换为更新的视觉模型）；每个执行步骤可追溯，便于失败诊断与系统调试。
- **任务泛化能力强**：同一组上下文示例、同一套模块，可适配目标导航、终身导航、EQA 三种不同任务。
- **记忆机制设计巧妙**：以特征向量地图形式压缩历史探索信息，在顺序目标切换时实现"记住曾见过的东西"，为终身导航提供了轻量且有效的方案。
- **对比实验合理**：与多种零样本 SOTA 方法对比，结果可信；失败分析增加了论文的工程实用价值。

## 8. 不足与局限

- **无明显性能碾压**：OVON 上仅与 VLFM/DAgRL+OD 持平，未见显著优势；EQA 低于最佳基线（虽差距很小）。
- **依赖 LLM 质量**：复杂/歧义的自然语言指令会导致 LLM 选错原语或目标，当前 GPT-4o 仍非完全可靠。
- **检测环节是瓶颈**：开放词汇检测器的误报/漏报是最大失败来源，框架的正确性很大程度受限于底层视觉感知模型的性能。
- **探索机制局限**：若记忆中的目标信息有误，会显著降低路径效率；价值图阈值的选取也未做系统讨论。
- **缺少真实机器人验证**：所有实验均在 Habitat 模拟器中完成，未在真实环境中评估 sim-to-real 迁移。
- **未开源实现细节**（推测）：论文未提供代码链接或可复现配置，限制了社区复现与二次开发。
- **评估指标层面**：EQA 的 LLM 评分本身存在主观性；SPL 对运动代价的计算是否完全公平也因不同基线配置不同而存疑。
- **未来方向**：作者自述可扩展到 VLN（视觉语言导航）和开源 LLM，但尚未实现验证。

> 总体而言，TANGO 在**无需训练即可处理多种具身任务**这一方向上迈出了扎实一步，验证了 LLM 编排底层导航原语的可行性与实用性；但其性能上限受制于底层感知模块的精度，且在实验深度上仍有提升空间。

（完）
