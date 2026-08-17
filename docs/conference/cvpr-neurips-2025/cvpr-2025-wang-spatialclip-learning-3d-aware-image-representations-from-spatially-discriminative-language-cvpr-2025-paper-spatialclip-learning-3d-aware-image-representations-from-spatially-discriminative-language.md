---
title: "SpatialCLIP: Learning 3D-aware Image Representations from Spatially Discriminative Language"
title_zh: SpatialCLIP：从空间判别语言学习三维感知图像表征
authors: "Wang, Zehan, Zhou, Sashuai, He, Shaoxuan, Huang, Haifeng, Yang, Lihe, Zhang, Ziang, Cheng, Xize, Ji, Shengpeng, Jin, Tao, Zhao, Hengshuang, Zhao, Zhou"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_SpatialCLIP_Learning_3D-aware_Image_Representations_from_Spatially_Discriminative_Language_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 5.0
evidence: 利用空间判别语言学习三维感知图像表征，增强空间理解，对语言引导导航有支撑作用
tldr: 针对CLIP对图像空间概念理解不足的问题，提出SpatialCLIP：设计三维启发的ViT并将图像token提升至三维空间，同时改进语言监督使用空间判别性描述，从而更好捕获图像中的三维空间关系。该方法可作为空间感知表征器，为依赖空间语义的视觉语言导航等具身任务提供更可靠的视觉编码。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1789, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1753, \"height\": 1123, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 741, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 451, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 451, \"height\": 331, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1753, \"height\": 1123, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1680, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1806, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1573, \"height\": 442, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-spatialclip-learning-3d-aware-image-representations-from-spatially-discriminative-language-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 867, \"height\": 302, \"label\": \"Table\"}]"
motivation: CLIP缺乏对图像中空间概念的理解，限制了具身智能系统的空间智能。
method: 采用三维启发式ViT替换标准ViT，结合空间判别语言监督，提升对三维空间关系的编码能力。
result: 在空间理解相关评估上显示相比标准CLIP更强的三维空间感知能力。
conclusion: 三维感知的图像语言预训练可增强视觉编码的空间智能，支持后续具身导航应用。
---

## Abstract
Contrastive Language-Image Pre-training (CLIP) learns robust visual models through language supervision, making it a crucial visual encoding technique for various applications. However, CLIP struggles with comprehending spatial concepts in images, potentially restricting the spatial intelligence of CLIP-based AI systems. In this work, we propose SpatialCLIP, an enhanced version of CLIP with better spatial understanding capabilities. To capture the intricate 3D spatial relationships in images, we improve both "visual model" and "language supervision" of CLIP. Specifically, we design 3D-inspired ViT to replace the standard ViT in CLIP. By lifting 2D image tokens into 3D space and incorporating design insights from point cloud networks, our visual model gains greater potential for spatial perception. Meanwhile, captions with accurate and detailed spatial information are very rare. To explore better language supervision for spatial understanding, we re-caption images and perturb their spatial phrases as negative descriptions, which compels the visual model to seek spatial cues to distinguish these hard negative captions. With the enhanced visual model, we introduce SpatialLLaVA, following the same LLaVA-1.5 training protocol, to investigate the importance of visual representations for MLLM's spatial intelligence. Furthermore, we create SpatialBench, a benchmark specifically designed to evaluate CLIP and MLLM in spatial reasoning. SpatialCLIP and SpatialLLaVA achieve substantial performance improvements, demonstrating stronger capabilities in spatial perception and reasoning, while maintaining comparable results on general-purpose benchmarks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与研究动机

- **核心痛点**：CLIP 虽然通过语言监督学习到了鲁棒的视觉表征，但对图像中的**空间概念**（如"在后面""在左边""更靠近相机""更大"等）理解能力显著不足。
- **关键证据（图 1）** ：论文通过扰动实验证明，当把正确描述中的**物体类别**或**属性**替换为错误内容时，CLIP 的图像-文本相似度分数会明显下降；然而将**空间短语**替换为错误描述时，CLIP 不仅无法识别错误，甚至会给错误空间描述**更高的匹配分数**（例如 "The darker-haired cat is behind the white cat" 得 22.28 分，而错误的空间描述 "to the right of" 反而得 23.66 分）。
- **深层影响**：空间智能是视觉感知的关键维度。CLIP 作为众多视觉系统（开放世界识别、多模态大语言模型 MLLM、具身智能等）的基础视觉编码器，其空间理解缺陷会向这些下游系统传导，限制 AI 对真实世界环境的理解与交互能力。
- **研究空白**：已有工作（如 SpatialVLM、SpatialRGPT、Cube-LLM）主要通过**扩充训练数据**来增强 MLLM 的空间能力，却忽视了**视觉表征本身**对空间智能的制约作用。本文从"视觉模型 + 语言监督"双管齐下，开辟了提升空间理解的新路径。

## 二、方法论

### 1. 总体框架
SpatialCLIP 从两个维度增强标准 CLIP：
- **视觉模型**：提出 **3D-Inspired ViT**，将 2D 图像 token 提升至 3D 空间，融入点云网络的设计思想；
- **语言监督**：提出 **Recaption & Perturbation** 策略，利用重标注 + 空间短语扰动生成"硬负样本"描述，迫使模型关注空间线索。

### 2. 3D-Inspired ViT（视觉模型）

**核心思想**：借助单目深度估计（Depth Anything v2）获取深度图，将 RGB 图像的 2D token 映射到 3D 体素空间中，从而在 3D 视角下建模物体间的空间关系。

**关键技术细节**：
- **输入**：RGB-D 四通道输入（RGB + 预测深度），相比标准 ViT 的纯 RGB 输入增加深度维度。
- **Token 提升（Lifting）** ：对每个 Transformer 层，输入 2D token 图 ZL ∈ R^{Hz×Wz×C}，根据每个 patch 的平均深度值将其映射为 3D 体素 Z³D_L ∈ R^{Hz×Wz×Dz×C}（体素网格高度稀疏）。
- **3D 深度可分离卷积**：借鉴点云网络结构，在每层 Transformer block 中植入 3D 卷积，通过残差连接融入原有特征，公式为：

  ZL = ZL + Compress(3D-Conv(Z³D_L))

  其中 Compress(·) 将稀疏 3D 体素压缩回 2D token 图。

- **3D 相对位置编码（3D RPE）** ：在自注意力计算中引入基于 3D 相对空间位置的偏置项：

  aij = (ziWQ)(zjWK)ᵀ + bij / √C

  其中 bij 从可学习的偏置矩阵 B ∈ R^{(2Hz−1)×(2Wz−1)×(2Dz−1)} 中按 3D 相对位置索引选取。

- **参数开销**：新引入的 3D CNN 与 3D RPE 均零初始化，仅新增约 1M 参数；深度估计模型额外引入 24.8M 参数。

### 3. 语言监督：Recaption & Perturbation

**动机**：现有 CLIP 训练数据（CC-12M、LAION 等）的图文标注大多只含简单全局摘要，缺乏准确的空间细节描述；而 MLLM 本身空间感知能力有限，直接生成的密集描述也难以完全准确。

**方法流程**：
- **重标注（Recaption）** ：使用 LLaVA-1.5-13B、CoCa 和 ShareGPT4V 三种模型对图像（SA1B 数据集）进行密集重标注，获得信息更丰富、语义对齐更好的空间描述。
- **空间短语扰动（Perturbation）** ：通过预设模板，将描述中的空间关系短语随机替换为其反义词，例如 "two cats are standing in front of a table, while the left cat is bigger than the right one" 被扰动为 "two cats are standing under a table, while the upper cat is smaller than the lower one"。扰动后的描述与原始描述在物体类别和属性上一致，仅在空间关系上完全错误，从而构成**硬负样本**。

**训练目标**（公式 3）：

L = −1/N Σᵢ [ log( e^(tᵢ·vᵢ/τ) / Σⱼ e^(tᵢ·vⱼ/τ) ) + log( e^(tᵢ·vᵢ/τ) / Σⱼ ( e^(tⱼ·vᵢ/τ) + e^(t̃ⱼ·vᵢ/τ) ) ) ]

其中 vᵢ 为第 i 张图像的视觉表征，tᵢ 为原始描述，t̃ᵢ 为扰动描述，τ = 0.01。

### 4. SpatialLLaVA

- 以 LLaVA-1.5 为框架，将其中标准的 OpenAI CLIP 视觉编码器替换为 SpatialCLIP-L（基于 CLIP-L/14@336px）。
- **完全遵循 LLaVA-1.5 两阶段训练协议**（相同的数据集、超参数），确保公平系统性对比，从而单独检验视觉表征对 MLLM 空间智能的贡献。

### 5. SpatialBench（新基准）

- **任务形式**：caption matching（标题匹配）。每张图提供 2~4 个人工撰写的描述，其中仅 1 个准确，其余为干扰项。
- **数据构成**：
  - 室外场景：COCO 验证集 + 互联网图片，共 159 张；
  - 室内场景：ScanNet，共 140 张。
- **评估对象**：可同时评估 CLIP（取最高匹配分数）与 MLLM（以多选问答形式）。

## 三、实验设计

### 1. 训练设置
- **训练数据**：SA1B（Segment Anything 1B）数据集（多数图像含多物体、空间关系复杂）。
- **重标注来源**：LLaVA-1.5-13B、CoCa、ShareGPT4V（三种标题随机混合使用）。
- **优化器**：AdamW；预训练 CLIP 编码器学习率 2e-7，新引入组件学习率 4e-6；训练 8,000 步，batch size 2,048。

### 2. CLIP 评估（表 1）
- **空间聚焦基准**：SpatialBench（Outdoor/Indoor）、BLINK 的 spatial relation 子集（改为 caption matching 任务）。
- **通用基准**：COCO、Flickr30K 零样本图文检索。
- **对比方法**：OpenAI CLIP-B/16@224px、OpenAI CLIP-L/14@336px。

### 3. MLLM 评估（表 2、表 3）
- **空间聚焦基准**：SpatialBench、BLINK、CV-Bench 3D（含 Depth/Corres/Jigsaw/Distance 等子任务）。
- **通用基准**：POPE（物体幻觉）、MM-Vet、VQAv2、GQA、RealWorldQA。
- **对比方法**：
  - 使用空间数据训练的专门模型：Spatial-RGPT-7B；
  - 使用更广泛通用数据训练的更强大模型：LLaVA-1.6-7B/13B、LLaVA-interleave-7B；
  - 同协议基线：LLaVA-1.5-7B。

### 4. 消融实验（表 4、表 5）
- **组件消融**（表 4，6 组）：逐步添加 recaption、3D CNN、3D RPE、caption perturbation。
- **深度融合方式对比**（表 5，4 组）：early fusion、late fusion、3D-Inspired ViT。

## 四、资源与算力

- 论文明确提到：训练在 **8 张 A100 GPU** 上进行，batch size 为 2,048，训练 **8,000 步**。
- 采用预训练的 Depth Anything v2 ViT-Small 作为单目深度估计模型（新增 24.8M 参数）。
- 但论文**未明确说明**总训练时长（小时数）、单卡显存占用、训练吞吐量等细节。

## 五、实验数量与充分性

### 实验规模
- **CLIP 层面**：2 个模型规模（B/L）× 4 类基准（SpatialBench、BLINK、COCO、Flickr30K）+ 6 组消融 + 4 组深度融合对比。
- **MLLM 层面**：7 个模型对比 × 多个空间/通用基准（表 2 涉及 7 个空间指标，表 3 涉及 5 个通用指标）。
- 另有大量定性可视化对比（图 2、图 4）。

### 充分性与公平性分析
- **优点**：SpatialLLaVA 与 LLaVA-1.5 使用完全相同的训练协议和数据，能干净地归因视觉表征的贡献；消融实验覆盖每个新组件；深度融合消融排除替代方案。
- **需注意的点**：
  - 与 Spatial-RGPT、LLaVA-1.6 等的对比属于"不公平"对比（对方使用更多或专门数据），论文也如实声明了这一点；
  - 消融实验仅在 SpatialCLIP-B 上进行，未在 L 规模上验证；
  - MLLM 通用基准中 GQA 分数反而略有下降（60.6 vs 62.0），说明空间增强并非完全无代价。

## 六、主要结论与发现

1. **SpatialCLIP 显著提升空间理解**：在 SpatialBench 上，SpatialCLIP-B 室外准确率从 35.22 提升至 41.51，室内从 31.43 提升至 34.28；BLINK Spatial 上从 51.05 提升至 57.34。
2. **空间能力与模型规模并非正相关**：OpenAI CLIP-L 的空间表现（32.07/30.00）反而不如 CLIP-B（35.22/31.43），说明现有预训练范式下单纯扩大参数无法解决空间理解缺陷，突显了针对性设计（而非扩大规模）的价值。
3. **通用能力同步受益**：重标注数据的信息密度使 SpatialCLIP 在 COCO/Flickr30K 零样本检索上也有大幅提升（如 R@1 从 34.40 提升到 38.86）。
4. **SpatialLLaVA 验证表征价值**：在相同训练协议下，仅替换视觉编码器即使 MLLM 在空间基准上大幅超越 LLaVA-1.5（室外 40.25 vs 29.55，室内 40.17 vs 32.47），并保持通用能力基本持平。
5. **各组件均有效**：3D CNN、3D RPE、caption perturbation 各自带来增益，叠加效果最佳；3D-Inspired ViT 显著优于 early/late fusion 等替代深度融合方案。

## 七、优点与亮点

1. **视角新颖**：不同于已有工作通过"加数据"提升空间智能，本文从**视觉表征本身**切入，并在相同数据/训练协议下证明了表征的独立价值，对社区有方法论启示。
2. **双管齐下**：视觉模型和语言监督同时改进，且两方面的设计相互呼应（3D 视觉结构 + 空间判别性语言），形成完整的解决方案。
3. **硬负样本设计巧妙**：对空间短语做反义扰动，构造类别和属性一致、仅空间关系错误的负样本，精准逼促使模型捕捉空间线索，且巧妙绕开了"MLLM 自身空间标注不准"的鸡生蛋问题。
4.

### 4. 优点与亮点（续）

4. **训练高效、资源友好**：整个训练仅需 8 张 A100、8,000 步、batch size 2,048，新增参数仅约 1M（深度模型 24.8M 参数为预训练固定权重），相比从零训练或大规模全量微调，成本极低，且能获得显著空间能力提升，具备较强的工程可复现性。
5. **基准设计具有通用性**：SpatialBench 采用 caption matching 形式，既能评估 CLIP 类表征模型的排序能力，又能以多选问答形式评估 MLLM，为后续空间理解研究提供了统一、轻量的评测工具。
6. **可视化与分析详实**：图 2、图 4 等定性结果直观展示了 SpatialCLIP/SpatialLLaVA 对空间短语（如“在后面”“在左边”）的响应变化，有助于理解模型行为改进的内在机制。

## 八、缺点与局限性

1. **依赖深度估计的准确性**：3D-Inspired ViT 依赖单目深度估计器（Depth Anything v2）输出的伪深度。深度预测存在误差时（尤其边缘、遮挡、透明物体等场景），3D 体素化过程可能引入噪声，从而限制空间感知的上限。论文未分析深度误差对结果的具体影响。
2. **空间扰动仅覆盖有限类型**：重标注的扰动集中在一组预设的空间关系模板（位置、大小等），对更复杂的空间语义（如“穿过”“环绕”“在…之间”的细微差异）覆盖不足；扰动生成依赖规则模板，缺乏对自然语言多样性的建模。
3. **消融规模有限**：消融实验只在 CLIP-B/16 上进行，没有在 L/14 上验证各设计组件的可扩展性与稳定性；MLLM 实验仅使用 L 模型，未测试在更大视觉骨干上的组合效果。
4. **通用基准存在轻微退化**：在 MLLM 评估中，SpatialLLaVA 在 GQA 上较 LLaVA-1.5 下降 1.4 分（60.6 vs 62.0），说明空间增强可能以牺牲部分复杂场景理解为代价，论文未深入分析退化原因与缓解方法。
5. **与强基线对比的公平性问题**：SpatialLLaVA 与 Spatial-RGPT、LLaVA-1.6 等模型的对比并非同协议，后者使用了更多或专门的空间训练数据。虽然论文明确声明，但仍使结论的说服力稍打折扣。
6. **对 MLLM 的验证仅基于 LLaVA 框架**：SpatialLLaVA 只验证了 LLaVA-1.5 一种架构，未覆盖其他流行 MLLM 架构（如 Qwen-VL、InternVL 等），视觉表征改进的泛化性尚待进一步证明。
7. **未涉及细粒度空间推理的深层测试**：SpatialBench 的 caption matching 属于选择性判断，未覆盖复杂的开放式空间问答（如“家具距离墙多少米”“从相机出发到目标的路径”等），缺少对空间推理深度（而非仅仅识别）的评估。

## 九、与相关方法的对比总结

| 方法 | 提升空间智能的途径 | 是否需要专门空间训练数据 | 是否改进视觉表征 | 代表性结果 |
|------|------------------|--------------------------|------------------|------------|
| SpatialVLM | 数据生成 + 空间问答 | 是 | 否 | MLLM 空间问答 |
| SpatialRGPT | 深度信息注入 + 数据增强 | 是 | 部分（深度分支） | SpatialRGPT-7B 空间问答 |
| Cube-LLM | 3D 信息注入 MLLM | 是 | 部分（3D token） | 3D 空间推理 |
| **SpatialCLIP (本文)** | **3D 视觉表征 + 语言硬负样本** | **否（使用通用 SA1B 重标注）** | **是（3D-Inspired ViT）** | CLIP/MLLM 空间基准大幅提升 |

本文的核心差异在于：不依赖人工标注的空间数据，而是通过“深度引导的 3D 视觉结构 + 自动重标注与扰动生成的空间硬负样本”来强化视觉编码器本身，因而能够直接替换现成 MLLM 中的 CLIP 编码器即可提升空间智能。

## 十、未来研究方向

1. **更鲁棒的深度估计与 3D 建模**：引入多目深度或学习型深度校正模块，降低对单目深度误差的敏感度；或探索无需显式深度图的隐式 3D 感知。
2. **扩展空间语义扰动覆盖**：利用大语言模型自动生成多样化空间关系反义扰动，而非依赖手工模板，以覆盖更丰富的空间表达。
3. **将 3D-Inspired ViT 推广到更多视觉骨干与 MLLM 架构**：在 ViT-H/giant 以及更多多模态模型上验证可扩展性，探索空间表征与其他能力（细粒度识别、视觉常识）的协同。
4. **分析空间增强对通用能力的影响机制**：针对 GQA 等基准的轻微退化进行归因，并提出联合优化策略以彻底消除负面影响。
5. **构建更全面的空间评测体系**：将 SpatialBench 扩展至三维空间、时间动态空间关系（视频）及开放式生成评估，从而更全面地覆盖空间智能的各个维度。

## 十一、总结与个人评价

SpatialCLIP 是一篇聚焦视觉基础模型空间理解缺陷的针对性工作。其核心贡献在于：以单目深度估计为桥梁，将 2D 视觉 token 提升至 3D 空间，并结合“重标注 + 空间扰动”构造高质量硬负样本，使 CLIP 类模型获得显式空间感知能力；并通过在相同训练协议下替换 MLLM 视觉编码器，令人信服地证明了视觉表征改进对空间智能的独立价值。

方法的创新性体现在**视觉结构与语言监督的双向协同**，而非单纯堆叠数据或参数。其低训练成本、模块化设计以及公开基准的构建，均有利于社区复现和后续拓展。不过，深度估计误差的隐性依赖、扰动模板覆盖有限以及消融规模较小等问题，仍限制了结论的普适性。总体而言，本文为提升视觉基础模型的空间理解开辟了新的、可行的技术路线，具有较高的学术价值与工程参考意义。

（完）
