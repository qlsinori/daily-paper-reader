---
title: "Reasoning in Visual Navigation of End-to-end Trained Agents: A Dynamical Systems Approach"
title_zh: 端到端训练智能体视觉导航中的推理：一种动力系统方法
authors: "Janny, Steeven, Poirier, Hervé, Antsfeld, Leonid, Bono, Guillaume, Monaci, Gianluca, Chidlovskii, Boris, Giuliari, Francesco, Del Bue, Alessio, Wolf, Christian"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Janny_Reasoning_in_Visual_Navigation_of_End-to-end_Trained_Agents_A_Dynamical_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 具身视觉导航; 端到端训练智能体; 语言条件行为; 潜在记忆
tldr: 现有具身导航研究多在仿真中评估，本文针对端到端训练智能体在真实机器人上的快速移动导航行为进行了大规模实验研究，分析其内部推理、学习到的动力学与感知的交互，并考察潜在记忆对行为的影响，揭示零样本和语言条件行为背后的机制，为评估端到端导航智能体提供了新的分析视角。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 787, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 453, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1835, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 435, \"height\": 191, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 856, \"height\": 354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 731, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1639, \"height\": 503, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1637, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 732, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 827, \"height\": 410, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1254, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 589, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 591, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 589, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 153, \"label\": \"Table\"}]"
motivation: 仿真评估为主但真实机器人行为分析不足，需要理解端到端训练智能体的推理和记忆机制。
method: 在真实环境中使用物理机器人开展大规模导航实验，分析开环预测中学习到的动力学、感知耦合以及潜在记忆的运用。
result: 揭示了端到端智能体在视觉导航中涌现的动力学推理模式，并展示潜在记忆如何支持语言条件下的导航行为。
conclusion: 表明端到端训练能在真实机器人上形成可解释的推理与记忆机制，为鲁棒的具身导航系统提供参考。
---

## Abstract
Progress in Embodied AI has made it possible for end-to-end-trained agents to navigate in photo-realistic environments with high-level reasoning and zero-shot or language-conditioned behavior, but evaluations and benchmarks are still dominated by simulation. In this work, we focus on the fine-grained behavior of fast-moving real robots and present a large-scale experimental study involving \numepisodes navigation episodes in a real environment with a physical robot, where we analyze the type of reasoning emerging from end-to-end training. In particular, we study the presence of realistic dynamics which the agent learned for open-loop forecasting, and their interplay with sensing. We analyze the way the agent uses latent memory to hold elements of the scene structure and information gathered during exploration. We probe the planning capabilities of the agent, and find in its memory evidence for somewhat precise plans over a limited horizon. Furthermore, we show in a post-hoc analysis that the value function learned by the agent relates to long-term planning. Put together, our experiments paint a new picture on how using tools from computer vision and sequential decision making have led to new capabilities in robotics and control. An interactive tool is available at https://visual-navigation-reasoning.github.io

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：具身 AI（Embodied AI）中端到端训练的导航智能体虽然在仿真环境中已能实现高层推理、零样本或语言条件行为，但大多数评估仍停留在仿真阶段。本文关注的是**真实机器人上快速移动时的细粒度行为**，探讨端到端训练究竟让智能体“学到了什么”。
- **核心问题**：端到端强化学习训练的视觉导航策略，是否在其内部涌现出可解释的推理机制——包括对机器人动力学的隐式建模、感知与预测的交互、潜在记忆的利用，以及短/中期的规划能力？
- **整体含义**：文章通过大规模真实机器人实验（262 个导航片段）证明，在仿真中引入真实机器人动力学模型后，端到端智能体会在内部形成类似“预测—校正”的动力学推理机制，并利用潜在记忆编码场景结构和探索信息。这一发现为理解视觉导航智能体的内部机制提供了新的视角，也为更精细的 sim2real 迁移提供依据。

## 2. 论文提出的方法论

- **基本框架**：基于 Bono et al. (CVPR 2024) 的工作，使用 PPO 算法在 Habitat 仿真器中端到端训练策略，并引入由真实机器人辨识得到的**二阶动力学模型**替代传统“瞬时位移”运动模型。智能体输出目标线速度/角速度命令，而非相对位置命令。
- **网络输入与记忆**：智能体在每步接收 RGB 图像、4 个 RealSense 深度传感器构成的扫描向量、起点相对极坐标目标、两种定位信息（轮式里程计积分和 AMCL 定位），以及上一动作。这些输入通过专用编码器（ResNet-18、1D-CNN、MLP 等）融合进一个双层 GRU 的隐状态 \(h_t\) 中，作为潜在记忆；策略网络为线性层输出 28 个离散速度命令对。
- **工程改进**（非核心贡献但影响性能）：
  - 训练步数从 200M 增加到 500M；
  - 角度输入改用 sin/cos 编码；
  - 测试时也进行 RGB 数据增强；这些改进使真实场景成功率相对原始工作提升约 +50%。
- **分析工具与技术细节**：
  - **输入 vs 动力学敏感性分析**：定义“距离到信念”（Dbelief，单位米）作为衡量环境扰动（动力学参数变化、里程计噪声）影响的统一度量；在一致性尺度下比较不同扰动对成功率的影响。
  - **动力学探针（probing）**：从隐状态训练线性探针预测未来姿态，评估智能体是否学到内部动力学。
  - **RMA 式自适应策略**：借鉴 RMA（Rapid Motor Adaptation），将环境动态参数编码为嵌入向量作为策略输入，训练对动态变化鲁棒的策略。
  - **记忆消融**：周期性置零隐状态，或在距目标 <2m 时清除记忆。
  - **占用图探针**：从隐状态预测局部占用栅格地图（3m×3m）。
  - **规划质量评估**：使用 Fast Marching Square 专家规划器构造成本函数，比较智能体动作与专家动作的成本差。
  - **Shapley 值分析**：量化各输入模态（里程计、定位、RGB、扫描、上一动作）对导航性能的贡献。

## 3. 实验设计

- **仿真环境**：
  - Habitat 仿真器 + 真实机器人二阶动力学模型（“Sim（+dyn.）”）。
  - 主要评估集：HM3D 验证集的 2500 个片段（HM3D/2.5k）、HM3D 验证子集 250 个片段（HM3D/250），以及真实测试楼层的仿真副本（Test-bldg/20）。
- **真实环境**：
  - 使用 Rookie 实体机器人，在真实办公楼中进行导航实验；
  - 评估片段：Test-bldg/20（20 个片段）、Test-bldg/14（14 个片段）；
  - 总计 262 个真实导航片段（多次重复实验累计）。
- **任务**：点目标导航（PointGoal Navigation），目标以起点相对极坐标给出。
- **对比方法**：
  - (a) D4：4 个离散动作（前进 25cm、左右转 10°、停止），无动力学模型；
  - (b) D28-instant：28 个速度命令对，但训练时使用瞬时速度（无动力学模型）；
  - (c) D28-dynamics：28 个速度命令对 + 辨识的真实动力学模型（本文主要分析对象）。
- **评价指标**：成功率（SR）、SPL（路径长度加权成功率）、SCT（完成时间加权成功率）。

## 4. 资源与算力

- 论文正文中**未明确报告 GPU 型号、数量及训练时长**。仅提到训练步数为 500M 环境步（相对原始 200M），且分析模型在 Nvidia Jetson AGX Orin 上执行前向推理耗时约 100ms（决策循环 3Hz，即 333ms 周期）。具体算力资源未说明。

## 5. 实验数量与充分性

- **实验规模**：
  - 真实环境：262 个导航片段（包括 4 次 ×20 片段的重复实验以报告均值/标准差）；
  - 仿真：HM3D/2.5k 验证集、HM3D/250 子集；
  - 大量分析性实验：动力学敏感性（两种动态扰动、多种参数水平）、RMA 鲁棒性（3 种动态参数 ×3 个扰动区间）、动力学探针（39k 轨迹、20 步预测）、记忆消融（3 种周期 + 距离阈值 + 无条件消融）、占用图探针（模拟/真实）、规划质量对比（60 个片段 + 单片段）、Shapley 值分析、视觉定位替换实验等。
- **充分性与公平性**：
  - 优点：实验覆盖了仿真与真实场景，真实实验重复 4 次以减小随机性，多种分析互相印证；对比了有/无动力学训练的智能体，验证了动力学建模的重要性；消融设计较为系统。
  - 不足：真实实验片段数相对有限（20 个/组），统计功效受限；对规划能力的分析较多依赖定性观察（如单 episode 的价值函数曲线），缺乏大规模统计检验；部分实验（如占用图探针）在真实数据上的精度受定位误差和动迁影响，作者也做了相应说明。

## 6. 论文的主要结论与发现

- **智能体确实学到了内部动力学模型**：通过探针实验，从隐状态可以以较低误差（20 步约 6 秒，平均位姿误差 0.76m）预测未来姿态，说明隐状态包含短至中期运动预测信息。
- **预测与感知形成“预测—校正”机制**：对输入（里程计）的扰动比对动力学参数的扰动更敏感，表明智能体在利用感知不断校正内部预测，类似于卡尔曼滤波思想。
- **真实动力学训练是 sim2real 的关键**：相比无动力学模型训练（瞬时速度），带动力学训练的智能体在真实环境中成功率从 10% 提升至 92.5%，且轨迹更平滑、更快速。
- **潜在记忆编码场景结构**：从隐状态可重建局部占用图，在门、玻璃墙等困难区域判断仍较准确；周期性清除记忆会显著降低成功率（如每 3 秒清空时 SR 下降约 25%）。
- **存在有限范围的规划能力**：价值函数估计在智能体改变策略时出现明显不连续，说明其具有路径级别的“长时”估计（但不一定是最优规划）；与专家规划器比较显示在瓶颈区域（门、窄通道）决策接近专家，但在需要全局路径选择时存在“隧道视野”失败案例。
- **输入模态重要性排序**：Shapley 值显示里程计和扫描最重要，RGB、定位和上一动作贡献较小。
- **未发现真正的长期规划能力**：智能体在需要长期战略选择的复杂场景中会陷入死胡同，缺少人类式的高层几何理解和情境感知。

## 7. 优点

- **真实场景大规模验证**：不仅限于仿真，262 个真实机器人导航片段为结论提供了直接证据。
- **分析手段新颖且多样**：提出“距离到信念”（Dbelief）统一扰动度量，设计动力学探针、占用图探针、价值函数后验分析等方法，从多个角度交叉验证智能体内部表征。
- **对比设计清晰**：通过有无动力学训练的两组策略对比，直接证明了真实动力学建模对端到端导航迁移的决定性作用。
- **工程改进可复现且有效**：简单修改（sin/cos 编码、测试时增强、更长的训练）带来真实场景成功率大幅提升，对实践有指导意义。
- **附有交互式工具和补充材料**，便于深入分析动力学行为。

## 8. 不足与局限

- **算力资源未透明**：未报告 GPU 型号、总数、训练总时长，不利于成本评估和复现计划。
- **真实实验规模有限**：每组真实实验仅 14–20 个片段，虽然多轮重复，但统计置信度仍有限；对规划能力的大多数分析基于少量示例（如单个 episode 的价值曲线），缺乏大规模定量验证。
- **长期规划能力未被证实**：作者承认智能体没有表现出正确的长期计划，存在“隧道视野”；这使得“推理”结论局限于短期动力学和有限规划。
- **视觉定位替代实验失败**：用纯视觉定位（R2D2+检索）替换 AMCL 后成功率大幅下降（42.9% vs 100%），表明当前策略对精确局部定位的依赖较强，泛化性受限。
- **结构性局限**：目标以起点相对坐标而非视觉目标给出，这使任务本质上依赖定位信息，可能掩盖视觉语义推理的涌现；语言条件行为在本文中并未直接涉及。
- **动力学敏感性分析中的扰动范围有限**：对动力学参数的扰动幅度可能未覆盖真实机器人老化、负载变化等极端情况；RMA 实验中使用了真值环境参数嵌入，实际部署时需额外估计这些参数。

（完）
