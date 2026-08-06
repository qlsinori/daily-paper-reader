---
title: "LOG-Nav: Efficient Layout-Aware Object-Goal Navigation with Hierarchical Planning"
title_zh: LOG-Nav：基于分层规划的高效布局感知物体目标导航
authors: "Jiawei Hou, Yuting Xiao, Xiangyang Xue, Taiping Zeng"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38893/42855"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向复杂多房间室内环境的布局感知物体目标导航
tldr: "复杂多房间室内环境中的物体目标导航面临长距离规划和局部感知的挑战。本文提出LOG-Nav，利用全局拓扑布局地图与局部场景记忆进行分层规划，由LLM智能体统一管理，无需人工交互或复杂训练。在MP3D基准上，LOG-Nav取得85%的成功率和79%的SPL，显著优于现有方法。该方法展示了布局感知分层规划在高阶导航任务中的有效性。"
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 873, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1629, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 878, \"height\": 565, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 662, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1683, \"height\": 591, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 860, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 863, \"height\": 266, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38893/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 835, \"height\": 540, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38893/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1501, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38893/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1759, \"height\": 498, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38893/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1455, \"height\": 277, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38893/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 794, \"height\": 282, \"label\": \"Table\"}]"
motivation: 复杂多房间环境中的物体目标导航需要高效布局感知与分层决策能力。
method: 采用全局拓扑布局地图与局部场景记忆，结合LLM智能体进行分层路径规划。
result: "在MP3D基准上实现85%成功率与79% SPL，大幅超过已有方法。"
conclusion: 布局感知与分层规划结合LLM可实现高效且无需训练的多房间物体目标导航。
---

## Abstract
We introduce LOG-Nav, an efficient layout-aware object-goal navigation approach designed for complex multi-room indoor environments. 
By planning hierarchically leveraging a global topologigal map with layout information and local imperative approach with detailed scene representation memory, LOG-Nav achieves both efficient and effective navigation.
The process is managed by an LLM-powered agent, ensuring seamless effective planning and navigation, without the need for human interaction, complex rewards, or costly training.
Our experimental results on the MP3D benchmark achieves 85% object navigation success rate (SR) and 79% success rate weighted by path length (SPL) (over 40% point improvement in SR and 60% improvement in SPL compared to exsisting methods). Furthermore, we validate the robustness of our approach through virtual agent and real-world robotic deployment, showcasing its capability in practical scenarios.

---

## 论文详细总结（自动生成）

# LOG-Nav：基于分层规划的高效布局感知物体目标导航 — 论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：家庭辅助机器人需要具备"根据用户指令定位并导航至目标物体"的核心能力。随着大语言模型（LLMs）和视觉-语言模型（VLMs）的快速发展，这一领域涌现出大量工作，但现有方法仍面临三大挑战：
  - **全局效率不足**：目标可能不在当前视野内，需要基于场景记忆规划全局高效路径，避免不必要的绕路。
  - **局部适应性差**：真实环境中场景可能发生动态变化（如新增障碍物），导航系统需要能实时适应。
  - **部署成本高**：许多方法依赖复杂奖励设计、人工交互或大规模训练，不利于实际部署。
- **研究空白**：现有方法（如L3MVN、ESC、VLFM等）要么缺乏全局布局级引导，要么使用从占用图中提取的静态拓扑路标，无法兼顾全局效率与局部鲁棒性。
- **核心回答**：本文提出 LOG-Nav，通过**分层规划**——将全局拓扑布局感知规划与局部动态自适应规划相结合——实现高效、鲁棒、无需训练的物体目标导航。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 2.1 核心思想
- **"先探索建图，后分层规划"**：机器人先自主探索未知环境，构建分层场景记忆；随后基于用户指令在大规模拓扑图上进行全局规划，再在机器人局部感知空间中进行精细路径生成。
- **LLM 智能体管控全流程**：无需人工干预、无需强化学习奖励或大规模训练。

### 2.2 分层场景表示（Hierarchical Scene Representation）
- 由两部分构成：
  - **全局拓扑度量地图（Topometric Map）**：\( G = (V, E) \)，其中 \( V \) 包含区域顶点（region vertices）和入口顶点（entrance vertices，如门、走廊口），\( E \) 为连接顶点的边。
  - **局部稠密神经隐式表征（Neural Implicit Representation）**：\( F: \mathbb{R}^3 \to \mathbb{R}^n \)（来自 Topo-Field），将 3D 位置映射到视觉-语言联合嵌入空间，用于语义目标定位。
- 输入仅需带位姿的 RGB-D 序列，场景表示训练无需额外标注。

### 2.3 分层规划（Hierarchical Planning）

**（1）全局拓扑规划（Global Topology Plan）**
- 将多模态指令（文本、图像或 3D 坐标）统一编码为目标嵌入（使用 CLIP 和 Sentence-BERT）。
- 在环境中均匀采样候选 3D 点集 \( P^* \)，通过神经隐式函数 \( F \) 计算各点的语义嵌入，与指令嵌入的余弦相似度最高者即为目标位置 \( p_{end} \)。
- 在拓扑图 \( G \) 上，从机器人当前位置 \( p_{start} \) 到目标 \( p_{end} \) 搜索最短路径，生成稀疏全局路标序列 \( V = \{v_1, v_2, \ldots, v_n\} \)（通常为房间出入口或走廊节点）。

**（2）局部自我中心规划（Local Ego-centric Plan）**
- 对于相邻全局路标 \( v_i \) 与 \( v_{i+1} \)，将 \( v_{i+1} \) 投影到机器人当前深度帧中。
- 采用**命令式学习（Imperative Learning, IL）** 规划器（基于 iPlanner），输入当前深度观测的特征嵌入与路标特征，规划出一组稠密局部路标 \( W_{i,i+1} = \{w_i^1, w_i^2, \ldots, w_i^m\} \)。
- 在导航逼近当前局部目标后，再继续规划下一段路线，实现**增量式局部重规划**，能实时应对环境变化。

**（3）整体路径结构**：
\[
p_{start} \to p_{end}: V = \{v_1, ..., v_n\}, \quad v_i \to v_{i+1}: W_{i,i+1} = \{w_i^1, ..., w_i^m\}
\]

### 2.4 LLM 驱动的导航智能体（LLM-powered Navigation Agent）
- LLM 智能体接收上下文 token 序列：\{背景信息 B, 用户指令 I, 场景地图 M, 规划数据 P, 轨迹 T, 状态 S, 可选技能 O, 行动决策 A\}。
- 智能体的三大职责：
  - **建图（Mapping）**：驱动机器人前沿探索（frontier-based），采集 RGB-D 数据构建场景表示。
  - **规划（Planning）**：根据场景记忆与指令，调用分层规划模块生成路径。
  - **导航（Navigation）**：执行路标序列，实时监测障碍与错误状态；若出现异常（如碰障、卡顿、超时等），智能体自动触发重规划或报告错误。
- 该设计使整个系统具备**自主决策、自更新**能力。

## 3. 实验设计

### 3.1 模拟仿真实验
- **数据集**：MP3D（Matterport3D），Habitat 仿真平台，超过 20 个多房间室内场景。
- **任务设置**：RGB-D 分辨率 480×640，帧率 15Hz，里程计提供位姿；自动探索采用"沿左侧前沿行驶"的简单策略。
- **评估指标**：
  - SR（Success Rate，成功率）
  - SPL（Success weighted by Path Length，按路径长度加权的成功率）
- **对比方法**：
  - 目标导航：CoW、ZSON、L3MVN、ESC、VLFM、PixNav、HOV-SG、PSL
  - 实例导航（text-goal / image-goal）：ZSON、PSL、LOG-Nav
  - 重复性比较：ZSON、PSL、L3MVN、ESC、LOG-Nav
- **主要结果（Tab.1）**：
  - 物体导航：LOG-Nav 取得 SR 85.6%、SPL 79.7%，相比已有最佳方法提升 >40%（SR）和 >60%（SPL）。
  - 实例导航（文本目标）：SR 78.6%、SPL 70.1%；实例导航（图像目标）：SR 67.3%、SPL 58.2%。
- **重复运行实验（Tab.3）**：LOG-Nav 的"先探索后规划"策略，单次地图构建成本可被多次规划任务摊薄（amortized），在 60 次重复运行中 SPL 达 0.656，远超所有对比方法。

### 3.2 真实世界部署实验
- **平台一**：SLAMTEC 移动底盘 + Franka Panda 机械臂 + RealSense D435 相机（眼在手上，手眼标定），约 225 平方米的多房间室内环境（含小型厨房台面、办公区、会议室、大厅）。
- **平台二**：Clearpath Jackal 移动机器人，相同相机配置。
- **任务内容**：物体目标导航（chair、sink、sofa，分别用文本和图像指令），每项测试 10 次。
- **鲁棒性验证**：在建图完成后，人为增设障碍物并微调场景，评估动态条件下的导航成功率（Tab.2）。
- **结果**：文本指令导航的 SR 在 60%–100% 之间；图像指令受目标外观遮挡与歧义影响，性能略有下降（30%–70%）。机器人能成功绕障或重规划，验证了局部自适应能力。

### 3.3 消融实验
- **全局规划消融（Fig.8）**：移除全局拓扑规划后，仅依赖局部 IL 规划直接导航至远程目标，SR 随距离增大显著下降，验证了全局规划的必要性。
- **局部规划消融（Tab.4）**：在真实场景中移除局部 IL 规划，改为直接调用移动基座的 API 导航，当障碍物数量从 0 增加到 3 时，SR 从 10/10 骤降至 1/10；而 LOG-Nav 在 3 个障碍物时仍保持 6/10 的 SR。

## 4. 资源与算力

- **论文未明确说明**具体的 GPU 型号、数量、训练时长、能耗等算力资源信息。
- 从方法描述推断：神经隐式场景表示（基于 Topo-Field）的训练需要一定 GPU 资源，但整体框架为"训练-free"（training-free）的零样本导航框架，不需要大规模强化学习训练或奖励设计。
- 可指出的是：论文未提供可复现性所需的详细算力清单，这是一个信息缺口。

## 5. 实验数量与充分性

### 5.1 实验数量
- **模拟实验**：1 个基准数据集（MP3D/Habitat），3 类任务（物体导航、文本实例导航、图像实例导航），对比 8 种以上方法，额外包含多轮重复运行实验。
- **真实实验**：2 个真实机器人平台，3 类目标、2 种指令模态（文本/图像），每个配置 10 次重复，共 60 次真实导航；另设障碍物抗干扰测试。
- **消融实验**：2 组（全局规划消融、局部规划消融）。

### 5.2 充分性与客观性评估
- **优点**：模拟与真实结合的验证充分；对全局与局部规划分别做了消融；重复运行实验验证了方法的可复用性优势；实例导航实验体现了布局信息的价值。
- **不足**：
  - 真实实验仅在**单一建筑（约 225m²）** 中进行，场景多样性有限，无法充分反映跨场景泛化能力。
  - 真实实验未有与其他方法的**同条件对比**，只能与模拟结果横向比较。
  - 图像指令任务的成功率（3/10~7/10）偏低，但没有深入分析失败原因。
  - 障碍物实验的规模较小（最多 3 个障碍物），未覆盖复杂动态场景（如移动的人、推开/关闭的门等）。

## 6. 主要结论与发现

1. **分层规划显著有效**：全局拓扑规划保证跨房间路径的全局最优性；局部 IL 规划解决局部避障与场景变化适应问题，二者缺一不可。
2. **使用 LLM 智能体整合流程可行**：无需人工干预、无需强化学习奖励或大量训练，即可完成"探索→建图→规划→导航→异常重规划"的完整闭环。
3. **MP3D 上性能大幅超越现有方法**：SR 从约 40% 提升至 85%，SPL 从约 24% 提升至 80%。
4. **"先探索后规划"的建图成本可摊薄**：在需要频繁部署或多任务执行的场景中，相比"边导航边建图"的增量式方法，总体效率更高。
5. **真实平台可部署且具有一定鲁棒性**：能够在出现新增障碍物的环境中成功绕行或重规划。

## 7. 优点

- **方法设计层面**：
  - 分层规划思路清晰：全局稀疏路标 + 局部稠密路标，兼顾效率与鲁棒性。
  - 利用拓扑图 + 神经隐式场景表示，实现开放词汇（open-vocabulary）的语义目标定位。
  - 多模态指令（文本/图像/3D 坐标）统一处理，具备良好的通用性。
  - 无需针对特定场景训练，零样本部署，成本低。
  - LLM 智能体管理全流程，自动化程度高，支持错误识别与迭代尝试。
- **实验验证层面**：
  - 模拟 + 真实双轨验证，覆盖多种任务模态（文本、图像、实例级）。
  - 消融实验设计针对性强，分别验证了全局规划和局部规划的贡献。
  - 创新性地引入了多轮重复运行实验，揭示了"先建图后规划"在长期使用场景中的成本优势。
  - 在真实平台上验证了动态障碍物场景，体现了实际部署价值。

## 8. 不足与局限

- **场景覆盖的局限性**：真实实验仅在一栋建筑内完成，未验证不同类型建筑（如多层、开放式办公室、商店等）中的泛化性；模拟实验虽在 MP3D 的 20+ 场景中进行，但也未报告跨场景及跨域（如 HM3D、RoboTHOR）的表现。
- **场景更新能力不足（作者自评）**：检测到的场景变化（如新障碍物）未实时更新到隐式表示与拓扑图中，限制了长期运行的记忆一致性。
- **局部记忆利用不充分（作者自评）**：局部规划未充分利用局部场景记忆中丰富的细节（如更精细的障碍物轮廓、物体位置），主要依赖当前帧的深度观测。
- **LLM 智能体的稳定性未量化**：未见关于 LLM 在不同 prompt 下的决策稳定性、失败模式分析或 token 成本分析的实验。
- **算力与时间成本未披露**：缺乏关于场景表示构建耗时、推理耗时、GPU 资源使用量的报告，影响复现与实际部署评估。
- **图像目标导航性能明显弱于文本目标**（SR 相差约 12–28 个百分点），且未深入分析原因，存在潜在的模态偏差风险。
- **对比公平性**：不同方法的探索效率差异较大（如 LOG-Nav 是先完整建图再导航，但其他方法是边探索边导航），尽管 Tab.3 探讨了这一差异，但整体对比中仍可能存在"更多先验信息"的争议性优势。

## （完）
