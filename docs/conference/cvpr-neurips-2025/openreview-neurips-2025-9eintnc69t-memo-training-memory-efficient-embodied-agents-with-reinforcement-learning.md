---
title: "Memo: Training Memory-Efficient Embodied Agents with Reinforcement Learning"
title_zh: Memo：用强化学习训练记忆高效的具身智能体
authors: "Gunshi Gupta, Karmesh Yadav, Zsolt Kira, Yarin Gal, Rahaf Aljundi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=9eIntNc69t"
tags: ["query:vln-memory"]
score: 7.0
evidence: 基于强化学习的记忆高效具身智能体策略
tldr: 为了让具身智能体在长时间跨度中保持环境上下文，本文提出带记忆机制的Transformer架构Memo，通过强化学习训练对视觉输入进行显式记忆压缩。相比固定大小循环网络或全上下文Transformer，Memo能在控制计算成本的条件下保留关键历史信息。实验显示其在具身序贯决策任务上表现出更强的长期记忆利用与泛化能力，为记忆增强策略提供了高效方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视觉输入常超出Transformer上下文限制，现有固定大小记忆或全上下文方法难以兼顾长期信息保留与计算效率。
method: 提出Memo架构，在Transformer策略中引入可学习的记忆压缩模块，并以强化学习端到端训练。
result: 实验表明Memo在具身决策任务上能够更高效利用长期上下文，提升导航等任务性能。
conclusion: 该工作为长时程具身策略提供了一种内存高效且可扩展的记忆增强范式。
---

## Abstract
To enable embodied agents to operate effectively over extended timeframes, it is crucial to develop models that form and access memories to stay contextualized in their environment. In the current paradigm of training transformer-based policies for embodied sequential decision-making tasks, visual inputs often overwhelm the context limits of transformers, while humans can maintain and utilize a lifetime of experience compressed as memories. Significant compression is possible in principle, as much of the input is irrelevant and can be abstracted. However, existing approaches predominantly focus on either recurrent models with fixed-size memory or transformers with full-context reliance. In this work, we propose Memo, a transformer-based architecture and training recipe for reinforcement learning (RL) on memory-intensive, long-horizon tasks. Memo incorporates the creation and retrieval of memory by interleaving periodic summarization tokens with the inputs of a model during training. We demonstrate Memo’s effectiveness on a grid-world meta-RL benchmark and a multi-object navigation task in photo-realistic indoor settings. Memo outperforms naive long-context transformer baselines while being more compute and storage efficient. Additionally, Memo generalizes better to longer contexts at inference time and remains robust in streaming settings, where historical context must be truncated to fit inference constraints.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：具身智能体需要在长时间跨度中与环境交互并保持上下文感知，但视觉输入的高维度和长序列特性容易超出 Transformer 的上下文长度限制。人类可以将大量经验压缩为记忆并长期利用，而现有方法要么依赖固定大小的循环状态，要么完全依赖完整上下文，难以兼顾长期记忆保留与计算效率。
- **核心问题**：如何在强化学习训练的 Transformer 策略中，以显式、可伸缩的方式对历史观察进行记忆压缩，从而在长时间跨度任务中保持高效且有效的上下文利用。

## 2. 论文提出的方法论

- **核心思想**：提出一种名为 **Memo** 的 Transformer 架构与训练流程，通过引入周期性生成的摘要 token，将历史信息压缩为紧凑的记忆表示，并在后续决策中检索这些记忆。
- **关键技术细节**：
  - 在训练过程中，模型会**定期插入“摘要 token”**，与当前的输入序列交错，用于汇总和压缩先前时间步的信息。
  - 这些摘要 token 参与 Transformer 的自注意力计算，从而实现记忆的**写入（创建）**与**读取（检索）**。
  - 整个策略通过**端到端强化学习**进行训练，无需额外的监督信号或预训练的记忆模块。
- **架构优势**：相比所有历史帧都保留的全上下文方法，Memo 仅维护固定数量的摘要 token，从而降低计算和存储开销；相比固定大小的循环网络，它可以利用注意力机制更灵活地选择相关信息。

## 3. 实验设计

- **基准/场景**：
  - 一个**网格世界 meta-RL 基准**（用于评估元强化学习与记忆能力）。
  - 一个**照片逼真室内环境中的多目标导航任务**（用于评估真实感场景下的长时间记忆利用）。
- **对比方法**：
  - 主要与**朴素的长上下文 Transformer 基线**（naive long-context transformer baselines）对比。
  - 同时隐含对比了**固定大小循环模型**与**全上下文 Transformer**这两类现有方法（作为背景）。
- **评估维度**：任务性能、计算与存储效率、在更长上下文下的泛化能力、以及流式设置（历史上下文必须被截断）下的鲁棒性。

## 4. 资源与算力

- 摘要与可见材料中**未提及**任何算力细节，例如 GPU 型号、数量、训练时长、显存占用等。
- 因此无法从现有信息中总结具体的资源消耗情况。

## 5. 实验数量与充分性

- 可见信息中仅提及两类实验场景（网格世界 meta-RL 和导航任务），以及一个主要基线（长上下文 Transformer）。
- **未提供**具体的实验数量、消融实验、不同记忆长度对比、或统计显著性的细节。
- 从摘要看，实验覆盖了从抽象网格到视觉真实环境，具有一定广度，但由于未展示具体表格和消融，**无法判断实验的完整充分性**；对公平性的评估（如基线调参、随机种子等）也无从得知。

## 6. 论文的主要结论与发现

- Memo 在记忆密集型的长时间跨度任务上**优于朴素长上下文 Transformer 基线**。
- 同时显著**降低计算和存储开销**。
- Memo 在**推理时面对比训练时更长的上下文**时，表现出更好的泛化能力。
- 在**流式设置**（必须截断历史上下文以适配推理约束）下，Memo 依然保持较好性能，说明其记忆压缩机制具有鲁棒性。

## 7. 优点

- **方法创新性**：将周期性摘要 token 与 Transformer 结合，通过 RL 端到端学习记忆压缩，思想简洁且易集成。
- **效率高**：在保证长期记忆能力的同时，避免了全上下文 Transformer 的高计算/存储成本。
- **泛化性强**：对更长的上下文和截断式流式输入均有较好表现，说明模型学到的是可泛化的记忆表示而不是对固定长度的过拟合。
- **实践意义**：面向真实具身智能的长时间任务，提供了一个内存高效且可扩展的记忆增强范式。

## 8. 不足与局限

- **信息不完整**：由于仅能获取摘要，无法评估方法在更多任务（如实际机器人控制）、更大规模场景上的表现。
- **实验覆盖有限**：只出现了两个 bench mark，且没有消融实验细节，无法判断各组件（如摘要频率、摘要 token 数量、记忆长度）对性能的具体影响。
- **潜在信息丢失风险**：显式压缩记忆可能丢失对当前任务重要但被摘要过程忽略的细节，摘要 token 的固定频率也可能不适用于时间变化不均匀的任务。
- **训练复杂度**：引入额外的记忆管理机制后，RL 训练的稳定性和超参数敏感性未知。
- **公平性/偏差**：论文未披露与基线对比时的具体实验设置（如上下文长度、计算预算等），无法验证比较的完全公平性。

（完）
