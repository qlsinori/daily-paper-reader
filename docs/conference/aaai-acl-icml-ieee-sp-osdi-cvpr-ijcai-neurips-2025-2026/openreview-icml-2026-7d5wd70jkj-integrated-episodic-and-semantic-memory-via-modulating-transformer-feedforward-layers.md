---
title: Integrated Episodic and Semantic Memory via Modulating Transformer FeedForward Layers
title_zh: 通过调制Transformer前馈层整合情景记忆与语义记忆
authors: "Yiqun Yao, Xiang Li, Xin Jiang, Xuezhi Fang, Naitong Yu, Siwei Dong, Wenjia Ma, Jing Li, Aixin Sun, Yequan Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/96b3a6d551885bf0b3b28a9bf42fcea315a722aa.pdf"
tags: ["query:semantic-map"]
score: 8.0
evidence: 通过超网络整合情景记忆与语义记忆的长期记忆架构
tldr: 大语言模型中的前馈层被视作语义记忆，KV缓存被视作情景记忆，但两类记忆通常被分开处理。本文证明同一组前馈参数可同时存储语义与情景记忆，并通过超网络将上下文映射为前馈层参数的定向更新，实现无需显式关注相关KV缓存的记忆检索。后训练采用续写和随机访问联想记忆目标，支持记忆的持续写入与长期保持。该工作为类脑记忆整合与持续学习提供了新的网络机制。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有Transformer模型将语义记忆和情景记忆分离，且检索依赖KV缓存访问，缺少统一的持续记忆机制。
method: 使用超网络将上下文递归映射为前馈层参数更新，使同一组参数同时充当语义与情景记忆，并通过联想记忆目标进行后训练。
result: 实验表明该模型无需显式访问KV缓存即可回忆相关事件，同时保持语义知识，支持随机访问联想记忆。
conclusion: Transformer前馈层可作为统一的长期记忆载体，为智能体的持续学习和记忆回放提供新途径。
---

## Abstract
It is widely recognized that, after generative pre-training, Transformer FeedForward layers implicitly function as semantic memory, encoding linguistic and factual knowledge, while the contexts in key–value (KV) cache contain raw events, serving as the source of models' episodic memory. In this work, we show that a same group of Transformer FeedForward-layer parameters can both be semantic and episodic memory, which is retrievable without explicitly attending to the related KV cache. To realize this idea, we introduce Hypermem, a hypernetwork that recurrently maps contexts into targeted updates of FeedForward parameters. We post-train the hypernetwork using continuation and random-access associative memory objectives, eliminating the need for test-time training. Extensive experiments demonstrate that our approach outperforms related methods, including MemoryLLM and generative adapter, on memory retrieval, long-context question answering, and personalization benchmarks, establishing a new state of the art for hypernetwork-based memory mechanisms. Our results suggest that directly bridging data and parameters provides a viable direction for exploring next-generation foundation models with more flexible and persistent memory capabilities.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

> 说明：由于所给材料仅包含论文摘要和元数据，以下总结主要基于这些有限信息，部分细节无法确证。

### 1. 核心问题与整体含义

- **研究动机**：现有 Transformer 模型在预训练后，其前馈层（FeedForward layers）隐含地扮演了**语义记忆**的角色，编码语言知识和事实；而 KV 缓存中的上下文则存储原始事件，构成**情景记忆**的来源。然而，这两类记忆通常被**分离处理**，检索情景记忆需要显式关注相关 KV 缓存，缺乏统一、持久的记忆机制。
- **核心问题**：是否能让**同一组前馈参数**同时承载语义记忆和情景记忆，并且在不显式访问 KV 缓存的情况下实现记忆检索？
- **整体含义**：该工作直接桥接“数据”与“参数”，探索一种更灵活、更持久的基础模型记忆机制，为未来智能体的持续学习和记忆回放提供了新方向。

### 2. 方法论

- **核心思想**：提出名为 **Hypermem** 的超网络（hypernetwork），将上下文递归映射为前馈层参数的**定向更新**，使同一组参数既存储语义知识，又能写入和检索情景记忆。
- **关键技术细节**：
  - 超网络以**递归方式**处理上下文序列，生成适用于当前输入的参数增量；
  - 该增量作用于 Transformer 的前馈层，实现“记忆写入”；
  - 检索时**无需显式关注相关 KV 缓存**，而是通过参数变化直接回忆起相关事件。
- **训练目标**：采用**续写目标**（continuation objective）和**随机访问联想记忆目标**（random-access associative memory objective）进行后训练。
- **重要性质**：整个后训练过程是**离线/后训练**的，不需要在测试时进行额外训练（test-time training），支持记忆的持续写入和长期保持。
- **公式/算法流程**：摘要未提供具体公式或伪代码，仅能从文字描述推断：上下文 → 超网络 → 前馈层参数更新 → 同一组参数用于语义推理和情景回忆。

### 3. 实验设计

- **评测场景**：摘要明确提到了三类任务：
  - **记忆检索**（memory retrieval）
  - **长上下文问答**（long-context question answering）
  - **个性化**（personalization）
- **对比方法**：
  - **MemoryLLM**
  - **生成适配器**（generative adapter）
- **数据集**：摘要未给出具体数据集名称、规模或任务细节。
- **基准**：声称在上述基准上取得了**新的最优结果**（state of the art）。

### 4. 资源与算力

- 论文摘要和提供的元数据中**未提及任何算力信息**，包括 GPU 型号、数量、训练时长、参数量级等。
- 因此无法评估方法在计算资源上的成本或可行性。

### 5. 实验数量与充分性

- **实验数量**：摘要中仅概括性地提到“大量实验”（extensive experiments），并列举了三类基准，但**未给出具体实验组数、数据集数量、消融实验细节**。
- **充分性评估**：
  - 覆盖面：三类任务（记忆检索、长上下文 QA、个性化）具有一定的代表性，能够初步验证方法的通用性。
  - 对比公平性：仅提到与 MemoryLLM 和生成适配器的对比，未说明超参数设置、参数量匹配、训练数据是否一致等细节，难以判断对比是否公平。
  - 消融实验：未提及是否对超网络结构、训练目标、更新幅度等进行了消融，因此方法的贡献分解尚不清晰。
  - 总体而言，由于信息不足，无法充分评判实验的完整性和严谨性。

### 6. 主要结论与发现

- **核心结论**：Transformer 前馈层可以同时作为语义记忆和情景记忆的**统一载体**，情景记忆的检索不需要通过显式关注 KV 缓存实现。
- **性能表现**：Hypermem 在记忆检索、长上下文问答和个性化基准上均优于 MemoryLLM 和生成适配器，成为基于超网络的记忆机制的新 SOTA。
- **理论意义**：结果表明“将数据直接桥接到参数”是可行的，为设计具有更灵活、更持久记忆能力的新一代基础模型提供了证据。

### 7. 优点

- **概念创新**：首次在同一组前馈参数中统一语义记忆和情景记忆，突破了传统“KV 缓存仅作情景记忆，FFN 仅作语义记忆”的割裂视角。
- **机制高效**：通过超网络实现参数级记忆检索，省去了显式注意力访问 KV 缓存的过程，可能带来推理效率上的优势。
- **无需测试时训练**：后训练式超网络支持记忆写入，避免了在线更新的昂贵开销，便于实际部署。
- **持久性**：参数化记忆天然具备长期保持的能力，与持续学习场景契合。

### 8. 不足与局限

- **信息缺失**：由于论文全文不可得，无法确认具体实验数据集、参数规模、计算成本、消融实验等关键细节，评估方法的可复现性受到限制。
- **潜在风险**：
  - 超网络生成参数更新的稳定性未知，更新不当可能破坏原有语义知识；
  - 递归映射上下文为参数更新可能带来额外计算开销，尤其在长上下文中；
  - 仅对比两种方法，且没有更广泛的基线（如常规微调、检索增强生成等），SOTA 声称的置信度有限。
- **应用限制**：当前验证场景为记忆检索、长上下文 QA 和个性化，尚未覆盖真实世界中的复杂多模态、多智能体交互等场景；其可扩展性和安全性有待进一步检验。

（完）
