---
title: "DynaNav: Dynamic Feature and Layer Selection for Efficient Visual Navigation"
title_zh: DynaNav：高效视觉导航的动态特征与层选择
authors: "Jiahui Wang, Changhao Chen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=D4j2K5lknb"
tags: ["query:embodied-nav"]
score: 8.0
evidence: DynaNav是面向视觉导航的框架，在模拟环境中评估，直接涉及具身导航智能体
tldr: 视觉导航通常依赖大规模基础模型，计算开销大且可解释性差。本文提出DynaNav框架，根据场景复杂度动态选择特征和层，结合可训练硬选择器与提前退出机制，并利用贝叶斯优化确定退出阈值，在保持导航性能的同时显著降低计算成本。在真实世界数据集和模拟环境中验证了高效性与可解释性，为边缘设备上的具身导航提供了实用方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有视觉导航基础模型计算开销大、可解释性差，难以在边缘设备部署。
method: 提出DynaNav，基于场景复杂度动态选择特征和层，采用可训练硬选择器与贝叶斯优化的早期退出机制。
result: 在真实数据集与模拟环境中验证，DynaNav在降低计算成本的同时保持了良好的导航性能。
conclusion: 为高效嵌入智能体的视觉导航提供了动态推理框架，促进了具身机器人的实际部署。
---

## Abstract
Visual navigation is essential for robotics and embodied AI. However, existing foundation models, particularly those with transformer decoders, suffer from high computational overhead and lack interpretability, limiting their deployment on edge devices. To address this, we propose DynaNav, a Dynamic Visual Navigation framework that adapts feature and layer selection based on scene complexity. It employs a trainable hard feature selector for sparse operations, enhancing efficiency and interpretability. Additionally, we integrate feature selection into an early-exit mechanism, with Bayesian Optimization determining optimal exit thresholds to reduce computational cost. Extensive experiments in real-world-based datasets and simulated environments demonstrate the effectiveness of DynaNav. Compared to ViNT, DynaNav achieves a $2.6\times$ reduction in FLOPs, 42.3% lower inference time, and 32.8% lower memory usage while improving navigation performance across four public datasets.

---

## 论文详细总结（自动生成）

# DynaNav：高效视觉导航的动态特征与层选择——论文总结

## 1. 核心问题与整体含义

- **研究背景**：视觉导航是机器人与具身智能（Embodied AI）的核心任务。当前主流方案依赖大规模基础模型，尤其是带有 Transformer 解码器的架构，虽取得了良好的导航性能，但存在两大关键瓶颈：
  - **计算开销巨大**：模型参数量大、推理 FLOPs 高，难以在算力受限的边缘设备（如无人机、家用机器人）上实时部署；
  - **可解释性差**：黑盒式的决策过程难以理解，模型无法根据场景复杂度自适应地调整计算资源。
- **核心问题**：如何在保持视觉导航性能的同时，显著降低计算成本并提升决策的可解释性？
- **整体含义**：本文提出一种“按需计算”的动态推理范式，旨在让导航智能体根据场景复杂度自适应地选择所需的特征和层，从而为具身机器人在真实世界中的高效部署提供可行方案。

## 2. 方法论：核心思想与技术细节

- **核心思想**：提出 **DynaNav**（Dynamic Visual Navigation）框架，核心原则是“动态分配计算资源”——简单场景使用少量特征和浅层网络推理，复杂场景才调用更多特征和深层网络，在不牺牲导航性能的前提下大幅降低平均计算成本。
- **关键技术一：可训练硬特征选择器（Trainable Hard Feature Selector）**
  - 设计一个可微分的硬选择器，对输入特征进行稀疏选择，只激活对当前场景最有判别力的特征子集；
  - 硬选择（而非软加权）可实现真正的稀疏计算，跳过未选中特征对应的计算路径，从而同时提升**效率**与**可解释性**（哪些特征被激活是显式可观测的）。
- **关键技术二：提前退出机制（Early-Exit Mechanism）**
  - 将特征选择与层级退出相结合：在 Transformer 解码器的不同层设置出口，当某层的输出置信度足够高时，提前终止推理，避免不必要的深层计算；
  - 提前退出策略是**自适应的**，由场景复杂度驱动。
- **关键技术三：贝叶斯优化（Bayesian Optimization, BO）确定退出阈值**
  - 提前退出中的关键超参数——退出阈值（何时判定置信度足够高）——通过贝叶斯优化自动确定，避免人工调参的繁琐和不稳定性；
  - BO 在效率与性能之间进行全局权衡，找到帕累托最优的阈值配置。
- **算法流程（文字描述）**：输入视觉观测 → 特征提取器生成多层特征 → 硬特征选择器按场景动态挑选特征子集 → 逐层通过解码器 → 每层出口评估置信度，若达到 BO 优化的阈值则提前输出动作 → 否则继续下一层推理，直至最终层输出。

## 3. 实验设计

- **数据集**：使用 **4 个基于真实世界数据的公开数据集**，覆盖多样化真实场景，具体数据集名称在摘要中未列出（原文未披露详细清单）。
- **场景**：真实世界数据集 + 模拟环境（simulated environments）双重评估。
- **基准（Benchmark）**：以 **ViNT**（Visual Navigation Transformer）作为主要对比基线。
- **对比方法**：主要与 ViNT 进行对比（摘要仅明确提及该基线；是否还有更多基线未知）。

## 4. 资源与算力

- **文中未明确披露**具体的 GPU 型号、数量或训练时长。
- 从摘要中无法获取训练阶段的算力消耗信息；仅能确认推理阶段的计算成本显著下降（FLOPs、延迟、内存均大幅降低）。
- 论文未提供能耗对比或端侧设备实测数据，资源相关分析仍有待补充。

## 5. 实验数量与充分性

- **实验数量**：摘要中提到的量化指标来自 4 个公开数据集上的对比实验，但未提及消融实验的具体组数（如：硬选择器 vs. 软选择器、有无提前退出、不同退出阈值等）。
- **充分性评估**：
  - **积极方面**：在 4 个不同数据集上验证，且报告了 FLOPs、推理时间、内存占用和导航性能等多个维度的指标，具备一定的说服力；
  - **不足方面**：由于摘要信息有限，以下问题尚未明确——是否做了消融实验？对比方法是否足够多样？是否与轻量化方法（如蒸馏、剪枝、量化）进行过对比？模拟环境与真实环境的差距如何评估？运行方差和统计显著性检验是否报告？因此，**实验的完整性难以完全判定**。

## 6. 主要结论与发现

- **DynaNav 在全面降低计算成本的同时，导航性能不降反升**。具体而言，相较于 ViNT：
  - **FLOPs 降低 2.6 倍**；
  - **推理时间降低 42.3%**；
  - **内存使用降低 32.8%**；
  - **在 4 个公开数据集上的导航性能均有提升**。
- 结论：动态特征与层选择是一种行之有效的范式，能够打破“性能-效率”之间的传统权衡，为边缘设备上的具身导航提供了实用且可解释的解决方案。

## 7. 优点

- **范式新颖**：将动态推理（动态特征选择 + 动态层数）引入视觉导航任务，超越了静态模型压缩的局限。
- **稀疏可控**：可训练硬选择器实现真正的稀疏计算，而非近似稀疏，从硬件层面就能受益（实际跳过计算）。
- **可解释性增强**：硬选择机制使模型决策过程透明化——用户可以观察到每个场景激活了哪些特征和层。
- **自动化调优**：贝叶斯优化确定退出阈值，避免手工调整，提高了方法的实用性和可复现性。
- **结果显著且多维验证**：并不只追求单一指标的改善，而是同步验证了 FLOPs、延迟、内存和导航成功率等多维指标，且性能全面优于强基线 ViNT。

## 8. 不足与局限

- **实验细节披露不足**：数据集具体名称、消融实验设计、基线数量、多轮随机种子下的方差等关键信息未在摘要中公开，难以完全评估结论的稳健性。
- **基线覆盖有限**：仅与 ViNT 对比，缺乏与模型剪枝、知识蒸馏、动态退出的其他代表性方法（如 AdaViT、Dynamic ViT 等）的横向比较。
- **真实部署验证欠缺**：虽然指标显示 FLOPs 和延迟降低，但未报告具体边缘硬件（如 Jetson、手机端 NPU）上的端到端实测性能，能耗节省是否线性对应实际收益尚不明确。
- **贝叶斯优化的开销**：BO 用于离线阈值寻优，但其计算开销和收敛效率文中未讨论；若场景分布剧烈变化，固定阈值可能失效。
- **适用范围局限**：不同任务（如目标导航 vs. 探索）下“场景复杂度”的定义可能不同，方法的泛化能力尚需进一步验证。
- **安全与鲁棒性**：提前退出机制可能在低置信度场景下无法正确评估自身不确定性，存在导航安全隐忧，论文未涉及失败模式分析。

（完）
