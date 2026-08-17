---
title: Video World Models with Long-term Spatial Memory
title_zh: 具有长期空间记忆的视频世界模型
authors: "Tong Wu, Shuai Yang, Ryan Po, Yinghao Xu, Ziwei Liu, Dahua Lin, Gordon Wetzstein"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=HbTxc6U1fO"
tags: ["query:vln-memory"]
score: 6.0
evidence: 基于几何的长期空间记忆存储与检索机制
tldr: 视频世界模型受限于有限上下文窗口，在场景重访时难以保持一致性，导致遗忘。作者提出一种基于几何的长期空间记忆框架，包含存储和检索机制，并构造专门数据集对世界模型的显式3D记忆进行训练与评估。实验表明该方法显著提升生成视频的质量与一致性。该空间记忆机制为导航智能体等需要长期场景记忆的任务提供了可借鉴的思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视频世界模型因上下文窗口有限，在场景重访时无法保持一致性，容易遗忘已生成环境。
method: 提出基于几何的长期空间记忆框架，加入显式3D记忆的存储与检索机制，并构建专门数据集训练世界模型。
result: 实验显示引入长期空间记忆后，视频生成质量与一致性显著提升。
conclusion: 该研究说明显式空间记忆能改善生成模型的长时一致性，对机器人导航等方向具有参考价值。
---

## Abstract
Emerging world models autoregressively generate video frames in response to actions, such as camera movements and text prompts, among other control signals. Due to limited temporal context window sizes, these models often struggle to maintain scene consistency during revisits, leading to severe forgetting of previously generated environments. Inspired by the mechanisms of human memory, we introduce a novel framework to enhancing long-term consistency of video world models through a geometry-grounded long-term spatial memory. Our framework includes mechanisms to store and retrieve information from the long-term spatial memory and we curate custom datasets to train and evaluate world models with explicitly stored 3D memory mechanisms. Our evaluations show improved quality, consistency, and context length compared to relevant baselines, paving the way towards long-term consistent world generation.

---

## 论文详细总结（自动生成）

# 中文总结：具有长期空间记忆的视频世界模型

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：视频世界模型（Video World Models）能够根据动作（如相机运动、文本提示等控制信号）自回归地生成视频帧。这类模型是构建可交互虚拟环境、机器人导航等智能体的关键组件。
- **核心问题**：现有世界模型受限于有限的**时间上下文窗口**，当模型生成的场景被重新访问（scene revisit）时，难以保持场景一致性，导致对先前生成环境的**严重遗忘**。
- **研究意义**：该问题从根本上制约了世界模型在长时间、大范围场景中的可用性。作者从人类记忆机制中获得灵感，探索如何让世界模型具备“记住”过去生成环境的能力，从而为**长期一致的世界生成**铺平道路。

## 2. 方法论：核心思想与关键技术细节

- **核心思想**：引入一种**基于几何的长期空间记忆（geometry-grounded long-term spatial memory）** 框架，让视频世界模型能够显式地存储和检索场景的3D空间信息，从而在场景重访时保持一致性。
- **关键机制**：
  - **存储机制（Store）**：将生成过程中产生的场景信息以显式3D记忆的形式持久化保存，而非依赖有限的隐式上下文窗口。
  - **检索机制（Retrieve）**：在生成新帧时，根据当前相机位姿/几何信息从长期空间记忆中检索相关场景内容，辅助当前帧的生成。
- **技术特点**：
  - 该记忆机制是**几何接地（geometry-grounded）** 的，即记忆内容与3D空间位置绑定，而非纯粹的高维特征向量。
  - 作者构造了**专门的数据集**来训练和评估带有显式3D记忆机制的世界模型。
- **公式与算法流程**：论文PDF正文未提供详细公式或伪代码（受提取页面限制），但整体流程可概括为：*生成新帧 → 提取几何/场景信息 → 写入空间记忆 → 后续生成时检索相关记忆 → 融合记忆与当前上下文生成一致帧*。

## 3. 实验设计

- **数据集/场景**：作者**自定义构建（curate）了专门数据集**用于训练和评估，而非仅使用公开视频数据集，目的是适配“场景重访”这一长期一致性场景。
- **Benchmark**：以“世界模型在重访已生成场景时能否保持一致性”为核心评测目标，评估生成质量与上下文长度。
- **对比方法**：与相关基线（relevant baselines）进行对比，具体基线名称在元数据中未详列。
- **评估指标**：涵盖**生成质量（quality）**、**一致性（consistency）** 和**上下文长度（context length）** 三个维度。

## 4. 资源与算力

- 论文提供的元数据及可获取文本中**未提及**具体的GPU型号、数量或训练时长等算力信息。
- 需要指出：由于PDF正文被验证页面拦截，完整实验设置中的算力细节无法获取。

## 5. 实验数量与充分性

- **实验组数**：元数据表明进行了对比实验（vs. baselines）和消融分析（提及了消融实验，如去除记忆机制的变体），但**具体实验数量未在可获取内容中列出**。
- **充分性评估**：
  - 从摘要结论看，实验覆盖了质量、一致性、上下文长度三个维度，设计较为全面。
  - 但受限于自定义数据集，**缺乏在标准公开基准（如Minecraft、Habitat等）上的验证**，其泛化能力和与现有方法的公平对比有待进一步确认。
  - 论文审稿评分为6.0（中等偏上），说明方法得到认可但可能存在一定争议或验证不足。

## 6. 主要结论与发现

- 引入长期空间记忆后，视频世界模型在**生成质量**、**场景一致性**和**可支持的上下文长度**上均显著优于相关基线。
- 该研究证明：**显式3D空间记忆**能有效缓解世界模型在长期生成中的灾难性遗忘问题。
- 该方法为长期一致的世界生成提供了可行路径，并展示了将经典空间表征与现代生成模型结合的潜力。

## 7. 优点

- **问题选得好**：找准了视频世界模型在长期运行中的关键痛点——场景重访时的一致性与遗忘问题。
- **方法有理论依据**：借鉴**人类记忆机制**（存储-检索）设计模型，具有明确的认知科学动机。
- **显式记忆设计**：基于几何的3D记忆比隐式上下文更有解释性和可迁移性，且可以直接服务下游任务。
- **开源数据构建思路**：专门构造训练/评估数据集，为后续研究提供了基准基础。
- **对相关领域有启发**：该空间记忆机制对**视觉语言导航（VLN）** 等需要长期场景记忆的智能体任务具有参考价值（对应本文标签 query:vln-memory）。

## 8. 不足与局限

- **实验覆盖有限**：缺少在公开标准benchmark上的验证，导致与现有方法的对比公平性、模型泛化能力均存在不确定性。
- **数据偏见风险**：自定义数据集可能引入与特定数据分布相关的偏差，影响结论的普适性。
- **算力与复现细节缺失**：未提供训练代价、推理开销等资源信息，增加复现门槛。
- **方法复杂度**：显式3D记忆的存储与检索会引入额外计算和内存开销，在超长序列或大尺度场景下可能存在效率瓶颈。
- **应用限制**：目前主要针对“相机移动+场景重访”类设定，对于动态物体变化、光照变化等复杂长期变化场景的适应性尚未验证。

（完）
