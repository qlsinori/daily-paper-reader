---
title: "ReasonGrounder: LVLM-Guided Hierarchical Feature Splatting for Open-Vocabulary 3D Visual Grounding and Reasoning"
title_zh: ReasonGrounder：LVLM引导的分层特征拼接用于开放词汇3D视觉定位与推理
authors: "Liu, Zhenyang, Wang, Yikai, Zheng, Sixiao, Pan, Tongying, Liang, Longfei, Fu, Yanwei, Xue, Xiangyang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_ReasonGrounder_LVLM-Guided_Hierarchical_Feature_Splatting_for_Open-Vocabulary_3D_Visual_Grounding_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: ReasonGrounder根据语言描述实现开放词汇3D定位，是视觉语言导航的核心能力
tldr: 开放词汇3D视觉定位与推理旨在根据自然语言描述在场景中定位物体，是视觉语言导航和自主机器人的关键能力。现有方法依赖3D标注和掩码微调，难以处理多样语义和常识推理。ReasonGrounder借助LVLM引导的分层3D特征高斯场，按物理尺度自适应分组，实现开放词汇的3D定位与推理，在定位被遮挡物体和复杂语言指令上取得显著效果，为具身导航提供可靠支持。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 851, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1758, \"height\": 923, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1603, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1610, \"height\": 1037, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1775, \"height\": 403, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 896, \"height\": 462, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 841, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 846, \"height\": 758, \"label\": \"Table\"}]"
motivation: 开放词汇3D视觉定位依赖3D标注和掩码微调，难以处理多样语义和常识推理，限制导航应用。
method: 提出ReasonGrounder，利用LVLM引导的分层3D特征高斯场，按物理尺度分组实现无需掩码的开放词汇定位。
result: 在3D视觉定位基准上验证了ReasonGrounder对被遮挡物体和隐式描述的定位能力，性能优于现有方法。
conclusion: 为视觉语言导航与自主机器人提供了可泛化的开放词汇3D定位框架。
---

## Abstract
Open-vocabulary 3D visual grounding and reasoning aim to localize objects in a scene based on implicit language descriptions, even when they are occluded. This ability is crucial for tasks such as vision-language navigation and autonomous robotics. However, current methods struggle because they rely heavily on fine-tuning with 3D annotations and mask proposals, which limits their ability to handle diverse semantics and common knowledge required for effective reasoning. To address this, we propose ReasonGrounder, an LVLM-guided framework that uses hierarchical 3D feature Gaussian fields for adaptive grouping based on physical scale, enabling open-vocabulary 3D grounding and reasoning. ReasonGrounder interprets implicit instructions using large vision-language models (LVLM) and localizes occluded objects through 3D Gaussian splatting. By incorporating 2D segmentation masks from the Segment Anything Model (SAM) and multi-view CLIP embeddings, ReasonGrounder selects Gaussian groups based on object scale, enabling accurate localization through both explicit and implicit language understanding, even in novel, occluded views. We also contribute ReasoningGD, a new dataset containing over 10K scenes and 2 million annotations for evaluating open-vocabulary 3D grounding and amodal perception under occlusion. Experiments show that ReasonGrounder significantly improves 3D grounding accuracy in real-world scenarios.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- 论文聚焦于 **开放词汇 3D 视觉定位与推理（Open-vocabulary 3D Visual Grounding and Reasoning）**：给定自然语言描述，在 3D 场景中定位目标物体，且要理解**隐含、间接、复杂的语言指令**，并能在目标物体**被部分或完全遮挡**时实现定位。
- 该能力是视觉语言导航、自主机器人、增强现实等应用的关键基础，因为这些场景中视觉数据往往不完整，语言指令也常是模糊或间接的。
- 现有 3D 视觉定位方法存在明显局限：
  - 大量依赖 3D 标注（如 bounding boxes、mask proposals）进行微调，泛化能力差；
  - 对开放词汇、常识推理和隐含语义的理解不足；
  - 难以处理遮挡场景下的目标定位，尤其是新视角下的“完整物体感知”；
  - 基于 NeRF/LangSplat 等方法通常只支持显式提示，对自然语言中的歧义和推理能力有限。
- 为此，论文提出 **ReasonGrounder**：一种 LVLM 引导的分层 3D 特征高斯场方法，实现无需 3D 标注、支持隐式指令理解、具备“amodal perception”的开放词汇 3D 定位与推理，并构建了新数据集 **ReasoningGD** 以支撑相关评测。

## 2. 提出的方法论

### 2.1 核心思想

- 使用 **3D Gaussian Splatting (3DGS)** 作为场景表示，并给每个 3D 高斯附加潜在特征向量。
- 通过两套 MLP 映射得到**分层语言特征**和**分层实例特征**：
  - 语言特征由 CLIP 嵌入监督，确保多视角一致性；
  - 实例特征通过对比学习和 3D 物理尺度监督，支持不同粒度的高斯分组。
- 引入 **LVLM（大型视觉语言模型）** 解析隐含指令，推理目标物体；再借助 CLIP 选择与推理结果最匹配的参考视角。
- 根据目标物体的 3D 尺度对高斯进行分组，选择与目标最相关的高斯组，实现精确 3D 定位，并能在新视角中渲染完整物体（即便被遮挡）。

### 2.2 关键技术细节

1. **训练监督生成**：
   - 先用 SAM 生成 2D 分割掩码，过滤并去重得到掩码候选集；
   - 利用已训练的 3DGS 渲染深度，计算每个掩码对应 3D 点的标准差，从而得到物理尺度；
   - 对每个掩码区域提取 CLIP 特征，形成 `(掩码, CLIP特征, 物理尺度)` 三元组。

2. **分层语言特征**：
   - 对 CLIP 特征做 PCA 压缩，降低高斯存储开销；
   - 语言映射器 `F_l` 以物理尺度 `s_i` 和高斯潜在特征 `f_gi` 为输入，输出分层语言特征：
     `φ_sgi = F_l(s_i, f_gi)`
   - 使用 Huber 损失监督渲染后的语言特征与压缩 CLIP 特征。

3. **分层实例特征**：
   - 实例映射器 `F_g` 同样以 `(s_i, f_gi)` 为输入，输出实例嵌入；
   - 利用 GARField 启发的对比损失：同一掩码内的像素实例特征应相近，不同掩码的实例特征应远离；
   - 该机制支持在场景中形成多层级高斯分组，有利于不同大小物体的定位。

4. **LVLM 引导的参考视角选择**：
   - 输入顶视图和隐含查询 `Q_im`，LVLM 推理出目标物体 `O_t` 和解释 `E`；
   - 通过 CLIP 图像-文本相似度，从训练视角中选出与目标物体最一致的参考视角 `V̂`。

5. **分层高斯分组与物体定位**：
   - 计算目标物体的 CLIP 嵌入与参考视角中渲染语言特征的相关性分数；
   - 根据相关性选择最匹配的物理尺度 `s_i*`；
   - 在选定尺度下用 `F_g` 生成分层实例特征，并利用 **HDBSCAN** 对高斯进行聚类；
   - 选取相关性最高像素的实例特征作为参考特征，在聚类中心中找到最匹配的高斯组；
   - 最终通过 alpha blending 渲染该高斯组，即可在新视角中实现“amodal perception”。

### 2.3 公式与算法流程

- 3D 高斯定义：`G(x) = exp(-0.5 (x-μ)^T Σ^-1 (x-μ))`
- 颜色渲染沿用 3DGS 的 tile-based rasterization：
  `C = Σ_i c_i α_i ∏_{j=1}^{i-1}(1-α_j)`
- 特征渲染同样采用 alpha blending：
  `f̄_i = Σ_i f_gi α_i ∏_{j=1}^{i-1}(1-α_j)`
- 语言特征损失：`L_lang = L_δ(φ_si, φ̂_i)`
- 实例特征对比损失：同掩码拉近、异掩码推远，公式如 `Lin = ||ψ_m - ψ_n||`（同掩码）或 `ReLU(λ - ||ψ_m - ψ_n||)`（异掩码）。
- 参考视角选择：`V̂ = argmax cosine(CLIP_img(V_i), CLIP_text(O_t))`
- 高斯组选择：`Gi* = {Gi | Ti = argmax cosine(T̂, Tj)}`

整体流程可概括为：3DGS 场景训练 → SAM 掩码与尺度生成 → 分层特征高斯场训练 → LVLM 推理意图 → 参考视角选择 → 尺度选择 → HDBSCAN 高斯聚类 → 目标高斯组渲染定位。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **LERF 数据集**：13 个真实场景，包含 in-the-wild 和长尾场景，用于开放词汇 3D 定位与推理测试。
- **3D-OVS 数据集**：多组真实场景，主要用于开放集 3D 语义分割和开放词汇定位测试。
- **ReasoningGD 数据集（本文新提出）**：
  - 超过 10K 个场景；
  - 263 类常见物体；
  - 约 200 万条标注；
  - 每个场景含 100 张 RGB-D 图像、相机位姿、2D 可见掩码和 amodal 掩码（即遮挡部分也标注）；
  - 用于评估隐式指令下的 3D 定位、遮挡条件下的 amodal 感知。

### 3.2 对比方法

- 2D 方法：LSeg、ODISE、OV-Seg。
- 3D 方法：FFD、LERF、3D-OVS、LangSplat。
- 主要对比任务：开放词汇 3D 视觉定位的 localization accuracy 和 mIoU。

### 3.3 主要实验设置

- LERF 上对比 localization accuracy 和 mIoU；
- 3D-OVS 上对比 mIoU；
- 在 LERF、3D-OVS、ReasoningGD 上测试**隐式指令 3D 定位**（例如 "Which object can hold coffee?"）；
- 在 ReasoningGD 上测试**amodal perception**（新视角下物体被遮挡时的完整定位）；
- 另选 5 个复杂挑战场景进行鲁棒性测试；
- 在 Figurines 场景和 ReasoningGD 001 场景上做消融实验。

## 4. 资源与算力

- 论文在“Implementation Details”中提到：
  - 使用 OpenCLIP ViT-B/16 提取语言特征；
  - SAM 使用 ViT-H；
  - 3DGS 训练 30,000 次迭代；
  - 分层特征高斯场固定 3DGS 参数，只训练潜在特征和两个 MLP，共 10,000 次迭代；
  - LVLM 使用 LLaVA 1.5；
  - 模型在 **NVIDIA RTX-3090 GPU** 和 **14 vCPU Intel Xeon Gold 6330 CPU @ 2.00GHz** 上训练；
  - 消融实验在 **NVIDIA H100 GPU** 上完成。
- 但论文**未明确说明**具体 GPU 数量、总训练时长、单场景训练耗时等详细信息，因此算力总成本无法从文中精确判断。

## 5. 实验数量与充分性

- 实验数量较为丰富：
  - 在 3 个数据集上做了开放词汇定位评测；
  - 包含显式查询和隐式指令两类任务；
  - 包含定性可视化结果和定量指标；
  - 包含标准定位对比、隐式推理定位、amodal 新视角感知、挑战场景鲁棒性测试；
  - 包含消融实验（有无 3DGS、有无 SHF、有无 LVLM、是否支持 amodal）。
- 总体来看，实验**覆盖了方法的各个核心卖点**：开放词汇、隐式指令推理、遮挡下定位、novel view amodal 感知，并与多个 SOTA 方法对比。
- 但也有一些充分性上的不足：
  - ReasoningGD 虽宣称 10K+ 场景，但定量实验仅选取了其中 5 个场景（001–005）的样本，未展示全数据集的整体性能；
  - 论文未报告多次重复实验的方差或统计显著性检验，结果可能存在一定偏差；
  - 消融主要在两个场景上进行，规模较小；
  - 未在真实机器人或视觉语言导航系统上做端到端应用验证。  
- 总体而言，实验设计相对系统、对比方法合理，但**全数据集评测和统计分析仍不够完整**。

## 6. 主要结论与发现

- ReasonGrounder 在开放词汇 3D 视觉定位上优于现有方法：
  - LERF 数据集 localization accuracy 达到 86.7%，mIoU 达到 55.1%；
  - 3D-OVS 数据集 mIoU 达 94.7%，超过 LangSplat 等此前 SOTA。
- 在隐式指令推理任务中，ReasonGrounder 能准确理解类似“Which object can hold coffee?”的间接描述，并定位到正确目标。
- 在遮挡场景中，ReasonGrounder 通过分层高斯分组实现了新视角下的 amodal 感知，即使物体被部分或完全遮挡，也能渲染和定位完整物体。
- 消融实验表明：
  - 3DGS 替代 NeRF 能提升效率与精度；
  - LVLM 的引入对于隐式指令理解至关重要；
  - 分层特征高斯场（SHF）是支持 amodal 感知和精确分组的关键模块。
- 作者还构建了 ReasoningGD 数据集，提供大规模场景和约 200 万标注，为开放词汇 3D 定位与遮挡感知研究提供了新评测资源。

## 7. 优点

- **方法设计有新意**：将 3DGS、层级特征、物理尺度、LVLM 推理结合，形成统一框架，兼顾定位精度和推理能力。
- **支持隐式语言指令**：不同于 LERF/LangSplat 只处理显式文本，ReasonGrounder 能借助 LVLM 进行常识推理和目标意图解析。
- **分层高斯分组机制**：基于物理尺度自适应分组，能够适应不同大小物体，并可借助 HDBSCAN 聚类完成完整的物体定位。
- **支持遮挡下的 amodal 感知**：通过高斯组渲染，即使物体在 novel view 中被遮挡，也能定位完整目标，这是很多既有方法不具备的能力。
- **不依赖 3D 检测器或 3D 标注**：训练过程中仅使用 2D 模型（SAM、CLIP）和已训练好的 3DGS 作为监督，提升了开放词汇泛化性。
- **数据集贡献**：ReasoningGD 规模大、包含 amodal 掩码，弥补了现有评测数据在“3D 推理 + 遮挡 amodal 感知”方面的不足。
- 实验对比了 2D 和 3D 的多种 SOTA 方法，并给出定量与定性结果，较为可信。

## 8. 不足与局限

- **依赖 2D 基础模型质量**：SAM 的掩码质量和 CLIP 的语义粒度会直接影响 3D 特征场的学习，进而影响定位精度。
- **LVLM 和 CLIP 的固有偏差**：对隐含指令的解析依赖 LVLM 的常识与视觉能力，CLIP 对长尾或抽象概念可能不鲁棒。
- **遮挡评测主要依赖合成数据**：ReasoningGD 是 Blenderproc 生成，真实复杂场景中的遮挡表现仍需要进一步验证。
- **全数据集评测不足**：论文对 ReasoningGD 的定量评测只展示部分场景，缺少对 10K+ 场景的整体统计结果。
- **算力细节不透明**：未报告训练总时长、GPU 数量、显存占用等，难以准确评估实际部署成本。
- **无端到端应用验证**：论文未在真实机器人、导航系统或 AR 场景中验证该方法的实用性和实时性。
- **推理速度仍有提升空间**：虽然 3DGS 渲染较快，但 LVLM 推理、CLIP 检索、HDBSCAN 聚类等环节可能在真实系统中形成瓶颈。
- **缺少失败案例分析**：论文展示了成功案例，但对复杂、歧义或多目标场景下的失败模式缺少深入分析。

（完）
