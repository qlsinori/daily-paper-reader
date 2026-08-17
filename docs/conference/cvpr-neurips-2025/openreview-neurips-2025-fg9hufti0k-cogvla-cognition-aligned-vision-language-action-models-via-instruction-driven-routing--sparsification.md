---
title: "CogVLA: Cognition-Aligned Vision-Language-Action Models via Instruction-Driven Routing & Sparsification"
title_zh: CogVLA：基于指令路由与稀疏化的认知对齐视觉-语言-动作模型
authors: "Wei Li, Renshan Zhang, Rui Shao, Jie He, Liqiang Nie"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Fg9HufTI0K"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向视觉-语言-动作模型的指令路由与稀疏化，与语言条件具身控制相关，但非导航特化
tldr: 针对视觉-语言-动作模型后训练开销大、现有稀疏化忽略跨模态语义耦合的问题，提出CogVLA框架，通过指令驱动的路由与稀疏化在降低计算成本的同时保持从感知到控制的端到端一致性。该方法可提升具身智能体的部署效率，对语言条件导航等下游任务具有通用支持价值，但未针对导航任务设计与评测。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLA模型依赖大规模后训练且计算开销大，现有稀疏化方法未考虑视觉-语言-动作的语义耦合。
method: 提出指令驱动路由与稀疏化机制，在保持端到端感知-控制连贯性的前提下裁剪冗余计算。
result: 在VLA基准上以更低的训练与推理成本取得有竞争力的性能。
conclusion: 指令感知的高效稀疏化可降低具身模型部署门槛，可迁移至导航控制等任务。
---

## Abstract
Recent Vision-Language-Action (VLA) models built on pre-trained Vision-Language Models (VLMs) require extensive post-training, resulting in high computational overhead that limits scalability and deployment. Existing sparsification strategies—such as Mixture-of-Depths, layer skipping, and early exit—fall short by neglecting the semantic coupling across vision-language-action modalities, and focusing narrowly on intra-LLM computation while overlooking end-to-end coherence from perception to control. To address these challenges, we propose **CogVLA**, a Cognition-Aligned Vision-Language-Action framework that leverages instruction-driven routing and sparsification to improve both efficiency and performance. CogVLA draws inspiration from human multimodal coordination and introduces a 3-stage progressive architecture. 1) **Encoder-FiLM based Aggregation Routing (EFA-Routing)** injects instruction information into the vision encoder to selectively aggregate and compress dual-stream visual tokens, forming a instruction-aware latent representation. 2) Building upon this compact visual encoding, **LLM-FiLM based Pruning Routing (LFP-Routing)** introduces action intent into the language model by pruning instruction-irrelevant visually grounded tokens, thereby achieving token-level sparsity. 3) To ensure that compressed perception inputs can still support accurate and coherent action generation, we introduce **V‑L‑A Coupled Attention (CAtten)**, which combines causal vision-language attention with bidirectional action parallel decoding.
Extensive experiments on the LIBERO benchmark and real-world robotic tasks demonstrate that CogVLA achieves state-of-the-art performance with success rates of 97.4\% and 70.0\%, respectively, while reducing training costs by 2.5$\times$ and decreasing inference latency by 2.8$\times$ compared to OpenVLA.

---

## 论文详细总结（自动生成）

## 论文总结：CogVLA

### 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：视觉-语言-动作模型（VLA）通常构建在预训练视觉-语言模型（VLM）之上，需要大量后训练以适配机器人控制任务，导致高昂的计算开销，限制了可扩展性与实际部署。
- **现有方法的不足**：已有的稀疏化策略（如 Mixture-of-Depths、层跳跃、早退出机制）主要聚焦于大语言模型（LLM）内部的计算裁剪，忽略了三模态（视觉-语言-动作）之间的语义耦合，且未考虑从感知到控制的端到端一致性，因此难以在保持控制质量的同时实现高效推理。
- **核心研究目标**：提出一种认知对齐的 VLA 框架，在降低训练与推理成本的同时保持端到端感知-控制连贯性，从而提升具身智能体的部署效率。

### 2. 方法论：核心思想、关键技术细节

- **总体思想**：受人类多模态协调机制启发，提出 **CogVLA** 框架，采用**指令驱动的路由与稀疏化**策略，在不同阶段根据指令语义裁剪冗余视觉信息和计算，实现"认知对齐"的高效稀疏化。
- **三阶段渐进架构**：
  1. **Encoder-FiLM 聚合路由（EFA-Routing）**
     - 将指令信息通过 FiLM（Feature-wise Linear Modulation）机制注入视觉编码器；
     - 选择性聚合和压缩双流视觉 token（如主干视图 + 操作视图等），形成指令感知的紧凑隐层表示。
  2. **LLM-FiLM 剪枝路由（LFP-Routing）**
     - 在语言模型层面引入动作意图信息；
     - 通过 FiLM 调制对与指令无关的视觉 grounded token 进行剪枝，实现 token 级别的稀疏化。
  3. **V-L-A 耦合注意力（CAtten）**
     - 将因果视觉-语言注意力与双向动作并行解码相结合；
     - 确保压缩后的感知输入仍能支持准确、连贯的动作生成。

### 3. 实验设计

- **Benchmark 与场景**：
  - **LIBERO 基准**：桌面操作任务模拟环境，用于评估任务完成成功率；
  - **真实机器人任务**：评测模型在物理环境中的实际操控能力。
- **对比方法**：主要以 **OpenVLA** 作为对比基线，从性能、训练成本、推理延迟三个维度进行评估。

### 4. 资源与算力

- 论文摘要中**未明确说明**使用的 GPU 型号、数量、训练时长等基础设施信息；
- 仅明确汇报了相对收益：训练成本降低 **2.5×**，推理延迟降低 **2.8×**（对比 OpenVLA）；如需完整算力细节，需查阅论文全文实验章节。

### 5. 实验数量与充分性

- 从摘要看涉及**两大赛道**：LIBERO 模拟基准 + 真实机器人任务；
- 当前可获取的论文信息仅包含摘要层面，**未提及消融实验细节**（如 EFA-Routing、LFP-Routing、CAtten 三模块的分别影响）；
- 总体而言，模拟与真实场景的"双轨验证"增强了结果可信度；但实验完整度（如多任务覆盖、跨实体泛化、更多基线对比）需以全文为准。整体设计有较好的客观性，不过仅凭摘要无法判断对比实验的全面性与公平性细节。

### 6. 主要结论与发现

- **性能显著提升**：LIBERO 上成功率 **97.4%**，真实机器人任务成功率 **70.0%**，均达到 SOTA 水平；
- **高效性突出**：相比 OpenVLA，训练成本降低 2.5×，推理延迟降低 2.8×；
- **核心结论**：指令感知的高效结构化稀疏化可以在不牺牲端到端控制能力的前提下显著降低训练与推理开销，验证了"认知对齐 + 跨模态稀疏化"这一思路的可行性，并可迁移至导航控制等下游具身任务。

### 7. 优点

- **方法创新性强**：将指令驱动机制贯穿视觉编码与语言模型两个阶段，优于仅关注 LLM 内部计算的现有稀疏化方法；
- **跨模态语义耦合意识**：显式建模视觉-语言-动作之间的关联，避免"只管裁剪、不管效果"的粗放稀疏化；
- **端到端一致性好**：通过耦合注意力机制保障压缩感知输入仍能支撑可靠动作生成；
- **实验验证有说服力**：模拟环境与真实机器人都做了评测，且同时报告了性能与效率指标，展示出实用部署价值。

### 8. 不足与局限

- **信息不完整风险**：当前仅能基于摘要分析，无法评估消融实验设计、超参数敏感性、稳定性分析等细节；
- **算力信息缺失**：未披露具体硬件配置与训练时长，影响复现性与成本评估；
- **应用范围有限**：论文本身并非导航特化，面向的是通用 VLA 效率优化，导航仅是潜在可迁移场景，因此与"语言条件导航"任务无直接评测证据；
- **潜在偏差风险**：若对比基线仅限 OpenVLA 一家，则结论的普适性需要更多基线（如不同规模的 VLA、不同稀疏化方法组合）来支撑；
- **真实场景广度未知**：真实机器人任务数量、任务难度与环境多样性在摘要中未说明，泛化能力仍需更多实验佐证。

（完）
