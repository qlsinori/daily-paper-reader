---
title: Zero-Shot 4D Lidar Panoptic Segmentation
title_zh: 零样本4D激光雷达全景分割
authors: "Zhang, Yushan, Ošep, Aljoša, Leal-Taixé, Laura, Meinhardt, Tim"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_Zero-Shot_4D_Lidar_Panoptic_Segmentation_CVPR_2025_paper.pdf"
tags: ["query:semantic-map"]
score: 7.0
evidence: 面向语义建图与定位的零样本4D激光雷达全景分割
tldr: 面向具身导航中的激光雷达感知，论文提出零样本4D全景分割方法SAL-4D。该方法利用多模态机器人传感器设置，将视频目标分割与现成视觉语言基础模型的知识蒸馏到激光雷达数据，为短时片段生成伪标签并识别任意物体。该技术可支撑流式感知、语义建图与定位，缓解激光雷达空间-时间理解标注稀缺的问题。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1718, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1796, \"height\": 675, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 443, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 330, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 884, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 863, \"height\": 447, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-zero-shot-4d-lidar-panoptic-segmentation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 662, \"label\": \"Table\"}]"
motivation: 激光雷达稀疏标注限制零样本4D场景理解，阻碍语义建图与定位。
method: 用多传感器桥接视频目标分割与视觉语言基础模型，生成伪标签并分割任意物体。
result: 实现零样本4D分割与识别，支持语义建图与定位。
conclusion: 为具身导航的感知、建图与定位提供低成本可扩展方案。
---

## Abstract
Zero-shot 4D segmentation and recognition of arbitrary objects in Lidar is crucial for embodied navigation, with applications ranging from streaming perception to semantic mapping and localization. However, the primary challenge in advancing research and developing generalized, versatile methods for spatio-temporal scene understanding in Lidar lies in the scarcity of datasets that provide the necessary diversity and scale of annotations. To overcome these challenges, we propose SAL-4D (Segment Anything in Lidar--4D), a method that utilizes multi-modal robotic sensor setups as a bridge to distill recent developments in Video Object Segmentation (VOS) in conjunction with off-the-shelf Vision-Language foundation models to Lidar. We utilize VOS models to pseudo-label tracklets in short video sequences, annotate these tracklets with sequence-level CLIP tokens, and lift them to the 4D Lidar space using calibrated multi-modal sensory setups to distill them to our SAL-4D model. Due to temporal consistent predictions, we outperform prior art in 3D Zero-Shot Lidar Panoptic Segmentation (LPS) over 5 PQ, and unlock Zero-Shot 4D-LPS.

---

## 论文详细总结（自动生成）

# 1. 核心问题与研究动机

- 论文关注 **零样本 4D 激光雷达全景分割（Zero-Shot 4D Lidar Panoptic Segmentation, ZS-4D-LPS）**，目标是在激光雷达点云序列中同时实现：
  - 任意物体的分割（segmentation）；
  - 跨时间帧的跟踪（tracking）；
  - 基于测试时文本提示的零样本识别（zero-shot recognition）。
- 动机：具身导航、语义建图、定位等应用需要理解 4D 时空场景；但激光雷达数据的标注非常稀缺，尤其缺乏多样化和大规模标注，限制了通用、可扩展的时空场景理解方法的发展。
- 现有方法大多只能处理单帧（3D）点云，且受限于预定义类别；本文希望将图像/视频基础模型的能力迁移到激光雷达序列，从而突破类别词汇与单帧限制。

# 2. 方法论：SAL-4D

## 核心思想
- 利用多模态传感器设置作为“桥梁”：将**视频目标分割（VOS）**与**视觉-语言基础模型（CLIP）**的知识蒸馏到激光雷达模型。
- 做法：先用 VOS 模型在短视频窗口生成伪标签，再用 CLIP 生成序列级语义特征，最后将这些标签“提升”（lift）到 4D 激光雷达空间，用来训练端到端的激光雷达分割模型。

## 关键技术细节

### 1）伪标签引擎
- 输入：激光雷达序列 + 多个未标注相机视频。
- 流程包含：
  - **Track**：在窗口首帧用 SAM 做网格提示生成物体 mask，再用 SAM 2 将 mask 传播到整个窗口；
  - 对每个 mask 用 CLIP 相对 mask attention 生成语义特征；
  - **Lift**：通过标定将图像 mask 投影到激光雷达点云；用 DBSCAN 聚类修正由于传感器不对齐造成的误差；
  - 融合多相机 mask，并做体积排序与 IoM 抑制的“Flatten”操作，保证每个点最多属于一个实例。
- 之后进行**跨窗口关联**：通过 3D-IoU 代价矩阵的线性分配（linear assignment）将不同窗口中的 masklet 关联为长序列轨迹，并聚合 CLIP 特征。

### 2）分割模型
- 使用 Minkowski U-Net 编码叠加的点云窗口；对 voxel 特征加入 Fourier 位置编码（空间+时间）。
- 采用 Transformer decoder，输入一组可学习 query，预测：
  - 时空 mask；
  - objectness 分数；
  - 表示物体语义的 CLIP token。
- 训练损失：
  \[
  L_{SAL-4D} = L_{obj} + L_{seg} + L_{token}
  \]
  - \(L_{obj}\)：物体存在性交叉熵；
  - \(L_{seg}\)：mask 的 BCE + Dice；
  - \(L_{token}\)：CLIP token 的余弦距离。

### 3）推理
- 模型处理固定大小叠加窗口，按 near-online 方式用 3D-IoU 做跨窗口关联。
- 零样本识别时，将测试文本提示用 CLIP 文本编码器编码，与预测的 CLIP token 做点积取 argmax。

# 3. 实验设计

## 数据集
- **SemanticKITTI**：64 线激光雷达，10 Hz，单前视相机；8 thing + 11 stuff 类别。
- **Panoptic nuScenes**：32 线激光雷达，5 相机，2 Hz；8 thing + 8 stuff 类别。

## Benchmark 与指标
- 4D 任务采用 **LSTQ**（LSTQ = √(S_assoc × S_cls)），分别评估时空分割/跟踪质量（S_assoc）与语义识别质量（S_cls）。
- 3D 单帧任务采用 **Panoptic Quality (PQ)**，包含 SQ 和 RQ。

## 对比方法
- 监督方法：DS-Net、PolarSeg、GP-S3Net、MaskPLS、4D-PLS、4D-StOP、4D-DS-Net、Eq-4D-PLS、Eq-4D-StOP、Mask4Former、Mask4D、EfficientLPS+KF 等。
- 零样本基线：
  - 3D 单帧基线 **SAL**（本文的强基线）；
  - 将 SAL 单帧结果关联成 4D 的三种基线：
    - **SAL + MinVIS**（数据驱动 query 匹配）；
    - **SAL + MOT**（Kalman 滤波 + 线性分配）；
    - **SAL + SW**（Stationary World，仅用 ego-motion 传播 mask）。

# 4. 资源与算力

- **论文正文未明确说明**训练所用的 GPU 型号、数量、训练时长等计算资源信息。
- 仅在作者单位等处提及工作完成于 NVIDIA 实习期间，但无具体算力细节。

# 5. 实验数量与充分性

## 已做的实验
- **伪标签引擎消融**：
  - 时间窗口大小 K = {2, 4, 8, 16}；
  - 是否有跨窗口关联；
  - 与单帧 SAL 伪标签的质量比较。
- **模型训练消融**：
  - 是否做 ego-motion compensation（None / Rand / Mix）；
  - 模型时间窗口大小（2/4/8）。
- **基准评测**：
  - 3D LPS 在 SemanticKITTI 上的 PQ 对比；
  - 4D-LPS 在 SemanticKITTI 和 Panoptic nuScenes 上的 LSTQ 对比；
  - 定性可视化。

## 充分性与客观性评估
- 实验整体较充分，覆盖了组件级消融、伪标签质量分析、3D 与 4D 两套 benchmark，并与多种监督/零样本基线比较。
- 评价指标选择合理，特别使用 LSTQ 将“关联质量”和“语义识别”解耦，很适合零样本 4D 分析。
- 但也存在局限：
  - 仅在两个公开自动驾驶数据集上验证，未覆盖更广泛场景（如室内、非自动驾驶）；
  - 零样本基线构造有限，未与更多近期开放词汇/跟踪方法比较；
  - 伪标签只在相机可见视锥内评估，完整点云评估依赖 FrankenFrustum 增强，可能引入一定偏差。

# 6. 主要结论与发现

- 本文首次提出 **Zero-Shot 4D Lidar Panoptic Segmentation** 任务，并给出可实现的训练方案 SAL-4D。
- 通过时间一致性伪标签，SAL-4D 在单帧 3D 零样本 LPS 上超越 SAL 超过 **5 PQ**（如 full point cloud 上 30.8 vs 25.3）。
- 在 4D 任务上，SAL-4D 明显优于所有零样本基线：
  - SemanticKITTI：LSTQ 42.2，达到监督方法 Mask4Former 的约 60%；
  - Panoptic nuScenes：LSTQ 45.0，达到 EfficientLPS+KF 的约 72%。
- 时间一致性对识别尤其重要：跨窗口 CLIP 特征平均可显著提高 \(S_{cls}\)。
- 当前剩余主要 gap 在语义识别（\(S_{cls}\)）和长时一致性，thing 类分割质量仍低于 stuff 类。

# 7. 优点与亮点

- **任务创新**：首次将“零样本 4D 激光雷达全景分割”形式化为可训练问题，并建立完整 benchmark 流程。
- **伪标签引擎设计巧妙**：利用现成 VOS（SAM 2）和 CLIP 生成“时空 mask + 语义 token”，避免昂贵的人工标注。
- **多模态桥接**：充分利用相机-激光雷达标定，把二维视频分割能力迁移到三维/四维点云。
- **时间一致性带来实质收益**：不仅在 4D 任务上解锁新能力，还反向提升了单帧 3D LPS 的伪标签质量。
- **训练策略合理**：ego-motion compensation 与随机丢弃补偿的混合策略提升了模型鲁棒性。
- **对任意物体开放**：不依赖预定义类别，能分割“advertising stand”等超出标准数据集词汇的物体。

# 8. 不足与局限

- **识别精度仍有明显差距**：\(S_{cls}\)（34.9）与监督方法（68.0）差距大，是主要短板。
- **伪标签覆盖有限**：仅覆盖相机可见视锥内的点云，SemanticKITTI 中只有约 14% 点可见；完整点云泛化依赖额外增强。
- **长时稳定性不足**：跨时间窗口的关联误差会累积，长时间跟踪一致性仍待提升。
- **物体类别不均衡**：thing 类分割质量明显低于 stuff 类，影响整体 PQ/LSTQ。
- **算力信息缺失**：论文未报告训练资源，无法评估方法在资源受限场景下的可复现成本。
- **评测范围有限**：仅在两个自动驾驶数据集上评估，缺乏对非驾驶场景（如机器人室内环境）的验证。

（完）
