---
title: "UniGoal: Towards Universal Zero-shot Goal-oriented Navigation"
title_zh: UniGoal：迈向通用零样本目标导向导航
authors: "Yin, Hang, Xu, Xiuwei, Zhao, Linqing, Wang, Ziwei, Zhou, Jie, Lu, Jiwen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yin_UniGoal_Towards_Universal_Zero-shot_Goal-oriented_Navigation_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 统一物体类别的通用零样本目标导向导航
tldr: 零样本目标导向导航通常针对不同目标类型（物体类别、实例图像、文本描述）设计独立流程，通用性差。本文提出UniGoal，以统一图表示编码各种目标，并将智能体观测在线转化为场景图，保留结构化信息。借助LLM的显式图推理，该方法在多种目标类型的零样本导航中均取得优异性能，为通用导航提供了统一框架。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 821, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 650, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 682, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1795, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 1222, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 782, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yin-unigoal-towards-universal-zero-shot-goal-oriented-navigation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 454, \"label\": \"Table\"}]"
motivation: 不同目标类型的零样本导航方法差异大，缺乏可泛化的统一框架。
method: 提出统一图表示与在线场景图，将目标和观测统一为图，用LLM进行图推理进行导航。
result: 在多个零样本导航基准上超越专门方法，验证了统一图表示的有效性。
conclusion: 统一图表示与场景图推理可实现跨目标类型的通用零样本导航。
---

## Abstract
In this paper, we propose a general framework for universal zero-shot goal-oriented navigation. Existing zero-shot methods build inference framework upon large language models (LLM) for specific tasks, which differs a lot in overall pipeline and fails to generalize across different types of goal. Towards the aim of universal zero-shot navigation, we propose a uniform graph representation to unify different goals, including object category, instance image and text description. We also convert the observation of agent into an online maintained scene graph. With this consistent scene and goal representation, we preserve most structural information compared with pure text and are able to leverage LLM for explicit graph-based reasoning.Specifically, we conduct graph matching between the scene graph and goal graph at each time instant and propose different strategies to generate long-term goal of exploration according to different matching states. The agent first iteratively searches subgraph of goal when zero-matched. With partial matching, the agent then utilizes coordinate projection and anchor pair alignment to infer the goal location. Finally scene graph correction and goal verification are applied for perfect matching. We also present a blacklist mechanism to enable robust switch between stages.Extensive experiments on several benchmarks show that our UniGoal achieves state-of-the-art zero-shot performance on three studied navigation tasks with a single model, even outperforming task-specific zero-shot methods and supervised universal methods.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- **问题定义**：目标导向导航是机器人领域的基础问题，要求智能体在未知环境中导航至指定目标。该任务按目标类型可分为三个主要子任务：
  - **Object-goal Navigation (ON)**：目标为物体类别（如“厨房”或“椅子”）。
  - **Instance-image-goal Navigation (IIN)**：目标为实例图像，需要找到图像中出现的特定物体实例。
  - **Text-goal Navigation (TN)**：目标为自由形式的文本描述。
- **现有方法的不足**：
  - 已有零样本方法（如 ESC、SG-Nav、Mod-IIN）大多针对单一子任务设计，整体流程差异大，**无法跨目标类型泛化**。
  - 现有通用方法（如 GOAT、PSL）虽然统一了目标表示，但**依赖大规模强化学习训练**，训练成本高且容易在仿真环境过拟合，缺乏零样本泛化能力。
  - 已有的统一零样本框架 InstructNav 只能处理语言相关导航，**无法处理视觉相关的 IIN 任务**。
- **核心目标**：提出一个**单一模型、无需训练/微调**的通用零样本目标导向导航框架，同时适用于物体类别、实例图像和文本描述三种目标类型。

## 2. 方法论（核心思想与关键技术细节）

### 2.1 核心思想
- 提出一份**统一的图表示**（Goal Graph）来编码三种不同类型的目标，并将智能体的观测在线转化为**场景图**（Scene Graph）。
- 通过**图匹配**（Graph Matching）衡量目标被观测到的程度，并根据匹配状态设计**多阶段场景探索策略**，引导 LLM 逐步推理和决策，实现从“探索未知”到“定位目标”再到“验证目标”的渐进式导航。

### 2.2 图构建与匹配（Graph Construction and Matching）
- **场景图构建**：随智能体移动，将新观测到的物体和空间关系增量式地构建为场景图 G_t；节点表示物体，边表示物体间的空间/语义关系。
- **目标图构建**：将物体类别、实例图像、文本描述三类目标分别处理为统一的目标图 G_g。
- **图匹配（公式）**：提出三种匹配指标：
  - **节点匹配**（公式1）：M_N = B(thr(Embed(V_t) · Embed(V_g)^T))
  - **边匹配**（公式2）：M_E = B(thr(Embed(E_t) · Embed(E_g)^T))
  - **拓扑匹配**（公式3）：S_T = 1 − D(S(F(G_t, M_N, M_E)), S(G_g))，即图编辑距离相似度。
  - 最终匹配分数 S = (S_N + S_E + S_T) / 3。
- 使用 CLIP 文本编码器提取节点和边的嵌入，并结合双分图匹配确定对应关系。

### 2.3 多阶段场景探索（Multi-stage Scene Exploration）
根据匹配分数 S 分为三个阶段：

- **阶段1：零匹配（Zero Matching）**（S < σ1）：
  - 目标几乎未被观测，核心任务是大范围探索。
  - 利用 LLM 将目标图分解为多个内部强相关的子图，每个子图作为物体目标调用 SG-Nav 式前沿选择，最终综合各前沿的分数和距离选出最优探索点。

- **阶段2：部分匹配（Partial Matching）**（σ1 ≤ S < σ2 且存在锚点对）：
  - 目标被部分观测，利用场景图与目标图的重叠部分推断目标位置。
  - **坐标投影**：将目标图中心节点投影到 BEV 坐标系原点，通过 LLM 逐边推断其他节点的相对 BEV 坐标（DFS 遍历）。
  - **锚点对对齐**：公式(4)中 P = S·R·T 为二维坐标变换矩阵，通过锚点对建立方程 v_t = P·v_g，求解平移、旋转、缩放参数；随后将目标图其余节点投影到场景图坐标系，并计算节点集合最小外接圆圆心 c*（公式5）作为探索目标。

- **阶段3：完美匹配（Perfect Matching）**（S ≥ σ2 且中心物体 o 匹配成功）：
  - 将匹配到的中心物体位置作为导航目标。
  - **场景图校正**：利用公式(6)、(7)进行图卷积式的信息传播，结合 VLM 的新观测，用 LLM 迭代更新不合理节点和边。
  - **目标验证**：公式(8) C_t = N_t + M_t + S_t − λD_t，综合校正节点/边比例、关键点匹配比例（IIN用 LightGlue 提取）、图匹配分数和路径长度，判断目标是否验证成功；成功则停止，失败则排除该目标。

### 2.4 鲁棒黑名单机制（Robust Blacklist Mechanism）
- 记录所有匹配失败的节点和边，冻结之后不再参与图匹配，避免智能体陷入重复探索。
- 两种触发条件：阶段2所有锚点对未能进入阶段3、或阶段3目标验证失败。
- 若场景图校正中修正了某些节点/边，则将其及其相连节点从黑名单中移出。

## 3. 实验设计（数据集、指标与对比方法）

- **数据集/基准**：
  - **ON**：Matterport3D (MP3D)、Habitat-Matterport 3D (HM3D)、RoboTHOR（沿用 SG-Nav 设置）。
  - **IIN**：HM3D（沿用 Mod-IIN 设置）。
  - **TN**：HM3D（沿用 InstanceNav 设置）。
- **评估指标**：成功率（SR）和路径加权成功率（SPL）。
- **对比方法**：
  - **ON**：监督方法 SemEXP、ZSON、OVRL-v2；零样本方法 ESC、OpenFMNav、VLFM、SG-Nav。
  - **IIN**：监督方法 Krantz et al.、OVRL-v2-IIN、IEVE；零样本方法 Mod-IIN。
  - **TN**：监督通用方法 PSL 和 GOAT。
- **实现细节**：使用 Habitat Simulator，LLM 为 LLaMA-2-7B，VLM 为 LLaVA-v1.6-Mistral-7B，CLIP 编码节点/边嵌入。

## 4. 资源与算力

- 论文正文**未明确说明**所用的 GPU 型号、数量、训练时长或推理算力开销。
- 由于 UniGoal 是零样本方法，**无需训练或微调**，因此不存在训练算力成本。但推理时需要在每个决策时间点调用 LLM 和 VLM（LLaMA-2-7B、LLaVA-v1.6-Mistral-7B），实际的推理延迟和计算资源消耗在正文中未被量化报告。这一信息缺失是论文在复现和部署成本估算方面的一个不足。

## 5. 实验数量与充分性

- **主实验（Table 1）**：覆盖 3 个任务、5 个 benchmark，对比 12+ 种方法，统一报告 SR/SPL。
- **管道设计消融（Table 2）**：3 组消融——简化图匹配、移除黑名单机制、简化多阶段探索策略。
- **各阶段子模块消融（Table 3）**：7 组消融——阶段1（替换为 FBE、移除图分解、移除前沿选择）、阶段2（简化坐标投影、移除锚点对对齐）、阶段3（移除场景图校正、移除目标验证）。
- **定性实验**：图 4 展示决策过程（阶段切换、匹配分数变化），图 5 展示 9 个场景中的三种任务导航路径可视化。
- **充分性评估**：整体实验设计较为充分，验证了每个核心模块的贡献，且主实验覆盖了多种方法类别的对比。但补充材料中的更多消融实验（如不同 LLM/VLM 选择、阈值灵敏度等）在正文中未展示，一定程度上限制了拆解全面性。

## 6. 主要结论与发现

- UniGoal 在**单一模型**下，同时实现三种目标类型（ON、IIN、TN）的零样本导航：
  - **ON**：SR 41.0/54.5/48.0（MP3D/HM3D/RoboTHOR），超越 SG-Nav，甚至超过部分监督方法（SemEXP、ZSON）。
  - **IIN**：SR 60.2，超越 Mod-IIN 4.1%（56.1 → 60.2），提升显著。
  - **TN**：SR 20.2，超越监督通用方法 PSL（16.5）和 GOAT（17.0）。
  - 在通用方法对比中全面超越监督方法 PSL 和 GOAT。
- **消融结论**：图匹配的分数计算、黑名单机制、多阶段探索策略、各阶段的子模块（图分解、前沿选择、坐标投影、锚点对齐、场景图校正、目标验证）均对最终性能有正向贡献，移除后性能均有不同程度下降。

## 7. 优点

- **统一的图表示**是最大创新点：将三类差异巨大的目标统一编码为图结构，并与场景图形成对称表示，极大降低了框架对任务类型的耦合度。
- **显式的图推理路径**：图匹配提供了可量化的匹配状态，多阶段策略将“探索—推断—验证”分解为清晰的结构化流程，使 LLM 的推理有明确目标，而非单次黑盒式猜测。
- **黑名单机制**是一个巧妙的设计，解决了零样本方法中因感知误差或目标混淆导致的重复探索问题，增强了阶段切换的鲁棒性。
- **零样本、免训练**的设定使其在实际部署中具有较强的泛化潜力，并在真实机器人平台上初步验证了可行性。
- 实验对比充分，在多个基准上达成 SOTA，且对每种任务类型均有明确的性能提升。

## 8. 不足与局限

- **ON 任务下的性能提升有限**：ON 中目标图退化为单节点，图分解、锚点对齐等模块失效，性能提升主要依赖阶段3的校正与验证机制，增量较小。
- **对感知模块依赖较强**：场景图构建和匹配的准确性依赖底层视觉感知（物体检测、关系提取）。感知错误可能会导致错误匹配、进入错误阶段，虽然黑名单和校正机制能部分缓解，但并未完全消除误差累积风险。
- **算力开销未量化**：LLM/VLM 的调用频率和推理延迟未被报告，这在实际机器人实时部署中可能是一个瓶颈。
- **实验环境集中在仿真**：虽然作者提到已在真实机器人平台部署，但正文未提供真实世界实验的定量结果，泛化结论主要基于仿真环境。
- **通用性与性能的权衡**：在 IIN 上提升显著（+4.1%），但在 ON 和 TN 上的增幅相对有限（ON +0.8%，TN 为首次零样本结果，无法横向对比提升幅度），说明统一框架在不同任务上的增益并不均匀，仍存在优化空间。
- **部分消融细节缺失**：正文未展示补充材料中的更多消融（如不同 LLM 模型的影响、阈值选择敏感性等），复现和进一步优化需要依赖完整补充材料。

（完）
