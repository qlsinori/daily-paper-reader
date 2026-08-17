---
title: "SpatialCLIP: Learning 3D-aware Image Representations from Spatially Discriminative Language"
title_zh: SpatialCLIP：从空间判别性语言学习三维感知图像表征
authors: "Wang, Zehan, Zhou, Sashuai, He, Shaoxuan, Huang, Haifeng, Yang, Lihe, Zhang, Ziang, Cheng, Xize, Ji, Shengpeng, Jin, Tao, Zhao, Hengshuang, Zhao, Zhou"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_SpatialCLIP_Learning_3D-aware_Image_Representations_from_Spatially_Discriminative_Language_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 通过空间判别性语言增强CLIP的三维空间理解，有助于视觉语言导航感知
tldr: 针对CLIP难以理解图像中空间概念的问题，论文提出SpatialCLIP，在CLIP的视觉模型与语言监督两方面同时改进：设计三维感知ViT将二维图像词元提升到三维空间，并引入空间判别性语言约束。在空间理解相关评测上，SpatialCLIP显著提升了3D感知图像表征质量。该工作可作为视觉语言导航中视觉编码器的增强模块，有助于智能体对空间关系与指令的对应理解。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1789, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1753, \"height\": 1123, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 741, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 451, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 451, \"height\": 331, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1753, \"height\": 1123, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1680, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1806, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1573, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 867, \"height\": 302, \"label\": \"Table\"}]"
motivation: CLIP缺乏对图像中三维空间关系的把握，制约了其空间智能与在导航等任务中的应用。
method: 设计三维感知ViT替代标准ViT，将2D图像词元提升至3D空间，并结合点云网络设计思路与空间判别性语言监督。
result: 在空间理解评测中优于原CLIP，获得更强的三维感知图像表征。
conclusion: 表明空间判别性语言与三维归纳偏置能有效提升CLIP的空间能力，可服务于空间相关的具身任务。
---

## Abstract
Contrastive Language-Image Pre-training (CLIP) learns robust visual models through language supervision, making it a crucial visual encoding technique for various applications. However, CLIP struggles with comprehending spatial concepts in images, potentially restricting the spatial intelligence of CLIP-based AI systems. In this work, we propose SpatialCLIP, an enhanced version of CLIP with better spatial understanding capabilities. To capture the intricate 3D spatial relationships in images, we improve both "visual model" and "language supervision" of CLIP. Specifically, we design 3D-inspired ViT to replace the standard ViT in CLIP. By lifting 2D image tokens into 3D space and incorporating design insights from point cloud networks, our visual model gains greater potential for spatial perception. Meanwhile, captions with accurate and detailed spatial information are very rare. To explore better language supervision for spatial understanding, we re-caption images and perturb their spatial phrases as negative descriptions, which compels the visual model to seek spatial cues to distinguish these hard negative captions. With the enhanced visual model, we introduce SpatialLLaVA, following the same LLaVA-1.5 training protocol, to investigate the importance of visual representations for MLLM's spatial intelligence. Furthermore, we create SpatialBench, a benchmark specifically designed to evaluate CLIP and MLLM in spatial reasoning. SpatialCLIP and SpatialLLaVA achieve substantial performance improvements, demonstrating stronger capabilities in spatial perception and reasoning, while maintaining comparable results on general-purpose benchmarks.

---

## 论文详细总结（自动生成）

# SpatialCLIP：从空间判别性语言学习三维感知图像表征——论文总结

## 1. 核心问题与研究动机

CLIP 通过语言监督学习了强大的通用视觉表征，但其对图像中的空间关系（如"在……后面""在……前面""在……之下""更远""更大"等）理解能力很弱。论文通过实验发现，当把图像对应的正确描述中的**物体类别**或**属性**替换为错误内容时，CLIP 的图文匹配分数会显著下降；但将**空间短语**替换为错误描述时，CLIP 的分数反而可能升高（+0.43～+1.38），说明 CLIP 几乎无法区分错误的空间描述。这种空间智能的缺失会进一步制约基于 CLIP 构建的 MLLM 系统对真实三维世界的理解和推理能力。

因此，论文的核心目标是：**提升 CLIP 对图像中三维空间关系的感知能力**，同时保持其通用的视觉语言理解性能，并验证改进后的视觉表征能否增强多模态大模型（MLLM）的空间智能。

## 2. 方法论：双管齐下的改进

论文从 CLIP 的两大组成部分——"视觉模型"和"语言监督"——同时入手，提出 SpatialCLIP。

### 2.1 视觉模型：3D-Inspired ViT

- **输入升级**：将原先的 RGB 单模态输入换成 **RGB-D 输入**，利用轻量级单目深度估计模型（Depth Anything v2 ViT-Small）为每张训练图像预测深度图。
- **2D 词元提升到 3D**：在 ViT 的每个 transformer 层中，将二维词元图 Z_L ∈ R^(Hz×Wz×CL) 按其对应的平均深度值沿深度轴分配到三维体素网格 Z^3D_L ∈ R^(Hz×Wz×Dz×CL) 中。由于词元原本是 2D 的，形成的 3D 体素网格高度稀疏，可通过沿深度轴压缩再还原为 2D 词元图。
- **3D 卷积**：借鉴点云网络常用的三维深度可分离卷积，在三维体素上捕捉跨高度、宽度、深度三个维度的局部空间模式，并将结果残差加回原始 2D 词元：
  \[
  Z_L = Z_L + \text{Compress}(\text{3D-Conv}(Z^{3D}_L))
  \]
- **3D 相对位置编码**：在自注意力计算中引入可学习的 3D 相对位置偏置：
  \[
  a_{ij} = \frac{(z_i W_Q)(z_j W_K)^T + b_{ij}}{\sqrt{C}}
  \]
  其中 \(b_{ij}\) 从可学习偏置矩阵 \(B\in R^{(2H_z-1)\times(2W_z-1)\times(2D_z-1)}\) 中按两个词元在三维空间中的相对位置索引得到，使模型能显式感知词元间的三维相对空间关系。
- **参数效率**：新增的 3D 卷积与 3D 相对位置编码均零初始化，仅带来约 1M 额外参数；深度估计模型额外带来 24.8M 参数。

### 2.2 语言监督：Recaption & Perturbation

- **重述（Recaption）**：现有 CLIP 训练数据（如 CC-12M、LAION）的空间描述稀疏且质量差。论文使用多个先进 MLLM（LLaVA-1.5-13B、CoCa、ShareGPT4V）对 SA1B 数据集中的图像重新生成内容更丰富、语义更精细的描述。
- **扰动（Perturbation）**：由于 MLLM 本身空间理解有限，生成描述中的空间关系也可能不准确，论文采用模板将描述中的空间短语随机替换为其反义表达，构造"硬负样本"描述。例如将 "in front of the table" 改为 "under the table"，将 "left cat is bigger" 改为 "upper cat is smaller"。
- **对比学习目标**：将正确描述与扰动后的错误描述同时用于对比训练，迫使模型通过区分"部分正确"与"完全错误"的描述来捕捉空间线索。总损失为：
  \[
  L = -\frac{1}{N}\sum_{i=1}^{N}\left[\log\frac{e^{t_i\cdot v_i/\tau}}{\sum_{j=1}^N e^{t_i\cdot v_j/\tau}}+\log\frac{e^{t_i\cdot v_i/\tau}}{\sum_{j=1}^N(e^{t_j\cdot v_i/\tau}+e^{\tilde{t}_j\cdot v_i/\tau})}\right]
  \]
  其中 \(v_i\) 为图像表征，\(t_i\) 为正确描述表征，\(\tilde{t}_i\) 为扰动描述表征。

## 3. 实验设计

### 3.1 数据集与训练设置

- **训练数据**：SA1B 数据集（因其图像多对象、空间关系复杂）；用 LLaVA-1.5-13B、CoCa、ShareGPT4V 三种模型重述图像描述，训练时随机使用其中一种描述。
- **训练配置**：8 张 A100 GPU，batch size 2048，训练 8000 步；优化器为 AdamW，预训练 CLIP 部分学习率 2e-7，新引入组件学习率 4e-6；温度系数 \(\tau=0.01\)。
- **模型变体**：基于 OpenAI CLIP-B/16@224px 与 OpenAI CLIP-L/14@336px 训练，得到 SpatialCLIP-B 与 SpatialCLIP-L。
- **MLLM 实验**：将 LLaVA-1.5 的视觉编码器替换为 SpatialCLIP-L，保持 LLaVA-1.5 的两阶段训练策略、数据集和超参数不变，得到 SpatialLLaVA-7B。

### 3.2 评测基准

- **CLIP 评测**：
  - 空间聚焦：**SpatialBench**（论文自建，包含 159 张户外图 + 140 张室内图，每个图像配 2～4 个人工构造描述，采用 caption matching 任务）和修改后的 **BLINK** 空间关系子集。
  - 通用：**COCO** 与 **Flickr30K** 零样本图文检索。
- **MLLM 评测**：
  - 空间聚焦：SpatialBench、BLINK、**CV-Bench 3D**（深度、距离、空间等）。
  - 通用：**POPE**、**MM-Vet**、**VQAv2**、**GQA**、**RealWorldQA**。
- **对比方法**：
  - CLIP 赛道：OpenAI CLIP-B/224px、OpenAI CLIP-L/336px（作为基线）；早期融合（AlphaCLIP 风格）、晚期融合（SpatialRGPT 风格）作为深度通道集成策略的对照。
  - MLLM 赛道：LLaVA-1.5-7B（同协议基线）、SpatialRGPT-7B、LLaVA-1.6-7B/13B、LLaVA-Interleave-7B（后三者使用了更广的训练数据，属于"不公平"但仍有参照意义的强基线）。

## 4. 资源与算力

论文在实现细节中明确说明：**使用 8 张 A100 GPU，batch size 2048，训练 8000 步**。但未给出精确的训练时长（小时数）、总参数量浮点计算量等信息。深度估计模型采用轻量级 Depth Anything v2 ViT-Small（额外 24.8M 参数），新增的 3D 卷积和位置编码仅约 1M 参数，训练开销相对可控。

## 5. 实验数量与充分性

论文实验整体较为丰富，主要包括：

1. **主实验**：CLIP 赛道在 SpatialBench（OutDoor + InDoor）与 BLINK 上对比 B/L 两种规模；MLLM 赛道在 SpatialBench、BLINK、CV-Bench 3D 上与多种强基线对比。
2. **通用性能验证**：CLIP 在 COCO/Flickr30K 检索任务上；MLLM 在 POPE、MM-Vet、VQAv2、GQA、RealWorldQA 五个基准上。
3. **消融实验**（表 4，基于 SpatialCLIP-B）：
   - 逐步加入 recaption 微调、3D CNN、3D RPE、caption perturbation，共 6 行对比；
   - 验证了每个组件的独立贡献和组合增益。
4. **深度通道集成策略对比**（表 5）：Early Fusion、Late Fusion 与 3D-Inspired ViT 的比较。
5. **定性可视化**：多组 SpatialBench 与自由描述示例，直观对比 LLaVA-1.5 与 SpatialLLaVA。

**充分性评价**：实验设计比较系统，覆盖了空间聚焦与通用性能、CLIP 与 MLLM、定量与定性多个维度，消融齐全。但也存在一些局限：如训练数据只用 SA1B，未评估在不同数据源下的鲁棒性；MLLM 只基于 LLaVA-1.5 架构，未在其他 CLIP 基座（如 EVA-CLIP、SigLIP）上验证泛化性；SpatialBench 规模相对较小（共 299 张图），采样偏向可能与真实分布有差异。

## 6. 主要结论与发现

1. **SpatialCLIP 显著提升空间理解**：在 SpatialBench 上，SpatialCLIP-B 户外/室内分别为 41.51/34.28（原 CLIP 为 35.22/30.71），SpatialCLIP-L 户外/室内为 35.84/33.57（原为 32.07/30.00）；BLINK 空间准确率也大幅提高（B 变体 51.05→57.34，L 变体 47.55→57.34）。
2. **通用性能不降反升**：在 COCO/Flickr30K 检索上，SpatialCLIP 比原版有 6～9 个点的 R@1 提升，说明 recaption 数据与空间增强并未损害类别/属性识别。
3. **模型规模与空间能力弱相关**：原 CLIP-L 的空间成绩甚至低于 CLIP-B，说明单纯扩大参数无法弥补空间监督的缺失，必须依靠结构与数据层面的改进。
4. **SpatialLLaVA 受益于更好的视觉表征**：在相同训练数据与协议下，SpatialLLaVA-7B 相比 LLaVA-1.5-7B 在 SpatialBench 户外/室内上从 29.55/32.47 提升到 40.25/40.17，在 BLINK 上从 61.54 提升到 71.32，通用基准基本持平（如 VQAv2 78.5→79.9、POPE 85.9→86.5、MM-Vet 30.5→30.7），证明改进视觉编码是提升 MLLM 空间智能的有效途径。
5. **消融确认各组件有效性**：recaption 本身主要提升通用检索；3D CNN 与 3D RPE 各自提升空间感知，且组合效果更好；caption perturbation 进一步带来明显增益；3D-Inspired ViT 显著优于简单的 Early/Late 深度融合（后者有时甚至带来负收益）。

## 7. 优点

- **问题洞察准确**：通过精细的 CLIP 分数扰动实验，直观、定量地揭示了 CLIP 对空间语义的盲区，动机扎实。
- **结构设计有创新性**：将 RGB 图像词元按深度提升到三维体素，并引入点云网络中成熟的 3D 卷积和 3D 相对位置编码，实现了用 3D 归纳偏置增强 2D ViT 的新路径，且新增参数极少（约 1M）。
- **语言监督策略巧妙**：利用 MLLM 重述提升描述质量，再通过空间短语反义扰动构造硬负样本，解决了"MLLM 本身空间描述不准"的鸡生蛋问题。
- **验证深入**：同时评估 CLIP 与 MLLM 两层系统；在 MLLM 上严格控制了训练数据与协议，只替换视觉编码器，形成干净的因果比较。
- **通用性与空间性兼顾**：在多个通用基准上保持或提升性能，说明空间增强没有过拟合到空间任务。

## 8. 不足与局限

- **数据与规模局限**：训练仅使用 SA1B 一个数据集，且训练步数较短（8000 步），未展示在更大规模、更多样化数据（如 LAION）上的表现。
- **深度估计依赖**：推理时需要额外运行单目深度估计模型，带来额外计算开销与潜在误差；深度估计的错误可能传导到视觉表征。
- **基准规模偏小**：SpatialBench 仅 299 张图（户外 159、室内 140），每个样本候选描述 2~4 个，统计显著性有限。
- **MLLM 泛化验证不足**：仅在 LLaVA-1.5 架构上验证，未测试其他 MLLM 框架；未评估 SpatialCLIP 作为视觉编码器在其他任务（检测、分割、导航）中的迁移效果。
- **扰动模板依赖**：caption perturbation 依赖手工模板，覆盖的空间关系类型有限，可能未穷尽所有空间语义形式；对复杂逻辑关系（如"虽然 A 在 B 左，但 B 比 A 高"）的扰动效果未讨论。
- **消融中未见数据规模影响分析**：没有具体分析"训练数据量 vs 空间性能"的曲线，无法判断是否已达到数据饱和或需要更多数据才能进一步提升。

（完）
