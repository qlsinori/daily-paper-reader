---
title: "RoomTour3D: Geometry-Aware Video-Instruction Tuning for Embodied Navigation"
title_zh: RoomTour3D：面向具身导航的几何感知视频指令微调
authors: "Han, Mingfei, Ma, Liang, Zhumakhanova, Kamila, Radionova, Ekaterina, Zhang, Jingyi, Chang, Xiaojun, Liang, Xiaodan, Laptev, Ivan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Han_RoomTour3D_Geometry-Aware_Video-Instruction_Tuning_for_Embodied_Navigation_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向视觉语言导航的视频指令数据集与几何感知调优
tldr: 视觉语言导航（VLN）训练数据受限于人工模拟器的标注，规模与多样性严重不足。本文利用网络房屋浏览视频构建RoomTour3D数据集，通过3D重建补充行走轨迹、房间类型、物体位置和3D形状信息，并采用几何感知的指令微调方法。该数据集可生成开放世界可导航指令，实验证明其显著提升VLN模型在真实室内场景的泛化能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1064, \"height\": 899}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 644, \"height\": 84}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1792, \"height\": 733}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1809, \"height\": 629}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1623, \"height\": 608}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 296}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 732, \"height\": 731}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1630, \"height\": 747}]"
motivation: 现有VLN数据依赖人工模拟器，规模与多样性不足，制约模型泛化。
method: 从网络房屋浏览视频构建RoomTour3D数据集，做3D重建补全轨迹与空间标注，进行几何感知视频指令微调。
result: 实验表明使用RoomTour3D训练的VLN模型泛化能力显著提升。
conclusion: 该数据集为VLN提供大规模真实世界训练资源，缓解了数据匮乏问题。
---

## Abstract
Vision-and-Language Navigation (VLN) suffers from the limited diversity and scale of training data, primarily constrained by the manual curation of existing simulators.To address this, we introduce RoomTour3D, a video-instruction dataset derived from web-based room tour videos that capture real-world indoor spaces and human walking demonstrations. Unlike existing VLN datasets, RoomTour3D leverages the scale and diversity of online videos to generate open-ended human walking trajectories and open-world navigable instructions. To compensate for the lack of navigation data in online videos, we perform 3D reconstruction and obtain 3D trajectories of walking paths augmented with additional information on the room types, object locations and 3D shape of surrounding scenes. Our dataset includes ~100K open-ended description-enriched trajectories with ~200K instructions, and 17K action-enriched trajectories from 1847 room tour environments.We demonstrate experimentally that RoomTour3D enables significant improvements across multiple VLN tasks including CVDN, SOON, R2R, and REVERIE.Moreover, RoomTour3D facilitates the development of trainable zero-shot VLN agents, showcasing the potential and challenges of advancing towards open-world navigation.

---

## 论文详细总结（自动生成）

# RoomTour3D：面向具身导航的几何感知视频指令微调——论文详细总结

## 1. 论文核心问题与整体含义（研究动机与背景）

- **核心问题**：Vision-and-Language Navigation（VLN，视觉语言导航）训练数据存在**规模不足**与**多样性匮乏**的严重瓶颈。
- **根源**：现有 VLN 数据集（如 R2R、CVDN、REVERIE、SOON）几乎全部依赖**人工设计的模拟器**和**人工标注的轨迹**，成本高、难以规模化，且模拟场景与真实世界在复杂度、物体多样性和几何结构上存在显著差距。
- **已有尝试的局限**：
  - AirBERT 使用离散的 Airbnb 全景图，缺乏场景一致性和自然语境；
  - ScaleVLN 依赖人工筛选的 3D 场景，重建质量和可扩展性受限；
  - YTB-VLN 虽用 YouTube 视频组成全景视角，但使用模板化指令且缺乏几何信息；
  - NaVid 依赖 MatterPort3D 与 R2R 标注，未能同时兼顾场景规模、物体开放度和几何感知。
- **本文方案**：提出 **RoomTour3D** 数据集——从互联网房屋浏览（room tour）视频中自动构建大规模、几何感知、开放词汇的 VLN 训练数据，以低成本突破模拟器数据的天花板，并验证其对全监督与零样本 VLN 任务的提升。

---

## 2. 论文方法论

### 2.1 总体思路

利用网络房屋浏览视频（第一人称手持相机连续拍摄）作为数据源，通过 **3D 重建** 补充几何信息，再借助**多个视觉专家模型**提取物体、空间与深度信息，最后用 **GPT-4** 生成开放词汇、空间感知的导航指令，构建两类轨迹：**描述增强轨迹（Description-Enriched Trajectories）** 和 **动作增强轨迹（Action-Enriched Trajectories）**。

### 2.2 描述增强轨迹生成流程

1. **轨迹采样**：以每 2 秒一帧的速率均匀采样（对应室内平均步行速度约 1.42 m/s）。
2. **物体多样性与空间感知标注**（图 2a）：
   - RAM → 开放词汇物体标签；
   - Grounding-DINO → 物体边界框定位；
   - Depth-Anything → 相对深度估计；
   - 将物体边界框中心 + 深度图信息组织为文本模板（如“当前视角右侧近处有床/毯子/桌子”），生成逐帧详细描述。
3. **房间类型标注**（图 2b）：
   - BLIP-2 以 VQA 判别模式回答“我在哪个房间？”，预定义 16 种常见房间类型；
   - 对帧级预测做时序平滑去噪；
   - 人工验证 50 段视频剪辑，准确率达 **85%**。
4. **可控指令生成**（图 2c）：
   - 采用“任务指令 + 上下文示例 + 预测”三段式 prompt；
   - 将房间位置与逐帧物体描述注入 GPT-4-Turbo，生成连贯的、描述物体沿轨迹变化过程的**开放式**导航指令。

### 2.3 动作增强轨迹生成流程

1. **3D 场景重建**：
   - 视频以 3 fps 采样，分割为 100 秒片段（相邻片段重叠 10 秒），并行执行 COLMAP 重建；
   - 通过“重叠帧 > 3”定义模型间连接关系，构建图结构并使用**深度优先搜索（DFS）** 迭代合并子模型。
2. **可导航动作采样**：
   - 利用重建的 3D 场景计算帧间相机位姿差异（距离 + 朝向），识别“显著视角变化点”（如转弯点）；
   - 采用余弦相似度阈值过滤 + 非极大值抑制（NMS）保留主要视角变化；
   - 用 **DBSCAN** 对空间邻近但视角不同的帧聚类，确保动作多样性；
   - 每条行走路径中，选择最近帧作为**正候选**，角度差异最大的帧作为**负候选**，构造导航决策训练样本。

### 2.4 模型训练任务设计（基于 NaviLLM）

- **预训练——摘要任务**（图 3a）：将描述增强轨迹的帧序列作为候选视角，模型输出包含物体变化与房间变化的轨迹摘要，以 next-token prediction 损失训练，增强模型对长序列变化的归纳能力。
- **微调——导航任务**（图 3b）：将动作增强轨迹中每一帧视为一个可导航动作候选，输入历史观测 `<hist>` + 指令，模型从候选帧 `<cand>` 中预测下一步动作；所选动作缓存在历史 token 中，最后一步再执行路径摘要任务。

> 注：全文没有给出显式数学公式，核心方法以自动化的多阶段数据流水线为主。

---

## 3. 实验设计

### 3.1 数据集与 benchmark

- **评测任务**（4 个 VLN benchmark）：
  - **CVDN**：对话式导航，指标为 Goal Progress（GP）；
  - **SOON**：无边界框的目标物体定位导航，指标为 SR/SPL；
  - **R2R**：逐步指令跟随，指标为 SR/SPL；
  - **REVERIE**：基于简洁指令的远距离物体定位，指标为 SR/SPL。
- **训练数据**：预训练使用 RoomTour3D 描述增强轨迹 + CVDN/SOON/R2R/REVERIE/ScanQA + R2R、REVERIE 增强数据；微调阶段追加 RoomTour3D 动作增强轨迹 + LLaVA-23k。

### 3.2 对比方法

- **单任务模型**：PREVALENT、HOP、HAMT、DUET、VLN-SIG、VLN-PETL、NavGPT2、BEV-BERT；
- **统一多任务模型**：NaviLLM（含复现结果）；
- **零样本方法**（R2R 上）：Random Walk、NavGPT（GPT-3.5/4）、MapGPT（GPT-4/GPT-4V）、DiscussNav（GPT-4）、LangNav、NavCoT、DuET。

### 3.3 主要实验结果

- **全监督多任务**（表 1）：
  - 预训练加入描述增强轨迹后，4 个数据集 Val 集全面稳定提升；
  - 微调加入动作增强轨迹后，在 SOON、R2R、REVERIE 的 Val-U 与 Test 上均取得 SOTA；
  - R2R Val-U 提升约 5.7%，REVERIE Val-U 提升约 6.0%。
- **零样本导航**（表 3）：
  - 仅用 RoomTour3D 动作增强数据训练（无传统动作标注），NaviLLM 达到 **SR 14.33% / SPL 10.86%**，超越所有开源模型（LangNav、NavCoT 等），可与基于 GPT-3.5 的 NavGPT 媲美。
- **消融实验**（表 2）：
  - 逐个添加物体标签、深度/边界框、房间类型三种信息模态；
  - 物体多样性显著提升 REVERIE，深度信息小幅提升 SOON/R2R/REVERIE，房间类型在所有任务上带来额外增益；
  - 动作增强数据的加入在 SOON、R2R、REVERIE 的 Test SPL 上均有提升。
- **数据质量验证**：人工对 100 条轨迹描述按 1–4 分评估，平均 **3.08 分**，74% 达到“基本相关”或“完全匹配”。
- **案例可视化**（图 4）：展示在 R2R-unseen 中，基线模型在转弯决策点选错方向，而本文方法正确左转。

---

## 4. 资源与算力

- **论文并未明确报告** GPU 型号、数量、训练时长等算力信息。
- 仅能推断：3D 重建采用多片段并行策略以提升时间效率；模型训练基于 NaviLLM（LLM 底座），但未给出具体硬件配置。如需复现，需作者提供附录或代码仓库的补充细节。

---

## 5. 实验数量与充分性

- **实验组数**：
  - 表 1：4 个数据集 × Val/Test 两个划分 × 两种数据变体（Desc / Action），对比 9–12 个基线；
  - 表 2：4 组消融（模态逐步叠加）；
  - 表 3：零样本对比 10 个方法；
  - 另有数据质量人工评估与导航路径可视化案例。
- **充分性评价**：
  - **优点**：覆盖了 VLN 的四大代表性任务与全监督/零样本两种范式，数据模态消融设计清晰，体现了几何信息（深度、房间类型）的独立贡献，实验规模对一篇数据集论文而言较为充分。
  - **不足**：
    1. 所有实验仅基于 **NaviLLM 一个模型框架**，未验证其他模型（如 DUET、BEV-BERT）上是否同样有效；
    2. 未与 YTB-VLN、ScaleVLN、PanoGen 等**同类数据生成方法**在同一框架下做直接对比，难以精确量化 RoomTour3D 的相对优势；
    3. 表 1 中 CVDN 的 Test GP 在加入数据后反而略有下降（7.90→7.55/7.22），论文未给出深入讨论。

---

## 6. 主要结论与发现

1. **网络视频 + 3D 重建可规模化构建几何感知 VLN 数据**：1847 个房屋环境、约 10 万条开放轨迹、20 万条指令、1.7 万条动作增强轨迹，验证了自动数据流水线的可扩展性。
2. **开放词汇与空间感知是收益关键**：物体多样性对物体定位任务（REVERIE）增益最大，深度与房间信息提供空间推理基础，共同解释 R2R 与 REVERIE 的显著提升。
3. **动作增强轨迹可直接训练零样本导航智能体**：无需传统导航标注即可学习动作选择，标志从“模拟器监督”到“开放世界自监督”的可行过渡。
4. **数据质量可控**：人工评分（3.08/4）证明自动生成的指令具备较高的视觉对齐度。

---

## 7. 优点

- **数据来源创新**：使用网络房屋浏览视频，天然具备真实场景多样性与第一人称行走连续性，避开模拟器的照片级真实感与成本瓶颈。
- **几何信息显式建模**：通过 COLMAP 重建、深度估计、房间类型识别，将 2D 视频升维为带几何上下文的导航数据，优于仅做全景拼接的 YTB-VLN。
- **开放词汇指令生成**：用 GPT-4 替代模板指令，生成自然、开放、与空间位置绑定的指令，提升模型泛化性。
- **负样本构造**：利用视角差异大的帧作为负候选，增强动作判别能力，对零样本导航尤为关键。
- **数据产品丰富**：释放物体标签、边界框、深度图、房间位置、代码与 prompt，后续研究可复用。

---

## 8. 不足与局限

- **实验泛化性不足**：仅验证 NaviLLM 一种架构；对 YTB-VLN、ScaleVLN、PanoGen 等同类数据方案的直接对比缺失，SOTA 结论的排他性证据有限。
- **自动化标注误差传递**：BLIP-2 房间分类准确率仅 85%，RAM/Grounding-DINO/Depth-Anything 均有噪声，GPT-4 生成指令可能引入幻觉或与画面不完全对齐（人工评分 3.08 也说明存在部分不相关描述）。
- **领域偏差风险**：房屋浏览视频多来自房产中介，场景偏向“样板间”——整洁、少人、家具风格单一，与真实居家环境的杂乱度、动态物体分布存在差异，可能影响开放世界迁移。
- **CVDN 增益有限甚至回退**：对话式导航任务提升不明显，Test 集上 GP 指标略降，说明数据对需要多轮对话理解的场景帮助有限。
- **零样本能力仍较弱**：14.33% SR 虽超越开源模型，但与 GPT-4 驱动的商业方法（MapGPT 43.7%、DiscussNav 43%）差距明显，离“开放世界导航”仍有很大距离。
- **未提供训练资源细节**：无 GPU 型号/数量/时长信息，影响复现成本评估。

---

（完）
