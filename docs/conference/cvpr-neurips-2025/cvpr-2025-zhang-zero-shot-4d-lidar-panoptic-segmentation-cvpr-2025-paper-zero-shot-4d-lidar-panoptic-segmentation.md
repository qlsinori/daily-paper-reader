---
title: Zero-Shot 4D Lidar Panoptic Segmentation
title_zh: 零样本4D激光雷达全景分割
authors: "Zhang, Yushan, Ošep, Aljoša, Leal-Taixé, Laura, Meinhardt, Tim"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_Zero-Shot_4D_Lidar_Panoptic_Segmentation_CVPR_2025_paper.pdf"
tags: ["query:semantic-map"]
score: 7.0
evidence: 面向语义建图与定位的分割方法，为导航中的语义地图构建提供支持
tldr: 针对4D激光雷达场景理解中标注数据稀缺的问题，论文提出SAL-4D方法，利用多模态机器人传感器桥接视频目标分割与视觉-语言基础模型，为激光雷达生成伪标注并实现零样本4D全景分割。该方法无需额外标注即可识别任意物体，能直接服务于语义建图与定位。实验表明其在零样本设置下取得优异的4D分割性能，为导航智能体的环境感知提供了可泛化的解决方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1718, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1796, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 330, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 662, \"label\": \"Table\"}]"
motivation: 4D激光雷达感知缺少大规模多样标注，限制了场景理解与语义建图。
method: 将视频目标分割与视觉-语言基础模型蒸馏到激光雷达，利用多模态传感器生成伪标签，实现零样本4D全景分割。
result: 在零样本4D分割基准上表现出色，支持流式感知与语义建图。
conclusion: 为无标注环境下的语义地图构建和导航感知提供了有效且通用的技术路径。
---

## Abstract
Zero-shot 4D segmentation and recognition of arbitrary objects in Lidar is crucial for embodied navigation, with applications ranging from streaming perception to semantic mapping and localization. However, the primary challenge in advancing research and developing generalized, versatile methods for spatio-temporal scene understanding in Lidar lies in the scarcity of datasets that provide the necessary diversity and scale of annotations. To overcome these challenges, we propose SAL-4D (Segment Anything in Lidar--4D), a method that utilizes multi-modal robotic sensor setups as a bridge to distill recent developments in Video Object Segmentation (VOS) in conjunction with off-the-shelf Vision-Language foundation models to Lidar. We utilize VOS models to pseudo-label tracklets in short video sequences, annotate these tracklets with sequence-level CLIP tokens, and lift them to the 4D Lidar space using calibrated multi-modal sensory setups to distill them to our SAL-4D model. Due to temporal consistent predictions, we outperform prior art in 3D Zero-Shot Lidar Panoptic Segmentation (LPS) over 5 PQ, and unlock Zero-Shot 4D-LPS.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 论文的核心问题与整体含义

- **研究背景**：4D激光雷达（Lidar）全景分割是具身导航（embodied navigation）、语义建图、定位等应用的基础感知能力。现有数据驱动方法高度依赖人工标注数据集（如SemanticKITTI、nuScenes），这些数据集存在两个核心限制：
  - **标注规模有限**：4D时空标注的采集成本极高，难以覆盖开放世界中丰富的物体类别；
  - **类别词汇封闭**：所有方法只能识别预定义的物体类别，无法泛化到训练中未见过的物体。
- **核心问题**：如何在**没有人工标注**的情况下，实现激光雷达序列中**任意物体的分割、跟踪与零样本识别**？即零样本4D激光雷达全景分割。
- **整体意义**：该工作是首个系统研究零样本4D激光雷达全景分割的工作，将视觉基础模型（VOS、CLIP）的知识通过多模态传感器桥接蒸馏到激光雷达模态，为开放世界4D场景理解提供了可行的技术路径，直接服务于语义地图构建与导航感知。

### 2. 论文提出的方法论

#### 核心思想

- 利用多模态机器人传感器（激光雷达 + RGB相机）作为**桥接媒介**，将图像/视频领域成熟的视觉基础模型（Segment Anything / SAM2 + CLIP）的知识**蒸馏到激光雷达模态**，从而在没有人工标注的条件下生成4D时空一致性的伪标签，用于训练端到端的4D激光雷达分割模型。

#### SAL-4D伪标签引擎（Pseudo-label Engine）

- 输入为一段激光雷达序列和对应的多视角相机视频。

**Step 1: Track（视频跟踪）**
- 使用SAM进行网格提示（grid prompting）在第一帧定位所有物体掩码；
- 使用SAM2将掩码在时间窗口 K 帧内传播，得到时间一致的"masklet"；
- 使用CLIP的相对掩码注意力（relative mask attention）为每个masklet生成序列级语义特征（CLIP token）。

**Step 2: Lift（提升至3D）**
- 通过标定的激光雷达-相机外参，将2D掩码投影/提升到3D点云空间；
- 使用DBSCAN密度聚类（多密度参数集成）修正传感器对齐误差；
- 融合多相机结果（IoU阈值 + 面积加权特征融合）。

**Step 3: Flatten（4D展平）**
- 在4D时空体中可能存在重叠的masklet，按照体积降序排序，通过IoM（交并最小值）抑制重叠实例，保证每个点唯一分配一个实例。

**Step 4: 跨窗口关联（Cross-window Association）**
- 对滑动窗口产生的局部实例，通过线性分配（最小成本匹配）基于3D-IoU进行跨窗口关联，为任意长度序列生成全局一致的实例ID并聚合语义特征。

#### SAL-4D模型

- **架构**：Minkowski U-Net稀疏卷积作为backbone编码叠加点云（4D时空体），配合Fourier位置编码（含时间维度）；随后使用Transformer解码器（类似Mask2Former / Mask4Former）通过可学习query预测每个实例的**时空掩码、objectness分数和CLIP token**。
- **训练**：通过二分图匹配建立预测与伪标签的对应关系，优化三个损失之和：
  - Lseg：BCE + Dice损失（掩码）；
  - Lobj：交叉熵损失（objectness）；
  - Ltoken：余弦距离损失（CLIP token对齐）。
- **推理**：模型在时间窗口内直接输出实例掩码与CLIP特征，通过近在线（near-online）IoU匹配跨窗口关联；零样本识别通过文本提示与CLIP特征点积的argmax完成。

### 3. 实验设计

#### 数据集

| 数据集 | 传感器配置 | 主要用途 |
|--------|-----------|---------|
| SemanticKITTI | 64线Velodyne + 前视相机（仅14%点云在相机可见范围） | 主要benchmark |
| Panoptic nuScenes | 32线Velodyne + 5个环视相机（48%点云可见） | 跨数据集验证 |

#### Benchmark与评估指标

- **4D评估**：LSTQ（核心指标），分解为Sassoc（时空关联质量）和Scls（语义识别质量）；
- **3D评估**：Panoptic Quality（PQ），分解为SQ和RQ。

#### 对比方法

- **监督方法**：DS-Net、PolarSeg、GP-S3Net、MaskPLS、EfficientLPS、4D-PLS、4D-StOP、4D-DS-Net、Eq-4D-PLS、Mask4Former、Mask4D等；
- **零样本基线**：
  - SAL（单扫描零样本LPS SOTA）；
  - SAL + MinVIS（基于查询嵌入的视频分割关联）；
  - SAL + MOT（基于卡尔曼滤波和线性分配的3D多目标跟踪）；
  - SAL + SW（Stationary World，仅利用自我运动传播掩码的简单基线）。

### 4. 资源与算力

- 论文正文和附录**均未明确说明**使用了多少GPU（型号、数量）、训练时长或具体算力消耗。仅能从方法描述中推断，训练涉及Minkowski U-Net + Transformer解码器，计算开销较大，但具体数值无从得知。

### 5. 实验数量与充分性

#### 实验数量概览

| 实验方向 | 具体组数 | 说明 |
|----------|---------|------|
| 伪标签引擎消融 | 4+组 | 窗口大小（K=2/4/8/16）、跨窗口关联有无、单扫描vs 4D标签对比 |
| 模型训练消融 | 6+组 | 时间窗口大小（2/4/8）、自我运动补偿三种方式（None/Rand/Mix） |
| 3D-LPS benchmark | 2组 | 在frustum内和有FrankenFrustum增强的全点云设置上对比 |
| 4D-LPS benchmark | 2组 | SemanticKITTI + Panoptic nuScenes |
| 零样本基线对比 | 3种基线×2数据集 | SW、MOT、MinVIS |

#### 充分性与客观性评估

- **优点**：消融实验较为系统，覆盖了伪标签引擎和模型训练两个关键环节的关键设计决策；在3D和4D两个维度、两个数据集上进行评估，对比方法全面（监督方法的SOTA和多种零样本基线）；
- **局限**：主要评估指标集中在LSTQ和PQ，附录中提供了部分补充分析，但伪标签质量（如与GT的实例级匹配精度）缺乏系统的定量分析；大部分详细的消融（如DBSCAN参数、IoU阈值等）位于附录中，正文呈现有限。

### 6. 论文的主要结论与发现

- **4D伪标签显著优于单扫描伪标签**：以相同模型训练，4D伪标签比单扫描伪标签在3D零样本LPS上提升PQ超过5个点（38.2 vs 33.1在frustum内；30.8 vs 25.3在全点云上），证明了时间一致性对于分割和识别的重要性；
- **首次解锁零样本4D-LPS**：SAL-4D在SemanticKITTI上达到LSTQ 42.2，在nuScenes上达到45.0，远超所有零样本基线，达到监督方法的59%-73%的性能水平而无需任何人工标注；
- **跨窗口关联与长时CLIP特征聚合**带来语义识别提升（Scls +2.6），验证了时间聚合对CLIP特征质量的正向作用；
- **自我运动补偿与随机dropout**的组合策略（90%随机参考帧 + 10%不补偿）显著提升分割性能（Sassoc 77.2 vs 61.3不补偿）；
- **时间窗口大小的选择**存在最优值（K=8左右），更大的窗口因SAM2长时传播误差而收益递减。

### 7. 优点

- **任务创新性**：首次正式定义并研究零样本4D激光雷达全景分割，填补了该方向空白；
- **方法论亮点**：
  - 提出"Track–Lift–Flatten"伪标签引擎，巧妙将视频分割模型的时空一致性优势与激光雷达的精确空间定位优势互补结合；
  - 利用SAM2的短程稳健性，避免长时视频分割不稳定的问题；
  - 将thing/stuff的区分去除，统一处理任何物体类别；
  - 跨窗口关联机制优雅地处理了物体进出传感器范围的问题；
- **实用价值**：无需任何人工标注即可训练对任意类别物体有感知能力的4D激光雷达分割模型，具备较强的可扩展性和实际部署潜力。

### 8. 不足与局限

- **语义识别仍是瓶颈**：零样本识别得分Scls（34.9）与监督方法（68.0）差距最大，说明CLIP token在激光雷达模态上的语义迁移仍有较大提升空间；
- **长时间一致性退化**：随着时空跨度增大，分割一致性明显下降，反映了叠加点云上保持长时间实例关联的挑战；
- **thing类分割质量偏低**：物体类别（动态实例）的分割质量（IoU_th）显著低于stuff类（静态背景），存在类别不平衡问题；
- **伪标签覆盖范围受限**：伪标签只覆盖相机可见的视锥区域（SemanticKITTI仅14%，nuScenes为48%），虽然通过FrankenFrustum增强缓解，但本质上仍存在传感器盲区问题；
- **依赖图像模态**：伪标签生成依赖相机图像，在夜间、恶劣天气等相机失效场景下无法使用；
- **算力信息缺失**：论文未报告训练成本，难以评估实际部署的经济可行性。

（完）
