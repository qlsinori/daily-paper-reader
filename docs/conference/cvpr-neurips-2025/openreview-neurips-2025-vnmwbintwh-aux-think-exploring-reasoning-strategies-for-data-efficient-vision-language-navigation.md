---
title: "Aux-Think: Exploring Reasoning Strategies for Data-Efficient Vision-Language Navigation"
title_zh: 辅助思考：探索数据高效视觉语言导航的推理策略
authors: "Shuo Wang, Yongcai Wang, Wanting Li, Xudong Cai, Yucheng Wang, Maiyue Chen, kaihui.wang, Zhizhong Su, Deying Li, Zhaoxin Fan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=vNmWbINtwH"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 视觉语言导航中的推理策略系统评估
tldr: 视觉语言导航（VLN）要求智能体遵循指令在复杂环境中导航，但其推理策略尚未被系统研究。本文首次对多种推理策略进行对比，包括直接动作预测、先推理后动作和辅助推理等，并探索其在数据高效微调下的表现。实验表明，采用合适的辅助推理策略可显著提升指令接地和泛化能力，为高效VLN智能体的设计提供了依据。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLN是长时程动作任务，但现有推理研究多聚焦静态任务，缺乏对导航推理策略的分析。
method: 对比No-Think、Pre-Think等推理模式，并通过辅助任务增强指令与场景的语义关联。
result: 辅助推理策略在少数据条件下显著提升导航指令跟随准确率与成功率。
conclusion: 推理策略是提升VLN数据效率与泛化能力的关键因素。
---

## Abstract
Vision-Language Navigation is a critical task for developing embodied agents that can follow natural language instructions to navigate in complex real-world environments.  Recent advances by finetuning large pretrained models have significantly improved generalization and instruction grounding compared to traditional approaches. However, the role of reasoning strategies in navigation—an action-centric, long-horizon task—remains underexplored, despite Chain-of-Thought reasoning's demonstrated success in static tasks like question answering and visual reasoning. To address this gap, we conduct the first systematic evaluation of reasoning strategies for VLN, including No-Think (direct action prediction), Pre-Think (reason before action), and Post-Think (reason after action). Surprisingly, our findings reveal the Inference-time Reasoning Collaps issue, where inference-time reasoning degrades navigation accuracy, highlighting the challenges of integrating reasoning into VLN. Based on this insight, we propose Aux-Think, a framework that trains models to internalize structured reasoning patterns through CoT supervision during training, while preserving No-Think inference for efficient action prediction. To support this framework, we release R2R-CoT-320k, a large-scale Chain-of-Thought annotated dataset.  Empirically, Aux-Think significantly reduces training effort without compromising performance.

---

## 论文详细总结（自动生成）

# 论文总结：Aux-Think: Exploring Reasoning Strategies for Data-Efficient Vision-Language Navigation

## 1. 核心问题与整体含义

- **研究背景**：视觉语言导航（Vision-Language Navigation, VLN）要求智能体在真实复杂环境中根据自然语言指令进行动作决策，是具身智能领域的核心任务。近年来，通过对大规模预训练模型进行微调，VLN 在泛化能力和指令接地（instruction grounding）上取得了显著进展。
- **核心问题**：尽管思维链（Chain-of-Thought, CoT）推理在问答、视觉推理等静态任务中被证明有效，但在以行动为中心、长时程（long-horizon）的导航任务中，**推理策略的作用尚未得到系统研究**。论文旨在填补这一空白，探究不同推理模式对 VLN 性能的影响。
- **整体含义**：论文首次系统评估了多种推理策略，并发现“推理时推理反而会降低导航精度”的反直觉现象（Inference-time Reasoning Collapse）。在此基础上提出的 **Aux-Think** 框架能够在不牺牲推理效率的前提下，保留结构化推理带来的训练收益，为数据高效的 VLN 智能体设计提供了新思路。

## 2. 论文提出的方法论：核心思想、技术细节与流程

- **核心思想**：将“推理”从推理阶段转移到训练阶段——通过训练时施加 CoT 监督让模型内化结构化推理模式，而在推理时恢复为“无思考”（No-Think）的直接动作预测，从而避免推理时推理带来的性能下降。
- **技术细节与流程**：
  1. **对比三种基线推理策略**：
     - **No-Think**：直接预测动作，无显式中间推理。
     - **Pre-Think**：在动作预测之前先生成理由/推理过程。
     - **Post-Think**：先预测动作，再生成事后解释。
  2. **发现问题**：实验发现 Pre-Think 和 Post-Think 在推理阶段会降低导航准确率，即“Inference-time Reasoning Collapse”。
  3. **提出 Aux-Think**：
     - 在**训练阶段**，使用 CoT 标注数据对模型进行监督，迫使模型学习结构化的思考模式；
     - 在**推理阶段**，丢弃显式推理输出，仅保留 No-Think 的动作预测路径，实现高效且准确的决策。
  4. **配套数据**：构建并发布 **R2R-CoT-320k**，一个大规模带有 CoT 标注的导航数据集（320k 条），用于支撑 Aux-Think 的训练。

## 3. 实验设计

- **数据集/场景**：使用 VLN 领域标准基准 **R2R**（Room-to-Room）相关任务；论文额外构建了 **R2R-CoT-320k** 作为 CoT 监督训练数据。
- **Benchmark**：R2R 数据集上的标准导航指标（如成功率、路径长度加权成功率等，摘要未列出具体数值）。
- **对比方法**：
  - 无推理的 **No-Think**（直接动作预测）；
  - **Pre-Think**（先推理后动作）；
  - **Post-Think**（先动作后推理）；
  - 以及论文提出的 **Aux-Think**。
- **实验内容**：主要考察不同推理策略在数据高效微调（data-efficient finetuning）情境下的表现，即采用较少训练数据时各策略的导航性能与指令跟随能力。

## 4. 资源与算力

- **论文摘要与元数据中未提及具体的算力资源**，包括 GPU 型号、数量、训练时长等。
- 由于提供的材料有限，无法获知训练成本、模型参数量或推理开销的定量细节。
- 仅能推断：Aux-Think 在推理时采用 No-Think 路径，因此推理计算开销较低；训练时需要额外使用 CoT 监督数据，可能增加训练成本，但论文强调其“显著减少训练努力”（reduces training effort）——这里的“训练努力”更可能指数据效率或训练所需样本量，而非 GPU 资源。

## 5. 实验数量与充分性

- **已知实验**：论文包含对 No-Think、Pre-Think、Post-Think 三种策略的对比实验，以及 Aux-Think 的验证实验；还包含在数据高效（少样本）场景下的评估。
- **可能存在的其他实验**：由于仅提供摘要，无法确认是否包含完整的消融实验、跨场景泛化测试、不同数据规模曲线等。通常此类论文会包含更多消融，但当前信息不足。
- **充分性评估**：
  - 从摘要看，实验设计聚焦于“推理策略”这一清晰维度，对比合理，能够支撑主要结论；
  - 但缺少详细数值、统计显著性和多基准验证（如 R2R 之外的 VLN 数据集）的说明，因此**实验的充分性和全面性在当前信息下无法完整判断**。
  - 数据高效场景的实验符合“Data-Efficient”标题，但训练数据的具体规模、微调协议（如参数高效微调 vs 全量微调）未明确。

## 6. 论文的主要结论与发现

- **发现“推理时推理崩溃”现象**：在 VLN 这类长时程动作任务中，显式地在推理阶段进行 CoT 推理（Pre-Think / Post-Think）反而会降低导航准确率，说明简单地将静态任务中的推理模式迁移到导航任务并不适用。
- **Aux-Think 的有效性**：通过在训练阶段注入 CoT 监督、推理阶段恢复无思考模式，Aux-Think 能够在保持高效推理的同时，显著降低训练所需数据量，且不牺牲性能。
- **推理策略是关键因素**：推理策略的选择显著影响 VLN 的数据效率与泛化能力，应作为智能体设计的重要考虑维度。
- **公开数据集**：R2R-CoT-320k 可作为后续 VLN 推理研究的公共资源。

## 7. 优点

- **问题新颖**：首次系统研究 VLN 中的推理策略，填补了该领域空白，动机明确。
- **发现有趣且反直觉**：“推理时推理崩溃”这一现象对社区有重要警示价值，纠正了“更多推理一定更好”的直觉。
- **方法简洁高效**：Aux-Think 的思路清晰——训练时思考、推理时不思考，兼具性能与效率，容易复现。
- **实用性强**：面向数据高效场景，实际应用中可降低标注和训练成本。
- **贡献数据集**：R2R-CoT-320k 为后续研究提供标准化资源。

## 8. 不足与局限

- **信息完整性**：当前提供的材料仅为摘要，缺乏详细的模型结构、公式、训练细节和定量结果，无法深入评估方法的技术价值和性能幅度。
- **基准覆盖有限**：仅提到 R2R 及构建的 CoT 数据集，未提及在其他 VLN 基准（如 RxR、REVERIE、CVDN）上的泛化效果；不同任务可能对推理策略有不同的敏感度。
- **推理崩溃的原因分析不足**：摘要只报告了现象，未解释为何推理时推理会降低精度（例如是错误累积、长程依赖、还是训练与推理分布不匹配），机制分析不够深入。
- **“训练努力”定义模糊**：论文声称显著减少训练努力，但未明确是减少了训练样本、训练时间还是计算成本，可能引起歧义。
- **应用限制**：Aux-Think 依赖 CoT 标注数据，构建高质量 CoT 标注本身成本较高；若任务无法获得类似标注，方法适用性受限。
- **潜在偏差风险**：R2R-CoT-320k 由论文自动或人工标注，可能存在标注噪声或风格偏差，可能影响结论的可靠性，但摘要未提供质量控制细节。

（完）
