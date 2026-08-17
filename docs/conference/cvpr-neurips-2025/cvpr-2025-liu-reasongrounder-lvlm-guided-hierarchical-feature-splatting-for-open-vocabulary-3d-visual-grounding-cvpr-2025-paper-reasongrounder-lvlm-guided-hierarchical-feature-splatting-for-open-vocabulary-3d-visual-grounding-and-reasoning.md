---
title: "ReasonGrounder: LVLM-Guided Hierarchical Feature Splatting for Open-Vocabulary 3D Visual Grounding and Reasoning"
title_zh: ReasonGrounder：LVLM引导的分层特征泼溅实现开放词汇3D视觉定位与推理
authors: "Liu, Zhenyang, Wang, Yikai, Zheng, Sixiao, Pan, Tongying, Liang, Longfei, Fu, Yanwei, Xue, Xiangyang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_ReasonGrounder_LVLM-Guided_Hierarchical_Feature_Splatting_for_Open-Vocabulary_3D_Visual_Grounding_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 开放词汇3D视觉定位，支持语言引导的导航
tldr: 开放词汇3D视觉定位与推理是视觉语言导航和机器人操作的关键能力，但现有方法依赖3D标注和掩膜提案，难以泛化。本文提出ReasonGrounder，利用LVLM引导的分层3D特征高斯场，按物理尺度自适应分组，实现开放词汇定位与推理。ReasonGrounder能定位被遮挡物体并依据隐式语言描述进行推理，无需密集3D微调。该工作为语言驱动的具身导航提供了高效的3D语义定位基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 851, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1758, \"height\": 923, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1603, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1610, \"height\": 1037, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1775, \"height\": 403, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 877, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 896, \"height\": 462, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 290, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 841, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-reasongrounder-lvlm-guided-hierarchical-feature-splatting-for-open-vocabulary-3d-visual-grounding-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 846, \"height\": 758, \"label\": \"Table\"}]"
motivation: 现有开放词汇3D定位依赖3D标注和掩膜提案，语义多样性有限，难以支撑视觉语言导航等复杂任务。
method: 利用LVLM指导，结合分层3D特征高斯场按物理尺度完成自适应分组，实现开放词汇的3D视觉定位与推理。
result: 在开放词汇3D定位和推理任务上取得较好性能，能处理被遮挡物体，减少对3D微调的依赖。
conclusion: 验证了LVLM与分层特征表征结合的有效性，为语言引导的导航和机器人应用提供支撑。
---

## Abstract
Open-vocabulary 3D visual grounding and reasoning aim to localize objects in a scene based on implicit language descriptions, even when they are occluded. This ability is crucial for tasks such as vision-language navigation and autonomous robotics. However, current methods struggle because they rely heavily on fine-tuning with 3D annotations and mask proposals, which limits their ability to handle diverse semantics and common knowledge required for effective reasoning. To address this, we propose ReasonGrounder, an LVLM-guided framework that uses hierarchical 3D feature Gaussian fields for adaptive grouping based on physical scale, enabling open-vocabulary 3D grounding and reasoning. ReasonGrounder interprets implicit instructions using large vision-language models (LVLM) and localizes occluded objects through 3D Gaussian splatting. By incorporating 2D segmentation masks from the Segment Anything Model (SAM) and multi-view CLIP embeddings, ReasonGrounder selects Gaussian groups based on object scale, enabling accurate localization through both explicit and implicit language understanding, even in novel, occluded views. We also contribute ReasoningGD, a new dataset containing over 10K scenes and 2 million annotations for evaluating open-vocabulary 3D grounding and amodal perception under occlusion. Experiments show that ReasonGrounder significantly improves 3D grounding accuracy in real-world scenarios.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与整体含义（研究动机与背景）

- **任务定义**：开放词汇 3D 视觉定位与推理（Open-Vocabulary 3D Visual Grounding and Reasoning）指根据自然语言描述（尤其是隐式、间接表达）在三维场景中准确定位目标物体，并且即使目标被遮挡或仅部分可见，也能完成定位。
- **现有挑战**：
  - 传统 3D 视觉定位方法（如 ScanRefer、ReferIt3D）严重依赖 3D 标注和 mask 提案，难以泛化到动态、非结构化环境。
  - 已有开放词汇方法（如 LERF、LangSplat）虽然摆脱了 3D 标注，但只能处理显式指令，难以理解复杂隐式语言（如“可以装咖啡的物体”），也无法处理遮挡情形下的目标完整定位。
- **应用价值**：视觉语言导航、自主机器人、增强现实等需要理解模糊语言并推断用户意图的真实场景。
- **本文核心思路**：引入大型视觉语言模型（LVLM）理解隐式指令，再结合基于 3D 高斯泼溅（3DGS）的分层特征场，按物理尺度对高斯分组，从而实现开放词汇 3D 定位与遮挡下的 amodal 感知。

## 二、论文提出的方法论

- **总体框架**：ReasonGrounder = 3D Gaussian Splatting + 分层特征高斯场（语言特征 + 实例特征） + LVLM 引导的参考视图选择与高斯分组。
- **关键技术细节**：

1. **Scale-Hierarchical Feature Gaussian Field（尺度分层特征高斯场）**
   - 先用标准 3DGS 重建场景，并利用 SAM 从训练视图中生成 2D 分割 mask。
   - 借助 3DGS 渲染的深度，将 mask 像素反投影到 3D，计算每个 mask 的物理尺度 \(s_i\)。
   - 对每个 mask 区域提取多视图 CLIP 特征 \(\phi_i\)，形成三元组 \(\{m_i, \phi_i, s_i\}\)。
   - 为每个 3D 高斯附加潜在特征 \(f_{g_i}\)，并通过两个浅层 MLP 映射：
     - **语言映射器 \(F_l\)**：输入（尺度 \(s_i\), 潜在特征），输出分层语言特征，用 PCA 压缩后的 CLIP 特征做 Huber 损失监督，保证多视角一致性。
     - **实例映射器 \(F_g\)**：输入同样为（尺度, 潜在特征），输出实例嵌入，使用基于 GARField 的对比损失训练，使同一尺度下同属一个 mask 的像素特征相近，不同 mask 的像素特征分离。
   - 渲染方式沿用 3DGS 的 alpha blending，实现 2D 特征图的可微渲染。

2. **LVLM-Guided Hierarchical Grouping（LVLM 引导的分层分组）**
   - **参考视图选择**：将俯视图和隐式查询输入 LVLM（如 LLaVA 1.5），得到推理出的目标物体名称和解释；再用 CLIP 图像-文本编码器从训练视图中选出与目标语义最匹配的 2D 视图作为参考视图。
   - **尺度选择**：计算目标物体 CLIP 嵌入与参考视图中各 mask 的 CLIP 嵌入的余弦相似度，选出对应最佳尺度 \(s_{i*}\)。
   - **高斯分组**：使用 HDBSCAN 对分层实例特征进行聚类，得到若干高斯组；用 alpha blending 渲染参考视图中的实例特征，选出与语言相关度最高像素对应的实例特征，再匹配最相似的聚类中心，最终确定目标高斯组 \(G_i^*\)。
   - **Amodal 感知**：在任意新视角下，直接渲染选定的高斯组，即可得到包含遮挡部分的完整目标区域。

## 三、实验设计

- **数据集**：
  1. **LERF 数据集**：13 个真实场景，用于开放词汇 3D 视觉定位基准。
  2. **3D-OVS 数据集**：长尾物体场景，主要评估开放集 3D 语义分割/定位。
  3. **ReasoningGD（新提出）**：由 Blenderproc 生成的超过 1 万场景、263 类物体、约 200 万标注的合成数据集；每个场景含 100 张 RGB-D 图像、相机位姿、2D 模态/非模态（modal/amodal）mask，专为评估隐式指令定位与遮挡下 amodal 感知而设计。
- **评估指标**：Localization Accuracy（定位成功即最高相关度像素落在标注框内）和 Mean IoU（用于 LERF、3D-OVS、ReasoningGD）。
- **对比方法**：
  - 2D 方法：LSeg、ODISE、OV-Seg。
  - 3D 方法：LERF、3D-OVS、LangSplat、Feature Field Distillation（FFD）等。
- **主要实验**：
  1. LERF 数据集上的定位准确率与 IoU 对比。
  2. 3D-OVS 数据集上的 IoU 对比。
  3. 隐式指令 3D 定位（在 LERF、3D-OVS、ReasoningGD 上的定量与定性实验）。
  4. 遮挡场景下的 amodal 感知（ReasoningGD 的 5 个场景定量评估）。
  5. 挑战性场景（多层级结构、相似物体、小目标）的鲁棒性测试。
  6. 消融实验：验证 SHF（尺度分层特征）、LVLM、3DGS 三个组件的贡献，同时对比 O-3DVG、I-3DVG、AP 三个能力维度。

## 四、资源与算力

- 论文中明确提到的算力信息有限：
  - 训练和推理使用 **NVIDIA RTX-3090 GPU** 和 14 vCPU Intel Xeon Gold 6330 CPU。
  - 部分消融实验（figurine 场景）在 **NVIDIA H100 GPU** 上完成。
  - 训练流程：先训标准 3DGS 30,000 迭代，再训练分层特征场（固定其他参数，只训练潜在特征和两个 MLP）10,000 迭代。
- **未说明的信息**：未提及使用的 GPU 数量、总训练时长、能耗等具体细节。

## 五、实验数量与充分性分析

- **实验数量**：较充分。
  - 在 3 个数据集上进行了定量评估，覆盖 2D 和 3D 方法对比。
  - 包含显式指令定位、隐式指令推理、amodal 感知、挑战场景鲁棒性、消融实验等多维度实验。
  - 定性可视化展示了与 LERF、LangSplat 的对比以及遮挡场景下的效果。
- **充分性与公平性**：
  - 对比方法选择合理，涵盖了主流开放词汇定位方法。
  - 在显式查询实验中，作者声明使用了与 LangSplat 相同的查询，保证对比公平。
  - 消融实验验证了各组件有效性，但仅在单一场景（Figurines 和 ReasoningGD 001 场景）上完成，覆盖范围有限。
  - 隐式指令实验没有与同类方法在相同隐式查询下进行对比，因为缺乏现有开放词汇推理定位方法，只能与显式方法进行间接比较。
  - ReasoningGD 是合成数据集，不能完全代表真实世界复杂遮挡，泛化性需进一步验证。

## 六、主要结论与发现

- ReasonGrounder 在 LERF 数据集上达到 **86.7%** 的平均定位准确率，在 3D-OVS 上达到 **94.7%** 的平均 IoU，优于现有方法（如 LangSplat）。
- 通过 LVLM 理解隐式指令，ReasonGrounder 不仅能定位目标，还能提供自然语言解释，展示出较强的推理能力。
- 通过分层高斯分组，ReasonGrounder 可以在新视角下恢复被遮挡物体的完整区域，实现 amodal 感知（ReasoningGD 上平均 IoU 约 90%+）。
- 消融实验证明：3DGS 相较于 NeRF 能显著提升推理速度；LVLM 带来的隐式指令理解是独立于显式定位能力的重要增益；尺度分层特征（SHF）对 amodal 感知必不可少。
- 总体表明：将 LVLM 的常识推理能力与 3D 高斯分层特征结合，是解决开放词汇 3D 定位与推理的有效路径。

## 七、优点

- **方法创新**：
  - 首次将 LVLM 引入 3DGS 开放词汇定位流程，实现隐式指令理解与推理。
  - 提出“物理尺度 + 分层特征”的高斯分组机制，使分组粒度可自适应，能定位完整目标（包括遮挡部分）。
  - 参考视图选择机制解决了 LVLM 直接处理复杂 3D 场景的难题，利用 CLIP 在 2D 视图之间做语义匹配，思路简洁有效。
- **数据集贡献**：构建了首个包含 modal/amodal mask、面向开放词汇推理的大规模合成数据集 ReasoningGD，为后续研究提供基准。
- **效率优势**：采用 3DGS 而非 NeRF，渲染和推理速度更快（消融中 0.895s vs 0.92s 每视图，且精度更高）。
- **实验设计较全面**：同时评估显式定位、隐式推理、遮挡感知、挑战场景、消融分析，充分展示了系统能力。

## 八、不足与局限

- **实验覆盖不完整**：
  - 消融实验只在两个场景上进行，缺乏跨场景的统计显著性。
  - 隐式指令测试缺少与专门针对隐式推理的现有方法对比（虽然现有方法稀缺，但至少可与 LLM-based 方法如 LLM-Grounder 做比较会更有说服力）。
- **数据集偏向**：
  - ReasoningGD 是合成数据，物体类别有限，遮挡模式由程序生成，与真实世界遮挡形态可能存在差距。
  - LERF/3D-OVS 规模较小，复杂隐式推理结果多为定性展示，缺乏大样本定量统计。
- **依赖限制**：
  - 对 LVLM 的推理质量有较强依赖，如果 LVLM 对隐式查询理解错误，后续定位会失败。
  - 依赖 SAM 生成的 2D mask 质量，mask 不准确时物理尺度估计和实例特征会有误差。
  - 使用 PCA 压缩 CLIP 特征，压缩比过高时可能损失细粒度语义。
- **未报告内容**：
  - 缺少模型参数量、训练时间、推理延迟的详细统计。
  - 缺少与最新推理型 3D 方法的横向对比（如 ScanReason、Reasoning3D），使得结论的外部效度受限于特定 baseline。
- **现实应用限制**：当前方法在单个场景上逐场景训练 3DGS，不具备跨场景泛化能力；对大规模动态环境的快速部署仍需进一步优化。

（完）
