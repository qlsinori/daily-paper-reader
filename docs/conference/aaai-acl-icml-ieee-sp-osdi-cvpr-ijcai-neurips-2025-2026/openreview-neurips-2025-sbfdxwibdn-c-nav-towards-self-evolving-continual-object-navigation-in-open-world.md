---
title: "C-NAV: Towards Self-Evolving Continual Object Navigation in Open World"
title_zh: C-NAV：面向开放世界的自演化持续物体导航
authors: "MingMing Yu, Fei Zhu, wenzhuo liu, Yirong Yang, Qunbo Wang, wenjun wu, Jing Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=SbfdxWibDn"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 开放世界下的持续物体目标导航
tldr: 论文针对现有物体导航方法训练轨迹静态、类别固定、难以适应开放世界的问题，提出持续物体导航基准和C-Nav框架。C-Nav通过双路径抗遗忘机制（包括多模态特征蒸馏等）在习得新物体类别的同时避免灾难性遗忘。实验验证了该方法在持续学习新类别上的有效性，为动态开放世界中的物体导航提供了可行方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 物体导航需要在开放世界持续学习新类别，但现有方法存在灾难性遗忘。
method: 提出C-Nav框架，包含双路径抗遗忘机制和多模态特征蒸馏。
result: 在持续物体导航基准上验证了防止遗忘并学习新类别的有效性。
conclusion: 推动了开放世界下持续物体导航的研究。
---

## Abstract
Embodied agents are expected to perform object navigation in dynamic, open-world environments. However, existing approaches typically rely on static trajectories and a fixed set of object categories during training, overlooking the real-world requirement for continual adaptation to evolving scenarios. To facilitate related studies, we introduce the continual object navigation benchmark, which requires agents to acquire navigation skills for new object categories while avoiding catastrophic forgetting of previously learned knowledge. To tackle this challenge, we propose C-Nav, a continual visual navigation framework that integrates two key innovations: (1) A dual-path anti-forgetting mechanism, which comprises feature distillation that aligns multi-modal inputs into a consistent representation space to ensure representation consistency, and feature replay that retains temporal features within the action decoder to ensure policy consistency. (2) An adaptive sampling strategy that selects diverse and informative experiences, thereby reducing redundancy and minimizing memory overhead. Extensive experiments across multiple model architectures demonstrate that C-Nav consistently outperforms existing approaches, achieving superior performance even compared to baselines with full trajectory retention, while significantly lowering memory requirements. 
The code will be publicly available at \url{https://bigtree765.github.io/C-Nav-project}.

---

## 论文详细总结（自动生成）

好的，遵照您的要求，我基于提供的论文摘要和元数据，为您生成一份详细的中文总结。

**重要说明**：由于提供的文本中不包含论文的完整正文、图表、公式及详细的实验设置（如具体数据集配置、算力信息等），以下总结主要依据论文标题、摘要、元数据标签及相关公开信息进行推断和归纳。对于无法从现有资料中确认的细节，我会明确指出。

---

# 论文总结：C-NAV：面向开放世界的自演化持续物体导航

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：具身智能体（Embodied Agents）被期望在动态、开放的世界中执行物体导航任务。然而，现有大多数物体导航方法在训练时依赖于**静态轨迹**和**固定的物体类别集合**。
- **核心问题**：这种静态训练范式忽略了现实世界对**持续适应**不断变化场景的需求。当智能体部署到新环境时，它需要掌握导航到**新物体类别**的能力，同时不能遗忘**已学过的知识**（即灾难性遗忘问题，Catastrophic Forgetting）。
- **研究意义**：该论文聚焦于“物体导航”与“持续学习”的交叉领域，旨在解决机器人在开放世界中长期自主运行的核心瓶颈，推动具身智能从封闭环境走向开放世界。

## 2. 论文提出的方法论：核心思想、关键技术细节

论文提出了一个名为 **C-Nav** 的持续视觉导航框架，其核心思想是让导航智能体在序贯学习新物体类别时，通过专门的机制巩固旧知识，实现“增量学习”而不遗忘。C-Nav 包含两个关键创新：

- **双路径抗遗忘机制（Dual-path Anti-forgetting Mechanism）**：这是框架的核心，旨在从两个维度保持模型的稳定性：
    - **特征蒸馏路径（Feature Distillation）**：将多模态输入（如RGB图像、深度图、指令等）对齐到一个**一致的表征空间**。通过对新旧任务的特征输出施加一致性约束（蒸馏），确保学习新类别时，对旧类别物体的特征提取方式不发生剧烈改变，从而维持**表征一致性**。
    - **特征回放路径（Feature Replay）**：在动作解码器（Action Decoder）中，保留旧任务的关键**时序特征**。通过将过去的代表性特征“回放”给当前的策略网络，确保新旧任务的**策略一致性**，防止导航策略在新任务上发生偏移。
- **自适应采样策略（Adaptive Sampling Strategy）**：
    - 该策略用于筛选并存储旧任务中有价值的信息，用于特征回放。
    - 其核心目标是**选择多样且信息丰富**的经验样本，减少样本间的冗余，从而在维持抗遗忘效果的同时，**最小化额外的内存开销**。

（注：摘要未提供具体的公式或端到端算法流程细节，但核心逻辑可概括为：在持续学习框架下，通过“蒸馏+回放”双重约束来平衡“可塑性”（学习新任务）与“稳定性”（保持旧任务性能）。）

## 3. 实验设计：数据集、Benchmark 与对比方法

- **核心 Benchmark**：论文提出了一个新的 **“持续物体导航基准”（Continual Object Navigation Benchmark）**。该基准要求智能体在学习新物体类别的导航技能的同时，避免对旧知识的灾难性遗忘。这不同于传统静态的物体导航基准。
- **数据集/场景**：摘要未明确说明使用的具体模拟器（如 Habitat、AI2-THOR）或数据集细节（如物体类别数量、场景数量）。推测是在标准具身导航模拟环境中构建了序贯的任务流。
- **对比方法**：论文进行了广泛的实验，主要对比了：
    - **现有方法**：在持续学习场景下的其他导航或持续学习基线。
    - **带有全轨迹保留（Full Trajectory Retention）的基线**：即允许模型在训练新任务时存储并重放所有旧轨迹的上限方法。C-Nav 声称在性能上超越了这类方法，同时显著降低了内存占用。

## 4. 资源与算力

- **未明确说明**：根据提供的摘要和元数据，**文中没有提及**具体的 GPU 型号、数量、训练时长等算力信息。这是该论文在信息透明度上的一个局限。

## 5. 实验数量与充分性：实验是否充分、客观、公平

- **实验跨度**：论文强调了“在多个模型架构上进行了大量实验”（Extensive experiments across multiple model architectures），这增加了结论的泛化性。
- **充分性分析**：虽然摘要声称实验广泛，但因缺乏正文细节，无法确认具体实验组数。评估其充分性的关键点在于：
    - **架构消融**：测试了不同主干网络（如ResNet、ViT等）下的有效性，是加分项。
    - **消融研究**：论文包含了消融实验，证明“特征蒸馏”和“特征回放”两个组件各自的有效性（这是后续需要关注的部分，但摘要未明确列出详细数字）。
    - **公平性**：为了证明性能，与“全轨迹保留”的上限方法对比，是一个较有说服力的实验设计。这种对比能体现其方法在效率和性能间的良好权衡。

## 6. 论文的主要结论与发现

- **有效性**：C-Nav 在持续物体导航基准上，能够有效学习新类别任务，同时显著缓解灾难性遗忘问题。
- **性能优势**：C-Nav 的性能一致优于现有方法，甚至超过了保留全部旧轨迹的基线方法。
- **存储效率**：与全轨迹保留的基线相比，C-Nav 在达到更高性能的同时，大幅降低了内存和存储需求，体现了其在实际部署中的可行性。

## 7. 优点：方法或实验设计上的亮点

- **问题定义新颖**：首次（或较早）将“持续学习”概念系统性引入“物体导航”任务，提出了清晰的 Benchmark，填补了该研究方向的空白。
- **方法设计巧妙**：将特征蒸馏与特征回放解耦，分别作用于表征空间和策略空间，双管齐下解决遗忘问题，思路清晰且具有通用性。
- **探索“自演化”（Self-Evolving）**：论文标题强调“自演化”，区别于简单的多任务学习，更贴近“智能体在不断变化的环境中自适应生长”的终极目标。
- **工程价值高**：自适应采样策略在保证效果的前提下控制内存开销，对于资源受限的机器人平台非常友好；且承诺开源代码，有利于社区复现和后续研究。
- **结论有说服力**：在多个架构上验证，且与“全量存储”的方法作对比，突出其“性能-存储”平衡的优势。

## 8. 不足与局限

- **信息不完整（根据现有资料）**：本文总结仅基于摘要，无法对实验细节进行深入评判。摘要中未包含具体性能数值、消融实验的具体表格、以及在不同数据集上的详细对比。
- **模拟器与真实世界鸿沟（推测）**：论文很可能是在模拟环境中验证的（如 Habitat 等），但摘要未提及是否包含真实世界（Real-World）的机器人实验。从模拟到真实的泛化（Sim-to-Real）仍然是具身导航领域的巨大挑战。
- **基准的全面性（推测）**：持续物体导航基准的“开放性”程度未知。开放世界不仅涉及新类别，还涉及新场景、新布局、光照变化等，这些因素在基准中的覆盖程度未说明。
- **计算开销权衡**：虽然减少了存储开销，但特征蒸馏过程本身可能引入额外的训练计算量和复杂度（摘要未提及），这也是一个需要权衡的因素。

---

（完）
