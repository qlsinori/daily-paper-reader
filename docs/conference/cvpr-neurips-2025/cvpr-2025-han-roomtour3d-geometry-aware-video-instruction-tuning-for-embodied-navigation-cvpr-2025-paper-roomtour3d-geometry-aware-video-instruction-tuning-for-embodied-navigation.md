---
title: "RoomTour3D: Geometry-Aware Video-Instruction Tuning for Embodied Navigation"
title_zh: RoomTour3D：面向具身导航的几何感知视频指令微调
authors: "Han, Mingfei, Ma, Liang, Zhumakhanova, Kamila, Radionova, Ekaterina, Zhang, Jingyi, Chang, Xiaojun, Liang, Xiaodan, Laptev, Ivan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Han_RoomTour3D_Geometry-Aware_Video-Instruction_Tuning_for_Embodied_Navigation_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 利用网络房间漫游视频生成3D轨迹与开放指令的VLN数据集
tldr: 视觉语言导航受限于人工构建的模拟器数据和指令多样性。RoomTour3D从网络房间漫游视频中提取室内空间与人类行走演示，通过三维重建生成开放式的3D轨迹和可导航指令。该数据集补充了房间类型、物体位置与3D形状等信息，扩大了训练数据的规模与多样性。实验显示利用该数据集可以显著提升VLN模型的泛化能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1064, \"height\": 899}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 644, \"height\": 84}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1792, \"height\": 733}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1809, \"height\": 629}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1623, \"height\": 608}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1647, \"height\": 296}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 732, \"height\": 731}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-han-roomtour3d-geometry-aware-video-instruction-tuning-for-embodied-navigation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1630, \"height\": 747}]"
motivation: VLN训练数据受限于模拟器人工采集，多样性和规模不足。
method: 利用网络房间漫游视频进行三维重建，生成带3D轨迹与开放词汇指令的视频指令数据集。
result: 提出的数据集显著提升了VLN训练的多样性，并改善了下游导航模型泛化性能。
conclusion: RoomTour3D为VLN提供了大规模开放世界训练数据的新来源。
---

## Abstract
Vision-and-Language Navigation (VLN) suffers from the limited diversity and scale of training data, primarily constrained by the manual curation of existing simulators.To address this, we introduce RoomTour3D, a video-instruction dataset derived from web-based room tour videos that capture real-world indoor spaces and human walking demonstrations. Unlike existing VLN datasets, RoomTour3D leverages the scale and diversity of online videos to generate open-ended human walking trajectories and open-world navigable instructions. To compensate for the lack of navigation data in online videos, we perform 3D reconstruction and obtain 3D trajectories of walking paths augmented with additional information on the room types, object locations and 3D shape of surrounding scenes. Our dataset includes ~100K open-ended description-enriched trajectories with ~200K instructions, and 17K action-enriched trajectories from 1847 room tour environments.We demonstrate experimentally that RoomTour3D enables significant improvements across multiple VLN tasks including CVDN, SOON, R2R, and REVERIE.Moreover, RoomTour3D facilitates the development of trainable zero-shot VLN agents, showcasing the potential and challenges of advancing towards open-world navigation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：视觉语言导航（VLN）旨在让智能体根据自然语言指令在未知环境中导航。现有VLN训练数据大多来自人工设计的模拟器（如R2R、CVDN、SOON、REVERIE），存在**场景多样性有限、规模小、人工标注成本高**的问题，难以反映真实世界的复杂性和开放性。
- **核心问题**：如何获得大规模、多样化、具有真实几何信息与开放词汇指令的训练数据，以提升VLN智能体的泛化能力并支持开放世界导航？
- **整体含义**：论文提出了一种全新的数据构建范式——**从网络房间漫游视频中自动挖掘**几何感知的导航轨迹和指令，而不是依赖人工模拟器。通过3D重建和多种视觉专家模型，将连续视频转化为带有空间语义的导航数据，从而弥补现有数据集在规模、开放词汇和几何结构上的不足，为VLN提供可扩展的数据来源。

---

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

- **核心思想**：将网络上的“房间漫游视频”作为原始素材，利用3D重建恢复真实行走轨迹的几何信息，并借助大语言模型生成开放词汇、空间感知的导航指令，最终形成两类训练数据：
  - **Description-enriched Trajectories（描述增强轨迹）**：用于预训练的开放轨迹描述。
  - **Action-enriched Trajectories（动作增强轨迹）**：用于导航决策微调的带正负候选的动作数据。

- **关键技术细节与流程**：

  - **视频采集与帧采样**：从网络收集1847个房间漫游视频，按平均人类行走速度（约1.42 m/s）每2秒采一帧，形成连续行走轨迹。
  
  - **3D场景重建**：使用COLMAP进行运动恢复结构（SfM），以3帧/秒采样并切分为100秒片段并行重建，再通过帧重叠图合并子模型（用深度优先搜索合并），获得相机位姿和场景几何。
  
  - **物体与空间感知标注**：
    - RAM用于开放类别物体标记；
    - Grounding-DINO进行物体边界框定位；
    - Depth-Anything估计深度；
    - 结合边界框中心与深度图，生成“物体在哪个方位、多远的文字化描述”。
  
  - **房间类型标注**：使用BLIP-2的视觉问答模式，在16个常见房间类型上进行判别式预测，并做时序平滑（人工验证准确率85%）。
  
  - **指令生成（GPT-4）**：将帧级房间类型 + 物体位置/深度描述组合为提示，通过“任务说明-上下文示例-预测”模板，让GPT-4生成两类指令：
    - 描述轨迹：按物体在画面中的渐进变化描述行走路径；
    - 导航指令：结合路径起止、房间顺序、物体提及，给出可执行的导航语言。

  - **可导航动作采样**：基于COLMAP重建的相机位姿，计算帧间航向角差异和距离；用余弦相似度阈值和非极大值抑制找出显著视角变化点；再用DBSCAN聚类将空间接近但视角不同的帧聚集；在每个聚类路径中，选取最近帧为正候选、最高角度差帧为负候选，构成动作增强轨迹。

  - **模型训练适配（NaviLLM）**：
    - **预训练总结任务**：将描述增强轨迹的帧作为候选视图，模型输出物体进展和房间位置变化的总结（视觉指令总结）。
    - **导航任务微调**：将动作增强轨迹的帧作为候选动作，模型根据历史观测和指令选择下一帧；选定动作作为历史token，并同样进行路径总结。

---

### 3. 实验设计：数据集、Benchmark与对比方法

- **数据集**：
  - 预训练：使用RoomTour3D（描述增强轨迹） + CVDN、SOON、R2R、REVERIE、ScanQA，以及R2R/REVERIE的增强数据。
  - 微调：使用RoomTour3D（动作增强轨迹） + CVDN、SOON、R2R、REVERIE、ScanQA + LLaVA-23k。
  - 评估：在CVDN（指标GP）、SOON、R2R、REVERIE（指标SR和SPL）上进行测试。
  
- **对比方法**：
  - **单任务模型**：PREVALENT、HOP、HAMT、DUET、VLN-SIG、VLN-PETL、NavGPT2、BEV-BERT。
  - **统一多任务模型**：NaviLLM（复现基线作为主要对比）。
  - **零样本方法**：商业模型（NavGPT/GPT-3.5、GPT-4、MapGPT、DiscussNav）和开源模型（LangNav、NavCoT、DuET、NaviLLM）。

- **主要实验设置**：
  - 监督任务：全监督微调四个VLN任务，比较不同NaviLLM变体（无RT3D、+描述数据、+动作数据）。
  - 零样本任务：去除所有动作和几何数据，仅用RoomTour3D动作增强轨迹训练NaviLLM，评估R2R未见环境。
  - 消融实验：对轨迹描述生成中使用的输入模态（物体标签、深度+边界框、房间类型）进行逐项消融。
  - 人工评分：100条随机轨迹描述在4点相关性量表上的评分。

---

### 4. 资源与算力

- 论文中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅在方法部分提到COLMAP重建时通过视频切块和并行重建以提高时间效率，但未给出实际计算资源消耗数据。

---

### 5. 实验数量与充分性

- **实验数量与覆盖**：
  - 表1：在4个VLN基准（CVDN、SOON、R2R、REVERIE）上的监督任务对比，涵盖验证集和测试集，并对比了单任务模型与统一模型。
  - 表2：输入模态消融（物体标签、深度、房间类型），覆盖4个数据集，验证各信息源对性能的实际贡献。
  - 表3：R2R未见环境上的零样本导航对比，与商用和开源SOTA方法比较。
  - 数据质量人工评估（100条样本）及导航路径可视化案例。
  
- **充分性与公平性**：
  - **优点**：实验较为全面，覆盖主要VLN任务、指标、消融，且对比了多种SOTA方法；零样本实验突出了动作增强数据的独特价值。
  - **不足**：
    - 所有训练实验仅基于**NaviLLM单一模型**，未验证RoomTour3D在其他VLN模型上的通用性。
    - 消融只针对描述增强轨迹的输入模态，未见对动作采样策略（聚类参数、正负候选选择）的消融。
    - 人工评估样本量较小（100条），且未评估GPT-4生成指令的多样性或与真实人工指令的差异。
    - 零样本设置中，未与完全基于真实数据训练的开放世界方法比较，仅与特定基准对比。

---

### 6. 论文的主要结论与发现

- 将RoomTour3D数据加入预训练和微调后，NaviLLM在**CVDN、SOON、R2R、REVERIE**上的性能均有提升，尤其在R2R Val-U上提升约5.7%，REVERIE Val-U提升约6%，并在SOON和REVERIE的测试集上取得新的SOTA结果（SPL指标）。
- 消融实验表明：**物体开放标签、深度信息、房间类型**对导航均有正向贡献；物体标签对REVERIE影响最大，深度提升SOON、R2R、REVERIE，房间类型带来全面小幅提升。
- 使用动作增强轨迹训练后，NaviLLM在**R2R零样本导航**达到14.33% SR、10.86% SPL，优于开源模型，接近使用GPT-3.5的NavGPT，证明了RoomTour3D可支持训练零样本导航智能体，向开放世界导航迈进。
- 人工评分（均值3.08/4）表明自动生成的轨迹描述与视频内容具有较高相关性。

---

### 7. 优点：方法或实验设计上的亮点

- **数据来源创新**：首次系统性利用网络房间漫游视频（而非模拟器或人工3D场景）构建VLN数据集，规模大（18万+指令、17K动作轨迹、1847个环境）、真实感强，且具有可扩展性。
- **几何感知**：通过COLMAP重建真实3D场景，获得相机位姿和空间布局，使得指令生成和动作采样都具备明确几何依据，优于仅使用2D帧的方法（如YTB-VLN）。
- **开放词汇与自由形式指令**：使用RAM+Grounding-DINO的开放词汇物体标注，结合GPT-4生成非模板化、包含物体和空间关系的自然语言指令，提升了指令的多样性和语义丰富度。
- **统一的自动管线**：从视频到最终训练数据端到端自动化，包含房间分类、物体定位、深度估计、3D重建、LLM生成，易于扩展到更多视频。
- **提出两种互补数据形式**：描述增强轨迹用于预训练总结任务，动作增强轨迹用于导航决策微调，并举证其在零样本导航中的价值。
- **实验充分且结果显著**：在4个主流VLN基准上验证了大规模数据提效，并提供了消融和可视化分析，结论有说服力。

---

### 8. 不足与局限

- **数据噪声依赖**：自动标注（RAM、Grounding-DINO、Depth-Anything、BLIP-2）存在误差，3D重建质量不稳定的视频可能产生错误轨迹或候选；GPT-4生成指令偶尔出现与视频不完全匹配的情况（人工评分仍有26%为“部分相关”或“不相关”）。
- **场景偏差**：房间漫游视频主要来自房地产展示，多为整洁、无遮挡、光线良好的环境，不能完全代表真实家庭场景的杂乱、动态或夜间情况，可能限制模型的现实泛化。
- **评估覆盖局限**：实验只基于NaviLLM一个模型，未展示在其他VLN模型（如HAMT、DUET）上的增益，数据有效性可能模型相关。
- **零样本性能仍有限**：虽然在开源模型中表现突出，但与商用LLM（如GPT-4、MapGPT）相比仍有明显差距，且实验仅使用R2R数据集，缺乏其他任务的零样本验证。
- **计算资源未报告**：未提供训练/重建的具体算力与时间，影响了复现和可扩展性评估。
- **缺少动作空间细节**：虽然动作增强轨迹使用了真实连续帧，但并未提供与真实机器人运动学（如转向半径、速度变化）对齐的约束，而只是基于相机轨迹的近似。

---

（完）
