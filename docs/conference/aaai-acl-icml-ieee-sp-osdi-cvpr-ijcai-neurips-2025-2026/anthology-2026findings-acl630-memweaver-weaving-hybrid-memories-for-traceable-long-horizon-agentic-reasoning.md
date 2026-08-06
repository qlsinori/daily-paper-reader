---
title: "MemWeaver: Weaving Hybrid Memories for Traceable Long-Horizon Agentic Reasoning"
title_zh: MemWeaver：编织混合记忆以实现可追踪的长程智能体推理
authors: "Juexiang Ye, Xue Li, Yang Xinyu, Chengkai Huang, Lanshun Nie, Lina Yao, Dechen Zhan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.630.pdf"
tags: ["query:semantic-map"]
score: 4.0
evidence: 面向LLM智能体的混合长期记忆架构；属于长期记忆设计，但非空间记忆
tldr: 针对长时程LLM智能体中记忆系统依赖非结构化检索或粗略抽象导致时间冲突与推理脆弱的问题，提出MemWeaver统一记忆框架。该框架由时间图记忆、经验记忆和段落记忆三类组件构成，分别支持结构化关系推理、重复交互模式抽象以及原始文本证据保留。通过将这些记忆组件织入智能体推理流程，实现了时序一致、多跳可追溯的跨会话复用。实验证明了其在长程推理中的有效性，为智能体长期记忆架构设计提供了新参考。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 887, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 823, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 798, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 348, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1601, \"height\": 208, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1605, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1604, \"height\": 210, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1588, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1597, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl630/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1650, \"height\": 1328, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1658, \"height\": 795, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 778, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1551, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 664, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1535, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1538, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1660, \"height\": 1036, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1661, \"height\": 1036, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 807, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1537, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl630/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1666, \"height\": 741, \"label\": \"Table\"}]"
motivation: 现有LLM智能体记忆系统依赖非结构化检索或粗略抽象，导致长程交互中出现时间冲突、推理脆弱和追溯困难。
method: 提出MemWeaver统一记忆框架，融合时间图记忆、经验记忆与段落记忆三类组件，支持结构化推理与证据保留。
result: 实验表明该框架能够改善长时程智能体推理的时序一致性与可追溯性，提升跨会话经验复用效果。
conclusion: MemWeaver为长程智能体推理提供了可解释的混合记忆架构，对持续学习和记忆管理具有参考价值。
---

## Abstract
Large language model-based agents operating in long-horizon interactions require memory systems that support temporal consistency, multi-hop reasoning, and evidence-grounded reuse across sessions. Existing approaches largely rely on unstructured retrieval or coarse abstractions, which often lead to temporal conflicts, brittle reasoning, and limited traceability. We propose MemWeaver, a unified memory framework that consolidates long-term agent experiences into three interconnected components: a temporally grounded graph memory for structured relational reasoning, an experience memory that abstracts recurring interaction patterns from repeated observations, and a passage memory that preserves original textual evidence. MemWeaver employs a dual-channel retrieval strategy that jointly retrieves structured knowledge and supporting evidence to construct compact yet information-dense contexts for reasoning. Experiments on the LoCoMo benchmark demonstrate that MemWeaver substantially improves multi-hop and temporal reasoning accuracy while reducing input context length by over 95% compared to long-context baselines.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究背景

- 面向长时程交互的 LLM 智能体需要具备**时序一致性**（temporal consistency）、**多跳推理**（multi-hop reasoning）和**跨会话、基于证据的记忆复用**能力。
- 现有记忆系统主要依赖**非结构化检索**（如向量相似度检索）或**粗略抽象**（如 summarization-based memory），导致三类典型缺陷：
  - **时间冲突**：无法正确建模事件之间的先后与因果关系；
  - **推理脆弱**：多跳关系信息被扁平化或截断，难以支撑复杂推理；
  - **追溯性有限**：缺乏对原始证据的保留，无法回溯验证。
- 本文提出 **MemWeaver**，一个统一的混合记忆框架，旨在通过**结构化图记忆 + 经验抽象 + 原始文本证据**三类记忆的协作，解决上述问题。

## 2. 方法论

MemWeaver 的核心思想是**将长程智能体经验编织为互补的三类记忆组件**，并通过双通道检索将它们织入推理上下文。

- **三大记忆组件**：
  - **时间图记忆（Temporal Graph Memory）**：将交互中的实体与事件以时间标注的图结构存储，支持结构化关系推理和时序查询。
  - **经验记忆（Experience Memory）**：从重复出现的交互模式中抽象出经验性规律（如常用策略、失败模式、用户偏好倾向等），支持跨会话的高层复用。
  - **段落记忆（Passage Memory）**：保留原始文本片段作为证据，支持精细追溯与事实核查。
- **双通道检索策略（Dual-Channel Retrieval）**：
  - 通道一：从时间图记忆中检索**结构化知识子图**；
  - 通道二：从段落记忆中检索**支撑性原始证据**；
  - 最终将结构化知识与证据融合，构建**紧凑但信息密集**的推理上下文。
- 整体推理流程可表述为：*query → 双通道检索 → 图/经验/段落证据融合 → 上下文压缩 → 推理输出*，实现时序一致、可追溯的跨会话复用。

## 3. 实验设计

- **Benchmark**：在 **LoCoMo benchmark**（长程会话记忆基准）上进行评估，该基准专注于长时间多轮对话中的多跳推理与时序推理能力测试。
- **对比方法**：元数据中未列出具体基线名单，但根据论文背景可推断其对比包括：
  - 长上下文直接推理基线（long-context baselines）；
  - 现有记忆系统方法（如基于摘要、向量检索的记忆方法）。
- **评估维度**：
  - 多跳推理准确率；
  - 时序推理准确率；
  - 输入上下文长度压缩率。
- 元数据中的图表清单（11张表格、10张图）表明实验包含主结果、多组消融实验与详细案例分析。

## 4. 资源与算力

- 元数据（PDF 提取文本）中**未明确说明**使用的 GPU 型号、数量、训练/推理时长等算力信息。
- 同样未提供模型参数量级、微调或仅推理等细节。
- 这一点需要在论文原文中进一步核实，或视为**作者未报告算力资源**。

## 5. 实验数量与充分性

- **实验体量**：从元数据可见约 11 张表格与 10 张图，涵盖主实验、消融实验和案例分析，实验数量较充足。
- **覆盖范围**：
  - 包含多跳推理、时序推理、上下文压缩等核心指标的对比；
  - 包含图记忆、经验记忆、段落记忆各组件的贡献消融（据图/表推断）；
  - 包含输入长度缩减效果的分析。
- **充分性评价**：
  - 优势：指标覆盖了论文核心主张（时序一致性、多跳推理、可追溯性），且有压缩率等实用性验证。
  - 不足：**仅使用 LoCoMo 单一 benchmark**，缺乏跨数据集或真实应用场景的验证；未提及使用多种基础模型验证泛化性；未提供统计显著性检验等信息。

## 6. 主要结论与发现

- MemWeaver 在 LoCoMo 上**显著提升多跳推理和时序推理准确率**。
- 相比长上下文直接推理基线，**输入上下文长度减少超过 95%**，同时保持甚至提升推理性能，证明了“压缩但信息密集”的记忆上下文构建策略的有效性。
- 三类记忆组件的协同（结构化推理 + 经验抽象 + 证据保留）是提升可追溯性和推理稳健性的关键。

## 7. 优点

- **记忆类型互补设计合理**：图记忆负责结构、经验记忆负责抽象、段落记忆负责证据，职责划分清晰，契合人类记忆的多层组织方式。
- **可解释性强**：由于保留了原始文本证据与结构化图路径，模型推理过程有据可查，适合需要审计或可信赖的智能体场景。
- **上下文高效性**：95%以上的输入压缩率显著降低了长程任务的计算开销，具有良好的实用潜力。
- **方法论迁移性**：该框架不仅适用于对话式智能体，也适用于通用长程任务型 agent 的持续学习场景。

## 8. 不足与局限

- **数据覆盖面有限**：仅使用 LoCoMo 一个长程对话 benchmark，缺乏多领域、多任务类型的评估，如工具调用型 agent 或具身智能场景。
- **泛化性待验证**：未报告在多种尺寸或多种 LLM 上的稳定性；方法对弱基座模型的鲁棒性未知。
- **算力信息缺失**：未说明模型部署的硬件资源，降低了可复现性信息完备度。
- **未提供开源链接**：元数据中未见代码或数据发布信息，影响他人复现与后续研究。
- **时效性评估不足**：记忆的长期累积效应（如超过数百轮会话后的稳定性、遗忘策略）未见明确实验设计。
- **可能存在基准偏向**：LoCoMo 对时序图结构的测试倾向可能与 MemWeaver 的设计高度匹配，需警惕过拟合于该基准形态的风险。

（完）
