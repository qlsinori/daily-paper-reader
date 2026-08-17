---
title: "UniGoal: Towards Universal Zero-shot Goal-oriented Navigation"
title_zh: UniGoal：迈向统一的零样本目标导向导航
authors: "Yin, Hang, Xu, Xiuwei, Zhao, Linqing, Wang, Ziwei, Zhou, Jie, Lu, Jiwen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yin_UniGoal_Towards_Universal_Zero-shot_Goal-oriented_Navigation_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 包含物体类别目标的通用零样本目标导向导航
tldr: 面向不同类型的零样本目标导向导航，本文提出UniGoal统一框架，用统一的图表示将物体类别、实例图像和文本描述三种目标统一建模，并将智能体观测转换为在线场景图。通过保持结构与语义信息并借助大语言模型进行显式图推理，模型可跨目标类型泛化。实验表明UniGoal在多个目标导航任务上取得领先效果，为零样本目标导航提供了通用解决方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 821, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 650, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 682, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1795, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 1222, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 782, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 454, \"label\": \"Table\"}]"
motivation: 现有零样本目标导航通常针对单一目标类型设计管线，无法统一处理物体类别、实例图像和文本描述等多样化目标。
method: 提出统一图表示编码各种目标，维护在线场景图，并通过LLM进行显式图推理以决策导航。
result: 实验验证UniGoal在零样本物体目标、实例与描述目标导航上均表现优异，泛化性强。
conclusion: 该工作实现了真正的通用零样本目标导向导航，降低了不同任务之间的方法迁移成本。
---

## Abstract
In this paper, we propose a general framework for universal zero-shot goal-oriented navigation. Existing zero-shot methods build inference framework upon large language models (LLM) for specific tasks, which differs a lot in overall pipeline and fails to generalize across different types of goal. Towards the aim of universal zero-shot navigation, we propose a uniform graph representation to unify different goals, including object category, instance image and text description. We also convert the observation of agent into an online maintained scene graph. With this consistent scene and goal representation, we preserve most structural information compared with pure text and are able to leverage LLM for explicit graph-based reasoning.Specifically, we conduct graph matching between the scene graph and goal graph at each time instant and propose different strategies to generate long-term goal of exploration according to different matching states. The agent first iteratively searches subgraph of goal when zero-matched. With partial matching, the agent then utilizes coordinate projection and anchor pair alignment to infer the goal location. Finally scene graph correction and goal verification are applied for perfect matching. We also present a blacklist mechanism to enable robust switch between stages.Extensive experiments on several benchmarks show that our UniGoal achieves state-of-the-art zero-shot performance on three studied navigation tasks with a single model, even outperforming task-specific zero-shot methods and supervised universal methods.

---

## 论文详细总结（自动生成）

# UniGoal：面向通用零样本目标导向导航

## 1. 核心问题与整体含义

- **研究背景**：目标导向导航（Goal-oriented Navigation）是具身智能中的基础问题，要求智能体在未知环境中导航至指定目标。根据目标类型可细分为三类：
  - 物体类别导航（Object-goal Navigation, ON）
  - 实例图像导航（Instance-image-goal Navigation, IIN）
  - 文本描述导航（Text-goal Navigation, TN）
- **现有方法的不足**：
  - 已有零样本方法大多基于大语言模型（LLM）为单一任务设计专用推理流程，难以跨目标类型泛化。
  - 通用方法（如 GOAT、PSL）虽然能处理多种目标，但仍需大规模强化学习训练，训练成本高且容易过拟合仿真环境，泛化到真实世界的能力有限。
  - 最近的 InstructNav 虽提出语言相关导航的通用框架，但仍无法处理视觉类目标（如 IIN）。
- **论文提出 UniGoal 的整体含义**：首次实现真正的“通用零样本”目标导向导航，用单一模型、无需训练或微调，统一处理物体类别、实例图像和文本描述三类目标，并在多个基准上达到领先效果。

## 2. 方法论

### 核心思想
- 用**统一图表示**来统一场景与目标，保留结构信息，使 LLM 能够基于图进行显式推理。
- 将智能体观测构建为**在线场景图（scene graph）**，将不同目标转换为**目标图（goal graph）**，两者格式一致。
- 每个时刻执行场景图与目标图的**图匹配（graph matching）**，根据匹配程度选择不同的探索策略。

### 关键技术细节

1. **图构建**
   - 定义图 G = (V, E)，节点为物体，边为物体间空间/语义关系，内容以文本描述。
   - 场景图 G_t 随 RGB-D 观测增量更新；目标图 G_g 针对三类目标分别构建。

2. **图匹配与匹配分数**
   - 节点匹配矩阵 M_N 和边匹配矩阵 M_E：通过 CLIP 提取嵌入，计算相似度矩阵，阈值化后做二分匹配。
   - 拓扑匹配 S_T：基于图编辑距离衡量场景图与目标图的结构相似度。
   - 最终匹配分数 S = (S_N + S_E + S_T)/3。

3. **三阶段场景探索策略**
   - **阶段一：零匹配（Zero Matching）**：当 S < σ1 时，将目标图分解为多个内部相关的子图，分别调用 SG-Nav 式的前沿选择，最终综合打分选出探索前沿。
   - **阶段二：部分匹配（Partial Matching）**：当 S ≥ σ1 且存在锚点对时，通过 LLM 进行**坐标投影**：以中心物体为原点，通过 DFS 遍历目标图并利用空间关系推断各节点 BEV 坐标；随后用**锚点对对齐**求解 2D 变换矩阵 P（尺度、旋转、平移），将目标图节点映射到场景图坐标系，以最小外接圆圆心作为探索目标。
   - **阶段三：完全匹配（Perfect Matching）**：当 S ≥ σ2 且中心物体 o 已匹配时，智能体向目标移动；同时进行**场景图修正**（利用 VLM 观测和图传播更新局部子图）与**目标验证**（结合节点/边修正比例、关键点匹配（IIN 用 LightGlue）、匹配分数和路径长度计算综合置信度）。

4. **黑名单机制**
   - 记录失败的匹配结果，冻结不匹配的节点和边，避免重复探索，支持阶段间稳健切换。

## 3. 实验设计

- **数据集与场景**：
  - 物体导航（ON）：Matterport3D（MP3D）、Habitat-Matterport 3D（HM3D）、RoboTHOR。
  - 实例图像导航（IIN）：HM3D。
  - 文本导航（TN）：HM3D。
- **评测指标**：成功率（SR）和路径加权成功率（SPL）。
- **对比方法**：
  - 监督方法：SemEXP、ZSON、OVRL-v2、IEVE、Krantz et al.、PSL、GOAT 等。
  - 零样本方法：ESC、OpenFMNav、VLFM、SG-Nav、Mod-IIN 等。
  - 通用方法：PSL、GOAT（亦为监督通用方法）。

## 4. 资源与算力

- 论文中**未明确说明**具体使用的 GPU 型号、数量、训练时长等算力信息。
- 仅指出使用 **LLaMA-2-7B** 作为 LLM、**LLaVA-v1.6-Mistral-7B** 作为 VLM、CLIP 文本编码器用于嵌入提取。
- 由于方法本身是 **training-free（零样本、无需训练）**，资源消耗主要用于推理时的 LLM/VLM 调用，但精确推理成本未在文中量化。

## 5. 实验数量与充分性

- **实验数量**：
  - 三类任务（ON、IIN、TN）在多个基准上的主实验，覆盖 5 个数据集设置。
  - 消融实验：管道设计（简化匹配、移除黑名单、简化多阶段策略）；各阶段子模块（阶段一：FBE 替换、去除目标图分解、去除前沿选择；阶段二：简化坐标投影、移除锚点对齐；阶段三：去除场景图修正、去除目标验证）。
  - 定性可视化：决策过程示例、跨场景路径可视化、真实机器人部署（文中提及但细节有限）。
- **充分性与公平性**：
  - 消融覆盖充分，验证了各模块的必要性。
  - 与不同范式（监督、零样本、通用）的 SOTA 方法在同一基准上对比，设置基本公平。
  - 但存在一定风险：主实验的 IIN 与 TN 仅在 HM3D 上评估，缺少跨数据集验证；真实机器人部分未给出详细指标，可能削弱泛化性证据。

## 6. 主要结论与发现

- UniGoal 在零样本 ON、IIN 上分别超越此前 SOTA 方法 SG-Nav 和 Mod-IIN（SR 提升 0.8% 和 4.1%），在 IIN 上提升尤为明显。
- 在通用目标导航方法中表现最佳，甚至超越需要训练的监督通用方法 PSL 和 GOAT：
  - ON：+3.9/1.0 SR/SPL；
  - IIN：+22.8/7.6；
  - TN：+3.2/2.6。
- 多阶段探索策略、匹配评分和黑名单机制均显著提升性能；图表示统一场景与目标可有效支持 LLM 推理。
- 单模型即可处理三种目标类型，无需训练，具备较强的跨场景和真实环境泛化潜力。

## 7. 优点

- **统一性与通用性**：首次用统一图表示将三类目标（类别、图像、文本）纳入同一框架，避免任务定制化管线。
- **结构信息保留**：相比纯文本描述，图表示保留空间与语义关系，提升推理准确性。
- **显式可解释推理**：基于图匹配的分数驱动三阶段策略，决策过程可解释、可视化。
- **训练免除了**：完全零训练，降低资源成本，且更容易迁移到新环境。
- **模块可设计性**：坐标投影、锚点对齐、黑名单等机制设计巧妙，消融实验证明各模块均有贡献。

## 8. 不足与局限

- **算力报告缺失**：未明确 LLM/VLM 推理的资源消耗和延迟，难以评估实际部署成本。
- **基准覆盖有限**：IIN 和 TN 仅在 HM3D 上评估，缺少 MP3D、RoboTHOR 等更多数据集的验证，泛化证据不够充分。
- **对基础感知能力依赖强**：场景图质量依赖视觉分割与识别模型，存在误差传播风险；论文虽设计了修正模块，但无法完全消除。
- **阶段切换依赖阈值**：σ1、σ2 等超参数需人工设定，可能影响在不同场景下的稳定性。
- **真实世界验证较弱**：仅提及部署真实机器人平台，但未展示定量实验，对“强泛化能力”的支撑力有限。
- **ON 场景下模块能力受限**：当目标图退化为单节点时，阶段一分解和阶段二锚点对齐无法发挥作用，说明通用框架在该子任务上未能完全发挥优势。

（完）
