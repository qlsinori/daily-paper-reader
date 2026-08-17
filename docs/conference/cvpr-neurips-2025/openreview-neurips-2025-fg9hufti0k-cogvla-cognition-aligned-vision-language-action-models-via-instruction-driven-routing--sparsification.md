---
title: "CogVLA: Cognition-Aligned Vision-Language-Action Models via Instruction-Driven Routing & Sparsification"
title_zh: CogVLA：通过指令驱动路由与稀疏化实现认知对齐的视觉-语言-动作模型
authors: "Wei Li, Renshan Zhang, Rui Shao, Jie He, Liqiang Nie"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Fg9HufTI0K"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向视觉-语言-动作的指令驱动路由模型，与具身导航弱相关
tldr: 大规模视觉-语言-动作（VLA）模型在预训练后仍需大量后训练，计算开销大，难以扩展和部署；现有稀疏化方法忽略了视觉-语言-动作模态间的语义耦合。本文提出CogVLA框架，采用指令驱动路由与稀疏化，兼顾端到端从感知到控制的连贯性，从而提升效率与性能。实验表明CogVLA在降低计算成本的同时改善了任务表现，为VLA模型在实际机器人系统中的应用提供了高效路径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLA模型后训练成本高，现有稀疏化策略忽略跨模态语义耦合，阻碍规模化部署。
method: 提出CogVLA框架，采用指令驱动路由与稀疏化机制，保持视觉-语言-动作端到端一致性。
result: 实验显示CogVLA在降低计算开销的同时提升了任务性能与部署可行性。
conclusion: 该工作为高效VLA模型设计提供了新思路，有助于具身智能体在机器人场景中的应用。
---

## Abstract
Recent Vision-Language-Action (VLA) models built on pre-trained Vision-Language Models (VLMs) require extensive post-training, resulting in high computational overhead that limits scalability and deployment. Existing sparsification strategies—such as Mixture-of-Depths, layer skipping, and early exit—fall short by neglecting the semantic coupling across vision-language-action modalities, and focusing narrowly on intra-LLM computation while overlooking end-to-end coherence from perception to control. To address these challenges, we propose **CogVLA**, a Cognition-Aligned Vision-Language-Action framework that leverages instruction-driven routing and sparsification to improve both efficiency and performance. CogVLA draws inspiration from human multimodal coordination and introduces a 3-stage progressive architecture. 1) **Encoder-FiLM based Aggregation Routing (EFA-Routing)** injects instruction information into the vision encoder to selectively aggregate and compress dual-stream visual tokens, forming a instruction-aware latent representation. 2) Building upon this compact visual encoding, **LLM-FiLM based Pruning Routing (LFP-Routing)** introduces action intent into the language model by pruning instruction-irrelevant visually grounded tokens, thereby achieving token-level sparsity. 3) To ensure that compressed perception inputs can still support accurate and coherent action generation, we introduce **V‑L‑A Coupled Attention (CAtten)**, which combines causal vision-language attention with bidirectional action parallel decoding.
Extensive experiments on the LIBERO benchmark and real-world robotic tasks demonstrate that CogVLA achieves state-of-the-art performance with success rates of 97.4\% and 70.0\%, respectively, while reducing training costs by 2.5$\times$ and decreasing inference latency by 2.8$\times$ compared to OpenVLA.

---

## 论文详细总结（自动生成）

# CogVLA 论文深度解读

## 1. 核心问题与研究动机

- **背景**：当前视觉-语言-动作（VLA）模型通常基于预训练的视觉-语言模型（VLM）进行大规模后训练，虽然能赋予机器人强大的多模态理解与控制能力，但**计算开销极大**，严重制约了模型的可扩展性与实际部署。
- **核心痛点**：现有稀疏化方法（如 Mixture-of-Depths、层跳过、早期退出机制）存在两方面缺陷：
  1. **忽略跨模态语义耦合**——视觉-语言-动作三种模态之间语义高度关联，仅对 LLM 内部计算做稀疏化，会破坏端到端感知-控制链路的连贯性；
  2. **优化视角过窄**——仅聚焦于 LLM 内部计算，未从感知到控制的全局视角进行整体效率优化。
- **核心问题**：**如何在不牺牲 VLA 任务性能的前提下，从感知到控制全链路实现高效稀疏化，同时保持跨模态语义的一致性？**
- **整体含义**：CogVLA 的提出为高效、可部署的具身智能模型设计提供了新的技术路径，对 VLA 模型走向真实机器人系统具有推动意义。

> 注：根据元数据，该工作与“具身导航”主题弱相关，其核心面向的是通用操纵任务。

## 2. 方法论

CogVLA 借鉴人类多模态协同处理机制，提出了 **三阶段渐进式架构**，核心思想是：以“指令”为认知锚点，逐级压缩视觉信息、稀疏化语言模型，并最终保证动作生成的质量。

### 阶段一：Encoder-FiLM 聚合路由（EFA-Routing）

- **目标**：在视觉编码端实现指令感知的视觉令牌压缩。
- **方法**：将指令文本信息通过 FiLM（Feature-wise Linear Modulation）机制注入视觉编码器（如 ViT），引导编码器对双流视觉令牌（如主干视图 + 手腕视图）进行**选择性聚合与压缩**。
- **产出**：生成紧凑且携带任务相关语义的“指令感知潜在表示”，从源头降低送入 LLM 的视觉令牌数量。

### 阶段二：LLM-FiLM 剪枝路由（LFP-Routing）

- **目标**：在 LLM 内部实现令牌级稀疏化。
- **方法**：将**动作意图**（action intent）通过 FiLM 方式注入语言模型，对与指令无关的视觉接地令牌进行剪枝。
- **作用**：在保留任务关键信息的前提下，进一步减少 LLM 需要处理的令牌规模，降低 Transformer 的计算复杂度。

### 阶段三：V-L-A 耦合注意力（CAtten）

- **目标**：确保压缩后的感知输入仍能生成准确连贯的动作序列。
- **方法**：设计了一种**耦合注意力机制**，将：
  - 因果视觉-语言注意力（自回归处理感知与推理），与
  - 双向动作并行解码（并行生成动作序列）有机组合。
- **效果**：在保证感知到控制端到端一致性的同时，显著加速动作生成。

### 流程概览

> 输入图像 + 指令 → EFA-Routing（视觉令牌聚合压缩）→ LFP-Routing（LLM 内令牌剪枝）→ CAtten（耦合注意力解码）→ 输出动作序列

## 3. 实验设计

- **仿真基准**：**LIBERO**（机器人操纵领域权威 benchmark），用于评估任务成功率与效率。
- **真实场景**：**真实机器人操纵任务**，验证方法的实际部署可行性。
- **对比方法**：主要与 **OpenVLA**（当前主流开源 VLA 模型）进行对比，并在论文中报告了 SOTA 结果。
- **主要评估指标**：任务成功率（Success Rate）、训练成本（Training Cost）、推理延迟（Inference Latency）。

## 4. 资源与算力

- 论文摘要中**未明确说明**使用的 GPU 型号、数量或具体训练时长。
- 仅提供了相对效率指标：
  - 训练成本降低：**2.5×**
  - 推理延迟降低：**2.8×**（均相对 OpenVLA）
- 若要评估绝对算力消耗，需查阅论文正文的实验设置部分（当前提取信息不足以给出具体算力清单）。

## 5. 实验数量与充分性

- **实验组数**：涵盖 LIBERO 仿真 + 真实机器人两个主要场景，同时报告了成功率、训练成本和推理延迟三类指标。
- **消融研究**：从方法设计来看，三个模块（EFA-Routing、LFP-Routing、CAtten）各自独立可消融，论文中应有对应的组件有效性验证。
- **充分性评估**：
  - **优点**：仿真 + 真实双轨验证增强了结论的可信度；与 OpenVLA 的对比清晰体现了效率提升。
  - **不足**：
    - 对比基线数量偏少（仅以 OpenVLA 为主要参照），未提及与其他稀疏化方法（如 MoD、早期退出）的直接对比；
    - 缺少跨多个不同任务集或不同机器人平台的泛化性测试；
    - 在真实场景中仅报告了一个整体成功率（70.0%），任务多样性信息有限，需依赖正文补充。

## 6. 主要结论与发现

- CogVLA 在 **LIBERO 上成功率达到 97.4%**，在 **真实机器人任务上达到 70.0%**，均为当时最优水平（SOTA）。
- 相比 OpenVLA，CogVLA 在降低 **2.5× 训练成本** 和 **2.8× 推理延迟** 的同时，任务表现不降反升。
- 结论：**指令驱动 + 跨模态耦合的稀疏化策略**能够有效兼顾 VLA 模型的性能与效率，为 VLA 在实际机器人系统中的高效部署提供了切实可行的路径。

## 7. 优点

- **跨模态一致性视角**：跳出“仅稀疏化 LLM”的传统思路，从感知→推理→控制全链路系统性优化，更具全局意义。
- **模块化三阶段设计**：编码端聚合、LLM 端剪枝、解码端耦合注意力各司其职，逻辑清晰，便于消融与扩展。
- **指令-视觉-动作三重耦合**：EFA-Routing 注入指令到视觉编码器，LFP-Routing 注入动作意图到 LLM，CAtten 保证动作解码质量，三者的有机结合具有较强技术新意。
- **效率与性能双赢**：训练与推理成本大幅下降的同时性能保持领先，在部署友好性方面具备明显优势。

## 8. 不足与局限

- **实验覆盖有限**：当前已知的评估集中于 LIBERO 基准与单一真实场景，缺少在多样化操纵任务、多类机器人本体上的广泛验证。
- **对照基线不足**：未明确提及与 Mixture-of-Depths、层跳过、早期退出等前述稀疏化方法在同等条件下的系统对比，影响对方法相对优势的精确判断。
- **泛化性存疑**：指令驱动路由高度依赖指令质量与多样性，在开放世界复杂指令下的表现仍未可知。
- **算力信息不透明**：未给出具体的 GPU 型号、数量、训练时长，外部研究者复现时需要自行摸索算力配置。
- **与具身导航弱相关**：根据元数据评估，本工作对具身导航领域的直接参考价值有限，其核心适配场景为操纵任务。

（完）
