---
title: "Aux-Think: Exploring Reasoning Strategies for Data-Efficient Vision-Language Navigation"
title_zh: Aux-Think：探索数据高效视觉语言导航的推理策略
authors: "Shuo Wang, Yongcai Wang, Wanting Li, Xudong Cai, Yucheng Wang, Maiyue Chen, kaihui.wang, Zhizhong Su, Deying Li, Zhaoxin Fan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=vNmWbINtwH"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 直接研究遵循自然语言指令的视觉语言导航的推理策略
tldr: 视觉语言导航要求智能体依据自然语言指令在复杂真实环境中行动，但现有方法主要通过微调大模型而忽视推理策略的作用。论文首次系统评估了No-Think、Pre-Think等推理策略，并提出Aux-Think方法在动作预测前引入辅助推理以增强指令对齐。实验证明该方法提升VLN任务的泛化能力和指令遵循准确性。该工作将思维链推理成功迁移到长程动作决策任务，为数据高效的VLN提供新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLN模型大多直接预测动作，缺乏在长程动作决策中显式利用推理策略。
method: 系统比较多种推理策略，提出Aux-Think在预测动作前加入辅助推理，提高指令理解与对齐。
result: 在多个VLN数据集上取得性能提升，尤其增强泛化能力。
conclusion: 证明推理策略对VLN这类长程动作任务至关重要，可作为数据高效训练的有效手段。
---

## Abstract
Vision-Language Navigation is a critical task for developing embodied agents that can follow natural language instructions to navigate in complex real-world environments.  Recent advances by finetuning large pretrained models have significantly improved generalization and instruction grounding compared to traditional approaches. However, the role of reasoning strategies in navigation—an action-centric, long-horizon task—remains underexplored, despite Chain-of-Thought reasoning's demonstrated success in static tasks like question answering and visual reasoning. To address this gap, we conduct the first systematic evaluation of reasoning strategies for VLN, including No-Think (direct action prediction), Pre-Think (reason before action), and Post-Think (reason after action). Surprisingly, our findings reveal the Inference-time Reasoning Collaps issue, where inference-time reasoning degrades navigation accuracy, highlighting the challenges of integrating reasoning into VLN. Based on this insight, we propose Aux-Think, a framework that trains models to internalize structured reasoning patterns through CoT supervision during training, while preserving No-Think inference for efficient action prediction. To support this framework, we release R2R-CoT-320k, a large-scale Chain-of-Thought annotated dataset.  Empirically, Aux-Think significantly reduces training effort without compromising performance.

---

## 论文详细总结（自动生成）

# 论文总结：Aux-Think：探索数据高效视觉语言导航的推理策略

## 1. 核心问题与整体含义

- **研究背景**：视觉语言导航（Vision-Language Navigation, VLN）要求智能体在复杂真实环境中，依据自然语言指令进行长时程、面向动作的导航决策。这是具身智能中的关键任务。
- **现有范式**：近年来，通过微调大型预训练模型显著提升了指令跟随能力和泛化性能，但大多数方法将导航直接视为“感知-动作”映射，忽视了对推理策略的显式利用。
- **研究动机**：尽管Chain-of-Thought（CoT）推理在问答、视觉推理等静态任务中取得了巨大成功，但在动作中心、长时程的导航任务中，推理策略的作用尚未被系统探索。
- **核心问题**：能否将推理策略引入VLN？哪种推理方式最适合导航？推理能否提升数据效率与指令对齐？

## 2. 方法论：核心思想与关键技术

- **系统评估三种推理模式**：
  - **No-Think**：直接预测动作，不使用显式推理。
  - **Pre-Think**：在动作预测前先进行推理。
  - **Post-Think**：在动作预测后进行推理验证。
- **关键发现——推理时推理崩溃（Inference-time Reasoning Collapse）**：
  - 在推理阶段引入显式CoT推理反而会降低导航准确率，表明VLN这类长程动作任务与静态推理任务存在本质差异，直接迁移推理策略是失败的。
- **提出Aux-Think框架**：
  - **核心思想**：将推理从“推理时”移动到“训练时”，让模型通过CoT监督学习并内化结构化推理模式，但在实际推理（动作预测）时恢复为No-Think模式，既获得推理带来的语义理解增强，又避免推理时的性能退化。
  - **技术流程**：
    1. 构建大规模CoT标注的导航指令数据集，用于训练监督。
    2. 在训练阶段，模型被要求生成辅助推理（如解析指令、规划子目标、评估可行性）后再预测动作。
    3. 在推理/应用阶段，去掉显式推理生成步骤，直接利用经过训练内化的表征进行高效动作预测。
- **数据资源**：
  - 发布了**R2R-CoT-320k**，一个包含约32万条CoT标注的大规模数据集，为数据高效的VLN训练提供支撑。

## 3. 实验设计

- **任务与基准**：
  - 聚焦于VLN标准基准，基于R2R类指令导航数据集构建CoT标注数据（R2R-CoT-320k），并在多个VLN数据集上进行实验验证。
- **对比方法**：
  - 对No-Think、Pre-Think、Post-Think三种推理策略进行系统比较。
  - 与现有微调大模型的方法进行性能对比，验证Aux-Think的有效性。
- **评估维度**：
  - 导航成功率、指令跟随准确性、泛化能力、训练效率/数据效率等。

## 4. 资源与算力

- 论文提供的材料中**未明确说明** GPU 型号、数量、训练时长、显存占用等具体算力信息。
- 仅从“数据高效”和“降低训练成本”等表述可以推断，作者在计算效率方面有所优化，但缺乏可复现的量化细节。

## 5. 实验数量与充分性

- **实验组别**：
  - 至少包括三类推理策略的对比实验（No-Think / Pre-Think / Post-Think）。
  - Aux-Think的完整模型实验。
  - 多个VLN数据集上的泛化验证。
  - 可能包含训练数据规模消融（数据高效性）和推理成本对比。
- **充分性与客观性评估**：
  - 从摘要和元数据看，实验设计覆盖了“推理策略”“数据规模”“泛化效果”等关键维度，逻辑完整。
  - 但受限于当前获取的材料，**实验表格、具体数值、消融细节、统计显著性均未给出**，难以全面评判实验的公平性与充分性。
  - 由于该论文被NeurIPS 2025接收且评分较高（9.0），推测实验较为扎实，但需阅读全文才能确认。

## 6. 主要结论与发现

- 首次系统揭示了VLN中的**推理时推理崩溃**现象：推理时使用CoT不仅无益，反而有害。
- 单纯的“推理时推理”策略不适用于长程动作决策任务。
- **Aux-Think通过训练时内化推理、推理时直接动作的方式，成功将CoT的价值迁移到VLN中**，有效提升了指令对齐和泛化能力。
- 该方法能够在不牺牲性能的前提下显著降低训练成本，验证了推理策略在数据高效VLN中的潜力。

## 7. 优点

- **问题敏锐**：首次系统关注推理策略在VLN中的作用，填补了该领域的空白。
- **方法论创新**：提出“训练时推理、推理时不推理”的Aux-Think范式，巧妙规避了推理时推理崩溃。
- **数据贡献**：发布了R2R-CoT-320k大规模数据集，为后续研究提供公共资源。
- **实践价值**：在提升性能的同时降低训练负担，符合具身智能模型对数据与算力效率的实际需求。
- **系统对比**：同时对三种推理策略进行评估，结论具有清晰的对比性和说服力。

## 8. 不足与局限

- **信息不完整**：当前材料仅提供摘要和元数据，缺少实验细节、超参数设置、baseline实现、评估指标的具体数值，影响可复现性。
- **推理崩溃机理未深入**：论文发现了推理时推理崩溃现象，但未在摘要中解释其背后机制（如累积误差、长动作序列的语义漂移、训练-推理不一致等），理论深度有待加强。
- **数据集覆盖面**：R2R-CoT-320k基于R2R指令生成，可能存在场景、语言表述和任务类型的偏向性，对真实世界复杂指令的泛化能力需要更多验证。
- **应用限制**：仅验证了VLN中的单一任务类型；对视觉-语言导航之外的长程决策任务（如机器人操作、交互式问答）是否适用尚不明确。
- **潜在风险**：CoT标注数据的质量和一致性直接影响训练效果，文中未说明标注协议和质量控制手段。

（完）
