---
title: Video World Models with Long-term Spatial Memory
title_zh: 具有长期空间记忆的视频世界模型
authors: "Tong Wu, Shuai Yang, Ryan Po, Yinghao Xu, Ziwei Liu, Dahua Lin, Gordon Wetzstein"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=HbTxc6U1fO"
tags: ["query:vln-memory"]
score: 5.0
evidence: 为世界模型提出几何为基础的长期空间记忆，与导航系统中的记忆机制相关
tldr: 视频世界模型受限于时序上下文窗口长度，在重新访问场景时容易遗忘已生成的环境，导致一致性差。受人类记忆机制启发，论文提出一种基于几何的长期空间记忆框架，包含存储与检索机制，并构建自定义数据集训练和评估带显式3D记忆的世界模型。实验表明，加入长期空间记忆后，视频生成的质量和一致性显著提升，为具身导航中的长期空间保持提供了可借鉴的记忆建模方式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视频世界模型在重新访问场景时因上下文有限而产生遗忘，影响长时一致性。
method: 引入几何锚定的长期空间记忆，实现记忆的存储与检索，并定制训练集以学习显式3D记忆。
result: 评测显示生成质量与场景一致性显著提升，减少长时间生成时的遗忘。
conclusion: 为生成模型中的长期空间记忆提供了有效框架，也对导航智能体的空间记忆设计有启发意义。
---

## Abstract
Emerging world models autoregressively generate video frames in response to actions, such as camera movements and text prompts, among other control signals. Due to limited temporal context window sizes, these models often struggle to maintain scene consistency during revisits, leading to severe forgetting of previously generated environments. Inspired by the mechanisms of human memory, we introduce a novel framework to enhancing long-term consistency of video world models through a geometry-grounded long-term spatial memory. Our framework includes mechanisms to store and retrieve information from the long-term spatial memory and we curate custom datasets to train and evaluate world models with explicitly stored 3D memory mechanisms. Our evaluations show improved quality, consistency, and context length compared to relevant baselines, paving the way towards long-term consistent world generation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：视频世界模型（Video World Models）能够根据动作（如相机移动、文本提示等控制信号）自回归地生成视频帧。然而，这类模型受限于有限的时序上下文窗口大小，在重新访问先前已生成过的场景时，往往难以维持场景一致性，导致对先前生成环境的严重遗忘。
- **核心问题**：如何在长时间视频生成过程中保持场景的时空一致性，尤其是在模型需要“回到”之前访问过的位置时，避免出现前后矛盾或遗忘现象。
- **研究意义**：这一问题直接关系到世界模型在长时程、具身化场景中的可信度与实用性，例如具身智能体的导航、探索和交互任务。若模型无法保持长期一致性，则其作为“世界模拟器”的价值将大打折扣。

## 2. 论文提出的方法论

- **核心思想**：借鉴人类记忆的机制，引入一种**基于几何的长期空间记忆**（geometry-grounded long-term spatial memory）框架，使视频世界模型具备显式的记忆存储与检索能力，从而增强长时间生成时的场景一致性。
- **技术要点**：
  - 该框架包含两个核心操作：**记忆存储**（store）与**记忆检索**（retrieve）。
  - 记忆以**显式3D空间**的形式组织，即模型在生成过程中将已生成的环境信息以几何结构存储起来，并在需要时（如重新访问某场景）按需检索相关信息，以指导后续帧的生成。
  - 论文还**定制了自定义数据集**，用于训练和评估带有显式3D记忆机制的world model，以便模型在训练过程中学习如何使用长期空间记忆。
- **算法流程描述**（基于文字说明）：
  1. 模型接收当前帧和动作指令；
  2. 在生成新帧之前，模型根据当前相机位姿或场景线索从长期空间记忆中检索相关区域的历史信息；
  3. 将检索到的记忆信息与当前观测融合，作为生成下一帧的条件输入；
  4. 生成新帧后，将新信息更新回长期空间记忆库中，供未来检索使用；
  5. 整个过程循环进行，使模型能“记住”访问过的场景并在重访时保持一致。

## 3. 实验设计

- **数据集与场景**：论文未明确公开所用的benchmark名称，但说明了使用**自定义数据集**进行训练和评估。这些数据集专门设计用于测试模型在重访场景时的长期空间一致性。
- **对比方法**：论文评估中与相关baseline进行对比，但文中未给出具体的baseline名称列表。代表性的对比维度包括：生成质量、场景一致性、上下文长度等。
- **评测指标**：包括视频生成质量、时间一致性、空间一致性以及可支持的上下文长度等。

## 4. 资源与算力

- 论文原文（提供的段落）中**未明确说明**训练所用的GPU型号、数量、训练时长或算力消耗等资源信息。
- 仅可推测该工作涉及大规模视频世界模型训练和自定义数据集构建，应需要较高的计算资源，但具体数值无从考证。

## 5. 实验数量与充分性

- **实验组数**：从提供内容看，论文进行了与baseline的整体对比实验，并涉及不同评估维度（质量、一致性、上下文长度）。但**具体实验组数、消融实验数量及细粒度分析未见明确描述**。
- **充分性评估**：
  - 优点：提及了多维度的评测，且验证了长期记忆机制对一致性的关键作用。
  - 不足：缺乏对记忆存储容量、检索效率、模型规模变化、不同场景类型（如室内vs室外、静态vs动态）等方面的细致消融分析。整体而言，实验设计方向上合理，但**详细程度不足以完全评估其普适性和鲁棒性**。

## 6. 论文的主要结论与发现

- 提出并验证了**几何锚定的长期空间记忆机制**能够显著提升视频世界模型在长时间生成下的**质量、一致性和可支持上下文长度**。
- 相比无记忆机制的baseline，加入长期空间记忆后模型在“重访场景”时的遗忘现象得到明显缓解。
- 作者认为该框架为生成模型中的长期空间记忆提供了有效范式，并对导航智能体的空间记忆设计具有启发意义。

## 7. 优点

- **问题选择有价值**：抓住了视频世界模型的长时一致性问题，现实意义强。
- **方法有生物启发性**：借鉴人类记忆的存储/检索机制，结合几何3D表示，思路新颖。
- **显式记忆机制**：区别于隐式上下文扩展，显式3D空间记忆更可控、可解释，也便于后续模块化扩展。
- **定制训练数据**：针对性地设计数据集来训练和评估长期记忆能力，体现工程上的细致考量。

## 8. 不足与局限

- **实验细节不透明**：数据集构建方式、baseline具体设置、评测指标的具体定义等均未在提供内容中展开。
- **算力资源未报告**：无法评估方法的训练成本与可复现性。
- **场景覆盖有限**：未说明是否覆盖多种复杂的真实世界场景（如动态物体、光照变化、视角剧变等），泛化性存疑。
- **潜在偏差风险**：自定义数据集可能偏向于验证方法有效性，需警惕评估偏向性。
- **实际部署未验证**：未涉及与真实具身导航系统的集成验证，实际应用效果尚需进一步检验。

（完）
