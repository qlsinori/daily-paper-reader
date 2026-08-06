---
title: "3D-Mem: 3D Scene Memory for Embodied Exploration and Reasoning"
title_zh: 3D-Mem：面向具身探索与推理的3D场景记忆
authors: "Yang, Yuncong, Yang, Han, Zhou, Jiachen, Chen, Peihao, Zhang, Hongxin, Du, Yilun, Gan, Chuang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yang_3D-Mem_3D_Scene_Memory_for_Embodied_Exploration_and_Reasoning_CVPR_2025_paper.pdf"
tags: ["query:semantic-map"]
score: 9.0
evidence: 面向具身探索与推理的3D场景记忆框架
tldr: 具身智能体在复杂环境中长期工作，需要紧凑且信息丰富的3D场景表示。现有基于物体中心的场景图将场景简化为孤立物体与文本关联，难以支持细粒度空间理解，也缺乏主动探索与记忆管理机制。为此提出3D-Mem框架，采用信息量丰富的多视角图像（即记忆快照）构建3D场景记忆，支持智能体主动探索并长期维护场景信息。实验证明该方法能显著提升场景理解与空间推理能力，为终身具身智能提供更自然的记忆基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1453, \"height\": 922, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1415, \"height\": 673, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 623, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 691, \"height\": 519, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 535, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 610, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 606, \"label\": \"Table\"}]"
motivation: 现有3D场景图表示过于简化空间关系，缺少主动探索与长期记忆管理机制，难以支撑终身具身智能。
method: 使用多视角记忆快照构建紧凑的3D场景记忆框架，支持主动探索和记忆长期维护。
result: 在具身探索与空间推理任务上相比场景图等方法显著提升理解精度和推理能力。
conclusion: 3D场景记忆可有效支持长期探索和精细空间理解，是终身具身智能的重要组件。
---

## Abstract
Constructing compact and informative 3D scene representations is essential for effective embodied exploration and reasoning, especially in complex environments over extended periods. Existing representations, such as object-centric 3D scene graphs, oversimplify spatial relationships by modeling scenes as isolated objects with restrictive textual relationships, making it difficult to address queries requiring nuanced spatial understanding. Moreover, these representations lack natural mechanisms for active exploration and memory management, hindering their application to lifelong autonomy. In this work, we propose 3D-Mem, a novel 3D scene memory framework for embodied agents. 3D-Mem employs informative multi-view images, termed Memory Snapshots, to capture rich visual information of explored regions. It further integrates frontier-based exploration by introducing Frontier Snapshots--glimpses of unexplored areas--enabling agents to make decisions by considering both known and potential new information. To support lifelong memory in active exploration settings, we present an incremental construction pipeline for 3D-Mem, as well as a memory retrieval technique for memory management. Experimental results on three benchmarks demonstrate that 3D-Mem significantly enhances agents' exploration and reasoning capabilities in 3D environments, highlighting its potential for advancing applications in embodied AI.

---

## 论文详细总结（自动生成）

# 论文详细总结：3D-Mem

## 1. 核心问题与整体含义（研究动机与背景）

具身智能体在复杂 3D 环境中长期运行时，需要紧凑而信息丰富的 3D 场景记忆来支撑探索与推理。现有场景表示方法主要存在两大流派，但均有显著缺陷：

- **以物体为中心的 3D 场景图**（如 ConceptGraphs、3D Scene Graph）：将场景建模为孤立物体节点 + 文本化关系边，过度简化了物体间的空间关系，丢失关键空间信息，难以回答需要细粒度空间理解的问题（例如“扶手椅前方是否有足够空间放咖啡桌”）。
- **稠密 3D 表示**（如点云、神经辐射场）：计算开销大，场景增长时缺乏可扩展性；且现有基础模型对稠密 3D 模态的推理能力不足。
- **共同缺陷**：两类表示都无法建模未探索区域，不能支持智能体的主动探索，缺乏长期记忆管理机制，难以应用于终身自主（lifelong autonomy）场景。

为此，论文提出 **3D-Mem**——一种面向具身智能体的 3D 场景记忆框架，用多视角图像（Memory Snapshots）表示已探索区域，用前沿快照（Frontier Snapshots）表示未探索区域，使智能体既能利用已有记忆完成任务，也能主动探索获取新信息。

## 2. 方法论

### 2.1 核心思想
用一个图像本身来代表一小块场景区域——因为单张图像天然包含该区域内所有共视物体（co-visible objects）及其背景上下文，远比文本化场景图保留更丰富的视觉与空间信息，且可直接作为 VLM 的视觉输入。

### 2.2 Memory Snapshot（记忆快照）
- 定义：每个记忆快照 `S_k = <O_Sk, I_Sk>`，由一张帧候选图像 `I_Sk` 和该图像中可见的一组物体聚类 `O_Sk` 组成。
- 要求：所有快照的物体集合互不相交且覆盖全部检测物体。
- **Co-Visibility Clustering 算法**（Algorithm 1）：
  1. 初始化聚类集合 C = {全部物体 O}，快照集合 S = ∅；
  2. 每次取出最大的未分配聚类 O*，在所有帧候选中寻找能完整包含 O* 中物体的帧 I*（即 O* ⊆ O_I*）；
  3. 若存在多个候选帧，用打分函数 `F(I) = |O_I|` 优先选包含物体最多的帧，并列时取检测置信度和最高者；
  4. 若无可行帧，则基于物体 2D 水平位置 (x,y) 用 K-Means 将 O* 分裂为两个子聚类继续迭代；
  5. 全部物体分配完毕后，合并共用同一帧的多个快照，得到最终紧凑的 3D-Mem 表示。

### 2.3 Frontier Snapshot（前沿快照）
- 定义：`F = <r, p, I_obs>`，r 为未探索区域，p 为可导航位置，I_obs 为朝向该区域拍摄的图像观测。
- 作用：将传统 frontier-based exploration 中的“前沿”扩展为图像快照，使 VLM 能够直接“看到”未探索区域的走廊、房间等结构线索，从而做出更有依据的探索决策。

### 2.4 增量式构建（Incremental Construction）
- **物体更新**：每步捕获 N 个 egocentric 视图，提取物体（设定 `max dist` 阈值只加入附近物体），与历史物体集合并更新。
- **记忆快照更新**：只对当前帧新检测物体及相关历史快照中的物体进行增量聚类，避免对整个场景重新聚类。
- **前沿快照更新**：移除已探索完的前沿、对新出现/变化的前沿重新拍照。

### 2.5 记忆检索：Prefiltering（预过滤）
- 将问题连同所有物体类别交给 VLM，由 VLM 按相关度排序并保留 top-K 个类别，仅保留包含这些类别的记忆快照作为后续输入。
- 例如在 A-EQA 上，每 episode 平均生成 10.94 个记忆快照（来自 39.76 个观测），经 K=10 预过滤后仅保留 3.26 个快照，显著降低计算开销和噪声。

### 2.6 探索与推理
- VLM 智能体综合记忆快照与前沿快照，决定是选择某个前沿继续探索，还是基于当前记忆直接回答问题/导航到目标物体。
- 导航策略：选择前沿后，朝其位置 p 前进，最多移动 1.0m 或到达 0.5m 范围内即停；假设存在无碰撞路径规划器（实验中使用 Habitat-sim 的 pathfinder）。

## 3. 实验设计

### 3.1 Benchmark 与数据集
| Benchmark | 数据集 | 规模 | 评估方式 |
|---|---|---|---|
| A-EQA（主动具身问答） | HM3D，63 个场景，557 问 | 因资源限制评估 184 问子集（另在 Appendix 6 报告全量结果） | LLM-Match、LLM-Match SPL |
| EM-EQA（情景记忆具身问答） | ScanNet + HM3D，152 场景，1600+ 问 | 全量 | LLM-Match、平均帧数 |
| GOAT-Bench（终身多模态导航） | Val Unseen 分割的 1/10 子集，36 场景，278 导航子任务 | 子集（全量测试集在 Appendix 6） | Success Rate、SPL |

### 3.2 对比方法
- **盲 LLM**：GPT-4、GPT-4o 无视觉输入直接回答。
- **问题无关探索基线**（来自 OpenEQA）：CG Scene-Graph Captions、SVM Scene-Graph Captions、LLaVA-1.5 Frame Captions、Multi-Frame（线性抽样 75 帧）。
- **VLM 探索基线**：Explore-EQA、ConceptGraph（CG）w/ Frontier Snapshots。
- **GOAT-Bench 自带基线**：Modular GOAT、Modular CLIP on Wheels、SenseAct-NN Skill Chain / Monolithic（基于 RL 的 RNN 模型）。
- **消融**：3D-Mem w/o memory（每个子任务后清空记忆）。
- **VLM 选择**：GPT-4o（主）、LLaVA-7B（消融）。

### 3.3 主要实验结果
- **A-EQA**：3D-Mem 取得 LLM-Match 52.6、SPL 42.0，显著优于 Explore-EQA（46.9/23.4）和 CG w/ Frontier Snapshots（47.2/33.3）及所有 OpenEQA 基线。
- **EM-EQA**：仅用 3.1 帧平均输入，LLM-Match 57.2，远超 Multi-Frame 的 48.1（3.0 帧）及所有 caption 类表示（34–38），帧效率显著更优。
- **GOAT-Bench**（GPT-4o）：Success Rate 69.1、SPL 48.9，优于 CG w/ Frontier Snapshots（61.5/45.3）、Explore-EQA（55.0/37.9）以及 3D-Mem w/o memory（58.6/38.5）；LLaVA-7B 下同样验证记忆系统有效（49.6/29.4 vs 40.6/14.6）。

## 4. 资源与算力

- **论文正文未明确报告**具体 GPU 型号、数量或训练时长。
- 原因在于：3D-Mem 不是端到端训练方法，而是基于预训练 VLM（GPT-4o 通过 OpenAI API 调用、LLaVA-7B 推理）的即插即用记忆框架，主要算力开销在物体检测/分割（ConceptGraph 流程）与 VLM 推理上。
- 论文提到因“资源限制”（resource limitations），A-EQA 和 GOAT-Bench 仅在子集上评估，暗示完整评估的计算成本较高，但未给出量化说明。

## 5. 实验数量与充分性

- **覆盖三个基准**，分别对应主动探索+推理（A-EQA）、纯记忆表示能力（EM-EQA）、终身导航记忆（GOAT-Bench），任务类型多样，评估角度较全面。
- **消融实验**：GOAT-Bench 上对比了 3D-Mem 与 3D-Mem w/o memory，验证了记忆在终身场景中的必要性；Appendix 13 还有更详细的消融（正文引用但未展开）。
- **对比公平性存在一定瑕疵**：A-EQA 中 3D-Mem 与部分 VLM 基线（带 † 标记）在 184 问子集上评估，但 OpenEQA 原始基线（CG Captions 等）在完整 557 问集上报告，两者数据分布不完全对齐；作者也提到子集评估受限于算力。
- **实验总体充分**：多基线与多任务验证了方法的核心主张，但全量评估缺失（虽在 Appendix 6 补充）仍是覆盖面不足。

## 6. 主要结论与发现

1. **图像记忆优于文本/物体级记忆**：多视角快照图像保留了物体间空间关系与房间上下文，使 VLM 能回答需要细粒度空间理解的复杂问题；3D 场景图的文本化关系表示在此类任务上明显受限。
2. **紧凑性显著**：3D-Mem 能以极少量快照（约 3–5 个经预过滤后的图像）替代大量原始观测帧，在 EM-EQA 上以 3.1 帧超越 Multi-Frame 的 3.0 帧且得分更高，综合帧效率优于线性抽样。
3. **前沿快照有效支持主动探索**：将未探索区域也表示为图像，使 VLM 能基于视觉线索选择有希望的探索方向，显著提升探索效率（A-EQA SPL 42.0 vs 23.4）。
4. **记忆对终身学习至关重要**：清空记忆（3D-Mem w/o memory）后 GOAT-Bench 成功率与 SPL 均大幅下降，验证了跨任务记忆累积的价值。
5. **3D-Mem 是一种通用的场景记忆**：可适配具身问答、物体导航等多种任务，且增量构建 + 预过滤机制使其能随探索规模扩展。

## 7. 优点

- **新颖的表示范式**：用图像快照替代文本场景图/稠密 3D 特征作为记忆单元，天然兼容 VLM 的感知与推理能力，无需训练、即插即用。
- **统一处理已知与未知区域**：Memory Snapshots 与 Frontier Snapshots 均为图像，VLM 可同时考虑已探索信息和潜在新信息做决策，设计优雅。
- **强调终身性与可扩展性**：增量聚类避免重复计算，Prefiltering 控制输入规模，使记忆在长期探索中保持高效。
- **实验设计较全面**：覆盖主动探索、记忆表示、终身导航三类场景，并用 GPT-4o 与 LLaVA-7B 两种 VLM 验证泛化性。
- **报告了记忆压缩的具体量化数据**（如 39.76 观测 → 10.94 快照 → 3.26 有效输入），支撑紧凑性主张。

## 8. 不足与局限

- **评估规模受限**：A-EQA 和 GOAT-Bench 仅报告子集结果（虽然 Appendix 6 补充全量），大规模基准上的结论有待完整验证。
- **对比公平性风险**：OpenEQA 基线在全量集上评估而部分方法在子集上评估，子集选择可能引入偏差；此外 GPT-4o 作为 VLM 的闭源 API 调用难以完全复现。
- **依赖上游感知管线**：物体检测/分割依赖 ConceptGraph 流程，其错误会传播到快照聚类与最终推理；`max dist` 超参也影响记忆质量。
- **依赖 VLM 能力**：方法效果受限于所选 VLM（GPT-4o 等）的视觉理解与推理水平，对空间关系理解较弱的 VLM 可能大幅降低性能。
- **缺乏计算资源细节**：未报告 GPU 数量、推理耗时、API 成本等，难以评估实际部署开销。
- **应用限制**：假设存在无碰撞路径规划器；Prefiltering 的 top-K 超参需人工设定；快照图像数量与场景规模的关系在更大场景（如整层楼）中尚不明确。

（完）
