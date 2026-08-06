---
title: "GROKE: Vision-Free Navigation Instruction Evaluation via Graph Reasoning on OpenStreetMap"
title_zh: GROKE：基于OpenStreetMap图推理的无视觉导航指令评估
authors: "Farzad Shami, Subhrasankha Dey, Nico Van de Weghe, Henrikki Tenkanen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1874.pdf"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 基于图推理的无视觉导航指令评估，支持语言引导导航研究
tldr: 针对导航指令评估中传统参考式指标难以反映功能效用、而VLN智能体评估依赖高保真模拟器且成本高的问题，提出GROKE评估框架。GROKE基于OpenStreetMap图推理，利用分层LLM对指令进行视觉无关且免训练的评估，判断其能否成功引导导航者到目的地。实验验证了GROKE的有效性和低成本特性，能规避视觉感知误差。该方法为VLN指令质量评估提供了一种可扩展的替代方案，支持大规模指令分析。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 794, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 433, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 803, \"height\": 533, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1641, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 812, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1874/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 793, \"height\": 590, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 808, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 746, \"height\": 254, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1492, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 697, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 801, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1649, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1651, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1653, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 797, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1647, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1874/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1649, \"height\": 276, \"label\": \"Table\"}]"
motivation: 传统参考式指标无法评测导航指令的功能效用，而基于VLN智能体的评估依赖高保真视觉模拟器且成本高。
method: 提出GROKE框架，基于OpenStreetMap图推理并通过分层LLM对指令进行视觉无关、免训练的评估。
result: 实验显示GROKE可以准确判断指令是否成功引导至目的地，避免感知误差并降低计算成本。
conclusion: 为VLN指令评估提供了一种高效、视觉无关的替代方案，有助于指令质量的自动化分析。
---

## Abstract
The evaluation of navigation instructions remains a persistent challenge in Vision-and-Language Navigation (VLN) research. Traditional reference-based metrics such as BLEU and ROUGE fail to capture the functional utility of spatial directives, specifically whether an instruction successfully guides a navigator to the intended destination. Although existing VLN agents could serve as evaluators, their reliance on high-fidelity visual simulators introduces licensing constraints and computational costs, and perception errors further confound linguistic quality assessment. This paper introduces GROKE (Graph-based Reasoning over OSM Knowledge for instruction Evaluation), a vision-free training-free hierarchical LLM-based framework for evaluating navigation instructions using OpenStreetMap data. Through systematic ablation studies, we demonstrate that structured JSON and textual formats for spatial information substantially outperform grid-based and visual graph representations. Our hierarchical architecture combines sub-instruction planning with topological graph navigation, reducing navigation error by 68.5% compared to heuristic and sampling baselines on the Map2Seq dataset. The agent’s execution success, trajectory fidelity, and decision patterns serve as proxy metrics for functional navigability given OSM-visible landmarks and topology, establishing a scalable and interpretable evaluation paradigm without visual dependencies.

---

## 论文详细总结（自动生成）

# GROKE：基于OpenStreetMap图推理的无视觉导航指令评估

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：如何有效评估导航指令（navigation instructions）的可导航性（navigability），即一条指令是否能够成功引导导航者到达预期目的地。
- **现有方法的缺陷**：
  - **传统参考式指标**（BLEU、ROUGE、METEOR、CIDEr）基于 n-gram 重叠，假定存在唯一正确的路线描述方式且词汇相似性与功能效用相关。然而在空间导航中，这一假设不成立——例如"Turn left at the bank"与"Turn right at the bank"词汇高度重叠但功能结果截然相反；而两条零 n-gram 重叠的指令可能描述完全相同的有效动作。
  - **基于 VLN 智能体的评估**虽理论上合理，但依赖高保真视觉模拟器（Matterport3D、Google Street View），存在许可限制、计算成本高、可复现性差等问题；且视觉感知错误会混淆语言质量评估（例如智能体因无法从图像中识别"stucco wall"而失败，却被归咎于指令质量）。
- **研究意义**：将评估问题从"智能体表现如何"逆转为"指令的可导航性如何"，为 VLN 指令质量评估建立一种可扩展、无视觉依赖的替代范式，支持大规模指令质量自动化分析、训练数据过滤和生成模型的改进。

## 2. 论文提出的方法论

### 2.1 核心思想
- 提出 **GROKE（Graph-based Reasoning over OSM Knowledge for instruction Evaluation）** 框架——一种无视觉（vision-free）、免训练（training-free）的分层 LLM 评估系统。
- 将环境抽象为基于 OpenStreetMap 的语义图表示（节点、边、POI），使智能体在符号空间而非原始像素上推理，从而解耦视觉感知与语言质量评估。
- 将智能体的执行成功率和轨迹保真度作为指令可导航性的代理指标。

### 2.2 系统结构（三模块）

**模块一：Sub-instruction Agent（子指令智能体）**
- 将完整自然语言指令 `I` 解析为原子子目标序列 `{g1, g2, ..., gK}`，子目标对应于三种基本操作之一：MOVE_FORWARD、TURN_LEFT、TURN_RIGHT。
- 提取指令中的地标引用 `L = {l1, l2, ..., lM}` 并按其语义类型分类。
- 通过 RapidFuzz 模糊字符串匹配将指令中的地标名与 OSM POI 标签进行接地（grounding），相似度超过阈值 τ 即建立匹配，并为每个接地地标分配唯一字母标识符（A、B、C…）。

**模块二：Visible Area Construction（可见区域构建）**
- 模拟人类导航的有限视野，沿当前航向方向遍历至预设数量的交叉口（visibility units, `u`），构建局部空间上下文 `Gt`。
- 核心算法（Algorithm 1）：从当前节点出发，沿最小航向偏差（`Δh < 100°`）逐节点前向推进，统计经过的交叉口数（`degree(v) > 2`），达到阈值或无法继续时停止，再额外延伸 3 个节点作为前瞻上下文。
- 使用球面方位角公式（spherical bearing formula）计算节点间航向。
- POI 邻近映射：对可见路径上的每个节点，在 50 米阈值内查找 POI；通过相对方位角差 δ 将 POI 分类为 Forward、Left、Right、Back。

**模块三：Navigator Agent（导航智能体）**
- 迭代执行每个子目标：接收当前子目标 `gk`、当前位置 `vt`、当前航向 `ht` 和可见区域 `Gt`，输出 `(status_k, v_{t+1})`，其中 `status_k ∈ {IN_PROGRESS, COMPLETED}`。
- 终止条件：所有子目标完成、总步数超过 100、或单子目标重试超过 15 次。

### 2.3 任务形式化
- 将 VLN 任务形式化为图结构环境中的序贯决策问题：`π: (I, v_t, h_t, G_t) → v_{t+1}`，目标是最大化预测轨迹与真实轨迹的一致性概率。

## 3. 实验设计

### 3.1 数据集
- **Map2Seq 数据集**（Schumann & Riezler, 2021），使用两个测试集：
  - **TestSet A**（对应 Test_Seen）：700 条实例，平均 53.5 tokens，平均 2.72 个地标/实例，人类导航成功率 0.86。
  - **TestSet B**（对应 Test_Unseen）：700 条实例，平均 54.2 tokens，平均 2.69 个地标/实例，人类导航成功率 0.84。
- 数据集特点：使用俯视地图界面而非自我中心全景图，指令围绕 OSM POI 构建。

### 3.2 评估指标
- **NE（Navigation Error）**：智能体最终位置与真实目的地的欧氏距离。
- **SR（Success Rate）**：25 米半径内到达目标的百分比。
- **OSR（Oracle Success Rate）**：轨迹上任意点落入 25 米半径即算成功。
- **SDTW / nDTW**：结合成功状态与轨迹几何相似性的路径保真度指标。

### 3.3 对比方法
- **Random Walker**：随机选边，随机基线。
- **Action Sampling**：忽略指令文本，按预计算的全局动作分布采样。
- **Heuristic Agent**：基于正则表达式提取方向关键词 + 贪心选边。

### 3.4 主要实验与消融
1. **主实验**：两组测试集上的完整导航执行对比。
2. **分层分解消融**：完整指令 vs 规则切分 vs LLM Divider（100 条验证实例）。
3. **空间表示格式消融**（4 种）：Textual（文本叙述）、JSON（结构化）、Graphviz 风格可视化、Grid 矩阵。
4. **POI 检测比较**：GLiNER、BERT-large-NER、Gemini-3 Pro 三种 NER 方案。
5. **思考级别消融**：Low / High / Auto 三种 LLM 思考配置。
6. **人类相关性分析**：100 条指令的双盲人工标注 vs 自动指标的相关性。
7. **失败模式分析**：492 条失败轨迹归类为语言（L）、拓扑（T）、智能体（A）、执行（E）四类。

## 4. 资源与算力

- 论文**未报告** GPU 型号、数量或训练时长——因为 GROKE 是免训练框架，不涉及模型训练。
- LLM 推理使用 **Gemini-3 Pro**（在线和批量 API），默认参数（temperature 1.0，思考级别默认 high）；框架基于 Google Agent Development Kit（ADK）实现。
- 计算成本以 token 消耗衡量：
  - TestSet A 平均总 token 44,438；TestSet B 平均总 token 46,305。
  - 思考级别消融中：Low 平均 33,236 tokens、High 平均 41,347 tokens、Auto 平均 43,700 tokens。
  - 边际成本分析（基于 $12/百万 tokens）：NE 每降低 1 米约需 1,334 tokens（1.60¢）；SR 每提高 1% 约需 1,356 tokens（1.63¢）；nDTW 每提高 0.01 约需 1,731 tokens（2.08¢）。

## 5. 实验数量与充分性

### 5.1 实验数量
- 实验覆盖面较广：2 个测试集 + 4 种空间表示消融 + 3 种指令切分方法对比 + 3 种 NER 模型比较 + 3 种思考级别对比 + 人类相关性分析 + 失败模式归类分析，总实验组数约 10 组以上。
- 消融实验在 100 条验证实例上进行（49 easy / 38 medium / 13 hard），并进行了难度分层统计。

### 5.2 充分性评估
- **优点**：消融设计系统全面，覆盖了空间表示、分层规划、POI 检测、推理成本等多个关键维度；难度分层分析有助于理解方法在不同复杂度下的表现差异；相关性分析为"Agent-as-Judge"提供了元评估（meta-evaluation）依据。
- **不足**：
  - 消融实验仅基于 100 条实例的一个子集，样本量有限，且 hard 类别仅 13 条，统计显著性可能不足。
  - 仅使用单一 LLM（Gemini-3 Pro），未在多个 LLM 上验证结论的泛化性。
  - 主实验仅在一个数据集（Map2Seq）上验证，未在 R2R、Touchdown 等主流 VLN 数据集上测试。
  - 人类相关性分析中 OSR 未达到统计显著（p > 0.05），说明部分指标可靠性存疑。

## 6. 主要结论与发现

1. **结构化 JSON 空间表示是最优编码格式**：JSON 达到 NE 41.3m、SR 74.0%（优化后），显著优于 Graphviz（NE 96.7m、SR 40.0%）和 Grid（NE 175.4m、SR 10.0%）；JSON 与 Textual 在简单任务上接近，但在 Hard 难度上 JSON 明显更优（SR 53.8% vs 38.5%）。
2. **分层子指令分解显著提升性能**：LLM Divider 相比完整指令 NE 降低 42.6%（71.9m → 41.3m），SR 从 51.0% 提升至 74.0%；相比规则切分也有 29.3% 的 NE 降低。优势在困难指令上最为显著。
3. **GROKE 大幅优于基线方法**：在 TestSet A 上 SR 66.4%、NE 56.8，远超最佳基线 Heuristic Agent（SR 18.0%、NE 180.6）；相比启发式和采样基线导航误差降低 68.5%。
4. **自动指标与人类判断显著相关**：NE 与人类导航性评分的相关性最强（Pearson r = −0.31, p < 0.01；Spearman ρ = −0.32, p < 0.01）；SR 和 SDTW 呈中等正相关（r ≈ 0.29）。
5. **POI 检测精度很高**：Gemini-3 Pro 在 382 个标注实体中仅漏检 4 个（正确率 98.95%），接近人类专家水平；GLiNER 正确率 64.13%，BERT 仅 50.00%。
6. **思考级别存在收益递减效应**：High 配置对 Hard 指令至关重要（SR 61.5%），但 token 成本显著增加；对于不要求严格轨迹保真的应用，Low 配置性价比更优。

## 7. 优点

- **视觉无关性**：完全基于 OSM 符号图数据，规避了视觉感知错误对语言评估的混淆，解决了视觉模拟器的许可和计算瓶颈。
- **免训练架构**：无需训练专用模型，直接利用 LLM 的现成能力，易于复现和部署。
- **"Agent-as-Judge"评估范式创新**：将标准 VLN 任务逆转为指令质量评估任务，并通过人类标注相关性验证了评估器本身的有效性。
- **系统的空间表示消融**：对四种空间编码格式（文本、JSON、Graphviz、网格）进行了严格的对照实验，为 LLM 空间推理的输入设计提供了有价值的经验证据。
- **分层架构设计合理**：子指令解析与路径执行解耦，降低了长时程导航的复杂度，使每个子目标可以被独立追踪和验证。
- **透明度高**：提供了完整的提示模板、算法描述和错误分析，便于社区复现和后续改进。
- **可解释性**：失败模式分析（语言/拓扑/智能体/执行）为理解评估失败原因提供了结构性视角。

## 8. 不足与局限

- **无法评估视觉依赖型指令**：框架仅基于符号表示，对于依赖纯视觉线索的指令（如"在红门的房子左转"、"沿着涂鸦墙走"）无法验证，适用范围受限。
- **计算成本仍然较高**：High 思考配置平均每 episode 消耗约 41,347 tokens，限制了大规模部署的可行性；LLM 推理延迟也不适合实时导航场景。
- **泛化性未验证**：实验结果仅基于 Gemini-3 Pro 单一模型，JSON 优于网格等结论是否适用于其他 LLM 架构尚未确认；仅在 Map2Seq 数据集上验证，未覆盖室内场景或其他城市环境。
- **消融实验规模有限**：核心消融仅基于 100 条实例，Hard 难度仅 13 条样本，统计功效有限。
- **指标有效性差异**：OSR 与人类判断无显著相关性（p > 0.05），暗示该指标在实际评估中的可靠性存疑。
- **人类标注存在主观性**：虽然 Cohen's κ = 0.67 达到"Substantial"一致性，但二元导航性判断的粒度较粗，可能遗漏指令质量的细微差异。
- **失败模式中智能体自身缺陷占主导**：492 条失败案例中，Agent 相关错误（过度/不足到达目的地、POI 接地失败等）是最主要的失败源，意味着部分评估误差可能归因于智能体能力而非指令质量。

（完）
