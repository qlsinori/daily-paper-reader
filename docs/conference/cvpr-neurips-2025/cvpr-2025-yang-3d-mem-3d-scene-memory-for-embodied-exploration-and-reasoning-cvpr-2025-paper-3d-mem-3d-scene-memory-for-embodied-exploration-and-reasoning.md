---
title: "3D-Mem: 3D Scene Memory for Embodied Exploration and Reasoning"
title_zh: 3D-Mem：用于具身探索与推理的三维场景记忆
authors: "Yang, Yuncong, Yang, Han, Zhou, Jiachen, Chen, Peihao, Zhang, Hongxin, Du, Yilun, Gan, Chuang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yang_3D-Mem_3D_Scene_Memory_for_Embodied_Exploration_and_Reasoning_CVPR_2025_paper.pdf"
tags: ["query:vln-memory"]
score: 9.0
evidence: 面向具身探索与推理的三维场景记忆
tldr: 面向复杂环境中的长期具身探索与推理，本文提出三维场景记忆框架3D-Mem，利用多视角信息丰富的Memory Snapshot表示场景，支持主动探索与记忆管理。相比对象级场景图，它保留了更细微的空间关系，能回答需要空间理解的查询。实验显示3D-Mem在具身探索和推理任务上表现更优，可支撑长期自主性，为场景记忆建模提供了新范式。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1453, \"height\": 922}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1415, \"height\": 673}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 623}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 691, \"height\": 519}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 535}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 610, \"height\": 330}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 606}]"
motivation: 现有对象级3D场景图把场景简化为孤立物体与受限文本关系，难以支持细粒度空间查询和主动记忆管理，长期自主性受限。
method: 提出3D-Mem框架，以Memory Snapshot多视角图像作为紧凑场景记忆，并结合探索与记忆管理机制。
result: 在具身探索与空间推理评测中，3D-Mem表现出更精细的空间理解和更好的记忆利用效果。
conclusion: 该工作为长时间具身自主提供了一个可扩展的三维场景记忆表示及管理方法。
---

## Abstract
Constructing compact and informative 3D scene representations is essential for effective embodied exploration and reasoning, especially in complex environments over extended periods. Existing representations, such as object-centric 3D scene graphs, oversimplify spatial relationships by modeling scenes as isolated objects with restrictive textual relationships, making it difficult to address queries requiring nuanced spatial understanding. Moreover, these representations lack natural mechanisms for active exploration and memory management, hindering their application to lifelong autonomy. In this work, we propose 3D-Mem, a novel 3D scene memory framework for embodied agents. 3D-Mem employs informative multi-view images, termed Memory Snapshots, to capture rich visual information of explored regions. It further integrates frontier-based exploration by introducing Frontier Snapshots--glimpses of unexplored areas--enabling agents to make decisions by considering both known and potential new information. To support lifelong memory in active exploration settings, we present an incremental construction pipeline for 3D-Mem, as well as a memory retrieval technique for memory management. Experimental results on three benchmarks demonstrate that 3D-Mem significantly enhances agents' exploration and reasoning capabilities in 3D environments, highlighting its potential for advancing applications in embodied AI.

---

## 论文详细总结（自动生成）

# 3D-Mem：用于具身探索与推理的三维场景记忆 —— 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：具身智能体在复杂3D环境中长期运行时，需要一种**紧凑、信息丰富且可终身更新**的场景记忆表示，以同时支持主动探索与空间推理。
- **现有方法的局限**：
  - **对象级3D场景图**（如ConceptGraphs）：将场景建模为孤立对象以及用受限文本描述的对象间关系，过度简化了空间结构，导致无法回答需要细微空间理解的问题（例如“扶手椅前方是否有足够空间放置茶几？”）。
  - **稠密3D表示**（点云、神经场等）：计算开销大、可扩展性差，且当前基础模型（VLM/LLM）对稠密3D模态的推理能力不足。
  - **两类方法的共同缺陷**：都无法表示未探索区域，缺少支持主动探索与记忆管理（添加、检索、更新）的自然机制，难以支撑终身自主性。
- **论文含义**：提出以**多视角图像快照**为核心的3D场景记忆范式，为具身智能的持续学习与长期自主提供更契合基础模型推理能力的场景表征方案。

---

## 2. 论文提出的方法论

### 2.1 核心思想

用一组**多视角快照图像**替代对象级文本图或稠密3D特征，来覆盖整个场景信息：

- **Memory Snapshot（记忆快照）**：用一张图像表示一个**共视对象簇**以及其背景环境。图像天然保留了对象间空间关系、房间级上下文等丰富视觉信息，可以被VLM直接理解。
- **Frontier Snapshot（前沿快照）**：将传统frontier-based探索中的“前沿”扩展为图像形式，即从未探索区域拍摄的观测图像，使智能体能够在**已知信息**与**潜在新信息**之间进行决策。

### 2.2 关键技术细节

1. **Co-Visibility Clustering（共视聚类）**：
   - 输入：所有检测到的对象集合、所有帧候选（图像+该帧可见对象集合）。
   - 流程（如Algorithm 1所示）：
     - 初始化簇集合C为全体对象，快照集合S为空；
     - 每次取出最大的对象簇O*，寻找能完整覆盖O*的帧候选I*；
     - 若存在，按打分函数F（优先对象数量多，其次检测置信度和高）选出最优帧，生成快照〈O*, I*〉；
     - 若不存在，使用K-Means按2D水平位置将O*分裂为两簇后继续迭代；
     - 最终合并共享同一帧的快照，得到紧凑的最终表示。
   - 输出：覆盖全部对象、对象在各快照间不重复的Memory Snapshot集合。

2. **增量构建（Incremental Construction）**：
   - 每步t仅对**新观测到的对象**以及它们可能关联的旧快照涉及的簇进行重新聚类，而非对全部历史对象重新聚类，从而支持实时更新。
   - 前向快照随occupancy map更新而同步添加、修改或删除。

3. **Prefiltering（记忆预筛选）**：
   - 决策时让VLM根据当前问题和所有已知对象类别，输出最相关的K个对象类别；
   - 只保留包含这些类别对象的记忆快照作为VLM的输入，**大幅降低token/帧数量与计算开销**，同时滤除与目标无关的噪音信息。

4. **探索与推理框架**：
   - 三个基准任务统一框架：若VLM认为已有记忆足以回答/完成目标，则直接作答/导航；否则选择最合适的前沿快照并导航前往，然后更新记忆、重新决策。
   - 导航假设有碰撞无碰撞路径规划器（实验中用Habitat-sim的pathfinder）。

---

## 3. 实验设计

### 3.1 数据集 / Benchmark

| Benchmark | 场景来源 | 规模 | 任务 |
| --- | --- | --- | --- |
| **A-EQA**（Active EQA） | HM3D | 557道题，论文评估184题子集 | 未知场景主动探索后回答开放式问题 |
| **EM-EQA**（Episodic-Memory EQA） | ScanNet + HM3D | 1600+题 | 给定轨迹的RGB-D观测与位姿，无需探索即可作答 |
| **GOAT-Bench** | Val Unseen 分集 | 36场景共278个子任务（1/10子集） | 多模态终身导航（按类别、语言描述或图像依次导航到多个目标） |

### 3.2 对比方法

- **盲LLM基线**：仅GPT-4/GPT-4o直接猜测答案。
- **问题无关探索基线**：ConceptGraph/Sparse Voxel Map语义图捕捉、LLaVA-1.5帧描述、Multi-Frame（直接输入约75帧）。
- **VLM探索基线**：Explore-EQA；ConceptGraph w/ Frontier Snapshots（用对象图像裁剪代替快照，其他设置保持一致）。
- **3D-Mem的变体**：3D-Mem w/o memory（每子任务后清除记忆）。
- **GOAT-Bench自带基线**：Modular GOAT、Modular CLIP on Wheels、SenseAct-NN（RL训练的RNN模型等）。

### 3.3 指标

- 使用GPT-4将预测答案与真值比较评分（1–5）映射为0–100的**LLM-Match**；
- 使用**LLM-Match SPL**（按路径长度加权）衡量探索效率；GOAT-Bench使用Success Rate与SPL。

---

## 4. 资源与算力

- **论文未明确给出**使用的GPU型号、数量、训练时长等算力信息。
- 仅能推断的点：
  - 主VLM为**GPT-4o（OpenAI API）**，附录提到也测试了**LLaVA-7B**；
  - 论文多次提到“due to resource limitations”，故A-EQA和GOAT-Bench均采用**子集评估**，说明作者存在一定算力约束；
  - 未涉及训练阶段（框架本身为免训练的感知+VLM决策管线）。

---

## 5. 实验数量与充分性

### 实验数量

- **三大Benchmark**：覆盖主动探索+推理（A-EQA）、纯场景记忆表示能力（EM-EQA）、终身导航记忆（GOAT-Bench）三个维度。
- **消融实验**：主要包括3D-Mem w/o memory、不同VLM（GPT-4o vs LLaVA-7B）、与ConceptGraph替换记忆模块的对比，另有附录中超参数K与更多消融。
- **对比基线**：每个benchmark有5–9个基线方法（含OpenEQA报告结果与GOAT-Bench官方基线），总体较充分。

### 客观性与公平性评估

- **优点**：在A-EQA和GOAT-Bench中，VLM探索类基线（Explore-EQA、CG w/ Frontier Snapshots）都被尽量改造成与3D-Mem一致的探索和回答管线，控制较为严格。
- **需要注意的偏差**：
  - A-EQA中3D-Mem只在184题子集上评估，而OpenEQA的盲LLM/CG等基线在557题全集上评估（表中也有*、†标注区分），**子集与全集的对比严格来说不完全对齐**；
  - Explore-EQA在GOAT-Bench上额外加了“目标在最终观测中可见即成功”的ground truth判定条件，**对基线有所增强**；
  - 论文提到3D-Mem在完整集上的结果放在附录，但正文主体依赖子集，可能在统计显著性上存疑（未报告方差或显著性检验）。
- 总体判断：实验设计**覆盖广、控制较好**，但受资源限制，部分对比的公平性和稳健性略有折扣。

---

## 6. 论文的主要结论与发现

- **A-EQA结果**：3D-Mem的LLM-Match达52.6，显著高于Explore-EQA（46.9）和CG w/ Frontier Snapshots（47.2）；LLM-Match SPL为42.0，而Explore-EQA仅23.4、CG仅33.3——表明3D-Mem在答案准确性和探索效率上双双领先。
- **EM-EQA结果**：3D-Mem只用平均3.1帧便取得LLM-Match 57.2，远超Multi-Frame（3.0帧，48.1）和所有基于文本描述的方法（约34–38）——证明**多视角快照图像比场景图文本/线性抽帧更适合作为3D场景记忆**。
- **GOAT-Bench结果**：3D-Mem在Success Rate（69.1）和SPL（48.9）上均优于Explore-EQA（55.0/37.9）和CG w/ Frontier Snapshots（61.5/45.3）；3D-Mem w/o memory相比完整版显著下降（58.6/38.5 vs 69.1/48.9），说明**跨任务保留记忆对终身导航至关重要**。
- **核心结论**：图像快照形式的3D场景记忆在信息密度、推理性能、可扩展性和与VLM的兼容性上均优于传统对象级或稠密3D表示，是一种更适用于终身具身智能的场景记忆方案。

---

## 7. 优点

- **表示方案新颖且自然**：“一张图像承载一个区域”的直觉简单有力，利用VLM强大的图像理解能力来提取空间关系，避开了3D场景图文本量化的信息瓶颈，也避开了VLM直接处理点云等非自然模态的能力不足。
- **同时覆盖已知与未知区域**：Memory Snapshot与Frontier Snapshot统一为图像形式，使VLM可以在“继续探索”和“利用已有知识”之间直接做视觉决策。
- **支持终身运行**：增量构建避免重复聚类；Prefiltering机制显著压缩输入规模（如A-EQA实验从39.76帧观测压缩到10.94个快照、预筛选后仅3.26个输入），使长期自主探索在计算上可行。
- **通用性强**：同一框架可适配主动EQA、情景记忆EQA和终身目标导航三种任务，只需调整提示词和目标形式。
- **出色的实验结果**：在三大benchmark中均大幅超越强基线，且对基线的消融设计合理，能清楚归因记忆模块的贡献。

---

## 8. 不足与局限

- **评估子集引入偏差风险**：A-EQA（184/557）和GOAT-Bench（1/10）均只用子集，结果可能与完整集存在差异；论文虽提及附录有完整集结果，但未在正文充分讨论子集选择可能带来的偏向。
- **基线对比不完全对齐**：部分基线来源于OpenEQA/GGOAT-Bench论文的原始数值，其探索长度、VLM版本、prompt等未完全统一，跨来源对比的公平性有限。
- **算力信息缺失**：未报告GPU型号、数量、推理耗时、API调用成本等，不利于他人复现和评估实际部署开销。
- **依赖闭源VLM**：核心决策依赖GPT-4o（OpenAI API），闭源模型更新会导致结果漂移，复现性受限；开源替代LLaVA-7B的效果明显更低，说明方法高度依赖VLM能力。
- **简化导航假设**：使用无碰撞规划器（Habitat pathfinder），未考虑真实机器人运动约束、动态障碍物、传感器噪音等现实问题。
- **对图像质量敏感**：光照差、遮挡严重或纹理稀疏的区域，快照图像可能包含的信息不足，VLM推理效果会打折扣。
- **场景类型局限**：实验仅涉及室内场景数据集，未能验证户外、大规模或动态场景中的记忆可扩展性。

---

（完）
