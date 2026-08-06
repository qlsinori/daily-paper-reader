---
title: Constructing coherent spatial memory in LLM agents through graph rectification
title_zh: 通过图修复为LLM智能体构建一致的空间记忆
authors: "Puzhen Zhang, Xuyang Chen, Yu Feng, Yuhan Jiang, Liqiu Meng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2222.pdf"
tags: ["query:semantic-map"]
score: 9.0
evidence: 一致的空间记忆; LLM智能体; 增量拓扑地图构建; 图修复
tldr: 大语言模型虽然能根据全局导航指令推断空间布局，但随着环境变大，基于上下文的查询难以应对，增量式地图构建成为必要。本文提出由LLM驱动的构建和地图修复框架，通过版本控制记录图编辑的历史与来源观察，能够检测、定位并纠正增量构建的导航图结构不一致，从而形成完整的拓扑空间记忆，提升LLM智能体在大规模环境中的空间记忆质量，并支持细粒度的回滚和冲突追溯。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2222/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1631, \"height\": 1428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2222/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 1046, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2222/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2222/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1411, \"height\": 796, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 727, \"height\": 426, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 641, \"height\": 564, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 702, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 653, \"height\": 376, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 847, \"height\": 1640, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1654, \"height\": 1335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 1791, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1081, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 837, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2222/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 854, \"height\": 254, \"label\": \"Table\"}]"
motivation: LLM从全局指令推断空间布局在大场景下不可扩展，需要增量式构建完整拓扑图并修复结构错误。
method: 提出LLM驱动的地图构建与修复框架，用版本控制记录编辑历史和观测来源，支持细粒度回滚和冲突追踪。
result: 该方法可检测和修正增量构建导航图中的结构不一致，从而生成完整可靠的拓扑空间记忆，并提升大规模环境下的可扩展性。
conclusion: 为LLM智能体提供了一种可追溯、可修复的空间记忆构建方式，对认知地图和机器人导航具有借鉴意义。
---

## Abstract
Given a map description through global traversal navigation instructions, an LLM can often infer the implicit spatial layout and answer user queries by providing shortest paths. However, such context-dependent querying becomes incapable as environments grow larger, motivating the need for incremental map construction that builds a complete topological graph from stepwise observations. We propose a framework for LLM-driven construction and map repair, designed to detect, localize, and correct structural inconsistencies in incrementally constructed navigation graphs. Central to our method is the Version Control, which records the full history of graph edits and their source observations, enabling fine-grained rollback, conflict tracing, and repair evaluation. We further introduce an Edge Impact Score to prioritize minimal-cost repairs based on structural reachability, path usage, and conflict propagation. To properly evaluate our approach, we create a refined version of the MANGO benchmark dataset by systematically removing non-topological actions and inherent structural conflicts, providing a cleaner testbed for LLM-driven construction and map repair. Our approach significantly improves map correctness and robustness, especially in scenarios with entangled or chained inconsistencies. Our results highlight the importance of introspective, history-aware repair mechanisms for maintaining coherent spatial memory in LLM agents.

---

## 论文详细总结（自动生成）

# 基于论文内容的详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：大型语言模型（LLM）在开放式推理、序列规划和基于文本的导航任务中表现出色。然而，在文本处理环境中，LLM 的空间认知主要依赖上下文窗口内的直接推理，这在大规模、长时程场景下面临**上下文长度受限、上下文遗忘、迭代推理不一致**等问题。
- **核心问题**：当环境规模变大时，LLM 如何从逐步观察中增量构建完整的拓扑图（空间记忆），并有效检测、定位和修复增量构建过程中产生的**结构不一致**（如错误边、节点重复、方向冲突等）。
- **关键挑战**：
  - 早期引入的小错误会静默传播，直到积累足够上下文后才以冲突形式显现（**时间滞后**）。
  - 错误之间存在**耦合依赖**，一个错误可能触发级联错误。
  - 大多数 LLM 缺乏持久记忆或版本控制，无法追溯错误来源或判断错误边何时被引入。
- **整体含义**：采用类人的认知方式——将局部空间认知渐进组装为复杂空间理解，通过图结构增量存储来缓解上下文压力，并为 LLM 智能体赋予可追溯、可修复的空间记忆机制，这对认知地图、具身智能和机器人导航具有借鉴意义。

## 2. 方法论：核心思想、关键技术细节与流程

### 2.1 整体框架思想
- 提出 **LLM-MapRepair** 框架，采用"**增量构建 + 周期修复**"的范式，将冲突检测、错误定位、版本控制三者结合，把冲突较多的图转化为结构一致、可靠的导航图。
- 框架循环式运行三个阶段：**冲突检测（Conflict Detection）→ 错误定位（Error Localization）→ 版本控制（Version Control）**，直到图中不再存在可检测冲突。

### 2.2 冲突检测（Conflict Detection）
检测三类结构冲突，这是物理空间的结构不变量：
- **拓扑冲突（Topological Conflict）**：两个不同节点被推断为占据同一物理位置（基于单位距离假设），等价症状包括树状空间中的环、不可达节点或过度连接组件。
- **方向冲突（Directional Conflict）**：同一节点有多个具有相同方向标签的出边，违反空间唯一性约束。
- **命名冲突（Naming Conflict）**：不同位置被分配了相同名称，导致推理和定位歧义。
- 检测模块是模块化设计的，新的检测器（包括语义检测器）可作为插件加入，无需修改后续定位或评分流水线。

### 2.3 错误定位（Error Localization）
解决三类核心难题：**延迟冲突**（早期错误后期才显现）、**纠缠冲突**（修复一个边反而引发新冲突）、**静默错误**（因缺乏矛盾证据而长期未被发现）。定位流程四阶段：

1. **最小冲突路径对识别**：找到通向冲突节点的两条不同路径。
2. **最低公共祖先（LCA）计算**：在**推理历史树 T**（而非空间图 G）上计算两条冲突路径的时间上最新的公共祖先：
   $$LCA(\pi_1, \pi_2) = \arg\max_{v \in \pi_1 \cap \pi_2} \tau(v)$$
   - **长距离冲突**（拓扑违规）：LCA 早于当前观测源节点，表示潜在错误引入于先前步骤。
   - **局部冲突**（方向违规）：LCA 与源节点重合（零长度发散），表示当前边直接违反局部几何约束。
3. **候选边提取**：提取从 LCA 到每个冲突节点的发散子路径上的所有边；静默错误也可作为全局排名的备用候选项。
4. **边评分与排序（Edge Impact Score）**：受 PageRank 启发，综合三个因子（均经过 min-max 归一化）：
   $$score(e) = \hat{Reach}(e) + \hat{Conflict}(e) + \hat{Usage}(e)$$
   - **可达性（Reachability）**：边 e 下游可达的节点数，反映传播潜力。
   - **冲突次数（Conflict Count）**：涉及 e 的不同冲突数量，反映贡献程度。
   - **使用量（Usage）**：包含 e 的冲突相关路径条数，反映经验相关性。
   - 优先处理高分数边，以获得最大的冲突揭示效率。

### 2.4 版本控制（Version Control）
- 维护版本化图历史链 $[G_0, G_1, \ldots, G_t]$，每个提交记录仅保存增量更新：
  $$G_i = \{Step\_id, Commit, Trigger\_event, Observation\_id, Analysis\}$$
- 三个核心操作：
  - **rollback_to(version)**：撤销后续步骤，恢复图到先前状态。
  - **recall_step(version)**：获取该步骤对应的思维历史和原始观测。
  - **diff(G_i, G_j)**：计算两个版本间的边级差异。
- 每次 LLM 交互（新观测或修复行动）都会触发图更新并记录新版本，确保即使失败或部分正确的决策也被保留供分析。
- 设计类比数据库系统的**预写日志（WAL）**，保证可恢复性和可追溯性。

### 2.5 关于"神经-符号"定位
- 冲突检测、LCA 计算、Edge Impact Scoring 均为**全符号化的确定性算法**，具有可证明的行为；仅文本→空间关系的感知和修复执行环节借助 LLM 能力。

## 3. 实验设计：数据集、Benchmark 与对比方法

### 3.1 数据集与 Benchmark
- **基础基准**：MANGO benchmark（Ding et al., 2024），包含 53 个交互式小说（IF）环境，源自 Jericho benchmark。每个 episode 由一系列移动命令和文本观测构成，用于增量构建拓扑地图。
- **数据集清洗**：发现原始数据集本身含有大量结构冲突和非拓扑动作，因此进行了系统化清洗：
  1. **动作过滤**：仅保留 14 个拓扑移动动作（north, south, east, west 等），去除祈祷等非空间动作。
  2. **方向冲突消解**：同一源节点有多个同方向出边时，保留最小步数边。
  3. **反向边/拓扑冲突消解**：去除违反空间对称性的一致性反向边。
  4. **命名冲突消解**：通过传递空间关系消除间接冲突。
  5. **自环去除**。
  - 清洗后：共移除 160 条边，边数从 1,673 降至 1,513；涵盖 930 个独特位置、1,511 条有向边、13,096 个遍历步骤。
  - 数据集特征：图稀疏且绝大多数为树状（平均密度 0.127，平均节点度 1.59）；75.4% 边为主方向动作，71.5% 边为双向遍历。
  - 文本复杂性包括：相同房间名、黑暗房间、非移动动作中的隐式转换、自然语言描述的阻塞通道。

### 3.2 主实验与对比方法
- **对比设置**（消融研究，基础 LLM 为 GPT-4o）：
  - **Edge-Impact Ranking Only**：仅用边影响分数对修复候选排序。
  - **Version Control Only**：仅依赖版本控制进行历史追溯和回滚。
  - **Version Control + Edge-Impact Ranking（完整方法）**：两者结合。
  - **Baseline**：无候选过滤或优先级机制，直接让 LLM 修复。

- **跨模型泛化实验**：将完整方法嵌入 GPT-4o、GPT-4.1、GPT-4o-mini、Claude-Haiku 四种模型，与各自 Baseline 对比。

### 3.3 算法验证（不含 LLM 的受控实验）
- 在**合成图**上注入已知错误（拓扑、方向、命名三类冲突），构建 6 个测试场景：
  - TC1：拓扑冲突（恢复论文图 3 挑战场景）
  - TC2：方向冲突（LCA = 源节点的退化情形）
  - TC3：级联次要冲突
  - TC4：混合冲突类型
  - TC5：长距离冲突（深度 2 的错误在深度 10 显现）
  - TC6：级联潜力预测（36 条边、5 个不同级联规模的注入错误）
- 另附两则案例研究（Zork I 局部冲突修复、长距离 EIS+VC 协同修复）。

## 4. 资源与算力

- **论文未明确说明使用的 GPU 型号、数量或训练/运行时长**。文中的计算复杂度分析提到每个修复周期中算法组件总耗时 <10ms，而 LLM 推理 API 调用约 2–5 秒/次，暗示主要计算成本来自 LLM API 推理，但具体硬件配置、部署规模等信息均未披露。

## 5. 实验数量与充分性

### 实验规模
- **主消融实验**：1 个基准设定（GPT-4o）下的 4 种方法对比。
- **跨模型实验**：4 种模型 ×（完整方法 + Baseline），共 8 组配置。
- **逐游戏分析**：附录表 A2/A3 给出了 53 个游戏逐一的修复效果统计。
- **合成算法验证**：6 个测试场景 + 2 个详细案例研究。

### 充分性与客观性评估
- **充分性**：
  - 消融实验覆盖了各组件独立效果和组合效果，能较好验证模块贡献。
  - 跨模型实验验证了方法的泛化性。
  - 合成实验独立于 LLM 性能验证算法本身的正确性。
  - 即使只有少数游戏（如 cutthroat、murdac、detective、inhumane）存在大量冲突，但正是这些"难例"提供了有效信号。
- **公平性**：基线、所有方法共享相同的冲突检测模块和最多 10 次修复尝试限制；仅传递信息不同，对比设计基本公平。
- **改进空间**：重复次数未提及，统计显著性检验未报告；未与除消融外的其他既有修复框架进行端到端对比。

## 6. 主要结论与发现

- **完整方法显著优于基线**：在《红楼梦》第 16–17 章上，MapRepair 将节点召回率提升 8.6 个百分点（达 94.3%），边召回率提升 55.8 个百分点（达 88.2%）。
- **主实验关键数据**（GPT-4o）：
  - Baseline：修复率仅 21.85%，正确率仅 5.77%，平均 9.52 轮。
  - Edge-Impact Ranking Only：修复率 75.21%，正确率 44.69%，平均 6.39 轮（最低）。
  - Version Control Only：修复率 63.03%，正确率 54.00%，平均 7.44 轮。
  - **完整方法**：修复率 68.91%，正确率 54.88%，平均 8.20 轮。
- **跨模型一致性**：完整方法在所有四个模型上均显著优于各自基线（如 GPT-4o-mini 正确率从 5.60% 提升至 58.40%；Claude-Haiku 从 6.67% 提升到 44.31%）。
- **算法验证结论**：
  - LCA 候选过滤平均将候选搜索空间削减 22.7%，方向冲突中最高达 75%。
  - Edge Impact Score 与真实级联潜力达到完美秩相关（Spearman ρ = 1.0, p < 0.001）。
  - 基于优先级的检查比随机遍历快 2.3 倍，减少 56.5% 的边检查数量。
- **案例研究验证**：在局部冲突中，版本控制的观测级证据是决策关键；在长距离冲突中，EIS 负责缩小搜索范围、VC 提供确认依据，二者协同高效。

## 7. 优点

- **问题选择前沿且务实**：针对 LLM 在长时程空间推理中的核心瓶颈（上下文依赖、错误累积、时间滞后），切中实际应用需求。
- **方法论设计有创新性**：
  - 将 SLAM 中的回环检测与图优化思想迁移到 LLM 生成导航图领域，跨领域类比自然且富有启发性。
  - 版本控制机制赋予系统"可追溯的推理历史"，这在 LLM 智能体持久化记忆方面提供了一个简单而优雅的实现方案。
  - LCA 统一定位框架对三类冲突提供数学上统一的解决方案，从拓扑到方向冲突均可适用。
- **模块化与可扩展性**：冲突检测器可即插即用，语义检测器也可在不修改流水线的情况下集成。
- **工程完整性**：对原始 MANGO 数据集进行了系统清洗，提供了对数据集固有偏差的修正，值得肯定。
- **算法验证与 LLM 实验分离**：合成实验排除了 LLM 随机性干扰，直接验证核心算法的正确性，证据链更完备。
- **诚实的启发式**：对 Edge Impact Score 无最优性保证的坦诚讨论，并用 A*、PageRank、Beam Search 等先例支撑经验启发式的合理性，同时给出完整性和优雅降级两个安全性质。

## 8. 不足与局限

- **连续空间推理不足**：清洗后的 MANGO 使用离散基本方向和单位距离，而真实文本（如小说）包含任意角度和模糊距离的连续空间描述。虽然离散化/弹性约束方法在《红楼梦》上展现潜力，但显著增加误报率。
- **语义冲突盲区**：当前冲突检测依赖可观测的结构违规，无法识别不表现为拓扑错误的潜在语义不一致（如"室内"位置通过"过河"连接到"室外"位置）。虽然引用了 LINC、Logic-LM 等作为未来语义检测器扩展方向，但尚未在本文实现。
- **上游感知脆弱性**：系统性、一致的感知错误（如始终把"Kitchen"命名为"Cooking Room"）不会产生结构冲突，因此会逃过检测。对一致性的实体识别错误，需要额外的实体链接或共指消解模块。
- **启发式排序缺乏理论保证**：EIS 在高度对称图（如规则网格）和具有外围错误的枢纽-辐射（hub-and-spoke）拓扑上判别力有限，缺乏最优修复顺序的理论保证。
- **实验统计不够严谨**：未报告多次运行的标准差或置信区间；部分游戏冲突数量极少（0–3 个），结果可能受单次 LLM 采样影响较大。
- **公平比较受限**：未与传统的符号式导航系统进行端到端对比（作者给出理由：符号系统无法直接处理自然语言观测、需要 NLP 前端等）；这使"MapRepair 优于其他符号方法"的说法缺乏直接验证。
- **计算资源信息缺失**：未披露底层 LLM 推理使用的具体硬件（GPU、TPU）及相应成本，可复现性和成本估算受限。

---

（完）
