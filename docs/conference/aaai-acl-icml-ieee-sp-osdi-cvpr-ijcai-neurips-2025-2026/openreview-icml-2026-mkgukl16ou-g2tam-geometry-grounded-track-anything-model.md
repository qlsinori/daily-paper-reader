---
title: "G$^2$TAM: Geometry Grounded Track Anything Model"
title_zh: G2TAM：几何约束的任意物体跟踪模型
authors: "Chenming Zhu, Peizhou Cao, Jingli Lin, Wenbo Hu, Yunlong Ran, Jiangmiao Pang, Tai Wang, Xihui Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a145c4bdeadbedef5312dda0e17186b513b62898.pdf"
tags: ["query:semantic-map"]
score: 6.0
evidence: 几何约束隐式记忆; 语义场景理解; 跨视角一致的物体定位
tldr: 人类的空间理解来自几何与语义的联合感知，而现有视频分割模型依赖外观记忆，难以应对大视角变化和长期遮挡。本文借助现代前馈3D重建模型的空间一致性，提出G2TAM统一框架，仅用无序RGB图像或视频即可进行可提示的3D实例跟踪，并利用空间对齐的几何表示作为隐式记忆，确保实例身份和位置在跨视角和时间上的稳定，为空间记忆与场景理解提供新思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 视频分割模型的外观记忆在视角剧变和长期遮挡下不稳定，需要借助几何与语义的联合空间理解来保持物体身份。
method: 利用前馈3D重建获得的空间一致性，将空间对齐的几何表示作为隐式记忆，支持从无序RGB图像或视频进行提示式3D实例跟踪。
result: G2TAM能够在大视角变化和长期遮挡下维持稳定的实例身份和定位，提升跨视点跟踪性能。
conclusion: 表明几何强化的隐式记忆可显著增强物体跟踪的鲁棒性，并为具身智能体的空间记忆建模提供可借鉴的方法。
---

## Abstract
Human spatial understanding arises from jointly perceiving geometry and semantics, enabling consistent object identification and localization across viewpoints and time. Current video segmentation models depend on explicit object appearance memory banks for instance tracking, yet they remain vulnerable to large viewpoint changes and long-term occlusions. Leveraging the spatial consistency afforded by modern feed-forward 3D reconstruction models, we propose the Geometry Grounded Tracking Anything Model (G$^2$TAM), a unified framework for promptable instance tracking in 3D using only unordered RGB images or videos. G$^2$TAM employs spatially aligned geometric representations as implicit memory, ensuring stable instance identity and localization across frames and views. At its core is a cross-modal spatial encoder that integrates visual and textual prompts into a shared geometric space, enabling end-to-end spatial reconstruction and instance-consistent mask prediction. To support training and evaluation, we construct InsTrack, a large-scale dataset with a dedicated validation split for benchmarking. Extensive experiments show that G$^2$TAM delivers strong cross-view consistency, promptable instance spatial tracking, video object segmentation, and spatial reconstruction, establishing a foundation for interactive, geometry-grounded spatial reasoning.

---

## 论文详细总结（自动生成）

## 论文总结：G²TAM——几何约束的任意物体跟踪模型

### 1. 核心问题与整体含义
- **研究背景**：人类的空间理解来源于对**几何信息**与**语义信息**的联合感知，这种联合使得我们能够在不同视角和时间上对物体进行一致的识别与定位。
- **现有问题**：当前视频分割模型主要依赖**显式的物体外观记忆库**进行实例跟踪，但这类方法在面对**大幅度视角变化**和**长期遮挡**时极易失效，导致实例身份丢失或漂移。
- **研究意义**：本文提出将**几何信息**与语义感知结合，利用现代前馈3D重建模型提供的空间一致性，为物体跟踪引入更稳定的“空间记忆”，从而提升跨视角和跨时间的跟踪鲁棒性，并为具身智能体的空间记忆建模提供了新思路。

### 2. 方法论：G²TAM框架
- **核心思想**：利用前馈3D重建模型获得的**空间一致性**，将**空间对齐的几何表示**作为**隐式记忆**，替代或增强传统的外观记忆库，从而稳定地保持实例身份与位置。
- **输入与输出**：G²TAM仅需**无序RGB图像或视频**，即可实现基于提示（如点击、文本）的**3D实例跟踪**，并同步完成空间重建与实例一致的掩码预测。
- **关键技术**：提出一种**跨模态空间编码器**，将视觉提示与文本提示统一映射到一个**共享的几何空间**中，实现端到端的空间重建与实例分割任务协同优化。
- **算法流程（文字描述）**：输入无序图像/视频 → 前馈3D重建提取空间几何特征 → 跨模态编码器将用户提示（视觉/文本）对齐到几何空间 → 隐式几何记忆引导实例身份关联 → 输出跨视角/跨帧一致的3D实例跟踪结果与掩码。
- **明确公式**：论文文本未提供具体数学公式，整体以架构和模块描述为主。

### 3. 实验设计
- **数据集**：作者构建了名为 **InsTrack** 的大规模数据集，并专门划分了**验证集**用于benchmark测评。
- **实验场景**（根据摘要）：包括**跨视角一致性**、**可提示实例空间跟踪**、**视频对象分割**以及**空间重建**等任务。
- **对比方法**：本次提供的文本中**未明确列出**具体对比的基线方法，也未给出定量评估指标，因此无法从现有信息中判断比较的全面性。

### 4. 资源与算力
- **未明确说明**：所给文本（标题与摘要部分）中**没有提及**任何关于训练算力的信息，包括GPU型号、数量、训练时长、参数量等。因此，无法从该文本回应资源消耗情况。

### 5. 实验数量与充分性
- **实验数量**：从摘要描述看，覆盖了至少四个方向的验证（跨视图追踪、视频分割、空间重建等），但具体**实验组数未知**。
- **充分性与公平性**：由于当前文本缺少消融实验、基线对比、指标明细和统计显著性分析，**无法客观判断实验的充分程度与公平性**。只能说实验覆盖面较广，但细节不足，有待查阅全文确认。

### 6. 主要结论与发现
- G²TAM能够在**大幅视角变化**和**长期遮挡**条件下维持稳定的实例身份与定位，显著提升跨视点跟踪性能。
- 实验表明，**几何强化的隐式记忆**可以显著增强物体跟踪的鲁棒性，优于依赖外观记忆的传统方法。
- 该框架为**交互式、几何引导的空间推理**（如具身智能）奠定了技术基础。

### 7. 优点
- **方法创新**：将几何信息与语义提示统一到共享空间，以隐式记忆替代外观记忆，思路新颖且符合人类空间感知机制。
- **统一框架**：仅用无序RGB图像或视频就能同时完成提示式3D实例跟踪、视频分割和空间重建，具有较好的泛化潜力。
- **构建数据集**：提出大规模InsTrack数据集，为后续研究提供基准资源，填补了该任务数据集缺失的可能空白。
- **应用前景**：对具身智能体的空间记忆建模、跨视角视频理解等领域具有参考价值。

### 8. 不足与局限
- **信息缺失风险**：当前提取的文本内容严重不完整（仅有标题、元数据与摘要），导致无法评估实验细节、算法复杂度、失败案例等。
- **实验结论可验证性**：缺少公开对比指标与消融研究，难以独立验证“几何隐式记忆”相对外观记忆的增量收益到底有多大。
- **依赖重建质量**：方法高度依赖前馈3D重建的准确性，在重建退化场景（如动态物体、低纹理区域、极端照明）下可能存在性能瓶颈，但文中未讨论。
- **应用限制**：目前主要面向机器人/具身智能等空间感知场景，在其他弱纹理或大规模开放域视频中的通用性有待探讨。

> **注**：以上总结仅基于论文提供的标题、元数据及摘要部分，若要获得关于实验细节、算力配置、对比基线等完整信息，需要进一步查阅原始论文全文。

（完）
