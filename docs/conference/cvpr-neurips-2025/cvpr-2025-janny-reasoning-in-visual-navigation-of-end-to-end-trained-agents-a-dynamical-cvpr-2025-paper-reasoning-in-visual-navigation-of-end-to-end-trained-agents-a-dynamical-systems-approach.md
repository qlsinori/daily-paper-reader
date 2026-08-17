---
title: "Reasoning in Visual Navigation of End-to-end Trained Agents: A Dynamical Systems Approach"
title_zh: 端到端训练智能体的视觉导航推理：一种动力系统方法
authors: "Janny, Steeven, Poirier, Hervé, Antsfeld, Leonid, Bono, Guillaume, Monaci, Gianluca, Chidlovskii, Boris, Giuliari, Francesco, Del Bue, Alessio, Wolf, Christian"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Janny_Reasoning_in_Visual_Navigation_of_End-to-end_Trained_Agents_A_Dynamical_CVPR_2025_paper.pdf"
tags: ["query:vln-memory"]
score: 8.0
evidence: 分析端到端智能体在视觉导航中的潜在记忆，与记忆增强的具身导航相关
tldr: 具身AI中的端到端导航智能体虽已具备高层推理和语言条件行为，但评测多以仿真为主。本文利用真实物理机器人大规模导航实验，系统分析端到端训练所涌现的推理方式、开放环预测的动态建模以及潜在记忆的使用机制。研究发现真实环境下的行为动态与记忆表征密切相关，为理解端到端导航智能体的内部推理和行为可解释性提供了重要实证。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 787, \"height\": 530}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 453, \"height\": 378}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1835, \"height\": 397}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 435, \"height\": 191}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 856, \"height\": 354}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 731, \"height\": 721}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1639, \"height\": 503}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1637, \"height\": 420}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 732, \"height\": 564}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 827, \"height\": 410}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1254, \"height\": 306}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 589, \"height\": 306}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 591, \"height\": 188}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 589, \"height\": 268}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 153}]"
motivation: 端到端导航智能体的行为推理和潜在记忆在真实机器人上缺乏大规模实证分析。
method: 在物理机器人上开展大规模导航实验，从动力学系统视角分析智能体学到的开放环预测动态与潜在记忆的交互。
result: 揭示了端到端训练中智能体所形成的现实动态和记忆使用模式，有助于解释语言条件下的导航推理。
conclusion: 强调真实环境实验对理解和改进端到端视觉导航智能体的重要性，为记忆增强导航提供实证基础。
---

## Abstract
Progress in Embodied AI has made it possible for end-to-end-trained agents to navigate in photo-realistic environments with high-level reasoning and zero-shot or language-conditioned behavior, but evaluations and benchmarks are still dominated by simulation. In this work, we focus on the fine-grained behavior of fast-moving real robots and present a large-scale experimental study involving \numepisodes navigation episodes in a real environment with a physical robot, where we analyze the type of reasoning emerging from end-to-end training. In particular, we study the presence of realistic dynamics which the agent learned for open-loop forecasting, and their interplay with sensing. We analyze the way the agent uses latent memory to hold elements of the scene structure and information gathered during exploration. We probe the planning capabilities of the agent, and find in its memory evidence for somewhat precise plans over a limited horizon. Furthermore, we show in a post-hoc analysis that the value function learned by the agent relates to long-term planning. Put together, our experiments paint a new picture on how using tools from computer vision and sequential decision making have led to new capabilities in robotics and control. An interactive tool is available at https://visual-navigation-reasoning.github.io

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：具身 AI（Embodied AI）中，端到端训练的导航智能体已在照片级真实环境中实现高水平的导航行为，甚至支持零样本或语言条件导航，但绝大多数基准仍以仿真为主。传统导航研究存在两条路线：一条是机器人学视角，强调感知重建 + 规划（如 SLAM）；另一条是机器学习视角，将导航建模为 POMDP 并用强化学习（RL）求解。
- **核心问题**：当端到端训练的智能体采用**真实物理机器人动力学模型**（而非传统 stepwise teleportation）时，智能体内部究竟学到了何种“推理”？具体而言：
  - 是否学到一个潜在动力学模型，用于开环预测？
  - 这种预测如何与感知观测相互作用（类似卡尔曼滤波）？
  - 潜在记忆如何编码场景结构和探索信息？
  - 是否涌现出短期或长期规划能力？
- **整体含义**：作者通过大规模真实机器人实验（262 个导航回合），揭示了端到端训练中涌现的动力学模型、预测-校正机制、记忆使用模式以及有限视野的规划能力，对理解具身智能体的内部推理机制和 sim2real 迁移具有重要意义。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **总体框架**：基于 Bono et al. [9] 的工作，使用 PPO 在 Habitat 模拟器中训练策略，但训练时在模拟器中引入**从真实机器人识别的二阶动力学模型**，使智能体学习的是连续速度控制而非离散位置跳变。
- **智能体结构**：
  - 输入：RGB 图像 \( I_t \)、Lidar 风格的距离向量 \( S_t \)、里程计 \( \hat{p}^r_t \)、AMCL 定位 \( \hat{p}^a_t \)、静态点目标 \( g_0 \)、上一动作 \( a_{t-1} \)。
  - 核心为两层 GRU，更新潜在记忆 \( h_t = d(h_{t-1}, v(I_t), u(S_t), g_0, \hat{p}^r_t, \hat{p}^a_t, e(a_{t-1})) \)。
  - 策略为线性层：\( a_t = \omega(h_t) \)，输出 28 个离散的线速度/角速度命令对。
- **关键改进（非贡献部分）**：
  - 训练步数从 200M 提升到 500M；
  - 将原始角度输入替换为 sin/cos 嵌入；
  - 测试时也进行 RGB 数据增强（单这一项使真实环境 SR 提升约 15%）。
- **动力学模型融入**：在 Habitat 中嵌入真实机器人的二阶动力学模型，使策略直接输出目标速度，而不是高层位置指令，从而训练出平滑、快速、可直接部署的导航策略。
- **分析工具与方法**：
  - **输入 vs. 模型敏感性分析**：定义“距离到信念”（distance to belief，\( D_{\text{belief}} \)）作为中介指标，量化环境参数变化（如阻尼、响应时间、最大速度、里程计噪声）对智能体行为的影响，从而比较不同扰动对策略的影响。
  - **RMA 式自适应策略**：受 RMA [43] 启发，将环境参数编码为嵌入 \( e_E \)，输入策略 \( a_t = \omega(h_t, e_E) \)，使智能体在动力学变化时仍能保持性能。
  - **动力学探针（probing）**：从隐藏状态 \( h_t \) 用线性模型或带上一动作/目标的模型预测未来位姿 \( p_{t+i} \)，检验智能体内部是否编码了未来状态预测。
  - **记忆消融**：周期性将 \( h_t \) 置零，观察性能变化。
  - **Shapley 值分析**：评估各输入模态对导航性能的贡献。
  - **专家规划器对比**：用 Fast Marching Square 方法构建成本函数 \( C(p_t, a_t) \)，计算动作质量指标 \( M(t) = C(p_{t+1}, a_{t+1}) - C(p_t, a_t) \)，绘制规划质量热图。

## 3. 实验设计：数据集/场景、Benchmark、对比方法

- **数据集与场景**：
  - **仿真**：HM3D 验证集（2500 episodes，HM3D/2.5k），HM3D val-mini（250 episodes，HM3D/250）。
  - **仿真+真实动力学模型**：上述场景均使用带真实动力学模型的 Habitat 模拟器。
  - **真实环境**：自建办公楼（Test-bldg/20 共 20 个 episode，Test-bldg/14 共 14 个 episode），使用 Rookie 物理机器人，搭载 Nvidia Jetson AGX Orin。
- **评估指标**：成功率（SR）、SPL（按路径长度加权成功率）、SCT（按完成时间加权的成功率，考虑动力学）。
- **对比方法**：
  - (a) **D4**：4 个离散动作（前进 25cm、左转/右转 10°、停止），无动力学模型；
  - (b) **D28-instant**：28 对速度命令，但模拟器为瞬时速度（teleportation），无动力学；
  - (c) **D28-dynamics**：28 对速度命令 + 识别的真实二阶动力学模型，即本文主要分析对象（对应 Bono et al. [9] 的复现+改进）。
- **主要实验类型**：
  - 敏感性分析（对动力学参数和输入噪声）；
  - RMA 自适应策略实验；
  - 动力学探针（未来位姿预测）；
  - 记忆消融（周期置零）；
  - 规划质量热图（60 个真实 episodes）；
  - Shapley 值分析；
  - 视觉定位替换（R2D2 vs AMCL）；
  - 决策延迟和最大速度的影响测试。

## 4. 资源与算力

- **论文中未明确提及**具体的 GPU 型号、数量或训练耗时。唯一提到的算力相关信息是：
  - 训练步数从 200M 提升到 500M（环境交互步数）；
  - 真实机器人上使用 Nvidia Jetson AGX Orin 进行 onboard 推理（网络前向约 100ms，决策循环 3Hz 下预留 333ms）。
- 因此，训练所用 GPU 集群规模、总计算量（如 GPU 小时数）在论文中**没有公开**，这是一个信息缺口。

## 5. 实验数量与充分性

- **实验规模**：
  - 真实机器人实验共 **262 个导航回合**，覆盖面广，是当前同类工作中较大规模的真实部署评估；
  - 主要对比实验（Table 3）中，D28-dynamics 在真实环境上进行了 4 次重复实验（每次 20 episodes），报告了均值和标准差，具有良好的统计意义。
- **消融与分析实验**：
  - 记忆消融（4 种频率设置）；
  - 最大速度限制（3 档）；
  - 决策延迟（6 档）；
  - 输入扰动（多种动力学参数和噪声水平）；
  - Shapley 值分析（对 5 类输入模态）；
  - 动力学探针（39k 条轨迹、20 步预测）；
  - 规划质量热图（60 episodes 聚合）；
  - 占位图探针（模拟和真实数据）。
- **充分性评价**：
  - **充分**：真实实验+仿真实验相结合，涵盖动力学、记忆、规划、感知多个层面，方法对比清晰。
  - **客观公平**：对比了有无动力学模型训练的影响，并针对真实世界场景做了重复实验；但也存在一些局限，例如部分分析基于单一测试建筑，视觉定位替换实验中 R2D2 的性能受限于 STOP 精度，不同输入扰动之间的可比性通过 \( D_{\text{belief}} \) 进行了标准化，设计较为严谨。

## 6. 论文的主要结论与发现

- **端到端训练涌现了潜在动力学模型**：智能体在无显式动力学监督的情况下，学会了用潜在状态进行开环预测，并通过感知（尤其是里程计）进行校正，形成类似卡尔曼滤波的预测-校正机制。
- **现实动力学训练至关重要**：带动力学模型训练的策略在真实环境上 SR 达到 92.5%，远高于无动力学模型训练的策略（D28-instant 为 10%，D4 为 0%），证明动力学建模对 sim2real 迁移具有决定性作用。
- **记忆编码场景结构和探索信息**：通过探针网络，从隐藏状态 \( h_t \) 可重建以机器人为中心的局部占用图（3m×3m），且与真实场景结构高度吻合；周期性清空记忆会导致 SR 下降（3s 清空时下降 25%），说明记忆对长期探索和避免重复访问至关重要。
- **存在有限视野的规划**：线性探针可从隐藏状态预测未来 6 秒内的位姿（平均误差约 0.76m），且预测轨迹能与真实轨迹在方向变化上对齐，说明记忆中存在短到中期计划；但自回归滚动预测效果一般，说明智能体并非显式地长期滚动潜在状态。
- **价值函数与长期规划相关**：通过一个真实演示 episode 的价值函数可视化，发现智能体在重新规划路径时价值估计会发生突变，表明 PPO 的 critic 在一定程度上捕获了长期回报预期。
- **长期规划仍不可靠**：存在“隧道视野”问题，智能体常选择人类一眼就能判断为无效的长远路径，缺乏高层几何理解。
- **输入重要性排序**：Shapley 分析显示，智能体高度依赖里程计和激光扫描，RGB 和定位贡献较小。用视觉定位（R2D2）替代 AMCL 时 SR 大幅下降（42.9% vs 100%），说明精确的最后一米定位能力并未从 RL 中自发涌现。

## 7. 优点

- **真实世界大规模验证**：262 个物理机器人导航回合，远超同类工作常见的纯仿真评估，结论更具说服力。
- **多维度的可解释性分析**：将动力学系统、记忆、规划、价值函数等抽象概念转化为具体可操作的探针实验和敏感性度量。
- **严谨的对照设计**：通过对比有无动力学训练、不同动作空间，以及通过“distance to belief”标准化不同扰动，使不同变量的影响可比较。
- **提供了实用工程改进**：测试时数据增强、sin/cos 嵌入、增加训练步数等简单手段显著提升了真实性能。
- **引入新的分析方法**：如输入 vs. 模型敏感性分析、动力学探针、规划质量热图，这些方法可推广到其他具身智能体分析。
- **开源交互工具**：附带动态模型交互工具，便于社区复现和进一步研究。

## 8. 不足与局限

- **算力细节缺失**：未报告 GPU 型号、数量、总训练时间，可复现性受到一定影响。
- **长期规划能力不足**：论文明确承认未发现可靠的长时规划，智能体存在“隧道视野”，因此结论仅支持短到中期规划。
- **真实实验场景单一**：真实实验仅在自建办公楼中进行，缺乏多样化的真实环境，且 episode 数量虽多但覆盖面积有限。
- **视觉定位失败**：用 R2D2 视觉定位替代 AMCL 时性能大幅下降，说明智能体未能从 RL 训练中自动学会精确视觉定位，限制了可解释性结论的适用范围。
- **记忆消融实验的公平性**：在周期性清空记忆时需要重置 episode 起点并重新定义目标，这可能引入额外变量，影响消融的纯粹性。
- **Shapley 分析基于改变输入模态**，使用“背景数据集”模拟缺失输入，可能不能完全反映真实部署中传感器故障的分布外情况。
- **动力学模型本身为二阶近似**，对于更复杂的非完整约束或地面摩擦变化，结论的泛化性有待进一步验证。

（完）
