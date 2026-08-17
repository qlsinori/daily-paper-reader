---
title: "Memo: Training Memory-Efficient Embodied Agents with Reinforcement Learning"
title_zh: 备忘录：利用强化学习训练记忆高效的具身智能体
authors: "Gunshi Gupta, Karmesh Yadav, Zsolt Kira, Yarin Gal, Rahaf Aljundi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=9eIntNc69t"
tags: ["query:vln-memory"]
score: 8.0
evidence: 面向具身智能体环境的记忆机制，支持长时程导航
tldr: 具身智能体需要在长时间跨度内保持上下文记忆，但视觉输入常超出Transformer上下文限制，而现有方法要么依赖固定大小循环记忆，要么需要完整上下文。为此，本文提出Memo，一种基于Transformer的架构，通过学习压缩和抽象无关视觉信息，形成可访问的高效记忆，并配合强化学习训练。该方法在有限上下文下支持长时程决策任务，显著提升记忆效率和训练效率，为具身导航等任务提供了可扩展的记忆解决方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 具身智能体的视觉输入超出上下文限制，现有记忆范式不够高效，难以支持长时间运行。
method: 提出基于Transformer的Memo架构，用可学习压缩机制将高维视觉观测抽象为紧凑记忆，并接入策略网络训练。
result: 实验表明Memo能显著降低上下文占用，同时保持或改善决策性能，支持长时间具身任务。
conclusion: Memo通过记忆压缩与强化学习结合，为长时程具身智能体提供高效记忆机制。
---

## Abstract
To enable embodied agents to operate effectively over extended timeframes, it is crucial to develop models that form and access memories to stay contextualized in their environment. In the current paradigm of training transformer-based policies for embodied sequential decision-making tasks, visual inputs often overwhelm the context limits of transformers, while humans can maintain and utilize a lifetime of experience compressed as memories. Significant compression is possible in principle, as much of the input is irrelevant and can be abstracted. However, existing approaches predominantly focus on either recurrent models with fixed-size memory or transformers with full-context reliance. In this work, we propose Memo, a transformer-based architecture and training recipe for reinforcement learning (RL) on memory-intensive, long-horizon tasks. Memo incorporates the creation and retrieval of memory by interleaving periodic summarization tokens with the inputs of a model during training. We demonstrate Memo’s effectiveness on a grid-world meta-RL benchmark and a multi-object navigation task in photo-realistic indoor settings. Memo outperforms naive long-context transformer baselines while being more compute and storage efficient. Additionally, Memo generalizes better to longer contexts at inference time and remains robust in streaming settings, where historical context must be truncated to fit inference constraints.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：具身智能体需要在长时间跨度内与环境交互并保持上下文感知，而当前基于 Transformer 的策略模型在处理视觉输入时容易超出上下文长度限制。相比之下，人类可以压缩并长期保存经验记忆，这说明高维视觉输入中存在大量可压缩、可抽象的冗余信息。
- **现有方法的不足**：
  - 循环模型（RNN 类）使用固定大小的记忆，容量有限且难以应对复杂长时程依赖。
  - 标准 Transformer 过度依赖完整上下文，导致计算和存储开销随序列长度急剧增长。
- **论文要解决的核心问题**：如何设计一种 Transformer 架构和训练方法，使具身智能体能够在**有限的上下文窗口**下高效地压缩、存储和检索长期记忆，从而支持**内存密集型、长时程**的强化学习任务。

## 2. 方法论

- **核心思想**：提出 **Memo**，一种基于 Transformer 的架构，通过**周期性插入“摘要标记”（summarization tokens）**与输入序列交错，让模型在训练过程中学习将高维视觉观测压缩为紧凑、可访问的记忆表示。这种方式类似于人类社会中的“记忆压缩”，只保留与任务相关的关键信息。
- **关键技术细节**（根据摘要推断）：
  - 在训练时，模型按固定间隔接收输入观测，并插入专门的摘要标记；模型需要学会将这些标记视为对过去信息的汇总。
  - 后续时间步可以通过注意力机制访问这些摘要标记，从而在不保留完整历史的情况下获取长期上下文。
  - 整个压缩和检索过程与策略网络端到端联合训练，采用强化学习（RL）优化目标。
  - 该方法不依赖固定大小的循环状态，也无需在推理时持有全部历史，因此支持**流式处理**（即历史上下文必须被截断以符合推理约束的场景）。
- 由于仅提供摘要，论文中未给出明确的公式或算法伪代码，后续需结合全文验证具体实现。

## 3. 实验设计

- **评测场景与基准**：
  1. **网格世界元 RL 基准**：用于验证 Meta-RL 场景下的记忆压缩能力。
  2. **照片级逼真室内多目标导航任务**：更接近真实具身环境，要求智能体在复杂视觉输入下完成多目标导航。
- **对比方法**：论文主要对比了**朴素长上下文 Transformer 基线**（即直接使用全部历史上下文的标准 Transformer）。
- **评估指标**：任务性能（如导航成功率）、计算效率、存储效率，以及**推理时对更长上下文的泛化能力**和**流式设置下的鲁棒性**。
- **未提供的信息**：
  - 具体数据集名称（如 Habitat、Matterport3D 等）未在摘要中说明。
  - 是否包含与循环记忆模型（如 RNN/GRU 类）或混合架构的对比不明确。
  - 未提及消融实验的具体设计（如摘要标记频率、压缩比例的影响等）。

## 4. 资源与算力

- 论文摘要和提供的信息中**完全没有提及**使用的 GPU 型号、数量、训练时长、参数量等资源细节。
- 仅能确认方法在**计算和存储效率**上优于基线，但具体数值和硬件配置需查看全文补充材料。

## 5. 实验数量与充分性

- **实验数量**：摘要明确列出了**两个主要实验场景**（网格世界元 RL 和室内多目标导航），未显示其他额外实验。
- **充分性评价**：
  - **优点**：两个场景覆盖了从抽象网格到视觉逼真环境的跨度，能够初步验证方法的通用性。
  - **不足**：实验场景数量偏少，缺乏多样化的长期记忆任务（如部分可观测的 POMDP、长程连续控制等）的验证。
  - **公平性**：需等全文确认是否与最强基线（如各类记忆增强模型）进行了严格对比，仅靠摘要无法判断是否所有方法都使用了相同的计算预算和超参数调优。
  - **消融研究**：摘要未提及，无法判断摘要标记频率、记忆容量等设计选择的贡献和敏感性。

## 6. 主要结论与发现

- **效率优势**：Memo 在保持甚至改善任务性能的同时，显著降低了计算和存储开销。
- **性能优势**：优于朴素的“长上下文 Transformer”基线，说明主动记忆压缩比简单堆叠上下文更有效。
- **泛化能力**：在推理时，Memo 能够**泛化到比训练时更长的上下文**，适合部署到真实世界。
- **流式鲁棒性**：在历史上下文必须被截断（如受限于固定窗口）的流式场景中，Memo 依然表现出鲁棒性，不受截断影响。

## 7. 优点

- **方法创新**：将“摘要标记”概念引入 RL 训练，为 Transformer 在长期记忆任务中的高效应用提供了新思路。
- **实用性强**：同时兼顾训练效率和推理效率，且能适应长度可变的流式输入，非常贴近真实机器人的部署需求。
- **普适性**：方法不依赖特定任务，理论上可推广到多种视觉或非视觉的部分可观测决策问题。
- **对齐人类记忆机制**：模拟了人类压缩长期经验的方式，具有认知科学上的启发性。

## 8. 不足与局限

- **实验覆盖范围有限**：仅验证了两个任务（网格世界和室内导航），难以证明方法在更复杂、更多样的长期记忆任务（如跨场景导航、视觉语言导航 VLN）上的有效性。
- **缺乏与代表性记忆模型的对比**：未明确提及与循环网络或记忆增强网络（如 MERLIN、Differentiable Neural Computer）的对比，可能不足以证明相对“现有方法”的综合优势。
- **资源信息缺失**：没有汇报硬件配置和训练成本，无法评估可复现性和实际应用门槛。
- **未披露消融细节**：摘要标记频率、位置、数量等技术参数的敏感性未知，模型设计空间未充分探索。
- **潜在风险**：由于记忆是模型隐式学到的抽象，可能缺乏可解释性，且对于需要精确编码位置或时间信息的任务，压缩可能造成信息损失。
- **应用限制**：尚未在真实机器人上验证，且 RL 训练本身的不稳定性可能在不同任务上需要额外调参。

（完）
