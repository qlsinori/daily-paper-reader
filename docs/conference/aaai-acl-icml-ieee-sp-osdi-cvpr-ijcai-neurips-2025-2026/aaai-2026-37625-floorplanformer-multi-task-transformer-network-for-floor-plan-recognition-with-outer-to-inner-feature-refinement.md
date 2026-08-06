---
title: "FloorPlanFormer: Multi-Task Transformer Network for Floor Plan Recognition with Outer-to-Inner Feature Refinement"
title_zh: FloorPlanFormer：用于平面图识别的多任务Transformer网络，由外到内的特征细化
authors: "Yun Liang, ZiHao Wu, Run Zheng, Shuai Xie, Bo Hong, Yishen Lin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37625/41587"
tags: ["query:semantic-map"]
score: 9.0
evidence: 平面图识别，房间类型分割
tldr: 论文针对平面图识别中门、外墙轮廓和内墙房间类型分割的困难，提出FloorPlanFormer多任务学习网络。网络分三阶段，先用Swin Transformer和像素解码器提取细粒度语义，再通过提示编码器和掩码解码器及全局上下文注意力模块生成高质量外轮廓，最后用掩码Transformer细化内轮廓。实验表明该方法能有效克服数据集间的风格差异，提升房间分割质量。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37625/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1733, \"height\": 1048, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37625/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1829, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37625/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1828, \"height\": 788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37625/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1725, \"height\": 845, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37625/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 959, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37625/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 846, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37625/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37625/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 757, \"height\": 483, \"label\": \"Table\"}]"
motivation: 平面图识别需要同时分割内外轮廓和房间类型，且数据集风格差异大。
method: 提出三阶段多任务Transformer，结合Swin骨干、GCAM和掩码Transformer进行由外到内细化。
result: 验证了该方法在房间分割和外轮廓生成上的有效性。
conclusion: 为平面图自动识别与房间分割提供了多任务学习框架。
---

## Abstract
Floor plan recognition requires accurate segmentation and classification of entrance doors, outer contours (walls and windows) and inner contours (various room types) , despite strong spatial dependencies and large stylistic differences between different datasets. To overcome these challenges, we propose FloorPlanFormer, a multi-task learning network divided into three phases: the first phase introduces a Swin Transformer backbone with a pixel decoder to extract fine-grained pixel-level semantics; the second phase employs prompt encoder and mask decoder, and a novel Global Contextual Attention Module (GCAM) is designed to generate clear, high-quality outer contour masks; the third stage uses mask transformer decoder to recognize targets and designs a Masked Feature Refinement Module (MFRM) to accurately delineate the inner contour by modeling the relationship between the local inner and outer contours. Finally, we constructed FloorPlan8K, a dataset containing 8200 images and 77434 instances, on which our model was trained and evaluated, and the results greatly outperformed the state-of-the-art general segmentation methods and specialized methods.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- 平面图识别需要同时分割和识别三类元素：**入口门**、**外轮廓**（墙与窗户）和**内轮廓**（不同类型房间），且存在强空间依赖性和跨数据集的显著风格差异。
- 传统方法（二值化、Hough变换、Canny边缘检测等）依赖手工阈值，面对复杂或非标准布局时准确率大幅下降；CNN方法虽有所改进，但仍存在边缘细节丢失、泛化能力不足的问题。
- 现有Transformer方法多聚焦于特定元素或结构，缺乏对内外轮廓关系的深度建模，导致预测结果出现元素重叠、边界不规则等问题。
- 论文旨在提出一种**多任务Transformer网络**，通过“由外到内”的特征细化机制，同时解决外轮廓、内轮廓和门的准确分割与分类问题，并构建大规模精细标注数据集以支撑训练和评估。

### 2. 论文提出的方法论

- **总体框架**：采用三阶段多任务学习结构：
  1. **特征提取与语义捕获**：使用Swin Transformer作为骨干网络，提取多尺度特征（x1–x4），再通过像素解码器（多尺度可变形注意力Transformer）细化像素级语义。
  2. **外轮廓预测**：利用GCAM增强全局特征，结合提示编码器（基于边界框和噪声掩码提示）和两层掩码解码器，生成清晰的外轮廓掩码。
  3. **内轮廓预测**：将外轮廓掩码作为注意力指导，输入Masked Feature Refinement Module（MFRM），精化多尺度特征，再经掩码Transformer解码器预测内轮廓（房间类型与入口门）。

- **关键模块**：
  - **GCAM（Global Contextual Attention Module）**：针对Swin Transformer长距离依赖建模不足的问题，对高分辨率特征进行下采样、通道扩展、自注意力计算，并引入位置嵌入，以捕获全局上下文信息，提升外轮廓预测准确性。
  - **MFRM（Masked Feature Refinement Module）**：双分支结构，上分支处理多尺度图像嵌入，下分支处理外轮廓掩码；通过注意力掩码加权（公式 `X_i = x_i · M_i`）和多方向固定卷积核（水平、垂直、对角、反对角）重复提取边缘信息，最后与原始多尺度特征拼接融合，强化内外轮廓之间的局部空间关系。
  - **掩码Transformer解码器**：采用注意力掩码机制，公式为 `F_l = F_{l-1} + softmax(Q_l K_l^T + M_{l-1}) V_l`，其中M为二进制掩码，用于引导模型关注有效区域。

- **损失函数**：
  - 外轮廓分支损失：`L_o = λ_o_ce L_ce + λ_o_dice L_dice`
  - 内轮廓分支损失：`L_rd = λ_r_ce L_ce + λ_r_dice L_dice + λ_cls L_cls`
  - 多任务联合损失：`L = λ_rd L_rd + λ_o L_o`，权重根据内外轮廓像素数量比例自适应计算（公式8），以平衡两个任务的贡献。

- **新数据集**：构建了**FloorPlan8K**，包含8200张图像、77434个实例，涵盖黑白线稿、未装饰线稿和全装修图纸三种风格；标注层级包括外轮廓（墙+窗）、入口门（扇形）和十种常见房间类型。

### 3. 实验设计

- **数据集**：主要在自建的FloorPlan8K上进行训练和评估（训练/测试划分未在文中明示，但训练设置部分提到在训练集上训练40个epoch）。
- **对比方法**：
  - 专业方法：DeepFloorplan（Zeng et al. 2019）
  - 通用分割方法：Mask2former（Cheng et al. 2022）
  - 表中还列出了DFPR、Ours、Ours++等变体，但正文未详细解释“Ours++”具体含义，推测为完整模型或加上额外模块的版本。
- **评估指标**：
  - 像素准确率（Accu）及各类别准确率（公式9-10）
  - 提出的**Unique Coverage Accuracy（UC）**（公式11-12），用于惩罚同一区域被过度分割为多个碎片的情况，更客观地评价分割连续性。
- **实验内容**：
  1. 与DeepFloorplan的定性对比（图4）和定量对比（表1）。
  2. 与Mask2former的对比（表1、图4）。
  3. 消融实验：移除GCAM和MFRM、单独加入、两者都加入（表2）。
  4. 损失函数分析：移除dice loss、移除cross-entropy loss、加入联合多任务损失（表3）。
  5. MFRM内部参数搜索：多方向卷积重复次数k（1/2/3）和通道卷积重复次数N（1/2/3）的组合（表4），最佳为k=2，N=3。

### 4. 资源与算力

- 论文在“Implementation Details”中说明：
  - 使用**单个NVIDIA A6000 GPU**，批量大小为4。
  - 训练**40个epoch**，优化器为AdamW，初始学习率1e-4，在第20和30个epoch时衰减0.1。
- 但**未提及训练总时长、单卡训练所需时间、GPU数量（仅为1张）是否足够、显存占用等细节**，也未说明推理速度或模型参数量。

### 5. 实验数量与充分性

- **实验数量**：相对丰富，包含两个对比方法、多组消融（模块、损失、超参数），并提供了可视化结果。
- **充分性与客观性**：
  - 在自建数据集上表现优异，但**未在公开基准（如CubiCasa5k、R2V等）上进行跨数据集验证**，泛化性存疑。
  - 对比方法较少，且缺少与近年其他Transformer专用方法（如Yue et al. 2022, CADTransformer等）的直接比较。
  - 提出了新的评估指标UC，虽能弥补传统准确率的不足，但该指标未被广泛使用，可能导致与既有研究结果不可直接比较。
  - 表1中“Ours”与“Ours++”的定义不明确，削弱了对比的清晰度。

### 6. 论文的主要结论与发现

- FloorPlanFormer在三阶段多任务框架下，通过GCAM和MFRM分别增强外轮廓与内轮廓的识别，有效解决了平面图元素边界模糊、空间依赖复杂的问题。
- 在FloorPlan8K上，完整模型（Ours++）在总体准确率、mIoU和UC指标上均优于DeepFloorplan和Mask2former，尤其在小类别（如cloakroom）和边缘细节上提升显著。
- 消融实验证明：GCAM和MFRM均能独立提升性能，同时使用效果最佳；dice loss是最关键的损失组成；自适应多任务权重有助于整体性能提升。
- MFRM中k=2、N=3的设置能较好地平衡边界细化与通道信息保留。

### 7. 优点

- **方法设计巧妙**：采用“由外到内”的特征细化策略，将外轮廓作为内轮廓的强先验，符合平面图结构逻辑。
- **模块创新性强**：GCAM融合自注意力与卷积，MFRM引入外轮廓掩码和多方向卷积，有效建模局部与全局关系。
- **新数据集贡献**：FloorPlan8K规模大、标注精细、风格多样，为后续研究提供了宝贵资源。
- **评估指标补充**：提出Unique Coverage Accuracy，更准确地反映模型在处理过度分割问题上的能力。
- **代码开源**：提供了GitHub链接，便于复现和扩展。

### 8. 不足与局限

- **实验验证范围有限**：仅在自建数据集上评估，未在公开数据集上测试或与其他方法公平比较，结论的普适性有待验证。
- **对比方法不够全面**：未包含更多近年SOTA方法（特别是其他Transformer专用方法），也缺少与实例分割、全景分割方法的对比。
- **暗含数据集偏差**：FloorPlan8K仅包含中国建筑图纸，风格和标签体系可能带有地域性，模型对其他地区或不同图纸风格（如欧美户型）的鲁棒性未知。
- **对开放布局效果差**：论文作者也承认，对于厨房+餐厅等开放区域，因缺乏明确边界，模型易误分割；对未标注或未装修房间的分类准确度较低。
- **资源/效率信息不足**：未报告参数量、FLOPs、推理延迟，也没有实时性优化方案，实际应用受限。
- **“Ours++”定义模糊**，不利于读者理解实验设置之间的差异。

（完）
