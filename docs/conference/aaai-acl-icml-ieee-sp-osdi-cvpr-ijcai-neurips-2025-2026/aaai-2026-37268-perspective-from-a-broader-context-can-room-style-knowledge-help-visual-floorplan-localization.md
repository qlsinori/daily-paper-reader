---
title: "Perspective from a Broader Context: Can Room Style Knowledge Help Visual Floorplan Localization?"
title_zh: 更广视角：房间风格知识能否帮助视觉楼层平面定位？
authors: "Bolei Chen, Shengsheng Yan, Yongzheng Cui, Jiaxu Kang, Ping Zhong, Jianxin Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37268/41230"
tags: ["query:semantic-map"]
score: 6.0
evidence: 基于平面图的视觉环境理解与房间风格信息
tldr: 论文针对建筑平面图结构重复导致的定位歧义问题，提出利用更广的视觉场景上下文和房间风格先验来增强视觉楼层平面定位。通过引入场景布局先验，方法在重复性强的室内结构中获得了更稳定的定位效果。该工作展示了视觉上下文信息对理解平面图环境的重要作用，可为空间语义地图构建提供参考。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37268/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 871, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37268/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37268/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37268/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 874, \"height\": 596, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37268/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1672, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37268/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37268/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 871, \"height\": 354, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37268/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37268/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 856, \"height\": 352, \"label\": \"Table\"}]"
motivation: 平面图结构重复导致视觉定位易出现歧义，现有方法未充分利用图像中的场景上下文信息。
method: 提出利用房间风格知识和视觉场景上下文为平面图定位算法注入场景布局先验。
result: 实验表明该方法可缓解重复结构下的定位歧义，提升定位准确率。
conclusion: 房间风格等上下文信息能有效辅助平面图定位，对空间理解具有价值。
---

## Abstract
Since a building's floorplan remains consistent over time and is inherently robust to changes in visual appearance, visual Floorplan Localization (FLoc) has received increasing attention from researchers. However, as a compact and minimalist representation of the building's layout, floorplans contain many repetitive structures (e.g., hallways and corners), thus easily result in ambiguous localization. Existing methods either pin their hopes on matching 2D structural cues in floorplans or rely on 3D geometry-constrained visual pre-trainings, ignoring the richer contextual information provided by visual images. In this paper, we suggest using broader visual scene context to empower FLoc algorithms with scene layout priors to eliminate localization uncertainty. In particular, we propose an unsupervised learning technique with clustering constraints to pre-train a room discriminator on self-collected unlabeled room images. Such a discriminator can empirically extract the hidden room type of the observed image and distinguish it from other room types. By injecting the scene context information summarized by the discriminator into an FLoc algorithm, the room style knowledge is effectively exploited to guide definite visual FLoc. We conducted sufficient comparative studies on two standard visual Floc benchmarks. Our experiments show that our approach outperforms state-of-the-art methods and achieves significant improvements in robustness and accuracy.

---

## 论文详细总结（自动生成）

# 论文总结：更广视角——房间风格知识能否帮助视觉楼层平面定位？

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：相机定位是计算机视觉中的经典问题，广泛应用于 3D 重建、AR/VR 和机器人导航。室内场景由于布局复杂、缺乏卫星定位信号，视觉定位尤其具有挑战性。传统方法依赖预采集数据库或复杂 3D 场景重建，构建、存储和维护成本高昂。
- **核心问题**：视觉楼层平面定位（FLoc）利用平面图的几何信息进行定位，但平面图作为建筑物布局的紧凑表示，包含大量重复结构（如走廊、墙角），且不同房间的布局可能高度相似，极易导致定位歧义和错误定位。
- **现有方法的不足**：
  - 依赖 2D 结构匹配或 3D 几何约束预训练的方法（如 SoTA 方法 3DP）无法有效解决由误导性场景布局引起的定位歧义。
  - 利用语义标注的方法（如房间类别、门窗标签）需要昂贵的人工标注，并非所有平面图都可用。
  - 基于贝叶斯滤波的序列定位方法只能通过图像序列**有限地**缓解歧义（只有当视觉外观发生显著变化时才有效）。
- **论文核心思想**：利用更广的**视觉场景上下文**——即房间风格知识（如卧室、浴室、厨房等具有不同的装饰风格和家具特征）——为 FLoc 算法注入场景布局先验，以消除定位不确定性和歧义。

## 2. 论文提出的方法论

### 2.1 整体框架

基于 F³Loc（Chen et al. 2024b）框架构建，由前端观测模型（观察模型）和后端直方图滤波器组成。通过将房间判别器总结的布局先验注入观测模型，利用场景上下文引导定位。

### 2.2 房间风格知识预训练（无监督学习）

- **自动数据采集**：
  - 基于 Gibson 数据集和对应的导航数据集自动收集无标注 RGB 图像。
  - 在导航片段的起始点和目标点放置配备第一视角 RGB 相机的机器人，从不同角度采集图像。
  - 为每张图像记录场景来源、导航片段、难度（根据轨迹长度分 easy/medium/hard 三级）三个属性。
  - 使用 Segment Anything Model (SAM) 清洗数据：若对象分割掩码数量过少（图像为空白/全黑/全白），则丢弃该图像。
- **带约束的无监督聚类学习**：
  - 构建约束矩阵 M，编码图像对之间的房间关系：
    - 不同场景 → 不同房间（-1）
    - 同一位置 → 同一房间（1）
    - 同一 easy 片段 → 可能同一房间（0.5）
    - 同一 hard 片段 → 可能不同房间（-0.5）
  - 使用 ResNet50（ImageNet 预训练）提取特征，基于余弦相似度构建距离矩阵 D。
  - 按公式 **RefinedMatrix = D − λM** 细化距离矩阵。
  - 采用 InfoMap 聚类算法对特征进行聚类，并为图像分配伪标签。
- **训练损失**：
  - **簇级对比损失**：L_C = −log(exp(Fθ(Ii)·φ+/τ) / Σ exp(Fθ(Ii)·φk/τ))，使图像特征与其所属簇中心对齐。
  - **交叉熵损失**：L_pred = −Σ[yi·log(Es(Fθ(Ii),Fθ(Ij)))+(1−yi)·log(1−Es(Fθ(Ii),Fθ(Ij)))]，训练风格网络判断两张图像是否来自同一房间。
  - **总损失**：L_loss = L_C + γ·L_pred。

### 2.3 注入房间风格知识增强 FLoc

- 将预训练的房间风格编码器 Fθ（已在无监督学习中获得场景布局先验）迁移到 FLoc 任务进行微调。
- 采用 F³Loc 框架的射线匹配思路：预测等角深度射线，与平面图中各候选位姿的 GT 射线比对生成概率图，支持单帧、多帧和自适应三种模式。
- FLoc 训练损失为 L1 损失加余弦相似度形状损失：
  - L_FLoc = ||d − d*||₁ + dᵀd* / max{||d||₂·||d*||₂, ε}

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **Gibson 数据集**（三个子集）：
  - Gibson(f)：仅前向运动，24,779 段序列视图，每段 4 帧。
  - Gibson(g)：含原地转向的一般运动，49,558 段序列视图，每段 4 帧，难度更高。
  - Gibson(t)：118 段长序列，每段 280~5,152 帧，用于轨迹跟踪评估。
  - 图像 FOV 108°，平面图分辨率 0.1 m，划分 108/9/9 为训练/验证/测试。
- **Structured3D (full)**：照片级真实数据集，3,296 个室内环境，78,453 张透视图像（非全景），FOV 80°，平面图分辨率 0.02 m，用于单帧 FLoc 对比。

### 3.2 对比方法

- PF-net（粒子滤波网络）、MCL（蒙特卡洛定位）、LASER（潜在空间渲染）、F³Loc（s/m/f 三变体）、3DP（s/m/f 三变体）。
- 所有对比方法均不使用语义标签或房间类别标注。

### 3.3 评估指标

- Recall @0.1 m / 0.5 m / 1 m，以及定位 1 m 内且朝向误差 <30° 的 Recall（即 1m 30°）。
- Gibson(t) 上还使用 RMSE(S)（成功轨迹跟踪的 RMSE）和 RMSE(A)（全部情况的 RMSE）。

## 4. 资源与算力

- 模型训练在 **4 块 NVIDIA 3090 GPU** 上进行（实施细节中明确提及）。
- 房间风格预训练：20 epochs，Adam 优化器，权重衰减 5e-4，batch size 64。
- FLoc 微调：学习率 0.001。Structured3D 上单帧模型训练 100 epochs；Gibson(f)/(g) 上单帧、多帧各训 100 epochs，自适应模式训 20 epochs（其中单帧和多帧参数冻结，仅训练选择网络）。

## 5. 实验数量与充分性

### 主要实验组

1. **主对比实验（表 1）**：在 Gibson(f) 和 Gibson(g) 上对比 Ours s/m/f 与 5 种基线方法（含 F³Loc 和 3DP 各三变体），报告 4 类指标。
2. **长序列轨迹跟踪（表 2）**：在 Gibson(t) 上与 LASER、F³Loc_s、3DP_s 对比 R@0.2 m、R@1 m、RMSE。
3. **跨数据集泛化（表 3）**：在 Structured3D (full) 上对比单帧方法与所有基线，并给出 Oracle（GT 深度）上界。
4. **消融实验（表 4）**：验证数据清洗（SAM 过滤）和距离细化（约束矩阵）两个组件的贡献。
5. **不同预训练方法对比（表 5）**：与 SimCLR、CRL、Ego 2-MAP、ECL、SPA、3DP 等无监督视觉预训练方法对比，均集成到 FLoc 中。
6. **历史帧数影响分析（图 3）**：比较不同历史帧数下与 3DP 的性能。
7. **定性对比（图 4）**：展示先验/后验概率图，与 F³Loc 和 3DP 进行可视化对比。

### 充分性评估

- **覆盖广泛**：涵盖两个标准 benchmark（Gibson、Structured3D），单帧/多帧/自适应三种模式，多个准确率阈值，兼顾定量与定性评估。
- **消融较完整**：验证了数据清洗和距离细化的必要性，并对比了多种预训练方法以突出房间风格建模的优势。
- **公平性**：所有基线均不含语义标注；对比预训练方法时均以相同方式集成到 FLoc 框架中；遵循 F³Loc 的数据划分和实验协议。
- **整体评价**：实验设计较为充分、客观，能够有效支撑方法有效性的论证。跨数据集（从 Gibson 预训练到 Structured3D 泛化）增强了结论的可信度。

## 6. 论文的主要结论与发现

- 房间风格知识可以**有效缓解由重复或相似结构造成的 FLoc 定位歧义**。
- 在 Gibson(f)/(g) 上，Ours_s 相对 3DP_s 在四类指标上分别提升最高 5.5%（R@1m）、5.2%（1m 30°）；Ours_f 达到最优性能，R@0.1m 提升 0.5%、R@1m 提升 1.7%。
- 在 Gibson(t) 长序列轨迹跟踪中，Ours_s 的 R@0.2 m 较 3DP_s 大幅提升 **13.5%**，RMSE 也显著降低（RMSE(S) 0.16→0.13，RMSE(A) 0.75→0.51）。
- 在 Structured3D (full) 上，Ours_s 在 R@1m 上较 3DP_s 提升 1.4%，表明房间风格知识可以跨数据域迁移。
- 消融与对比实验证实：数据清洗和距离矩阵细化对性能均有贡献；相比纯 RGB 对比学习和 2D/3D 跨模态预训练，房间风格知识的场景上下文建模具有优势。

## 7. 优点

- **创新性**：首次系统性地将房间风格知识（场景上下文）引入视觉 FLoc，以消除定位歧义，视角新颖且合理。
- **无监督方案**：提出基于聚类约束的无监督学习，无需房间标注，降低了对人工标注的依赖。
- **自动化数据收集**：基于现有数据集构建自动采集管线，并使用 SAM 清洗数据，流程可复制、拓展性强。
- **通用性与可集性**：方法基于 F³Loc 框架，可平滑集成到单帧/多帧/自适应多种 FLoc 变体，且预训练编码器可迁移至其他任务。
- **实验充分且效果显著**：在两个标准 benchmark 上进行大量对比，多个指标显著超越 SoTA；消融和预训练方法对比增强了论证的严谨性。
- **可复现性**：提供代码开源地址（GitHub），有助于社区验证与后续研究。

## 8. 不足与局限

- **预训练数据源有限**：房间风格预训练数据仅来自 Gibson 训练集，虽然通过 Structured3D 验证了迁移性，但房间风格的多样性可能仍不足以覆盖现实世界的全部场景（如医疗建筑、工业厂房等特殊场所）。
- **房间风格先验的鲁棒性问题**：当房间无显著风格差异（如标准化的办公区、实验室），或图像中包含大量非典型家具/遮挡时，房间判别器的区分能力可能受限——文中未对此类边界场景展开专门分析或实验。
- **对比范围有待扩展**：虽然对比了多种无监督预训练方法，但未与使用真实房间类别监督的预训练方法进行上界对比；也未对比语义标注方法（文章虽声明不使用，但未量化说明与语义方法间的差距）。
- **多帧实验覆盖不均衡**：在 Gibson(t) 和 Structured3D 上仅报告了单帧方法的结果，多帧/自适应方法在长序列和跨数据集上的表现未充分展示，一定程度上限制了论证的全面性。
- **超参数依赖**：损失平衡系数 γ 和约束矩阵中的人工规则依赖经验设定，λ 虽设为可学习参数但其他规则（如难度阈值界定和赋值）的主观性较强，迁移到新数据集时可能需要重新调整。
- **尚未统一几何与场景上下文**：论文作者在结论中明确承认，当前工作强调房间风格知识的作用，并非否定几何线索的重要性；将 3D 几何先验与场景上下文统一在一个框架中仍是未来方向，可视为当前方法在信息利用上的一个局限。
- **算力与实施细节披露**：文中仅提及使用了 4 块 NVIDIA 3090 GPU，未说明具体训练时长（小时数）、预训练数据量规模等，不利于复现成本和能耗评估。

（完）
