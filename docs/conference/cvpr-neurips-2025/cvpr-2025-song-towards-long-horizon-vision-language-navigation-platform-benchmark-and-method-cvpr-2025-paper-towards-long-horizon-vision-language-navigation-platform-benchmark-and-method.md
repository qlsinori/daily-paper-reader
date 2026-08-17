---
title: "Towards Long-Horizon Vision-Language Navigation: Platform, Benchmark and Method"
title_zh: 面向长时程视觉语言导航：平台、基准与方法
authors: "Song, Xinshuai, Chen, Weixing, Liu, Yang, Chen, Weikai, Li, Guanbin, Lin, Liang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Song_Towards_Long-Horizon_Vision-Language_Navigation_Platform_Benchmark_and_Method_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 明确研究基于自然语言指令的视觉语言导航与长时程规划
tldr: 现有视觉语言导航（VLN）方法主要针对单阶段任务，难以处理复杂动态环境中的多阶段长时程导航。为此，作者提出长时程视觉语言导航（LH-VLN）任务，强调跨连续子任务的长时规划与决策一致性。同时构建自动化数据生成平台NavGen和长时程规划推理基准LHPR-VLN，并给出相应方法，推动VLN向复杂现实任务迈进。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1546, \"height\": 641, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1540, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 705, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1625, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1658, \"height\": 385, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1309, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1756, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 821, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 202, \"label\": \"Table\"}]"
motivation: 现有VLN方法局限于单阶段导航，无法应对复杂动态环境中的多阶段长时程任务。
method: 提出LH-VLN任务，构建自动化数据平台NavGen与基准LHPR-VLN，并设计强调决策一致性的导航方法。
result: 新任务与基准能有效评估长时程规划能力，方法在长时程VLN上表现更优。
conclusion: 该工作为长时程视觉语言导航提供数据、基准和方法，拓展了VLN研究边界。
---

## Abstract
Existing Vision-Language Navigation (VLN) methods primarily focus on single-stage navigation, limiting their effectiveness in multi-stage and long-horizon tasks within complex and dynamic environments. To address these limitations, we propose a novel VLN task, named Long-Horizon Vision-Language Navigation (LH-VLN), which emphasizes long-term planning and decision consistency across consecutive subtasks. Furthermore, to support LH-VLN, we develop an automated data generation platform NavGen, which constructs datasets with complex task structures and improves data utility through a bidirectional, multi-granularity generation approach. To accurately evaluate complex tasks, we construct the Long-Horizon Planning and Reasoning in VLN (LHPR-VLN) benchmark consisting of 3,260 tasks with an average of 150 task steps, serving as the first dataset specifically designed for the long-horizon vision-language navigation task. Furthermore, we propose Independent Success Rate (ISR), Conditional Success Rate (CSR), and CSR weight by Ground Truth (CGT) metrics, to provide fine-grained assessments of task completion. To improve model adaptability in complex tasks, we propose a novel Multi-Granularity Dynamic Memory (MGDM) module that integrates short-term memory blurring with long-term memory retrieval to enable flexible navigation in dynamic environments. Our platform, benchmark and method supply LH-VLN with a robust data generation pipeline, comprehensive model evaluation dataset, reasonable metrics, and a novel VLN model, establishing a foundational framework for advancing LH-VLN.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **现有 VLN 的局限**：当前 Vision-Language Navigation（VLN）研究主要聚焦于单阶段、短时程导航任务，目标单一、动作序列有限，适用于受控环境，但难以应对真实世界中需要持续决策、动态重规划与跨长时间跨度的复杂任务。
- **现实需求缺口**：在自主助手、服务机器人等应用中，智能体需要在复杂动态环境中完成多阶段、上下文丰富的长时程任务，这要求其具备长期规划、跨子任务的一致决策能力与记忆保持能力。
- **三大关键挑战**：① 缺乏能够自动生成复杂多阶段任务结构数据的平台；② 缺乏专门针对长时程多阶段任务的高质量基准与精细化评估指标；③ 缺乏具备自适应记忆机制、能在动态环境中长时间保持决策连续性的导航方法。
- **核心贡献概要**：论文首次提出 **LH-VLN（Long-Horizon Vision-Language Navigation）** 任务，并围绕平台、基准、方法三个维度给出系统性解决方案——自动化数据生成平台 **NavGen**、长时程规划推理基准 **LHPR-VLN** 以及多粒度动态记忆模型 **MGDM**。

## 2. 论文提出的方法论

### 2.1 LH-VLN 任务定义

- 任务形式为“找到某处的某物，将其带到某处的某物，然后……”，一个完整任务包含 **2~4 个子任务（subtask）**，智能体须按顺序连续完成。
- 每个子任务的成功判定：智能体需到达目标物体 **1 米测地距离** 以内，且目标位于水平 **60° 视场角** 范围内。
- 动作空间为原子动作：前移（+0.25m）、左转（+30°）、右转（−30°）、停止（stop）。智能体在每个时间步从三个视角（+60°、0°、−60°）获取 RGB 观测（可选深度）。

### 2.2 NavGen 数据生成平台

- **双向生成机制**：
  - **前向生成（Forward Data Generation）**：以 HM3D 场景资产和机器人配置（Spot、Stretch）为资源池，通过精心设计的提示词驱动 GPT-4 生成多阶段复杂任务指令；随后在 Habitat 3 仿真器中由专家模型（navmesh + 贪心寻路）或训练好的导航模型执行，生成轨迹数据。
  - **后向生成（Backward Data Generation）**：通过轨迹分割算法将复杂任务轨迹拆分为“前移、左转、右转、绕行”等连续动作段，配合 RAM 图像标注模型的高置信度视觉标注，输入 GPT-4 生成逐步（step-by-step）VLN 任务，构成细粒度的单阶段导航任务集合。
- **多粒度特性**：同一轨迹可生成多层级指令（复杂多阶段指令、子任务级指令、逐步动作指令），支持对模型指令理解与执行的精细评估。

### 2.3 LHPR-VLN 基准

- 由 NavGen 平台构建，包含 **3,260 个任务**，平均 **150 个任务步**，平均指令长度 18.17，覆盖 **216 个 HM3D 场景**，为首个专为 LH-VLN 设计的数据集。
- 子任务数量分布：2 子任务任务占 39.0%，3 子任务占 52.4%，4 子任务占 8.6%；Spot 与 Stretch 机器人任务各约占 50%。

### 2.4 新评估指标

针对传统粗粒度指标（SR、OSR、SPL、NE）不足以评估多阶段复杂任务的不足，提出三个新指标：

- **ISR（Independent Success Rate，独立成功率）**：衡量各子任务独立完成的成功率，公式为 ISR = (∑ⱼ∑ᵢ sⱼᵢ) / (M·N)，其中 M 为任务数，N 为每个任务的子任务数，sⱼᵢ 表示第 j 个任务中第 i 个子任务是否成功。
- **CSR（Conditional Success Rate，条件成功率）**：考虑子任务之间的依赖关系，前序子任务的成功会影响后续子任务，公式为 CSR = (∑ⱼ∑ᵢ sⱼᵢ(1 + (N−1)sⱼ,ᵢ₋₁)) / (M·N²)，其中 sⱼ,ᵢ₋₁ 为前序子任务成功情况。
- **CGT（CSR weighted by Ground Truth，按真值路径加权的条件成功率）**：在 CSR 基础上引入子任务真值路径长度 Pᵢ 与整条任务路径长度 P 的比值作为权重，以反映不同子任务路径难度差异，公式为 CGT = (∑ⱼ∑ᵢ (Pᵢ/P)·sⱼᵢ(1 + (N−1)sⱼ,ᵢ₋₁)) / (M·N)。
- 另有 **TAR（Target Approach Rate）** 指标，基于 NE 设计，用于反映导航成功率较低时模型对目标的逼近程度（详见补充材料）。

### 2.5 MGDM 模型（Multi-Granularity Dynamic Memory）

模型基于通用 VLN 流程，包含三个核心组件：

- **基础模型（Base Model）**：使用预训练视觉编码器（EVA-CLIP-02-Large 的 ViT）编码多方向图像，通过 Transformer 编码器融合多视角特征，并加入方向 token（左/前/右）与时间步 embedding 构建场景表示与历史观测表示，统一输入 LLM（Vicuna 7B v0）进行动作选择。
- **CoT 反馈模块（Chain-of-Thought Feedback）**：在每个子任务开始及导航过程中，将任务指令、当前观测、历史观测与提示词输入 GPT-4，生成思维链（CoT），对任务进行上下文理解与分解，从而指导智能体即时行动、增强推理能力、缓解 LLM 幻觉问题。
- **自适应记忆整合与更新模块（AMIU，Adaptive Memory Integration and Update）**：
  - **短期记忆（Short-term Memory）**：由历史观测编码构成，长度超过阈值时触发动态遗忘——对记忆置信度向量做窗口大小为 2 的平均池化（pooling），计算池化后向量的熵，选择熵最小的池化索引对应的记忆元素进行模糊与遗忘，再将新观测加入，从而实现对长序列记忆的压缩与更新。
  - **长期记忆（Long-term Memory）**：从 LHPR-VLN 数据集中检索与当前观测最匹配的 top-k 观测-动作对，通过余弦相似度匹配，将检索到的动作加权平均以影响当前决策向量。
  - 训练目标为最小化模型决策 a 与专家决策 e 之间的交叉熵损失。

## 3. 实验设计

### 3.1 数据集与场景

- **主数据集**：HM3D（216 个大规模室内 3D 重建场景，带语义标注），用于构建 LHPR-VLN 基准。
- **额外场景**：HSSD（211 个高质量室内场景），用于测试 NavGen 的数据生成能力。
- **仿真器**：Habitat 3（主实验环境，连续 3D 场景）；Isaac Sim（用于高质量渲染与物理交互实验）。

### 3.2 对比方法（Baseline）

- **Random**：随机动作基线。
- **GLM-4v prompt**：使用提示工程引导 GLM-4v（视觉-语言模型）输出导航动作。
- **NaviLLM**：离散环境 SOTA 导航模型，被适配到连续环境，分为预训练（Pretrain）与微调（Finetuned）两个版本。
- **GPT-4 + NaviLLM**：先用 GPT-4 将复杂任务分解为子任务，再由 NaviLLM 顺序执行各子任务。
- **ETPNav**：基于图的导航模型（实验中有提及但表中未单独列出性能，论文指出其因 waypoint predictor 局限而无法有效预测可导航点）。

### 3.3 实验设置

- 视觉编码器：EVA-CLIP-02-Large 的 ViT（冻结）。
- LLM：Vicuna 7B v0。
- 优化器：Adam，学习率 3e-5。
- 训练方式：交替使用模仿学习与基于轨迹的监督学习。

### 3.4 实验任务划分

- 按子任务数量分为两组：**2-3 子任务**（较短 LH-VLN 任务）与 **3-4 子任务**（较长 LH-VLN 任务）。
- 实验涵盖两类任务：**多阶段复杂任务**（LH-VLN）与**逐步分解的单阶段任务**（step-by-step LH-VLN）。

## 4. 资源与算力

- 论文**未明确说明**训练所使用的 GPU 型号、数量、训练时长等具体算力信息。
- 可推断的配置信息：LLM 为 Vicuna 7B v0（7B 参数规模），视觉编码器为 EVA-CLIP-02-Large 的 ViT（冻结），使用 Adam 优化器（lr=3e-5）。这些信息表明训练开销相对可控，但论文未披露硬件细节，这是可复现性方面的一个缺口。

## 5. 实验数量与充分性

已开展的实验组：

- **主实验（表 2）**：在 LH-VLN 复杂任务上，对 2-3 子任务与 3-4 子任务两组设置，对比 5 个方法（Random、GLM-4v、NaviLLM-Pretrain、NaviLLM-Finetuned、GPT-4+NaviLLM、MGDM），报告 SR、NE、ISR、CSR、CGT 五个指标。
- **逐步任务实验（表 3）**：在 step-by-step LH-VLN 任务上，对比 Random、GLM-4v、NaviLLM、MGDM，报告 SR、OSR、SPL、NE。
- **消融实验（表 4）**：对 MGDM 分别去除自适应记忆模块（w/o Adap Mem）、长期记忆模块（w/o LT Mem）、CoT 模块（w/o CoT），报告 NE、ISR、CSR、CGT。
- **可视化分析**：展示了一次部分成功的长时程导航案例，分析智能体在记忆序列积累前后的行为差异。

充分性与客观性评估：

- **实验规模适中**：覆盖主任务、逐步任务与消融实验，能较全面地验证各组件贡献。
- **公平性考量较好**：包含预训练/微调的 NaviLLM 对照，以及 GPT-4 任务分解 + 单阶段模型的组合对照，能有效区分“单阶段能力”与“多阶段长时程能力”的差异。
- **不足之处**：① 表 2 中所有模型在 2-3 子任务上的 SR、ISR、CSR、CGT 均为 0，说明该基准难度极高，但论文未提供足够分析说明这是否反映模型能力不足还是基准设计存在不合理之处；② 3-4 子任务上所有指标绝对值均很低（如 MGDM 的 SR=0 但 ISR=4.69），模型实际完成率有限，缺乏更高性能参考；③ 未与其他长时程方法（如基于记忆的 IVLN 方法等）进行对比；④ 消融实验仅各去除一个模块，未进行组合消融；⑤ 论文未给出跨场景、跨机器人配置的泛化性实验，也未见对 HSSD 场景的定量评估结果。

## 6. 论文的主要结论与发现

- **现有 VLN 模型在 LH-VLN 任务上表现很差**：即便是较短的 2-3 子任务，各模型的 SR、ISR、CSR、CGT 均为 0，说明现有模型无法有效理解并完成多阶段复杂导航任务。
- **GPT-4 任务分解能部分提升单阶段模型表现**：GPT-4+NaviLLM 相比微调后的 NaviLLM，ISR 提升约 23%，说明单阶段模型在独立子任务上确实具备基本导航能力，任务分解策略有帮助但缺乏对复杂任务的整体理解，导致 CGT 反而下降，存在记忆碎片化问题。
- **记忆对长时程任务至关重要**：MGDM 在 3-4 子任务上优于所有基线，且在 CGT 指标上优势明显，表明直接执行复杂任务能保持更连贯完整的记忆。消融实验也证实记忆模块与 CoT 模块的移除会显著降低性能。
- **逐步任务中发现的问题**：MGDM 在 step-by-step 任务中 OSR 较高、NE 较低，但 SR 和 SPL 为 0，说明模型存在“接近目标但无法正确判断是否到达”的问题，停止决策能力有待加强。
- **长时程任务中记忆的积累效应**：所有模型在 3-4 子任务上的 ISR、CSR、CGT 均优于 2-3 子任务，提示前序阶段的记忆积累可能有助于后续子任务的完成。
- **MGDM 的综合优势**：在最长、最难的任务设置中展现出最佳的整体表现与最低的 NE，说明其在长时程规划与决策一致性方面具有较大潜力。

## 7. 优点

- **问题定义具有前瞻性**：首次正式提出 LH-VLN 任务，填补了 VLN 领域多阶段长时程任务定义的空白，拓展了研究边界，更贴近真实机器人应用场景。
- **平台与基准的一体化设计**：NavGen 的“前向+后向”双向生成机制设计巧妙，既能生成复杂多阶段任务，又能将轨迹反向分解为细粒度逐步任务，大幅提高了数据利用率与任务多样性，且平台不依赖单一仿真器/资产，具备一定的通用性。
- **精细化评估指标**：ISR/CSR/CGT 三个指标分别从独立子任务、条件依赖、路径难度加权三个角度刻画模型表现，比传统粗粒度 SR 更能反映多阶段任务的执行细节，是一项方法论贡献。
- **方法设计紧扣任务需求**：MGDM 的短期记忆“模糊+遗忘”机制与长期记忆检索机制，针对长时程任务中记忆过度累积和关键信息丢失的痛点，设计思路合理且有消融实验支撑。
- **实验分析深入**：论文明确围绕三个研究问题（Q1-Q3）组织实验分析，对“现有模型能否完成”“单阶段与多阶段关系”“记忆的价值”给出了有针对性的回答，行文逻辑清晰、论证完整。

## 8. 不足与局限

- **基准难度设置可能过于苛刻**：所有模型在 2-3 子任务上全部指标为 0，缺乏区分度；虽然论文归因于模型能力不足，但基准本身的任务规模和判定条件（如 1 米测地距离 + 60° 视场角）可能同时存在过严的问题，未来需要进一步校准。
- **算力信息缺失**：未披露 GPU 型号、数量、训练时长等关键信息，增加了复现难度。
- **对比方法覆盖不全面**：未与 IVLN、Goat-Bench 等同样涉及多阶段/持续性导航的近期方法进行对比；ETPNav 虽被提及但未在表中给出数据；消融仅限 MGDM 内部组件，未与其他记忆机制（如固定长度滑动窗口记忆、随机丢弃记忆等）进行消融对照。
- **指标理解门槛较高**：ISR/CSR/CGT 的公式较为复杂，论文对其直观含义的解释篇幅有限，读者理解成本较高。
- **泛化性验证不足**：缺乏跨场景类型（如 HSSD）、跨仿真器（Isaac Sim 实验未给出定量结果）、跨语言指令类型的系统泛化实验；机器人配置（Spot/Stretch）的差异对模型表现的影响也未见分析。
- **可视化分析偏定性**：仅展示一个案例，支撑力度有限。
- **长期记忆的机制细节有限**：长期记忆从数据集中检索观测-动作对的做法在真实部署中依赖预收集数据集，其在线适用性和可扩展性有待进一步讨论。

（完）
