---
title: Distilling LLM Prior to Flow Model for Generalizable Agent’s Imagination in Object Goal Navigation
title_zh: 将LLM先验蒸馏至流模型以实现目标物体导航的可泛化想象
authors: "Badi Li, Ren-Jie Lu, Yu Zhou, Jingke Meng, Wei-Shi Zheng"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=W0sqoTL7rL"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向目标物体导航的生成式流模型与LLM语义先验
tldr: 针对目标物体导航中语义地图补全过于确定化、难以泛化到未知环境的问题，论文提出生成式流框架GOAL。该方法将大语言模型推断的全场景语义先验编码为二维高斯场注入目标地图，以建模室内布局的语义分布。实验表明生成式建模显著增强智能体对未观测区域的想象能力，提高未知环境下ObjectNav的成功率。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有ObjectNav方法用确定性语义地图补全，忽略室内布局的不确定性，泛化能力受限。
method: 基于生成式流模型，将LLM提供的语义先验以二维高斯形式注入地图，建模语义分布。
result: 在未知环境目标导航中显著提升成功率，验证了生成式语义想象的有效性。
conclusion: 生成式语义分布建模可为具身目标导航提供更强的泛化能力。
---

## Abstract
The Object Goal Navigation (ObjectNav) task challenges agents to locate a specified object in an unseen environment by imagining unobserved regions of the scene. Prior approaches rely on deterministic and discriminative models to complete semantic maps, overlooking the inherent uncertainty in indoor layouts and limiting their ability to generalize to unseen environments. In this work, we propose GOAL, a generative flow-based framework that models the semantic distribution of indoor environments by bridging observed regions with LLM-enriched full-scene semantic maps. During training, spatial priors inferred from large language models (LLMs) are encoded as two-dimensional Gaussian fields and injected into target maps, distilling rich contextual knowledge into the flow model and enabling more generalizable completions. Extensive experiments demonstrate that GOAL achieves state-of-the-art performance on MP3D and Gibson, and shows strong generalization in transfer settings to HM3D.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **任务背景**：论文聚焦于**目标物体导航（Object Goal Navigation, ObjectNav）**任务，要求智能体在未知环境中通过想象场景中未观测到的区域，定位并导航至指定类别的物体。
- **现有方法的缺陷**：以往方法普遍采用**确定性、判别式模型**对语义地图进行补全，将室内布局视为单一确定性的结果，忽略了室内环境结构固有的**不确定性与多样性**（如家具摆放、房间布局的多模态可能性）。
- **核心问题**：这种确定性的语义地图补全方式**缺乏泛化能力**——面对训练中未见过的新环境时，模型难以合理推断未观测区域的语义分布，导致导航成功率受限。
- **研究意义**：若能显式建模室内环境语义分布的**不确定性**，并借助大语言模型（LLM）的常识性先验，即可提升智能体对未知场景的想象能力，进而增强其在全新环境中的导航性能。

### 2. 论文提出的方法论

- **总体思路**：提出 **GOAL**（Generative flow-based framework for Object-goal nAvigation with LLM priors），一个基于**生成式流模型（Flow-based Generative Model）**的框架，用于对室内环境的语义分布进行建模，而非确定性地补全地图。
- **核心思想**：通过将已观测区域的信息与LLM增强的全场景语义地图桥接起来，生成式地建模室内环境的语义分布，从而使补全结果具有多模态性和泛化性。
- **关键技术细节**：
  - **LLM语义先验蒸馏**：在训练阶段，利用大语言模型对场景布局进行常识性推断，提取**全场景语义先验**（例如不同物体之间的空间共现关系、典型房间布局）。
  - **二维高斯场编码**：将该语义先验编码为**二维高斯场（2D Gaussian Field）**，以概率分布的形式注入到目标语义地图中，从而将丰富的上下文知识“蒸馏”进流模型。
  - **流模型训练**：通过这种注入机制，训练生成式流模型学习从观测部分到完整语义地图的条件分布；模型在推理时能够采样生成合理的未观测区域语义补全。
- **算法流程概要**（文字描述）：
  1. 输入当前观测到的部分场景语义地图；
  2. 利用LLM对全场景语义进行推断，生成语义先验；
  3. 将LLM先验编码为二维高斯场并注入目标地图；
  4. 训练流模型学习观测地图与完整语义地图之间的映射分布；
  5. 推理时，从训练好的分布中采样，生成对未观测区域的语义想象，辅助导航决策。

### 3. 实验设计

- **使用的数据集 / 场景**：
  - **MP3D**（Matterport3D）——大规模真实室内场景数据集；
  - **Gibson**——真实室内环境数据集；
  - **HM3D**（Habitat-Matterport 3D）——用于**跨数据集迁移测试**，评估模型的泛化能力。
- **Benchmark**：目标物体导航（ObjectNav）标准基准任务，评价指标包括**成功率（Success Rate）**等。
- **对比方法**：论文未在摘要中明确列出具体对比方法，但声称与“先前的方法”（prior approaches，即确定性/判别式语义地图补全方法）进行了对比，并达到了**最先进水平（State-of-the-Art, SOTA）**。

### 4. 资源与算力

- **文中未明确说明**：摘要中完全没有提及所使用的GPU型号、数量、训练时长、参数量等计算资源信息。
- **需要指出**：由于本文为简要摘要版本，缺乏算力相关细节；正式论文正文中可能有更详细说明，但本处所给内容不足以回答该问题。

### 5. 实验数量与充分性

- **已报告实验**：
  - 在 **MP3D** 上达到SOTA；
  - 在 **Gibson** 上达到SOTA；
  - 在 **HM3D** 上进行了跨数据集迁移实验，展示了较强的泛化能力。
- **未报告实验**：摘要中未提及消融实验的具体组数（如去除LLM先验的影响、高斯场注入方式对比、生成式vs判别式对比等）。
- **充分性评估**：
  - **公平性/客观性**：使用两个主流基准数据集（MP3D、Gibson）加上一个迁移数据集（HM3D），覆盖面较广，与同类工作基准一致，实验设计具有较好的说服力；
  - **不足之处**：基于摘要信息，无法判断是否进行了充分的消融分析；完整的实验充分性需要查阅正文中的详细实验表格和设置来进一步确认。

### 6. 论文的主要结论与发现

- **生成式建模更具泛化能力**：实验表明，采用生成式流模型对语义分布建模，相比传统确定性补全方法，显著增强了智能体对未观测区域的“想象”能力。
- **LLM先验有效**：将LLM推断出的语义先验以二维高斯场形式注入，能够有效地将常识性布局知识融入生成模型，提升补全质量与导航成功率。
- **跨环境泛化**：在未知环境（以及跨数据集HM3D）的目标导航任务中，GOAL显著提升了成功率，验证了生成式语义分布建模的有效性和通用性。

### 7. 优点

- **创新性强的思路**：将ObjectNav中的语义地图补全从“确定性判别”转向“生成式分布建模”，明确建模室内布局的不确定性，这是对已有方法的重要突破。
- **巧妙融合LLM先验**：利用大语言模型的常识性空间语义知识，通过二维高斯场的连续空间编码方式注入生成模型，实现了离散先验与连续地图表示的桥接，技术设计较为精巧。
- **实证表现突出**：在MP3D和Gibson两个主流benchmark上同时达到SOTA，并且在跨数据集场景（HM3D）中保持强泛化，实验结果具有较强的说服力。
- **研究价值高**：为具身智能中“预测-想象-规划”范式提供了新的生成式建模思路，对后续研究具有启发意义。

### 8. 不足与局限

- **摘要信息有限，局限性未明确报告**：从提供的摘要看，论文没有显式讨论方法的局限，但可推测以下几个方面：
  - **LLM先验的偏差风险**：LLM的语义先验主要来自互联网文本知识，可能包含对特定文化、地域或场景的偏见，在极特殊或非典型室内环境中可能导致错误先验；此外LLM推断的准确性本身也受模型能力限制。
  - **计算复杂度**：流模型通常需要较多计算资源进行训练和推理，同时需要额外调用LLM来生成先验，可能带来更高的整体算力开销，不利于实时导航部署。
  - **实验覆盖面**：虽然验证了三个数据集，但实际上MP3D、Gibson和HM3D都主要来自北美居所场景，对办公室、商店、医院等其他室内场景类型的泛化未做验证；此外摘要未展示失败案例或边界情况的详细分析。
  - **导航下游整合**：摘要仅说明语义补全提升了导航成功率，未详细说明生成的地图如何与导航策略（如探索策略、路径规划）具体耦合，中间环节的误差积累问题有待进一步讨论。
- **说明**：上述不足部分是基于方法特性和常见同类工作局限所做的合理推断，正式论文中的局限性分析需以原文为准。

（完）
