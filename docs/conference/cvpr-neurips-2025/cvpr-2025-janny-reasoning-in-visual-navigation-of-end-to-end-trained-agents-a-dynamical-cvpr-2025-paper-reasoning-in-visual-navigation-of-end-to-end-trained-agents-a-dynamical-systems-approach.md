---
title: "Reasoning in Visual Navigation of End-to-end Trained Agents: A Dynamical Systems Approach"
title_zh: 端到端训练智能体视觉导航中的推理：动力系统方法
authors: "Janny, Steeven, Poirier, Hervé, Antsfeld, Leonid, Bono, Guillaume, Monaci, Gianluca, Chidlovskii, Boris, Giuliari, Francesco, Del Bue, Alessio, Wolf, Christian"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Janny_Reasoning_in_Visual_Navigation_of_End-to-end_Trained_Agents_A_Dynamical_CVPR_2025_paper.pdf"
tags: ["query:vln-memory"]
score: 8.0
evidence: 分析端到端视觉导航智能体的潜在记忆与推理机制，包含语言条件行为，与具身导航记忆高度相关
tldr: 针对端到端导航智能体在仿真中表现好但真实机器人行为细粒度理解不足的问题，在真实环境开展大规模导航实验，用动力系统视角分析智能体如何利用潜在记忆进行开环预测与感知交互。结果显示端到端训练中涌现的推理模式与动态预测关系密切，为评估和设计具身导航记忆机制提供了实证基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 787, \"height\": 530}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 453, \"height\": 378}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1835, \"height\": 397}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 435, \"height\": 191}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 856, \"height\": 354}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 731, \"height\": 721}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1639, \"height\": 503}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1637, \"height\": 420}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 732, \"height\": 564}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 827, \"height\": 410}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1254, \"height\": 306}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 589, \"height\": 306}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 591, \"height\": 188}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 589, \"height\": 268}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-janny-reasoning-in-visual-navigation-of-end-to-end-trained-agents-a-dynamical-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 153}]"
motivation: 具身智能导航评估仍以仿真为主，对真实机器人端到端导航中推理和记忆机制缺乏细粒度理解。
method: 在真实物理机器人上开展大规模导航实验，从动力系统角度分析潜在记忆、开环预测与感知的相互作用。
result: 揭示了端到端训练导航智能体涌现的动态推理模式，并阐明潜在记忆在其中的作用。
conclusion: 该分析框架有助于弥合仿真训练与真实部署之间的差距，指导导航记忆机制设计。
---

## Abstract
Progress in Embodied AI has made it possible for end-to-end-trained agents to navigate in photo-realistic environments with high-level reasoning and zero-shot or language-conditioned behavior, but evaluations and benchmarks are still dominated by simulation. In this work, we focus on the fine-grained behavior of fast-moving real robots and present a large-scale experimental study involving \numepisodes navigation episodes in a real environment with a physical robot, where we analyze the type of reasoning emerging from end-to-end training. In particular, we study the presence of realistic dynamics which the agent learned for open-loop forecasting, and their interplay with sensing. We analyze the way the agent uses latent memory to hold elements of the scene structure and information gathered during exploration. We probe the planning capabilities of the agent, and find in its memory evidence for somewhat precise plans over a limited horizon. Furthermore, we show in a post-hoc analysis that the value function learned by the agent relates to long-term planning. Put together, our experiments paint a new picture on how using tools from computer vision and sequential decision making have led to new capabilities in robotics and control. An interactive tool is available at https://visual-navigation-reasoning.github.io

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：近年来，Embodied AI（具身智能）的进展使得端到端训练的智能体能在照片级逼真的环境中实现高层级推理、零样本或语言条件化导航行为。然而，绝大多数评估和基准测试仍以仿真环境为主，对真实世界中快速移动机器人的细粒度行为理解不足。
- **核心问题**：本文关注的核心问题是——**端到端训练（End-to-End Training）的视觉导航智能体在实际部署到真实物理机器人后，其“推理”能力（尤其是与动力系统相关的推理）是如何涌现的？** 具体包括三个子问题：
  1. 智能体是否从与仿真环境的交互中**内在地学习到了一种隐式动力学模型**？
  2. 智能体的**潜在记忆（latent memory）**中编码了哪些场景结构信息与探索信息？
  3. 智能体的记忆与价值函数是否反映了**一定视界内的规划能力**？
- **整体意义**：本文通过大规模真实机器人实验，从动力系统（Dynamical Systems）视角揭示了端到端训练智能体的内部工作机制，表明模型无关的强化学习（Model-free RL）能够在智能体中催生出预测—校正（Prediction-Correction）式的滤波机制、隐式动力学模型以及有限时域内的规划能力。这为理解、评估并改进具身导航智能体的记忆与推理机制提供了实证基础，对弥合仿真训练与真实部署之间的鸿沟具有重要参考价值。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **总体思路**：复现并改进了 Bono et al. (2024) 的端到端视觉导航智能体 [9]，在此基础上从动力系统视角对智能体的行为进行深入剖析。核心思想是：如果在仿真器中加入真实的机器人动力学模型，端到端训练的智能体会“无中生有”地学到一个潜在动力学模型，并通过类似卡尔曼滤波的“预测—校正”机制进行状态估计。

- **智能体架构**：
  - 输入观测：RGB图像 \(I_t\)，Lidar/深度传感器扫描向量 \(S_t\)（4个RealSense深度传感器生成），当前位置估计（轮式编码器里程计 \(\hat{p}_t^r\) + AMCL定位 \(\hat{p}_t^a\)），静态点目标坐标 \(g_0\)，上一动作 \(a_{t-1}\)。
  - 隐状态更新（核心公式）：
    \[
    h_t = d(h_{t-1}, v(I_t), u(S_t), g_0, \hat{p}_t^r, \hat{p}_t^a, e(a_{t-1}))
    \]
    \[
    a_t = \omega(h_t)
    \]
    其中 \(d\) 是两层 GRU，\(v(\cdot)\) 是 ResNet-18 编码器，\(u(\cdot)\) 是 1D-CNN 编码器，\(e(\cdot)\) 是动作嵌入，\(\omega\) 是线性策略网络。
  - 辅助任务：线性头 \(l\) 从隐藏状态 \(h_t\) 动态预测相对目标位置 \(\hat{g}_t\)（在仿真中由特权信息监督）。
  - 动作空间：28个离散动作，每个动作对应一对线速度 \(a_v\) 与角速度 \(a_\omega\) 指令。

- **真实动力学建模**：在 Habitat 仿真器中集成了从真实机器人轨迹中辨识出的二阶系统动力学模型，策略输出目标速度（非位置控制），由动力学模型模拟真实机器人行为。

- **本文的工程改进（非贡献点）**：
  1. 训练步数从 200M 提升至 500M；
  2. 用 sin/cos 嵌入替代原始角度输入；
  3. 测试时也应用 RGB 数据增强（TTA），仅此一项即在真实环境中将 SR 提升 15%。

- **关键分析方法**：
  - **输入 vs. 模型敏感性分析**：通过扰动动力学参数（阻尼比、响应时间、最大速度）和里程计输入噪声（均值、标准差），以统一的“距离信念”（Distance to Belief, \(D_{belief}\)）指标衡量环境扰动幅度，对比策略在两种扰动下的成功率变化，从而判断智能体对输入和动力学模型的敏感程度。这用于验证是否学到了“预测—校正”式机制。
  - **RMA 式鲁棒性增强策略**：受 RMA [43] 启发，在训练时将环境参数变化 \(\Delta E\) 编码为嵌入向量 \(e_E\) 传入策略：\(a_t = \omega(h_t, e_E)\)，测试智能体能否适应动力学参数扰动。
  - **动力学探测（Probing dynamics）**：用隐藏状态 \(h_t\) 通过线性/非线性探测网络预测未来位姿 \(p_{t+i}\)，验证隐状态中是否编码了短中期动力学模型。
  - **占用图探测**：训练探测网络从 \(h_t\) 重建以机器人为中心的 3×3m 局部占用图。
  - **规划质量评估**：引入 Fast Marching Square 专家规划器 [78] 得到代价函数 \(C(p_t, a_t)\)，定义评估指标 \(M(t) = C(p_{t+1}, a_{t+1}) - C(p_t, a_t)\)，量化智能体每一步决策相对专业规划器的优劣。
  - **代理模型可解释性分析**：对输入模态（里程计、定位、RGB、扫描、上一动作）进行 Shapley 值分析 [72]，衡量各输入对 SR 和 SPL 的贡献。

## 3. 实验设计：使用数据集 / 场景、Benchmark、对比方法

- **测试环境与平台**：
  - **真实环境实验（Real）**：在真实办公楼层中使用 Rookie 物理机器人，共执行 **262 个导航情节**（主要实验集中在 Test-bldg/14（14个情节）和 Test-bldg/20（20个情节），另有若干附加实验）。
  - **仿真实验（Simulation + dyn. model）**：使用加入了真实动力学模型的 Habitat 仿真器。
    - **HM3D/2.5k**：HM3D [61] 验证集的 2,500 个情节。
    - **HM3D/250**：HM3D 验证集的一个子集（250 个情节）。
    - **Test-bldg/20 和 Test-bldg/14**：仿真器中对真实测试楼层的扫描复现版本。

- **任务设置**：静态点目标导航（PointGoal Navigation），智能体需要在纯视觉/传感器输入条件下导航至给定起始坐标系中的目标点。目标以极坐标形式给出，智能体需通过车载定位（轮式里程计 + AMCL）自行换算。

- **对比方法**：
  - **(a) D4** [66]：仅4个运动命令（前进25cm，左转10°，右转10°，停止），无动力学模型；
  - **(b) D28-instant** [80]：28对瞬时+恒定的速度指令，无动力学模型（即普通 Habitat 中的“瞬移”式运动）；
  - **(c) D28-dynamics** [9]：28对速度指令 + 辨识的真实动力学模型（本文复现并改进）。
  - 额外对比了**视觉定位方案**：用 R2D2 [63] + 图像检索 [46] 替代 AMCL 定位输入。

- **评估指标**：成功率（SR）、按路径长度加权的成功率（SPL）[1]、按完成时间加权的成功率下限（SCT）[80]。

## 4. 资源与算力

- **论文中未明确提供 GPU 型号、GPU 数量或具体训练时长等算力信息**。
- 仅提到训练步数从 Bono et al. [9] 的 200M 提升到 **500M 环境步数**，但未给出对应的 GPU 卡时数。这表明论文重点是实验分析与方法验证，而非资源效率报告。

## 5. 实验数量与充分性

- **实验规模**：
  - 真实环境：共 **262 个导航情节**，包括主实验（Table 3(c) 中 4 次重复 × 20 情节 = 80 个情节）、消融实验（14个情节/组）、延迟测试、速度限制测试等。
  - 仿真验证：HM3D/2.5k 和 HM3D/250 上的大规模评估。
  - 动力学探测：39k 条轨迹（HM3D 训练集生成，评估在未见场景上进行）。
  - 占用图探测：HM3D 训练集训练，在 Test-bldg 仿真和真实数据上评估。
  - 规划质量分析：60 个真实情节。

- **实验充分性评价**：
  - **优点**：实验数量在真实机器人研究中属于较大规模，且覆盖了仿真与真实环境、多种消融（记忆消融、速度限制、决策延迟、输入模态、视觉定位替换等），实验设计较为全面。真实场景重复了 4 次（每次 20 episodes）并报告了均值和标准差，体现了统计严谨性。提出的多种探测方法（动力学探测、占用图探测、价值函数分析）从多个角度交叉验证结论，增强了说服力。
  - **潜在不足**：真实环境的场景较为单一（仅一栋特定办公楼层，20 个目标点的导航），场景多样性有限；部分消融实验仅基于 14 个情节，样本量较小，结论可能存在一定偶然性。此外，主实验与消融实验在真实环境中使用不同情节数量，严格意义上并非完全对齐的对照组。

## 6. 论文的主要结论与发现

- **结论1：端到端智能体能隐式学到动力系统模型，并采用“预测—校正”机制**。输入/模型敏感性分析显示，智能体对里程计输入最敏感（依赖感知校正），对动力学参数变化（响应时间、阻尼比）也高度敏感。这表明智能体内部学到了一个潜在动力学模型用于开环预测，并通过传感输入进行闭环校正——类似于卡尔曼滤波的机制。
- **结论2：加入真实动力学模型的仿真训练对真实部署至关重要**。带动力学模型的策略（D28-dynamics）在真实环境中达到 92.5% SR（均值），远超无动力学模型变体（D28-instant 仅 10% SR）。
- **结论3：智能体潜在记忆编码了场景结构和探索信息**。从记忆 \(h_t\) 可高精度重建局部占用图；周期性清零记忆会显著降低性能（清零周期 3s 时 SR 下降 25%），表明记忆对保持已探索区域信息和最后几米的精确停靠至关重要。
- **结论4：存在短中期视界的规划能力，但长期规划能力有限**。通过探测实验，智能体可从记忆中以较低误差（6s 后约 0.76m）预测未来位姿，说明具备短中期规划/动力学预测能力。但长期规划存在“隧道视野”问题：当智能体选定某条长距离路径后，即使人类一眼即可判断该路径无效，智能体仍然难以主动放弃并重规划。
- **结论5：PPO 的 Critic 价值函数与长期规划相关**。对单情节价值函数的可视化分析发现，智能体在改变策略（重规划）时价值估计会出现明显跳变，说明价值函数反映了智能体对未来回报的长期预估。
- **结论6：不同输入模态的重要性存在显著差异**。Shapley 值分析显示，智能体高度依赖里程计和扫描输入，而 RGB、AMCL 定位和上一动作的贡献相对较低。用视觉定位（R2D2+检索）替换 AMCL 后性能大幅下降（SR 42.9% vs. 100%），表明在静态 PointGoal 任务中精确定位主要依赖里程计/激光而非视觉。
- **其他发现**：真实环境中将最大速度限制在训练速度的 70% 可提升成功率；决策延迟从 333ms 降至 150ms 左右对性能影响不大。

## 7. 优点

- **真实环境的大规模实证验证**：以 262 个真实机器人导航情节为核心实验数据，这在端到端导航分析工作中较为罕见。相比纯仿真分析，结论对真实部署具有更强的参考价值。
- **创新的分析方法**：
  - 提出“距离信念”（\(D_{belief}\)）指标，统一了不同物理量纲的扰动比较，使输入敏感性与动力学敏感性可公平叠加对比；
  - 将探测网络（probing）方法系统性地用于动力学预测与占用图重建，从隐状态中直接“读取”内存信息，方法简洁有效；
  - 引入经典控制理论视角（卡尔曼滤波类比、系统辨识），为深度 RL 智能体的可解释性分析提供了新的认知框架；
  - 结合 Shapley 值对多种输入模态进行量化归因分析，客观衡量各传感器对导航成功率的贡献。
- **多角度交叉验证**：从敏感性分析、动力学探测、内存消融、占用图重建、价值函数分析、专家规划器对比等多个维度对同一核心问题（智能体推理机制）进行交叉验证，结论相互印证、说服力强。
- **可视化与交互工具**：提供了占用图叠加、规划质量热力图、价值估计轨迹等多类可视化分析，并附有交互式工具，利于读者直观理解与复现。

## 8. 不足与局限

- **真实实验的广度有限**：真实环境实验仅在单一办公建筑内进行（14/20个目标点），场景类型和几何结构多样性不足，结论对其他类型环境（如家庭、仓库、室外）的可推广性有待验证。
- **样本量偏小**：部分消融实验（记忆清零、速度限制、延迟测试）仅基于 14 个情节，统计功效有限。且不同实验组之间的情节数不一致（14 vs. 20 vs. 60），严格对照性有所欠缺。
- **长期规划能力缺陷未被解决**：论文明确指出智能体存在“隧道视野”，无法有效评估并放弃长时程无效路径，但未提出改进方案，仅建议未来借助大规模几何基础模型来缓解。
- **算力信息缺失**：未报告 GPU 型号、数量、训练时长等资源信息，影响可复现性和对训练成本的理解。
- **可推广性限制**：
  - 训练任务限定为静态 PointGoal 导航，未覆盖更复杂的语义导航、语言导航或动态障碍物场景；
  - 动力学结论是基于特定机器人（Rookie 及其辨识模型）得出的，对其他平台（如四足、轮式差异驱动、无人机）的普适性缺乏讨论；
  - 视觉定位（R2D2）方案在本文设定下表现不佳，但这可能受限于训练数据与检索库的规模，不代表视觉定位方法本身的局限。
- **分析数据的代表性风险**：价值函数分析仅基于单个情节进行定性观察，虽然结果具有启发性，但缺乏跨多个情节的系统性定量统计。

（完）
