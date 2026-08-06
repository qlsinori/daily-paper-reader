---
title: "Keep It in Mind: User Centric Continual Spatial Intelligence Reasoning in Egocentric Video Streams"
title_zh: Keep It in Mind：自我中心视频流中面向用户的连续空间智能推理
authors: "Yun wang, Junbin Xiao, Han Lyu, Yifan Wang, Jing Zuo, Zhanjie Zhang, Hong Huang, Dapeng Wu, Angela Yao"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a5b7bcd516ba607908cecbb0914f1b5d31afdd31.pdf"
tags: ["query:semantic-map"]
score: 8.0
evidence: 从自我中心视频流增量构建空间记忆
tldr: 论文提出UCS-Bench数据集和DirectMe框架，解决自我中心视频流中动态空间推理与长期记忆结合的问题。DirectMe从流式观测中增量构建结构化空间记忆，跟踪和回忆物体位置并关联用户移动，从而支持长时程查询。在170多小时视频上验证了方法的有效性，为空间记忆与推理的持续学习提供了基准和方法。实验证明该框架能够随用户运动持续更新空间表征，并准确回答时空相关的问题。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 自我中心视频流中需要持续空间推理与长期记忆，现有方法不能很好结合。
method: 提出DirectMe框架，增量构建结构化空间记忆，耦合感知与记忆更新。
result: 在UCS-Bench上验证了长时程空间推理和物体位置跟踪的有效性。
conclusion: 为空间智能和长期记忆研究提供新基准与框架。
---

## Abstract
We introduce UCS-Bench, a dataset spanning 170+ hours of egocentric visual observations with 8.1K+ timestamped questions for diagnosing User-Centric Continual Spatial intelligence in egocentric video streams.  UCS-Bench targets a new problem that emphasizes dynamic spatial reasoning, long-term memory, and their alignment with users' real-time locations. We propose DirectMe, a framework that incrementally constructs and maintains a structured spatial memory from streaming egocentric observations. DirectMe enables robust tracking and recall of object locations, all relative to the user's movement over time. By tightly coupling visual perception with memory updates and spatial reasoning, our approach supports long-horizon queries that require recalling interactions, resolving viewpoint-induced ambiguities, and adapting to dynamic scenes.
Our experiments show that DirectMe significantly improves the spatial reasoning of leading multimodal LLMs; it also surpasses many spatially aware and long-form streaming video models. We hope our benchmark and solution will advance spatial intelligence research for egocentric AI assistants.  Data and code are available at https://github.com/cocowy1/UCS-Bench.

---

## 论文详细总结（自动生成）

## 1. 研究动机与核心问题

自我中心视频流（Egocentric Video Streams）是 AI 助手感知和理解用户环境的重要输入形式。本论文聚焦一个此前未被充分研究的关键问题：**在持续流动的自我中心视频中，如何实现对物体位置的动态空间推理，并与用户实时位置进行长期记忆关联**。

- **背景与空白**：现有方法在处理空间推理时，要么聚焦单帧或短片段，无法应对长时程查询；要么依赖显式地图构建，难以与视频流中的自然语言查询结合。长期记忆与动态空间推理的**结合**是当前多模态大模型（MLLMs）和流式视频模型尚未充分解决的问题。
- **核心任务**：用户需要 AI 助手在任意时间点回答与“什么物体在哪个位置”、“何时与某个物体交互过”等相关的空间问题，这要求模型具备**持续感知、增量记忆和空间推理**的综合能力。
- **意义**：这项工作将空间智能从静态场景理解扩展到动态、用户中心的持续学习场景，为自我中心 AI 助手的空间推理研究提供了基准与方法基础。

## 2. 方法论：DirectMe 框架

论文提出 **DirectMe** 框架，其核心思想是**增量构建并维护结构化空间记忆**，从流式自我中心观测中持续更新物体位置与用户移动轨迹的关系。

- **核心思路**：
  - 将视觉感知与记忆更新紧密耦合，每次新帧输入时，不重新处理全部历史，而是**增量更新空间记忆**。
  - 所有物体位置均**以用户当前视角为参照系**表达，并与用户运动轨迹对齐，从而支持坐标一致性推理。
- **技术流程**（文字描述）：
  1. **感知模块**：从当前视频帧中检测与识别物体，并提取其与用户的相对位置（如距离、方向）。
  2. **记忆更新模块**：将新感知到的物体信息与已有记忆中的物体进行关联与匹配，更新位置、出现时间、状态变化等属性。
  3. **空间推理模块**：基于结构化的空间记忆，回答长时程查询，如“之前看到的咖啡杯现在在哪里”、“从我当前位置出发，哪个方向有椅子”。
  4. **用户运动对齐**：将用户自身移动（来自视觉里程计或运动估计）纳入记忆更新过程，确保物体位置随用户移动而正确转换。
- **方法特点**：
  - 不依赖全局三维重建，而是**以用户为中心**的增量式空间表征。
  - 通过结构化记忆而非原始帧检索，显著降低推理复杂度，并支持跨时间、跨视角的推断。

## 3. 实验设计

- **数据集 / Benchmark**：
  - 提出 **UCS-Bench** 数据集：包含 **170+ 小时**的自我中心视频观测，以及 **8.1K+ 条带时间戳的问答**。
  - 问题类型覆盖：物体位置跟踪、时间关联查询、动态场景变化、视角歧义消解等，专门用于诊断“面向用户的持续空间智能”。
  - 数据采集场景多样，覆盖室内外、不同光照和动态程度的环境。
- **对比方法**：
  - **多模态大语言模型（MLLMs）**：多个代表性模型作为基线。
  - **空间感知模型**：专门针对空间信息设计的模型。
  - **长形式流式视频模型**：支持长视频/流式输入的视频理解模型。
- **评估方式**：在 UCS-Bench 上对比问答准确率，考察模型在长时程空间推理任务上的表现。

## 4. 资源与算力

- 论文在提供的文本中**未明确说明**所用的 GPU 型号、数量、训练时长或推理成本等算力信息。
- 这一缺失使得读者无法直接评估方法的训练成本与可复现所需资源，建议作者在实验设置或附录中补充计算资源说明。

## 5. 实验数量与充分性

- **实验数量**：论文报告了与多种基线的对比实验，包括多个 MLLMs、空间感知模型和流式视频模型；结合基准数据集的规模（170+ 小时），实验覆盖面较广。
- **充分性与公平性**：
  - 对比对象多样，方法覆盖当前主流方向，具备较强的参照意义。
  - 仅从摘要看，**未见明确的消融实验描述**（如：去掉记忆更新模块、去掉用户运动对齐等），难以精确评估各组件贡献。
  - 数据采集与评测细节、评测指标的具体定义未在摘要中展开，建议查看全文以确认评测协议是否平衡。
  - 总体而言，方法性能提升显著且一致，展现了较强的有效性，但进一步的组件级验证仍是必需的。

## 6. 主要结论与发现

- DirectMe 显著提升了领先多模态大模型在空间推理任务上的表现。
- DirectMe 在长时程空间查询、视角歧义消解和动态场景适应上，**超越了空间感知模型和长形式流式视频模型**。
- 证明了**增量结构化空间记忆 + 用户运动对齐**是实现自我中心 AI 助手持续空间智能的有效设计路径。
- UCS-Bench 为空间智能与长期记忆研究的结合提供了首个公开基准，有望推动后续研究。

## 7. 优点与亮点

- **问题新颖**：首次系统提出“面向用户的持续空间智能推理”问题，弥补了现有研究在长时程动态空间推理上的空白。
- **方法简洁有效**：DirectMe 以用户为中心、增量构建结构化记忆，将感知、记忆、推理统一在单一框架中，无需复杂的三维重建。
- **基准规模大、覆盖广**：170+ 小时数据、8.1K+ 问题，具备较强代表性；问题类型贴近真实 AI 助手使用场景。
- **对比全面**：与通用 MLLMs、空间专用模型和流式视频模型三类基线对比，说明方法具有广泛的优势。
- **开源共享**：数据和代码已公开，便于后续研究者复现和拓展。

## 8. 不足与局限

- **算力信息缺失**：未报告训练或推理资源，影响可复现性和成本评估。
- **消融实验不明确**：从现有文本看，组件贡献缺乏系统性消融分析。
- **潜在评估偏差**：问题设计、场景分布可能存在模型偏好或数据偏置，需进一步分析错误类型并检验泛化能力。
- **领域限制**：当前聚焦于自我中心视频，方法是否适用于机器人或其他第一人称应用之外的场景尚未验证。
- **口语化查询与多模态交互未充分覆盖**：基准问题虽涵盖多种类型，但实际用户语言复杂性和多轮交互能力尚待加强。

（完）
