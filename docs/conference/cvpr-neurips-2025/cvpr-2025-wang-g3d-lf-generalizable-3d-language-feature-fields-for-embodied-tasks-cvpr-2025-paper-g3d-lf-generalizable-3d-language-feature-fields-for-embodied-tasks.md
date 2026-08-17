---
title: "g3D-LF: Generalizable 3D-Language Feature Fields for Embodied Tasks"
title_zh: "g3D-LF: 面向具身任务的可泛化三维语言特征场"
authors: "Wang, Zihan, Lee, Gim Hee"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_g3D-LF_Generalizable_3D-Language_Feature_Fields_for_Embodied_Tasks_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 面向具身任务的语言可查询3D特征场与BEV地图，支持按语言查询目标位置
tldr: 针对具身智能体在未知环境中进行语言目标导航的需求，论文提出可泛化的三维语言特征场g3D-LF。该方法以带位姿的RGB-D图像为输入，通过体渲染与多尺度编码构建可实时更新的特征场，可生成以智能体为中心的BEV地图并用多粒度语言查询目标。实验表明预训练表示能泛化到新场景，为语言指令驱动的导航与环境理解提供基础表示。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 929, \"height\": 739, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1754, \"height\": 953, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 866, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 864, \"height\": 439, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 923, \"height\": 345, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 912, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 892, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 906, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 744, \"height\": 266, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 882, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-g3d-lf-generalizable-3d-language-feature-fields-for-embodied-tasks-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 797, \"height\": 105, \"label\": \"Table\"}]"
motivation: 具身任务需要在三维场景中实现语言与空间对应，现有表示缺乏可泛化性。
method: 在大规模三维语言数据上预训练特征场，利用体渲染和多尺度编码支持视图预测、BEV地图与语言查询。
result: 可泛化到未知环境，并支持实时构建和动态更新，提升语言目标定位能力。
conclusion: 为具身语言导航提供了统一且可实时更新的三维语言表示基础。
---

## Abstract
We introduce Generalizable 3D-Language Feature Fields (g3D-LF), a 3D representation model pre-trained on large-scale 3D-language dataset for embodied tasks. Our g3D-LF processes posed RGB-D images from agents to encode feature fields for: 1) Novel view representation predictions from any position in the 3D scene; 2) Generations of BEV maps centered on the agent; 3) Querying targets using multi-granularity language within the above-mentioned representations. Our representation can be generalized to unseen environments, enabling real-time construction and dynamic updates. By volume rendering latent features along sampled rays and integrating semantic and spatial relationships through multiscale encoders, our g3D-LF produces representations at different scales and perspectives, aligned with multi-granularity language, via multi-level contrastive learning. Furthermore, we prepare a large-scale 3D-language dataset to align the representations of the feature fields with language. Extensive experiments on Vision-and-Language Navigation under both Panorama and Monocular settings, Zero-shot Object Navigation, and Situated Question Answering tasks highlight the significant advantages and effectiveness of our g3D-LF for embodied tasks. Our source code and dataset will be made open-source upon paper acceptance.

---

## 论文详细总结（自动生成）

# g3D-LF: 面向具身任务的可泛化三维语言特征场（中文详细总结）

## 1. 核心问题与研究动机

- 具身智能体（embodied agents）需要在真实三维环境中执行语言导航、视觉问答、零样本目标导航等任务，因此需要一种能够同时表达**三维空间结构**与**开放词汇语义**的场景表示。
- 现有三维表示方法主要分为几类：点云模型、体素模型、可泛化特征场（generalizable 3D feature fields）等。其中可泛化特征场具备对未见场景的泛化能力、实时构建/更新能力和开放语义空间，但存在三个关键缺陷：
  1. 监督信号仅来自 2D 基础模型（如 CLIP、DINOv2），缺乏 3D 空间关系的显式理解；
  2. 训练过程缺少语言监督，导致表示与语言语义存在显著 gap；
  3. 大尺度表示（panorama、BEV map）难以与长文本描述对齐。
- 为此，论文提出 **g3D-LF（Generalizable 3D-Language Feature Fields）**：在大规模 3D-语言数据集上预训练一个可泛化三维语言特征场，使智能体能够用多粒度语言查询场景中的任意位置、生成 BEV 地图，并泛化到未知环境。

## 2. 方法论

### 2.1 总体框架
- 输入：智能体观测到的**带位姿的 RGB-D 图像序列**。
- 输出：
  - 任意视点的**新视图表示**（novel view representation）；
  - 以智能体为中心的**BEV 地图表示**；
  - 支持用**多粒度语言**（物体类别、属性、关系、场景布局）查询上述表示。
- 训练方式：在大规模 3D-语言数据上进行**多级对比学习**，对齐不同尺度表示与语言。

### 2.2 3D-语言数据构建
- 数据集来源：ScanNet（单房间）、HM3D（多房间）、Structured3D（多房间），合计约 5K 室内场景。
- 语言标注：主要来自 SceneVerse 自动生成的物体级/场景级描述，以及 ScanRefer 的人类标注物体指代，总语言描述近 100 万条。
- 组织形式：
  - 每个场景提供多帧 RGB-D 图像与对应位姿；
  - 实例级点云带有实例 ID，可关联到语言描述；
  - 训练时可快速检索任意 3D 点附近实例的语言描述，用于监督视图/BEV 区域。

### 2.3 特征场编码
- 使用 CLIP 图像编码器提取每帧 RGB 图像的细粒度视觉特征 `g_t,i`（768 维），结合深度图和相机参数投影到 3D 世界坐标 `P_t,i`，并记录观测方位角 `θ_t,i` 和区域尺寸 `s_t,i`。
- 特征点集合 `M` 随时间在线更新：`M_t = M_{t-1} ∪ {[g, P, θ, s]}`。

### 2.4 Ray-View-Panorama 编码
- 对每个新视图，用 MLP 视图网络聚合特征场中 k 近邻特征，预测采样点的语义表示 `r_n` 和体积密度 `σ_n`。
- 沿射线进行体积渲染得到子区域特征 `R(u,v)`：
  ```
  R(u,v) = Σ_n τ_n (1 - exp(-σ_n Δ_n)) r_n
  ```
  其中 `τ_n` 为体积透射率，`Δ_n` 为采样点间距。
- 将 12×12 的特征图与可学习的 view token 输入 transformer 视图编码器，得到编码后视图表示 `R′` 和全局视图表示 `V′`。
- 进一步以 30° 间隔预测 12 个新视图，组合后输入 transformer 全景编码器，得到全景表示 `{V″_i}`。

### 2.5 Ray-BEV 编码
- 为支持大规模场景理解，构建以智能体为中心的 BEV 地图（16.8 m × 16.8 m，168×168 网格）。
- 渲染射线从天花板下方垂直向下发射，通过 MLP BEV 网络聚合特征点，并用与视图渲染类似的体渲染得到 BEV 射线表示 `R̂(h,w)`。
- 经 7×7 非重叠卷积降采样到 24×24，再经 transformer BEV 编码器得到 `R̂′`。

### 2.6 多级对比学习
- **物体级对齐（Object-level Alignment）**：用覆盖 1883 个室内物体类别的词表 `O` 与射线表示做对比学习：
  ```
  L_object = CrossEntropy({CosSim(R, O_i)/τ}, O_gt)
  ```
  针对室内场景长尾分布，使用**平衡损失**：对交叉熵最高的前 10% 射线损失赋予更大权重，提升小物体/罕见物体识别。
- **长文本细粒度对比学习（Fine-grained Contrastive）**：将 BEV 中窗口区域的 25 个特征与长文本的词特征构造亲和矩阵 `A(m,l) = CosSim(R̂′_m, W_l)/τ`，取 Top-k 平均作为细粒度相似度，再对窗口与文本做双向对比损失。全景表示同样参与该损失，用于理解物体关系与空间布局。
- **CLIP 知识蒸馏**：将真实视图/区域的 CLIP 视觉特征作为监督，对新视图、全景、BEV 表示做对比损失，以保留 2D 基础模型的泛化能力。

### 2.7 下游任务适配
- **Vision-and-Language Navigation (VLN)**：
  - 单目设置：基于 VLN-3DFF，使用 g3D-LF 预测候选路径点的新视图表示，并将 BEV 地图输入跨模态图编码器。
  - 全景设置：基于 HNR，用 g3D-LF 生成候选路径点的全景表示。
- **Zero-shot Object Navigation**：用 g3D-LF 预测周围 12 视图特征和 BEV 地图，计算与目标文本特征的最大相似度，构建局部与全局价值地图，控制点目标导航策略。
- **Situated Question Answering (SQA)**：用 g3D-LF 的 BEV 和全景表示，训练位置、朝向、答案三个 transformer 解码器。

## 3. 实验设计

### 3.1 预训练设置
- 数据集：ScanNet、HM3D、Structured3D 合成的 5K 场景。
- 训练：每场景采样 30 帧构建特征场，随机选一帧作为新视图预测；对 HM3D 用 Habitat 模拟器随机轨迹采样。
- 预训练 50K episodes（约 10 天），使用两张 RTX 6000 Ada GPU。
- 保证公平性：所有训练数据仅包含 train split，val/test split 被剔除。

### 3.2 任务与基准
| 任务 | 数据集/基准 | 指标 |
|------|-------------|------|
| 单目 VLN | R2R-CE (Matterport3D + Habitat) | NE↓, OSR↑, SR↑, SPL↑ |
| 全景 VLN | R2R-CE | 同上 |
| Zero-shot Object Navigation | HM3D val、MP3D val | SR↑, SPL↑ |
| Situated QA | SQA3D | Acc@0.5m/1.0m, Acc@15°/30°, EM@1 |

### 3.3 对比方法
- 单目 VLN：CM2、WS-MGMap、NaVid、InstructNav、VLN-3DFF 等。
- 全景 VLN：Sim2Sim、VLN-BERT、GridMM、Ego2-Map、DREAM、ScaleVLN、ETPNav、BEVBert、HNR、Energy 等。
- 零样本目标导航：ZSON、ESC、VLFM、InstructNav、GAMap、SG-Nav 等。
- SQA3D：ClipBERT、ScanQA、SQA3D、3D-VisTA、SceneVerse、LEO、Scene-LLM 等。

### 3.4 主要结果
- **单目 VLN**：g3D-LF 在 Val Unseen 上 SR=47.2 / SPL=34.6，Test Unseen 上 SR=46.3 / SPL=32.2，均优于所有对比方法（包括 LLM 方法）。
- **全景 VLN**：在 Test Unseen 上 SR=58 / SPL=51，达到 SPL 最优、SR 持平 SOTA。
- **Zero-shot Object Navigation**：HM3D 上 SR=55.6 / SPL=31.8，MP3D 上 SR=39.0 / SPL=18.8；在 SPL 上超过所有方法，SR 上略低于 InstructNav（HM3D 未报告 SPL 时 SR=58）但 g3D-LF 无需 VLM/LLM。
- **SQA3D**：定位精度大幅优于基线（Acc@0.5m=23.4, Acc@1.0m=45.7, Acc@15°=29.8, Acc@30°=54.7），EM@1=47.7 与使用点云的方法接近，但低于 LLM 方法（LEO、Scene-LLM）。

## 4. 资源与算力

- 预训练：**2 张 RTX 6000 Ada GPU，耗时约 10 天（50K episodes）**。
- 推理速度（RTX 4090）：新视图渲染 73.6 FPS（含视图编码器 71.1 FPS），12 视图全景 5.9 FPS，BEV 渲染 6.3 FPS（含 BEV 编码器 6.1 FPS）。
- 得益于与 HNR 相同的稀疏采样策略（仅渲染含邻近特征点的区域），渲染时间减少 10 倍以上。

## 5. 实验数量与充分性分析

- **实验组数**：覆盖 4 个具体任务（单目 VLN、全景 VLN、零样本目标导航、SQA3D），每组与大量 SOTA 对比。
- **消融研究**：两组关键消融：
  - 模块消融（Table 5）：移除新视图/BEV 对单目 VLN 和物体导航的影响；
  - 预训练损失消融（Table 6）：分别移除物体级对比、CLIP 蒸馏、长文本细粒度对比，并对比“非平衡损失”和“粗粒度文本特征”等变体，共 6 行结果。
- **充分性评价**：
  - 优点：任务覆盖广、基线数量多、消融设计合理，能验证各组件贡献。
  - 不足点：
    - SQA3D 上未与不使用点云的其他 LLM 方法（如 Scene-LLM 也使用图像）进行公平的“仅图像”对比，导致 EM@1 差距原因未完全归因；
    - HM3D 零样本实验并非严格零样本，因为 g3D-LF 预训练使用了 HM3D 训练场景；
    - 未做超参数敏感性分析或不同规模数据训练的 scaling 实验；
    - 未在真实机器人上验证，全部为仿真环境。

## 6. 主要结论与发现

- g3D-LF 首次证明**用大规模 3D-语言数据预训练可泛化特征场**是可行的，且能显著提升多种具身任务性能。
- 多级对比学习（物体级、长文本细粒度、CLIP 蒸馏）对于同时保持视觉泛化能力和语言对齐至关重要，缺一不可。
- 新视图预测和 BEV 地图分别对单目 VLN 和物体导航有显著贡献，二者互补。
- 平衡损失缓解室内物体长尾分布问题，显著改善小物体目标导航。
- 细粒度长文本对比（基于亲和矩阵的 Top-k 相似度）优于简单使用 [SEP] 向量。
- 模型推理速度可满足实时具身任务需求。

## 7. 优点

- **创新性**：首次构建面向特征场的 3D-语言预训练数据与方法，提出多级对比学习框架，填补了可泛化特征场语言对齐空白。
- **通用性**：统一了多尺度（物体/视图/全景/BEV）表示，可适配导航、问答、目标定位等多种任务。
- **实用性**：输入仅为 RGB-D + 位姿，不依赖完整点云，更适合真实机器人；支持实时在线更新。
- **消融透彻**：多个消融实验清晰证明各模块和损失项的必要性。
- **实验全面**：在 4 个任务上均与当前 SOTA 比较，且代码开源。

## 8. 不足与局限

- 无法处理动态场景：特征场假设静态环境，不适用于物体或人移动的场景。
- 未验证动态任务（如物体操纵、人机交互）中的表现。
- 3D-语言数据规模有限（约 5K 场景 / 100 万描述），远小于图像-语言数据，可能限制泛化上限。
- 与 LLM 结合不足：论文指出的未来方向“3D特征场 + LLM”可提升文本生成能力，但当前 SQA 的 EM@1 明显低于 LLM 方法，说明语义推理仍有差距。
- 零样本评估的严格性有限：HM3D 场景参与预训练，不是完全零样本设置。
- 长文本对齐仅关注词级特征，未利用 LLM 的高层语义；对极长多句指令可能仍有困难。

（完）
