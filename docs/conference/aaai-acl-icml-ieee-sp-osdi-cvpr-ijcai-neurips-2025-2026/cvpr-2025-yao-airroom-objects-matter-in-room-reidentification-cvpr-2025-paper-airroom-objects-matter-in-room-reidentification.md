---
title: "AirRoom: Objects Matter in Room Reidentification"
title_zh: AirRoom：物体在房间重识别中至关重要
authors: "Yao, Runmao, Du, Yi, Chen, Zhuoqun, Zheng, Haoze, Wang, Chen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yao_AirRoom_Objects_Matter_in_Room_Reidentification_CVPR_2025_paper.pdf"
tags: ["query:semantic-map"]
score: 8.0
evidence: 面向室内场景识别的物体感知房间重识别
tldr: 房间重识别在增强现实和家庭机器人中有广泛应用，但现有视觉地点识别依赖全局描述子或局部特征聚合，在堆满人造物体的杂乱室内环境中容易失效。AirRoom提出物体感知的粗到精检索管线，融合全局上下文、物体块、物体分割和关键点等多层级物体信息。在多个新构建的房间重识别数据集上，该方法显著优于传统视觉地点识别方法，为室内场景识别提供了利用物体信息的有效范例。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1803, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1805, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 857, \"height\": 516, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1811, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1812, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 877, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 877, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 876, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 872, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yao-airroom-objects-matter-in-room-reidentification-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 876, \"height\": 318, \"label\": \"Table\"}]"
motivation: 现有点地点识别方法在布满人造物体的杂乱室内环境中忽略物体信息，导致房间重识别效果差。
method: 提出AirRoom，在粗到精检索框架中融合全局上下文、物体块、物体分割和关键点的多层物体信息。
result: 在MPReID、HMReID、GibsonReID和Replica等四个数据集上验证了该方法优于现有VPR方法。
conclusion: 显式利用物体级线索可以显著提升室内房间重识别和地点识别的鲁棒性。
---

## Abstract
Room reidentification (ReID) is a challenging yet essential task with numerous applications in fields such as augmented reality (AR) and homecare robotics. Existing visual place recognition (VPR) methods, which typically rely on global descriptors or aggregate local features, often struggle in cluttered indoor environments densely populated with man-made objects. These methods tend to overlook the crucial role of object-oriented information. To address this, we propose AirRoom, an object-aware pipeline that integrates multi-level object-oriented information--from global context to object patches, object segmentation, and keypoints--utilizing a coarse-to-fine retrieval approach. Extensive experiments on four newly constructed datasets--MPReID, HMReID, GibsonReID, and ReplicaReID--demonstrate that AirRoom outperforms state-of-the-art (SOTA) models across nearly all evaluation metrics, with improvements ranging from 6% to 80%. Moreover, AirRoom exhibits significant flexibility, allowing various modules within the pipeline to be substituted with different alternatives without compromising overall performance. It also shows robust and consistent performance under diverse viewpoint variations.

---

## 论文详细总结（自动生成）

## AirRoom: Objects Matter in Room Reidentification —— 论文总结

### 1. 核心问题与研究动机

- **问题定义**：房间重识别（Room Reidentification, ReID）旨在从参考数据库中准确检索出与给定查询图像相同的房间实例。该任务是增强现实（AR）、家庭服务机器人等应用的关键基础技术。
- **现有方法的不足**：
  - **全局描述子方法（如 DINOv2）**：能够捕获场景级语义特征，但在布局和装饰高度相似的相邻房间中缺乏判别力。
  - **局部特征聚合方法（如 Patch-NetVLAD、AnyLoc）**：通过聚合局部特征增强判别性，但在布满相似、重复人造物体的室内环境中仍易混淆。
  - **房间分类方法**：只能判断房间的语义类别（如厨房、卧室），无法精确区分同一类房间的不同实例。
- **核心原因**：室内场景被大量人造物体密集填充，而现有视觉地点识别（VPR）方法在设计上更针对城市级、结构差异显著的室外场景，**忽略了物体导向信息在房间级识别中的关键作用**。
- **核心问题**：什么样的物体属性对于房间重识别是真正必不可少的？——论文针对这一问题展开首个系统性研究。

### 2. 方法论：AirRoom 物体感知粗到精检索管线

AirRoom 是一个**无需训练（training-free）**的物体感知管线，包含三个阶段、四层级物体导向信息：

#### 2.1 四层级物体导向信息
| 层级 | 作用 |
|------|------|
| **全局上下文（Global Context）** | 如沙发+电视的组合，传递房间的语义类别（客厅）；用于初步粗筛选。 |
| **物体块（Object Patches）** | 提供更细粒度的差异，如区分卧室的床头柜与办公室的书桌。 |
| **物体分割（Object Segmentation）** | 隔离单个物体（如将餐桌从周围椅子中分离出来），厘清房间布局。 |
| **关键点（Keypoints）** | 如抽屉把手，可过滤其他房间中视觉相似但并非目标的家具。 |

#### 2.2 三阶段流程

**① 全局阶段（Global Stage）**
- **Global Feature Extractor**：使用预训练模型（ResNet、DINOv2 等）提取全局上下文特征。
- **Global Retrieval**：计算查询与参考图像的余弦相似度矩阵，为每个查询选取 **Top-5** 候选房间。

**② 局部阶段（Local Stage）**
- **Instance Segmentation**：对查询图像及5个候选图像进行实例分割（Mask R-CNN 或 Semantic-SAM），得到物体的掩码和包围框，计算每个物体的中心点坐标。
- **Receptive Field Expander（感受野扩展器，创新模块）**：
  - 基于物体中心点集合应用 **Delaunay 三角剖分**，构建物体邻接矩阵，编码物体间的空间邻近关系。
  - 将每个物体的包围框扩展至包含其所有相邻物体，形成信息更丰富的**物体块**。
  - 应用 **NMS** 去除高重叠的冗余包围框。
- **Object Feature Extractor**：分别提取物体块和物体分割的特征。
- **Mutual Nearest Neighbors（互最近邻）**：通过双向最近邻匹配获得查询-参考特征对的余弦相似度集合 P（公式见下文）。
- **Object-Aware Scoring（创新模块）**：综合全局分数、块分数和物体分数，为每个查询选出 **Top-2** 候选：
  - **s = s_global + s_patch(Q_p, R_p) + s_object(Q_o, R_o)**
  - 其中 s_patch 和 s_object 可选择均值策略 s_mean 或最大值策略 s_max。
  - s_global 作为先验，反映初始5个候选的关联程度差异。

**③ 细粒度阶段（Fine-Grained Stage）**
- **Fine-Grained Retrieval**：使用 LightGlue（兼顾精度和效率的深度特征匹配器）对查询图像与 Top-2 候选图像进行关键点匹配，选择匹配关键点对数更多的候选作为最终检索结果。

#### 2.3 关键公式

- 余弦相似度矩阵：S_ij = (Q_i · R_j) / (‖Q_i‖‖R_j‖)
- Top-5 选取：Top5(S_i, :) = argsort(−S_i, :)[:5]
- 物体中心点：c = (x + W/2, y + H/2)
- 互最近邻匹配及分数计算（公式 4-7、9a、9b）如原文所示。

### 3. 实验设计

#### 3.1 数据集
- 由于现有室内数据集不适合房间重识别任务，论文基于 **Habitat Simulator** 和高质量 3D 室内数据集（Matterport3D、Habitat-Matterport3D、Gibson、Replica），**构建了四个新数据集**：

| 数据集 | 场景数 | 房间数 | RGB-D 图像数 |
|--------|--------|--------|--------------|
| MPReID | 15 | 105 | 16,231 |
| HMReID | 21 | 105 | 15,781 |
| GibsonReID | 24 | 45 | 6,743 |
| ReplicaReID | 12 | 19 | 2,862 |

- **数据库构建**：每个房间仅选择一张最具代表性的参考图像（通过 CLIP 特征 + K-means 聚类中心选取），查询图像包含不同视角变化。

#### 3.2 对比方法
- **图像检索**：CVNet
- **全局描述子 VPR**：DINOv2
- **局部特征聚合 VPR**：Patch-NetVLAD、AnyLoc

#### 3.3 评估指标
- Accuracy、Precision、Recall、F1 Score。

### 4. 资源与算力

- **论文中未明确说明**所使用的 GPU 型号、数量及训练时长等算力信息。
- 值得注意的推论是：AirRoom 是**无需训练（training-free）**方法，所有模块均使用预训练模型（如 DINOv2、Mask R-CNN / Semantic-SAM、LightGlue），因此不需要大规模训练算力，仅需推理计算。

### 5. 实验数量与充分性

实验较为充分，主要包含以下五组：

1. **总体性能对比**：在四个数据集上与四种主流基线方法对比，AirRoom 在几乎所有指标上超越 SOTA。
2. **分组（Group-wise）对比**：以相同骨干网络为基准，对比 AirRoom 的物体感知增强机制与 CVNet（ResNet50 组）、Patch-NetVLAD（NetVLAD 组）等增强机制的有效性。
3. **管线灵活性评估**：逐一替换关键模块（Global Feature Extractor、Instance Segmentation、Object Feature Extractor、Object-Aware Scoring），验证管线不依赖特定模型。
4. **消融实验**：分别移除 s_global、s_patch、s_object、Fine-Grained Retrieval 等组件，验证每个模块的必要性。
5. **运行时分析**（附录提及）。

**公平性评估**：所有对比均采用相同骨干网络分组进行，且灵活性实验中展现了多种配置下的性能，结果客观可信。实验覆盖了多数据集、多模块组合、多消融设置，整体充分性较好。

### 6. 主要结论与发现

- **AirRoom 在四个数据集上全面超越现有 SOTA 方法**，在已有改进空间上实现了 20%~40% 的额外提升（相对于 AnyLoc），最大改进幅度达 6%~80%。
- **四层级物体导向信息缺一不可**：全局上下文用于语义粗筛，物体块区分同类房间，物体分割厘清布局，关键点提供最细粒度的判别。
- **管线高度灵活**：任一模块均可替换为不同模型（如用 ViT 替换 ResNet50、用 Semantic-SAM 替换 Mask R-CNN），性能仍能保持在较高水平。
- **对视角变化有较强的鲁棒性**，适用于真实场景中不同视角下的房间重识别。

### 7. 优点

- **新颖的问题视角**：首次系统性地研究了多层级物体导向信息在房间重识别中的作用，明确回答了"什么样的物体属性对房间重识别至关重要"这一核心问题。
- **无需训练的设计**：全部使用预训练模型，易于部署和推广，避免了室内大规模训练数据难以收集的问题。
- **两个创新模块**：Receptive Field Expander 利用 Delaunay 三角剖分扩展物体感受野，巧妙捕获了物体间的空间共现关系；Object-Aware Scoring 融合了全局先验、物体块和物体分割的多重分数，实现了有效的粗到精筛选。
- **数据集贡献**：构建了四个新的房间重识别数据集（MPReID、HMReID、GibsonReID、ReplicaReID），填补了现有数据集缺少房间级标注和室内场景适配的空白。
- **实验设计严谨**：分组对比、灵活性评估和消融实验多层次验证了方法的有效性和可扩展性。

### 8. 不足与局限

- **物体重排的鲁棒性未验证**：论文明确指出，当前数据集缺乏物体被移动/重排的场景。尽管互最近邻机制对轻度物体重排有一定鲁棒性，但未经过专门验证。
- **动态场景未覆盖**：室内若有移动物体或人员活动，方法可能受到影响；论文提到动态场景理解是未来方向。
- **数据集规模有限**：所有数据集来自仿真环境（Habitat + 3D 数据集），尚未在真实室内场景图像上进行验证，真实世界的泛化能力有待检验。
- **参考图选取策略**：每房间仅取一张参考图像，在面对较大视角变化和部分遮挡时可能不够稳健，实际应用中可能需要多参考视图。
- **算力信息缺失**：论文未报告运行推理的具体硬件配置和耗时细节，附录中虽有运行时分析但正文未能充分体现。

（完）
