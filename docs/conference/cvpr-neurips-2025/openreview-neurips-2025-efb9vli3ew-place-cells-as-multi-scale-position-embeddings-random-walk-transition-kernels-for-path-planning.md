---
title: "Place Cells as Multi-Scale Position Embeddings: Random Walk Transition Kernels for Path Planning"
title_zh: 位置细胞作为多尺度位置嵌入：用于路径规划的随机游走转移核
authors: "Minglu Zhao, Dehong Xu, Deqian Kong, Wenhao Zhang, Ying Nian Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=eFB9VlI3ew"
tags: ["query:vln-memory"]
score: 8.0
evidence: 基于位置细胞和随机游走转移核的空间嵌入，用于认知地图与路径规划
tldr: 海马体通过位置细胞的群体活动编码认知地图以支持空间导航，本文将其建模为随机游走转移核谱分解得到的非负空间嵌入。位置间的内积或欧氏距离编码多尺度转移概率相似性，形成邻接认知图，非负性和内积结构自然产生稀疏性，解释位置细胞局部放电野。该框架为空间长期记忆和路径规划提供了一种可解释的连续嵌入表征，可服务于导航系统的记忆机制设计。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 从位置细胞群体活动出发，建立可解释的认知地图嵌入，以支撑空间导航和路径规划。
method: 将位置细胞表示为多步随机游走转移核的谱分解所得非负嵌入，利用内积相似性编码位置间多尺度转移关系。
result: 该嵌入自然诱导稀疏局部放电野，并能形成可用于路径规划的邻接认知图。
conclusion: 为空间记忆的神经机制提供了计算模型，也可为导航系统的长期空间记忆提供算法启示。
---

## Abstract
The hippocampus supports spatial navigation by encoding cognitive maps through collective place cell activity. We model the place cell population as non-negative spatial embeddings derived from the spectral decomposition of multi-step random walk transition kernels. In this framework, inner product or equivalently Euclidean distance between embeddings encode similarity between locations in terms of their transition probability across multiple scales, forming a cognitive map of adjacency. The combination of non-negativity and inner-product structure naturally induces sparsity, providing a principled explanation for the localized firing fields of place cells without imposing explicit constraints. The temporal parameter that defines the diffusion scale also determines field size, aligning with the hippocampal dorsoventral hierarchy. Our approach constructs global representations efficiently through recursive composition of local transitions, enabling smooth, trap-free navigation and preplay-like trajectory generation. Moreover, theta phase arises intrinsically as the angular relation between embeddings, linking spatial and temporal coding within a single representational geometry.

---

## 论文详细总结（自动生成）

基于提供的论文摘要与元数据，以下总结仅覆盖可获得的信息；论文全文未在本次文本中完整给出，因此涉及实验、算力等细节将如实标注为“未明确说明”。

# 论文总结

## 1. 核心问题与整体含义

- **研究动机**：海马体通过位置细胞的群体活动编码认知地图，从而支持空间导航。论文希望从计算角度解释位置细胞为何表现出局部放电野，并如何支撑路径规划。
- **核心问题**：如何将位置细胞群体活动建模为一种可解释的空间嵌入，使其既能反映位置之间的邻接关系，又能天然产生稀疏、局部化的神经表征，并服务于导航与轨迹生成。
- **整体含义**：将位置细胞理解为“多尺度随机游走转移核”谱分解得到的非负嵌入。嵌入之间的内积或欧氏距离编码多尺度转移概率相似性，由此形成用于路径规划的“邻接认知图”。该框架统一解释了位置细胞稀疏性、场大小沿背腹侧层级变化、theta相位调制，以及平滑无陷阱导航等神经与行为现象。

## 2. 方法论

- **核心思想**：位置细胞群体活动被建模为从随机游走转移核谱分解中得到的非负空间嵌入。不同位置的嵌入向量之间的距离/内积表示它们在多步转移中的连通性。
- **关键技术细节**：
  - 使用**多步随机游走转移核**定义位置间的“多尺度转移概率相似性”；
  - 对该转移核进行**谱分解**，得到位置的非负嵌入；
  - 嵌入间的**内积**或等价地**欧氏距离**作为位置间邻接关系的度量，构成认知图；
  - **非负性**与**内积结构**的组合会自然诱导**稀疏性**，从而解释位置细胞局部放电野，而无需显式添加稀疏约束；
  - 转移核中的**时间参数/扩散尺度**决定放电野大小，与海马体**背腹侧层级**对应；
  - 通过**递归组合局部转移**构建全局表示，能够在无全局度量信息的情况下生成平滑、无陷阱的导航路径，并产生类似“preplay”的轨迹；
  - **theta相位**作为嵌入向量之间的角度关系内在涌现，从而在同一几何框架中将空间编码与时间编码联系起来。
- **算法流程（文字描述，基于摘要）**：
  1. 定义环境中的局部转移概率（随机游走核）；
  2. 考虑多步扩散，构造多尺度转移核；
  3. 对转移核进行谱分解，得到非负位置嵌入；
  4. 用嵌入内积/欧氏距离构造邻接认知图；
  5. 在邻接图上执行路径规划，或利用嵌入几何生成轨迹。

## 3. 实验设计

- **可用信息有限**：本次文本仅包含摘要，未给出具体数据集、场景、基准或对比方法。
- 从摘要推断，可能的验证方向包括：
  - 位置细胞放电野的模拟（稀疏性与场大小随扩散时间变化）；
  - 与海马背腹侧层级数据的对比；
  - 导航任务中的路径规划效果（平滑性、陷阱回避）；
  - 轨迹生成是否出现类似“preplay”现象；
  - theta相位与嵌入几何角度的一致性。
- 但以上均为合理推断，**不能作为论文实际实验内容的定论**，需查阅全文确认。

## 4. 资源与算力

- **未明确说明**：提供的摘要和元数据中没有涉及 GPU 型号、数量、训练时长或任何计算资源信息。
- 如果论文包含大规模导航仿真或神经数据拟合，可能需要一定算力，但无法从当前文本中获取。

## 5. 实验数量与充分性

- **无法评估**：由于缺少实验章节，无法统计实验组数、消融实验数量或对比方法。
- 从方法论角度看，该工作属于“计算建模 + 理论解释”类型，其充分性取决于是否做到：
  - 与真实位置细胞数据定量对比；
  - 与现有导航模型（如基于网格细胞、SLAM、强化学习）对比；
  - 对非负性、内积结构、扩散尺度等关键设计进行消融。
- 当前文本不足以判断实验是否客观、公平或充分。

## 6. 主要结论与发现

- 位置细胞群体可作为多尺度随机游走转移核的非负谱嵌入，形成邻接认知图。
- 稀疏局部放电野无需显式正则化，而是由非负内积结构自然涌现。
- 扩散时间参数决定放电野大小，模拟了海马背腹侧层级。
- 通过局部转移的递归组合可构建全局表征，实现平滑、无陷阱的导航，并生成类似 preplay 的轨迹。
- theta 相位作为嵌入间的角度关系出现，实现了空间编码与时间编码的统一解释。

## 7. 优点

- **理论统一性强**：用一个谱嵌入框架同时解释位置细胞稀疏性、场大小、导航、轨迹预演和 theta 相位。
- **可解释性高**：非负性和内积结构具有明确的神经生理学含义，而非黑箱表征。
- **无需显式稀疏惩罚**：从结构上自然产生局部放电野，更具原则性。
- **潜在计算优势**：通过递归组合局部转移构造全局表示，可能避免全局度量计算，有利于大规模环境扩展。

## 8. 不足与局限

- **文本信息不完整**：无法验证实验部分是否充分，缺少对数据集、baseline、消融和统计显著性的细节。
- **模型假设范围**：将位置细胞完全归因于转移核谱分解，可能弱化了感觉输入、运动指令等其他因素的作用。
- **谱分解的可扩展性**：在超大或动态环境中，随机游走转移核的谱分解可能面临计算复杂度挑战，文中未给出高效实现细节。
- **定量神经预测有限**：摘要中没有展示与真实神经数据的定量拟合（如放电野大小分布、theta相位调制强度），结论更多停留在概念模型层面。
- **导航性能未知**：与现有路径规划算法（如基于图搜索、强化学习或动物行为模型）的优劣对比不清晰。

（完）
