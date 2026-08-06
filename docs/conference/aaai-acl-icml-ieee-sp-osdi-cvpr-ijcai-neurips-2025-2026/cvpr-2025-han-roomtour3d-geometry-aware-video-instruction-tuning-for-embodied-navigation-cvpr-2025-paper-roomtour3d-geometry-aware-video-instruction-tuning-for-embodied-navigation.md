---
title: "RoomTour3D: Geometry-Aware Video-Instruction Tuning for Embodied Navigation"
title_zh: RoomTour3D：面向具身导航的几何感知视频指令微调
authors: "Han, Mingfei, Ma, Liang, Zhumakhanova, Kamila, Radionova, Ekaterina, Zhang, Jingyi, Chang, Xiaojun, Liang, Xiaodan, Laptev, Ivan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Han_RoomTour3D_Geometry-Aware_Video-Instruction_Tuning_for_Embodied_Navigation_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 利用网络房间漫游视频构建VLN训练数据集
tldr: 该论文针对VLN训练数据多样性和规模受限的问题，提出RoomTour3D数据集，从网络房间漫游视频中生成开放世界行走轨迹和指令。通过3D重建补充房间类型、物体位置与形状信息，并设计几何感知的视频指令微调方法。实验表明该数据集拓宽了导航指令的开放度，显著提升了模型在真实场景上的泛化能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1064, \"height\": 899, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 644, \"height\": 84, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1792, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1809, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1623, \"height\": 608, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 732, \"height\": 731, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1630, \"height\": 747, \"label\": \"Table\"}]"
motivation: 现有VLN模拟器数据依赖人工整理，规模与多样性不足，限制模型泛化。
method: 利用网络室内漫游视频重建3D轨迹，并加入房间类型与物体布局信号进行指令微调。
result: 实验显示RoomTour3D能增强VLN模型对开放指令和新场景的适应能力。
conclusion: 网络视频驱动的大规模重建数据是缓解VLN数据瓶颈的有效途径。
---

## Abstract
Vision-and-Language Navigation (VLN) suffers from the limited diversity and scale of training data, primarily constrained by the manual curation of existing simulators.To address this, we introduce RoomTour3D, a video-instruction dataset derived from web-based room tour videos that capture real-world indoor spaces and human walking demonstrations. Unlike existing VLN datasets, RoomTour3D leverages the scale and diversity of online videos to generate open-ended human walking trajectories and open-world navigable instructions. To compensate for the lack of navigation data in online videos, we perform 3D reconstruction and obtain 3D trajectories of walking paths augmented with additional information on the room types, object locations and 3D shape of surrounding scenes. Our dataset includes ~100K open-ended description-enriched trajectories with ~200K instructions, and 17K action-enriched trajectories from 1847 room tour environments.We demonstrate experimentally that RoomTour3D enables significant improvements across multiple VLN tasks including CVDN, SOON, R2R, and REVERIE.Moreover, RoomTour3D facilitates the development of trainable zero-shot VLN agents, showcasing the potential and challenges of advancing towards open-world navigation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：Vision-and-Language Navigation（VLN）任务长期受限于训练数据的多样性和规模不足。现有数据集（如 R2R、CVDN、SOON、REVERIE）大多依赖人工设计的模拟器和人工标注轨迹，成本高、场景多样性有限，且难以覆盖真实世界的复杂性和开放词汇量。
- **研究动机**：为了突破这一瓶颈，作者希望利用互联网上海量、易获取的房间漫游视频（room tour videos）来构建大规模、开放世界、几何感知的 VLN 训练数据，从而提升导航智能体的泛化能力。
- **整体含义**：论文提出 RoomTour3D 数据集及配套的自动数据生成管线，将真实室内视频与 3D 重建、开放词汇目标检测、深度估计、大语言模型等技术结合，为 VLN 提供“几何感知”的轨迹级指令数据，并验证了其在多个 VLN 基准上的有效性，同时支持零样本导航智能体的训练。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：从网络房间漫游视频中自动挖掘连续的、带几何信息的行走轨迹，并生成开放词汇、符合人类行走习惯的导航指令。利用 3D 重建补偿视频中缺失的空间几何信息，将轨迹转化为可训练的动作序列。
- **数据生成管线**（分为两类轨迹）：
  - **描述增强轨迹（Description-Enriched Trajectories）**：
    - 以每秒 1 帧（约 1.42 m/s 行走速度）的速率采样生成连续行走轨迹。
    - 使用 RAM 进行开放词汇物体打标，Grounding-DINO 进行目标定位，Depth-Anything 生成深度图，从而得到物体类别、空间位置（左/右/中）和相对距离。
    - 使用 BLIP-2 以 VQA 模式预测每帧所在房间类型（16 类），并通过时序平滑去噪，准确率约 85%。
    - 将物体信息、距离、房间类型等文本化后，使用 GPT-4-Turbo 结合“任务指令 + 上下文示例”的提示模板生成自由形式的、描述物体沿轨迹变化的指令文本。
  - **动作增强轨迹（Action-Enriched Trajectories）**：
    - 使用 COLMAP 对视频进行 3D 重建，得到相机位姿和场景几何。
    - 将视频切分为 100 秒片段（重叠 10 秒）并行重建，再通过重叠帧的图结构合并子模型。
    - 基于相机方向余弦相似度、非极大值抑制和 DBSCAN 聚类，识别显著视角变化点（如转身点），并在空间相近但视角不同的帧中采样正/负候选动作。
    - 最终形成“历史观测 + 候选视角 + 指令 → 下一个动作”的导航训练样本。

- **模型训练方法**（基于 NaviLLM 框架）：
  - **预训练任务（Summarization Task）**：将轨迹中的帧作为候选观测，输入 NaviLLM，要求输出描述物体进展和房间变化的轨迹摘要。
  - **微调任务（Navigation Task）**：将每个轨迹帧视为一个可导航动作，模型根据历史观测和指令，从候选视角中选择正确的下一帧，并持续累积历史信息。

## 3. 实验设计：数据集 / 场景、Benchmark、对比方法

- **数据集与场景**：
  - **预训练阶段**：使用 RoomTour3D 的描述增强轨迹 + CVDN、SOON、R2R、REVERIE、ScanQA 以及 R2R/REVERIE 的增强数据。
  - **微调阶段**：使用 RoomTour3D 的动作增强轨迹 + CVDN、SOON、R2R、REVERIE、ScanQA、LLaVA-23k。
  - **测试基准**：CVDN（对话导航，评估 GP）、SOON（无框物体导航，评估 SR/SPL）、R2R（指令跟随，评估 SR/SPL）、REVERIE（远程物体定位，评估 SR/SPL）。
- **对比方法**：
  - **单任务模型**：PREVALENT、HOP、HAMT、DUET、VLN-SIG、VLN-PETL、NavGPT2、BEV-BERT 等。
  - **统一多任务模型**：NaviLLM（含作者复现版本）。
  - **零样本方法**：随机游走、NavGPT（GPT-3.5/GPT-4）、MapGPT（GPT-4/GPT-4V）、DiscussNav（GPT-4）、LangNav、NavCoT、DuET（LXMERT）、NaviLLM（无动作数据）。

## 4. 资源与算力

- 论文正文与附录并未明确提及训练的 GPU 型号、数量、训练时长或具体的硬件资源消耗。
- 仅能推断使用了 COLMAP 进行 3D 重建（多片段并行），以及 GPT-4-Turbo 的 API 调用用于指令生成，但具体的算力规模未披露。

## 5. 实验数量与充分性

- **实验组数**：
  1. 监督任务对比实验（CVDN、SOON、R2R、REVERIE 的 Val 与 Test 集，对比 NaviLLM 基线及多种历史方法）。
  2. 零样本任务实验（R2R 上的 SR/SPL，与商业模型和开源模型对比）。
  3. 消融实验（表 2）：依次加入物体标签、深度/边界框、房间类型，观察各 VLN 指标变化。
  4. 动作增强数据消融（表 1 中 RT3D Desc vs RT3D Action）。
  5. 数据正确性人工评分（100 条随机描述，4 分制平均 3.08）。
  6. 导航案例可视化分析（对比基线与本方法在关键转弯点的决策差异）。
- **充分性评估**：
  - 覆盖面较广：涵盖主流 VLN 任务、监督和零样本设置，并有消融验证各信号贡献。
  - 客观性：对比了单任务和多任务 SOTA 模型，并采用标准指标（SR、SPL、GP）。
  - 公平性：作者复现了 NaviLLM 基线（标注 ω），但未报告多次随机种子的方差，且测试集结果来自单次运行，统计显著性未说明。
  - 整体实验设计较充分，但缺少对数据规模、轨迹长度、模型参数量等因素的深入分析。

## 6. 论文的主要结论与发现

- RoomTour3D 数据能够显著提升 NaviLLM 在 CVDN、SOON、R2R、REVERIE 上的表现，尤其在 REVERIE 上提升约 6% SPL，R2R 上提升约 5.7% SPL。
- 在 SOON 和 REVERIE 上取得了新的 SOTA 结果。
- 动作增强轨迹数据使模型能够学习可执行的导航动作选择，仅使用 RoomTour3D 训练即可实现零样本导航（R2R Val-Unseen SR 14.33%，SPL 10.86%），优于同类开源模型，并接近基于 GPT-3.5 的 NavGPT。
- 消融实验表明：物体标签、深度/空间位置、房间类型三种信息均有正向贡献，其中物体标签对 REVERIE 作用明显，深度信息对 SOON/R2R/REVERIE 有边际提升，房间类型对整体有中等提升。
- 数据正确性人工评分（3.08/4）说明自动生成的轨迹描述与真实场景基本对齐，方法可靠。

## 7. 优点：方法或实验设计上的亮点

- **数据来源创新**：利用互联网房间漫游视频，绕过了人工模拟器构建的高成本和低扩展性，大幅提升了场景多样性和真实性。
- **几何感知**：通过 COLMAP 3D 重建和深度估计，引入轨迹级别的空间几何信息，突破了以往视频数据“无几何”的限制。
- **开放词汇指令**：使用 GPT-4 生成自由文本指令，避免了模板化指令的僵化，更贴近真实导航语言。
- **动作级轨迹**：将转弯点、视角变化等作为可导航动作，形成类 Agent 的决策样本，为训练零样本导航智能体提供了可能。
- **系统化消融**：分模块验证物体标签、深度、房间类型的贡献，对数据设计具有指导意义。
- **实用性强**：发布中间产物（物体标签、边界框、深度图、房间位置）和代码，便于社区复现和扩展。

## 8. 不足与局限

- **未报告算力资源**：论文未说明 GPU 型号、数量、训练时间，不利于可复现性评估。
- **统计验证不足**：未提供多次实验的均值和标准差，性能提升是否统计显著未知。
- **依赖第三方模型质量**：BLIP-2、RAM、Grounding-DINO、Depth-Anything、GPT-4 等均可能引入错误，人工评分仅 3.08 分（满分 4），说明仍有部分描述与视觉内容不符。
- **零样本性能仍有限**：虽然优于开源模型，但与商业 GPT-4 方法（如 MapGPT、DiscussNav）相比仍有较大差距。
- **3D 重建鲁棒性**：COLMAP 对视频质量敏感，重建失败或误差可能导致轨迹采样和候选动作不准确；论文仅通过合并策略缓解，未详细分析失败案例。
- **房间分类受限**：BLIP-2 仅使用 16 类房间类型，可能丢失更细粒度的空间语义，作者也承认通过 GPT 生成部分弥补，但仍有局限。
- **应用边界**：训练数据来自房产漫游视频（通常光线良好、场景整洁），未覆盖杂乱、动态或极端光照的现实环境，泛化到真实机器人场景仍有距离。

（完）
