---
title: "3D-Mem: 3D Scene Memory for Embodied Exploration and Reasoning"
title_zh: 3D-Mem：面向具身探索与推理的3D场景记忆
authors: "Yang, Yuncong, Yang, Han, Zhou, Jiachen, Chen, Peihao, Zhang, Hongxin, Du, Yilun, Gan, Chuang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yang_3D-Mem_3D_Scene_Memory_for_Embodied_Exploration_and_Reasoning_CVPR_2025_paper.pdf"
tags: ["query:vln-memory"]
score: 9.0
evidence: 面向具身智能体的3D场景记忆框架，支持长期空间记忆与探索
tldr: 具身智能体在长期复杂环境中探索与推理需要紧凑、信息丰富的三维场景表示，现有对象级场景图谱过度简化空间关系且缺乏记忆管理机制。本文提出3D-Mem，通过多视角记忆快照构建三维场景记忆，以支持持续的主动探索和管理空间记忆。该方法能够更好地支撑长时自主性和细粒度空间推理，为具身智能体的长期导航与记忆研究提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1453, \"height\": 922}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1415, \"height\": 673}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 623}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 691, \"height\": 519}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 535}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 610, \"height\": 330}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yang-3d-mem-3d-scene-memory-for-embodied-exploration-and-reasoning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 606}]"
motivation: 现有三维场景表示过度简化空间关系且缺乏长期记忆管理，难以支撑长时具身探索与推理。
method: 提出3D-Mem框架，利用多视角Memory Snapshots构建动态三维场景记忆，支持主动探索与记忆管理。
result: 在具身探索与空间推理任务中增强了复杂空间关系的理解，提升了长期自主性。
conclusion: 3D场景记忆是突破具身智能长时导航与推理瓶颈的有效手段。
---

## Abstract
Constructing compact and informative 3D scene representations is essential for effective embodied exploration and reasoning, especially in complex environments over extended periods. Existing representations, such as object-centric 3D scene graphs, oversimplify spatial relationships by modeling scenes as isolated objects with restrictive textual relationships, making it difficult to address queries requiring nuanced spatial understanding. Moreover, these representations lack natural mechanisms for active exploration and memory management, hindering their application to lifelong autonomy. In this work, we propose 3D-Mem, a novel 3D scene memory framework for embodied agents. 3D-Mem employs informative multi-view images, termed Memory Snapshots, to capture rich visual information of explored regions. It further integrates frontier-based exploration by introducing Frontier Snapshots--glimpses of unexplored areas--enabling agents to make decisions by considering both known and potential new information. To support lifelong memory in active exploration settings, we present an incremental construction pipeline for 3D-Mem, as well as a memory retrieval technique for memory management. Experimental results on three benchmarks demonstrate that 3D-Mem significantly enhances agents' exploration and reasoning capabilities in 3D environments, highlighting its potential for advancing applications in embodied AI.

---

## 论文详细总结（自动生成）

# 3D-Mem：面向具身探索与推理的3D场景记忆——论文总结

## 1. 核心问题与整体含义（研究动机与背景）

**研究问题**：具身智能体在复杂3D环境中长期运行（lifelong autonomy）时，需要一个既紧凑又信息丰富的3D场景记忆模块来存储空间与语义信息，以支持高效的探索与推理。当前的两类主流场景表示均存在明显缺陷：

- **对象中心的3D场景图表示（如ConceptGraphs、3D Scene Graph）**：将场景建模为孤立对象节点和受限文本关系边，严重过度简化了空间关系。面对需要细粒度空间理解的问题——例如判断"扶手椅前方是否有足够空间放置咖啡桌"——仅凭文本关系和3D边界框难以量测自由空间或确定朝向性空间关系。
- **稠密3D表示（如点云、神经场）**：计算开销大、随场景增长缺乏可扩展性；且当下基础模型（LLM/VLM）对稠密3D模态的推理能力因训练数据缺乏而明显弱于图像和文本。
- **无法表示未探索区域**：已有两类表示都不能建模agent尚未访问的区域，故无法支持主动探索（active exploration），难以支撑agent利用场景记忆扩展知识并达成具身任务目标。

**核心思路**：作者提出 **3D-Mem**——一种基于多视角图像快照（snapshots）的3D场景记忆框架，将已探索区域表示为"内存快照"（Memory Snapshots）、未探索区域表示为"前沿快照"（Frontier Snapshots），借助VLM的图像推理能力，同时解决空间信息丰富性、主动探索和终身记忆管理三大问题。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 2.1 核心思想

- **用图像代替对象/点云作为记忆载体**：一张快照图像自身就包含丰富、鲁棒的视觉信息，可以同时涵盖前景对象、对象间空间关系及背景房间级上下文，比文本化的对象关系描述更完整，也天然适配近年在图像上推理能力日益增强的VLM。
- **Memory Snapshot（内存快照）**：定义为 `S_k = ⟨O_{S_k}, I_{S_k}⟩`，其中 `I_{S_k}` 是一帧候选观测图像，`O_{S_k}` 是该图像中所有共可见对象构成的簇。所有快照的对象簇覆盖全部检测对象、两两不重叠。
- **Frontier Snapshot（前沿快照）**：将经典frontier-based exploration的"前沿"—扩展到快照表示：`F = ⟨r, p, I_obs⟩`，包含未探索区域r、可导航位置p和朝向该区域的图像观测。前沿快照与内存快照同为原始图像，可直接供VLM作为视觉输入，使agent决策时同时考虑已知信息和潜在新信息。

### 2.2 关键技术细节

- **共可见性聚类（Co-Visibility Clustering，Algorithm 1）**：
  1. 初始化聚类集合C = {全部对象集合O}，内存快照集合S = ∅；
  2. 每次取C中最大的未分配对象簇O*，在所有帧候选中寻找能完全包含O*的帧I*；
  3. 若存在多个候选帧，用评分函数 `F(I_i) = |O_{I_i}|` 选择包含对象最多的帧（并列时取检测置信度和最高的帧），生成快照 `S* = ⟨O*, I*⟩`；
  4. 若无可行帧，用K-Means按2D水平位置把O*分裂为两个子簇，继续迭代；
  5. 所有对象分配完毕后，合并共享同一帧候选的多个快照，得到最终紧凑记忆表示。
- **增量构建（Incremental Construction）**：在探索每一步t，agent获取新观测后，只对"当前帧检测到的对象"以及"这些对象已归属的旧快照"进行重新聚类，而非对全量对象重跑算法，从而支持实时更新。对象集合更新为 `O_t = O_{t−1} ∪ O`，记忆集合为 `S_t = (S_{t−1} \ S_prev) ∪ Cluster(O_input, I_t)`。
- **记忆检索——Prefiltering**：当记忆规模增长后，将所有对象类别与问题一起交给VLM，让其输出与任务最相关的对象类别（取top-K，K为超参数），过滤掉不包含这些类别的记忆快照，显著降低VLM的输入规模与计算开销。
- **导航策略**：VLM每步决策选择探索某个前沿快照或直接作答；若探索，则用Habitat-sim的pathfinder在已探索区域内导航至目标前沿位置（移动距离上限1.0m，目标范围内0.5m）。

## 3. 实验设计：数据集、Benchmark与对比方法

### 3.1 实验一：主动具身问答（A-EQA）

- **数据集**：HM3D场景，OpenEQA基准中的A-EQA，557题/63场景；作者评估了184题子集（OpenEQA官方子集）。
- **任务设定**：agent在未知场景初始化，需主动探索后回答开放词汇问题（对象识别、功能推理、空间理解）。
- **指标**：LLM-Match（GPT-4对预测答案与真实答案评分1-5，映射至0-100）、LLM-Match SPL（对探索路径长度加权）。
- **对比方法**：盲LLM（GPT-4/GPT-4o）、Question-agnostic探索方法（CG/SVM场景图描述、LLaVA-1.5帧描述、Multi-Frame多帧直接输入）、VLM探索方法（Explore-EQA、ConceptGraph w/ Frontier Snapshots、3D-Mem）、人类表现。
- **VLM选择**：GPT-4o（OpenAI API）。

### 3.2 实验二：情景记忆具身问答（EM-EQA）

- **数据集**：OpenEQA的EM-EQA，1600+问题/152个ScanNet与HM3D场景；提供离线RGB-D轨迹和相机位姿，**无需探索**，纯测试记忆表示的效率。
- **对比方法**：盲LLM、CG/SVM/Frame Caption文本表示、Multi-Frame（线性采样2-6帧直接输入GPT-4o）、3D-Mem。
- **指标**：LLM-Match、平均输入帧数（Frame Efficiency）。

### 3.3 实验三：GOAT-Bench（多模态终身导航）

- **数据集**：GOAT-Bench "Val Unseen" split，36场景、278个连续导航子任务（1/10子集）。
- **任务设定**：agent在同一场景中顺序导航至多个目标对象（目标为类别名、语言描述或目标图像）。
- **指标**：Success Rate、SPL。
- **对比方法**：GOAT-Bench自带RNN强化学习基线（Modular GOAT、Modular CLIP on Wheels、SenseAct-NN等）、Explore-EQA、ConceptGraph w/ Frontier Snapshots、3D-Mem及其消融变体（3D-Mem w/o memory）；VLM使用了GPT-4o和LLaVA-7B。

### 3.4 消融与效率分析

- 消融变体：3D-Mem w/o memory（每个子任务后清空记忆）用于验证终身记忆的有效性。
- 效率指标：每episode生成的memory snapshot数量 vs. 原始观测数量、prefiltering后保留数量（A-EQA：39.76个观测→10.94个快照→prefilter后3.26个；GOAT-Bench：91.37个观测→16.58个快照→prefilter后4.66个）。

## 4. 资源与算力

**论文正文未明确报告**：

- 未说明使用的GPU型号、数量；
- 未说明训练时长（3D-Mem本身不涉及模型训练，属于免训练/零样本框架）；
- 未说明推理时间或token成本；
- VLM采用GPT-4o闭源API，具体调用次数和费用未披露。

需要指出的是，完整的资源与算力细节在论文主文的10页篇幅中并未展开。

## 5. 实验数量与充分性

### 实验覆盖面

- **3个benchmark**覆盖了三种典型任务范式：
  1. 主动探索+推理（A-EQA）；
  2. 纯记忆表示效率（EM-EQA，无需探索）；
  3. 终身连续导航（GOAT-Bench）。
- 在A-EQA与GOAT-Bench上均使用了两组VLM（GPT-4o和LLaVA-7B，后者仅GOAT-Bench），验证了对不同VLM的兼容性。
- 在EM-EQA上额外做了帧效率对比（3D-Mem vs. Multi-Frame在不同帧数下的LLM-Match），展示了紧凑性。
- 消融实验：3D-Mem w/o memory（GOAT-Bench）验证了记忆系统价值；Pre-filtering的K值等超参数分析在Appendix 13中报告（正文未展开）。

### 充分性评估

- **优势方面**：三个场景互补（有探索/无探索/终身连续），VLM选择多样，与当前最强的相关基线（Explore-EQA、ConceptGraph w/ Frontier）直接对比，且对基线做了公平适配（如为ConceptGraph替换快照而非用原始设置，为Explore-EQA增加GT grounding的成功判定）。
- **不足方面**：
  1. 两个benchmark均只评估了子集（184/557问，1/10的GOAT-Bench），全量结果仅在附录中提及；
  2. 部分OpenEQA基线（如CG Captions、SVM Captions）在全文上评估，与3D-Mem的子集结果不完全可比（论文在表格中已用符号标注）；
  3. 消融仅做了"有无记忆"一项，对聚类算法、快照数量、prefiltering K值等关键组件的系统消融依赖附录，且正文未展示主要结果；
  4. 未与稠密3D表示（点云/神经场）类方法进行直接对比。

## 6. 主要结论与发现

1. **快照图像优于对象级表示**：在A-EQA上，3D-Mem（LLM-Match 52.6）大幅优于ConceptGraph w/ Frontier Snapshots（47.2）和Explore-EQA（46.9）；在SPL上优势更显著（42.0 vs. 33.3 vs. 23.4），表明图像快照在复杂空间推理问题中确实比文本化对象图更有效。
2. **紧凑性是最大亮点**：EM-EQA上3D-Mem仅用平均约3帧就达到57.2的LLM-Match，同时显著优于同样使用3帧左右的Multi-Frame（48.1），验证了"哪些帧值得保留"比"多帧输入"更重要。
3. **终身记忆有效**：GOAT-Bench上3D-Mem（69.1/48.9）显著优于清空记忆的3D-Mem w/o memory（58.6/38.5），证明跨子任务的记忆积累显著提升导航效率。
4. **3D-Mem可直接利用VLM的图像推理能力**，无需针对3D模态的专门微调模型，是相对3D-LLM等方法的实际优势。
5. 3D-Mem可作为任务无关的通用3D场景记忆模块，适配QA、目标导航、终身导航等不同任务。

## 7. 优点

- **方法设计新颖且简洁**：用"图像快照+共可见性聚类"替代对象图，直接绕开了"将空间关系量化为文本"这一信息瓶颈；一个图像同时解决对象特征、空间关系和背景上下文的存储问题。
- **统一已探索/未探索区域表示**：将记忆快照与前沿快照统一为图像形式，让VLM的探索决策与回答决策使用相同的模态输入，架构自然简洁。
- **强调"记忆管理"而非仅"场景表示"**：增量构建+Prefiltering检索机制，使记忆规模可控，真正面向终身学习场景；实测压缩比高（约1/4到1/20）。
- **无需训练**：纯零样本框架，仅需VLM推理，落地成本低。
- **实验验证扎实**：三个benchmark任务互补，对基线的适配较为公平，并提供人类表现作为上界参考。

## 8. 不足与局限

- **依赖VLM的感知与推理质量**：3D-Mem的性能上限取决于所用VLM（如GPT-4o）对图像的理解能力；VLM可能对图像产生幻觉或忽略细节，且闭源API的版本更迭会影响可复现性。
- **共可见性聚类的合理性依赖对象检测质量**：对象检测漏检、错误匹配可能导致快照划分不理想；K-Means按2D水平位置分裂可能破坏有意义的垂直空间关系（如"在……上面"）。
- **Prefiltering存在信息丢失风险**：若VLM在排序对象类别时遗漏关键对象，则对应快照会被过滤掉，可能影响后续决策；top-K作为超参数需要调优。
- **实验覆盖不完整**：主文以子集评估为主（A-EQA 184/557，GOAT-Bench 1/10），全量结果放在附录，削弱了主文实验的完整性；与OpenEQA全文基线的对比存在题目范围不一致问题。
- **未与其他记忆类方法（如拓扑图TSGM、RoboHop）做直接定量对比**，仅在相关工作提及。
- **应用限制**：框架假设可用碰撞避免的路径规划器（Habitat pathfinder），在真实机器人场景中还需考虑位姿误差与动态障碍物；目标为QA等离线问答型任务时，探索终止条件依赖VLM的置信判断，可能不适用于所有场景。
- **成本问题**：每步探索都调用

继续补全上一条未完成内容：

- **成本问题**：每步探索都调用VLM进行视觉理解与决策，当场景规模大、探索步数多时，闭源API（如GPT-4o）的调用次数与token消耗会显著增加。尽管Prefiltering降低了单步输入帧数，但整个探索过程仍需反复调用模型，且OpenAI等API按用量计费，实际部署的经济成本可能成为限制因素。若改用本地开源VLM（如LLaVA），虽然降低API成本，但推理性能可能下降，需在效果与成本之间权衡。

此外，还存在以下未尽局限：

- **缺少动态场景支持**：3D-Mem假设场景在探索过程中是静态的，所有快照和对象位置在任务期间保持不变。若环境中有移动物体或动态变化，记忆会逐渐失效，需要额外的更新机制，而论文未对此进行讨论或实验。
- **对语言问题分词与对象类别关联的敏感性**：Prefiltering依赖VLM从问题中提取相关对象类别，若问题表述较为抽象或隐含关系（如“这个房间适合做什么？”），VLM可能无法准确映射到具体对象类别，导致关键快照被过滤。

## 9. 总结与展望

3D-Mem为具身智能体的长期场景记忆提供了一种新颖且务实的范式——以多视角图像快照为核心，结合共可见性聚类实现紧凑存储，并将未探索区域统一表示为前沿快照，从而在单一框架内同时支持主动探索、空间推理与终身记忆管理。其在三个不同benchmark上的实验结果表明，图像快照比对象图表示更具信息密度，也比直接采样多帧更高效；终身记忆的积累能显著提升连续导航任务的性能。该方法的“免训练+即插即用”特性，使其具备较强的实际部署潜力。

未来工作可沿以下方向展开：
1. **自适应快照更新**：引入动态场景中的记忆刷新机制，处理环境变化与长期任务中的信息过时；
2. **更强的基础模型适配**：评估与开源VLM（如LLaVA系列、Qwen-VL等）的兼容性，降低闭源依赖；
3. **与稠密3D表示的融合**：探索图像快照与点云/隐式神经场结合的混合表示，兼顾细节与可扩展性；
4. **跨任务记忆共享**：将3D-Mem泛化到更多具身任务（如操作、交互式问答），并验证其作为通用记忆模块的鲁棒性。

（完）
