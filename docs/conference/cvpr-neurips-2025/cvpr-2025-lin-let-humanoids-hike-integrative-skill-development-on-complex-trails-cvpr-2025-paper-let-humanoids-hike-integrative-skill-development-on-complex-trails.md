---
title: "Let Humanoids Hike! Integrative Skill Development on Complex Trails"
title_zh: 让人形机器人远足！在复杂小径上的综合技能发展
authors: "Lin, Kwan-Yee, Yu, Stella X."
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Lin_Let_Humanoids_Hike_Integrative_Skill_Development_on_Complex_Trails_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向人形机器人复杂小径的具身视觉导航，结合长期目标与情境感知
tldr: 针对当前人形机器人研究中运动控制与语义导航割裂、难以应对复杂野外小径的问题，论文提出 LEGO-H 训练框架，让具备视觉的类人机器人独立完成复杂小径徒步。该方法利用时间视觉 Transformer 预测未来步态，统一局部运动与情境感知，实现视觉感知、决策和运动执行的综合技能学习。实验表明该方法能提升机器人在复杂地形上的适应性与决策能力，为户外具身导航提供了系统化训练范式。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1790, \"height\": 1025, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 796, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 1008, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1717, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 247, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 861, \"height\": 265, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 855, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-lin-let-humanoids-hike-integrative-skill-development-on-complex-trails-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 907, \"height\": 248, \"label\": \"Table\"}]"
motivation: 现有人形机器人研究割裂运动技能与语义导航，缺乏长期目标与地形感知，难以应对复杂小径。
method: 提出LEGO-H学习框架，用时间视觉Transformer预测未来步态，整合视觉感知、决策与运动执行。
result: 在复杂小径上训练的视觉人形机器人可独立徒步，表现出对不可预测地形的适应与决策能力。
conclusion: 综合技能训练是让具身智能体在复杂户外环境中进行长时导航的关键路径。
---

## Abstract
Hiking on complex trails demands balance, agility, and adaptive decision-making over unpredictable terrain. Current humanoid research remains fragmented and inadequate for hiking: locomotion focuses on motor skills without long-term goals or situational awareness, while semantic navigation overlooks real-world embodiment and local terrain variability. We propose training humanoids to hike on complex trails, fostering integrative skill development across visual perception, decision making, and motor execution. We develop LEGO-H, a learning framework that enables a humanoid with vision to hike complex trails independently. It has two key innovations. (1) A Temporal Vision Transformer anticipates future steps to guide locomotion, unifying local movement and goal-directed navigation. (2) Latent representations of joint movement patterns combined with hierarchical metric learning allow smooth policy transfer from privileged training to real-world training. These techniques enable LEGO-H to handle diverse physical and environmental challenges without relying on predefined motion patterns. Experiments on diverse simulated hiking trails and humanoids with different morphologies demonstrate LEGO-H's robustness and versatility, establishing a strong foundation for future humanoid development.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：在复杂野外小径上徒步，要求机器人具备平衡、敏捷与对不可预测地形（陡坡、宽沟、树根、高程突变等）的适应性决策能力。然而，现有人形机器人研究是“割裂”的：
  - **运动控制（locomotion）方向**：集中于行走、跑步、跳跃等低级运动技能，通常简化地形交互为静态模式，缺乏长期目标与情境感知。
  - **语义导航（navigation）方向**：依赖场景建图或结构化假设，忽略真实世界中的具身性（embodiment）与局部地形变化。
  - 现有复杂技能（如跑酷）多依赖人工工程和用户指令，LLM/VLM 虽可高层规划但未与运动控制耦合，无法保证“最后一步可行”。
- **核心问题**：如何构建一个统一框架，将视觉感知、高层决策和运动执行整合起来，让人形机器人能够独立、安全、高效地穿越复杂自然小径？
- **整体含义**：论文提出将“徒步”作为人形机器人综合技能发展的测试场，强调**多层级技能的集成发展**（integrative skill development），而非单一技能的孤岛式学习。这为户外具身导航与运动控制的统一提供了一种系统化训练范式。

## 2. 方法论（LEGO-H 框架）

论文提出 **LEGO-H**，一个面向视觉人形机器人的端到端具身学习框架，包含两大核心创新：

### 2.1 核心思想
- 基于**分层强化学习（HRL）**范式，构建“导航模块 H + 运动技能模块 E”的统一训练管道。
- 采用**特权学习（Privileged Learning）**：先训练一个拥有特权信息（地形类型、摩擦系数、精确状态、专家导航目标）的教师策略（oracle policy），再将其蒸馏到仅依赖视觉和本体感知的学生统一策略中。
- 导航目标不作为静态 token，而是通过 **TC-ViTs** 建模时间-空间关系，**软性引导（soft guidance）**运动策略，而非强制对齐，促进自涌现技能的多样性。

### 2.2 TC-ViTs（Temporal Information Conditioned Vision Transformer Variants）
用于局部导航预期，解决三个关键问题（感知过去/现在/未来、预测可适应未来的目标、跨时间尺度协调导航与运动）：

- **（a）目标导向的时间Transformer编码器**：基于 ViViT，处理 16 帧深度图（降采样至4帧），通过时空注意力提取长期依赖；将终点信息 `PB` 平铺成图像通道与时空 token 拼接，确保每个 token 与最终目标对齐。
- **（b）当前帧双路处理**：当前深度帧通过浅层 CNN 提取高分辨率近场空间特征 `β`，与时间编码器的输出 `α` 拼接后经 MLP 得到视觉表征 `γ`，保留即时空间细节。
- **（c）循环目标适应机制**：将视觉表征 `γ`、终点 `PB`、中间路点 `Drm`、本体感知 `Xpro` 输入 GRU，输出统一控制潜变量 `z_uni`、目标残差 `δg0` 和 N 个未来局部导航目标 `G = {g1,...,gN}`。
- **跨时间尺度策略**：
  - **最近目标转发（Nearest Goal Forwarding）**：仅将最近的局部目标 `g1` 传给运动模块，避免长期误差累积。
  - **潜状态平铺（Latent State Tiling）**：`z_uni` 平铺5次后传给运动模块，保证视觉导航与运动执行之间的连续信息广播。

### 2.3 特权教师策略训练（Oracle Policy Learning）
- 输入：本体感知 `Xpro`、当前导航目标、scandots（脚部周围扫描高度 `S ∈ R^{66×2}`）、特权信息 `Xpri`。
- 奖励设计：速度跟踪奖励（朝向路点方向）、躯干高度约束（保持直立）、脚部离地时间累积（促进跳跃/跨步等自然步态），不预设运动模式。

### 2.4 统一策略训练（Unified Hiking Policy Learning）
- 学生策略接收深度序列，通过 TC-ViTs 生成 `z_uni`、`δg0`、`g1`，结合本体感知输出动作。
- 基础蒸馏损失：包含潜变量、导航目标、动作三个层面的重建（L2 / SmoothL1 损失）。

### 2.5 分层损失度量集（Hierarchical Loss Metric Set）
- **动机**：传统特权蒸馏仅监督整体分布或逐关节误差，忽略关节间依赖；容易导致学生策略产生机械损伤风险。
- **方法**：
  - 使用带掩码的变分自编码器（VAE）学习教师动作空间的分层结构先验，随机掩码部分关节并要求重建完整动作，促使 VAE 捕获关节间结构依赖（并加入正弦/余弦位置编码处理无序关节）。
  - 蒸馏时用 VAE 编码器在结构特征空间中计算师生动作的余弦相似度损失 `L_ts`，并引入带掩码的 triplet 距离 `L_trip`（对比教师动作、学生动作、掩码学生动作）。
- **效果**：迫使学生的动作行为符合机器人自身物理结构的内在一致性，提高动作合理性与机械安全性，且不依赖来自人类数据的行为先验。

## 3. 实验设计

### 3.1 机器人平台
- **Unitree H1**（成人尺寸，5.9 ft / 47 kg）
- **Unitree G1**（儿童尺寸，4.26 ft / 35 kg）
- 两者体形、扭矩密度、形态差异大，用于验证方法的跨形态泛化性。

### 3.2 仿真环境
- 基于 **Isaac Gym** 物理仿真器。
- 使用了 **5 种不同 trail 类型**，每种含 **5 个难度等级**。
- 每个实验配置 **512 个随机生成的机器人**，每回合时长 **30 秒**，结果在 **5 次独立运行**上取平均。

### 3.3 评估指标（6 个）
- **目标完成度**：成功率 SR（%）、小径完成率 TC（%）、穿越率 TR（%）
- **安全性**：脚部边缘碰撞率 MEV（%）、摔倒前存活时间 TTF（秒）
- **效率**：成功回合到达终点的时间 T2R（秒）

### 3.4 对比方法
- **Oracle**：教师策略上界，拥有特权信息和专家导航目标。
- **w TC-ViTs**：LEGO-H 去掉分层损失度量集（HLM）的变体。
- **Vanilla**：LEGO-H 将 TC-ViTs 替换为 ConvGRU 的变体。
- **EP-H**：将四足机器人极端跑酷方法 EP 改编为适于 H1 的版本——逐帧处理深度图，不考虑长期目标对齐。
- **RMA-H / RMA-B**：将 RMA（快速运动适应）改编为有视觉输入/盲区两种版本，使用冻结教师策略 + 适配器网络映射感知数据。

## 4. 资源与算力

- **论文未明确提及任何具体算力信息**（GPU 型号、数量、训练时长等）。仅在“Implementations”中提到使用 PPO 算法、Dagger 和 Actor-Critic 辅助特权学习，全部在 Isaac Gym 中完成仿真。未提供训练能耗、硬件配置等量化数据。

## 5. 实验数量与充分性

### 已进行的实验
- **消融实验**（主成分）：对比 Oracle、LEGO-H、w TC-ViTs、Vanilla 在 6 项指标上的表现。
- **行为涌现分析**：不同类型地形下的运动行为（行走、跨步、跳跃、侧倾、绕行等）；堵路场景下的导航决策（绕行/尝试跨越）；H1 与 G1 在相同地形上的不同行为风格（步行下台阶 vs 跳跃下台阶）。
- **基准对比**（Table 2）：LEGO-H 与 EP-H、RMA-H、RMA-B 的全面对比。

### 充分性与客观性评估
- **优点**：消融设计能够分离“时间视觉 Transformer”和“分层损失度量集”的独立贡献；对比方法覆盖了“无视觉”、“逐帧视觉”、“纯运动适应”等典型代表，能有力地回答“视觉是否必要”“何种视觉有效”“统一学习是否关键”三个问题；多地形、多难度、多随机种子、512 机器人并行统计增强了结论的可靠性。
- **不足**：
  - 仅在一个仿真器（Isaac Gym）中验证，没有真实世界实验（但论文提到 LEGO-H 为 sim2real 训练设计，实际部署留待未来）。
  - 基准对比方法数量有限，且均为从四足/RMA 改编，并非专门针对人形徒步的成熟算法。
  - 附录中提及的更多消融和实验细节在正文中没有完整列出（正文只说“Refer to Appendix”），审阅时评估完整性需依赖附录。
  - 对“未见过的 trail/test-time 泛化”没有明确单独评估（训练与测试地形可能来自同一分布）。

## 6. 主要结论与发现

- **TC-ViTs 是基础**：将导航重构为顺序预期问题、融合目标信息与时空视觉特征，显著优于 ConvGRU 变体（Vanilla），是多层级协调的关键。
- **分层损失度量集提升安全性**：加入 HLM 后，成功率从 64.73% 提升到 68.40%，脚部碰撞率从 10.40% 降至 7.84%，存活时间提高，说明结构一致性约束对机械安全和任务效率均有益。
- **LEGO-H 接近 Oracle 上界**：在效率（T2R）和安全性（MEV、TTF）上，LEGO-H 与 Oracle 相当甚至略优，尽管在成功率和完成率上仍落后，说明视觉条件下的统一学习具有优异实用潜力。
- **视觉是刚需**：RMA-B（盲）在所有指标上显著落后。
- **目标对齐的多尺度视觉感知比其他形式更有效**：EP-H 因缺乏连续目标对齐，容易出现绕圈和路径丢失。
- **统一学习带来适应性**：RMA-H 只能在直道上表现好，遇到转弯/障碍时失败，说明仅靠运动反馈无法支持具身决策。
- **涌现行为多样化**：不同地形触发不同步态；机器人会自主选择绕行或跨越；不同物理结构的机器人（H1/G1）发展出不同运动风格。

## 7. 优点

- **问题定位新颖且具有现实意义**：将“复杂小径徒步”定义为人形机器人综合技能测试床，弥补了运动控制与语义导航长期割裂的空白。
- **架构设计巧妙**：
  - TC-ViTs 通过“目标平铺成通道+当前帧双路处理+GRU 循环适应”，同时兼顾长期目标、即时空间细节和本体感知。
  - 隐式导航-运动接口（只传最近目标 + 潜变量平铺）解决了真实硬件上视觉频率和运动频率不匹配的问题。
- **特权学习改进有深度**：用带掩码的 VAE 学习关节间结构依赖，而非简单模仿教师动作，大大提升了蒸馏后的运动安全性和合理性。
- **跨形态验证**：在 H1 和 G1 两种不同体形/扭矩特性的机器人上验证，展示方法的普适性。
- **实验指标全面**：覆盖任务完成度、安全性、效率三个维度，且统计了均值和标准差，展现随机性。

## 8. 不足与局限

- **缺乏真实世界部署验证**：所有实验均为仿真结果，未提供实体机器人测试，真实环境中的视觉噪声、延迟、执行器限制等尚未考虑。
- **算力信息缺失**：未报告 GPU 型号、数量、训练时间、显存等资源开销，不利于复现和成本评估。
- **简化假设**：为了简化任务，冻结了机器人上半身姿态，仅使用下肢运动；现实中许多小径需要手臂支撑或全身协调，限制其适用范围。
- **对比基线有限**：只改编了两个代表性子类（EP、RMA），缺少与其他 HRL 或视觉导航方法的直接比较。
- **未展示不同 trail 类型的单独结果**：表 2 只给总分，未按 5 类地形/难度细分，无法评估在何种地形下表现最弱。
- **行为多样性依赖仿真随机性**：涌现行为是否能在真实世界重复，未得到证明。
- **任务设定简化了真实徒步**：假设只有一个中间路点、GPS 信息可用、全部在小径上起始等，而与真实徒步中可能出现的 GPS 漂移、通信丢失、地图不确定性等复杂条件仍有距离。

（完）
