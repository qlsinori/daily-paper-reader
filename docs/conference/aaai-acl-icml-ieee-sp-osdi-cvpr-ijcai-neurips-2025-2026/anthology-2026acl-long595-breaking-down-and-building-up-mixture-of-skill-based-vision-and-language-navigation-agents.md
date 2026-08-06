---
title: "Breaking Down and Building Up: Mixture of Skill-Based Vision-and-Language Navigation Agents"
title_zh: 分解与构建：基于技能的视觉语言导航智能体混合
authors: "Tianyi Ma, Yue Zhang, Zehao Wang, Parisa Kordjamshidi"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.595.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 基于技能分解的视觉语言导航智能体，理解自然语言指令并在3D环境导航
tldr: 针对VLN智能体在复杂时空推理和未见场景泛化上的不足，提出SkillNav模块化框架。该框架将导航任务分解为垂直移动、区域识别、停止与暂停等可解释原子技能，每个技能由专门的智能体处理，从而引入结构化技能推理。实验表明这种方法能够提升VLN智能体在未知环境中的泛化能力，并增强决策可解释性。该工作为视觉语言导航提供了一种技能级分解与组合的新范式，有助于实现更稳健的语言指令跟随导航。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 705, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 785, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 774, \"height\": 852, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1648, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 797, \"height\": 691, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 622, \"height\": 606, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1476, \"height\": 979, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1625, \"height\": 1571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1625, \"height\": 1534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long595/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1623, \"height\": 1418, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 724, \"height\": 450, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 697, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1488, \"height\": 461, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 795, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 801, \"height\": 423, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1379, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1662, \"height\": 484, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1426, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 798, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1648, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1161, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 690, \"height\": 147, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1310, \"height\": 620, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 797, \"height\": 188, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 796, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1623, \"height\": 1418, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1616, \"height\": 1769, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long595/table-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1616, \"height\": 1871, \"label\": \"Table\"}]"
motivation: VLN智能体在大规模预训练和数据增强后仍难以在未见场景中泛化，尤其是复杂时空推理不足。
method: 提出SkillNav模块化框架，将导航分解为垂直移动、区域识别、停止等可解释原子技能，由专门智能体分别处理。
result: 实验证明结构化技能推理能够提升VLN智能体在未知场景中的泛化性能与可解释性。
conclusion: 为视觉语言导航提供了技能级分解与组合的新思路，增强了复杂3D环境下的语言指令导航能力。
---

## Abstract
Vision-and-Language Navigation (VLN) poses significant challenges for agents to interpret natural language instructions and navigate complex 3D environments. While recent progress has been driven by large-scale pre-training and data augmentation, current methods still struggle to generalize to unseen scenarios, particularly when complex spatial and temporal reasoning is required. In this work, we propose SkillNav, a modular framework that introduces structured, skill-based reasoning into Transformer-based VLN agents. Our method decomposes navigation into a set of interpretable atomic skills (e.g., Vertical Movement, Area and Region Identification, Stop and Pause), each handled by a specialized agent. To support targeted skill training without manual data annotation, we construct a synthetic dataset pipeline that generates diverse, linguistically natural, skill-specific instruction-trajectory pairs. We then introduce a novel training-free Vision-Language Model (VLM)-based router, which dynamically selects the most suitable agent at each time step by aligning sub-goals with visual observations and previous actions. SkillNav obtains competitive results on commonly used benchmarks and establishes state-of-the-art generalization to the GSA-R2R, a benchmark with novel instruction styles and unseen environments.

---

## 论文详细总结（自动生成）

# 《Breaking Down and Building Up: Mixture of Skill-Based Vision-and-Language Navigation Agents》论文总结

## 1. 核心问题与研究动机

- **研究背景**：视觉语言导航（VLN）要求智能体在复杂 3D 环境中理解自然语言指令并执行序列化导航决策，是具身智能中融合语言理解、视觉感知与序列决策的关键任务。
- **核心问题**：尽管大规模预训练和数据增强推动了 VLN 的进展，现有方法在**未见过的环境**和**新颖指令风格**下仍难以泛化，尤其是在需要**复杂空间与时间推理**的场景中表现不佳。
- **两类现有方法的不足**：
  - **端到端监督模型**（如基于 Transformer 的 DUET、ScaleVLN、SRDF）：依赖大规模数据增强，倾向于记忆训练样本而非掌握组合式推理能力，面对新环境和新指令时泛化能力受限。
  - **零样本 LLM/VLM 智能体**（如 MapGPT、NavGPT 等）：具备一定的泛化能力，但缺乏精确的视觉-空间锚定，在动作执行上明显落后于微调模型，成功率差距可达约 36%。
- **作者的核心论点**：导航任务本质上具有**组合性**，应将导航分解为可复用的原子技能，并通过高层推理动态组合这些技能，从而兼顾 LLM 的泛化能力和专用模型的动作精度。

## 2. 方法论：SkillNav

### 2.1 核心思想

- 提出 **SkillNav** 模块化框架：将 VLN 任务显式分解为一组**可解释的原子技能**，每个技能由一个**专用智能体（skill agent）**负责执行；再由一个**基于 VLM 的动作路由器（Action Router）**在每一步动态选择最合适的技能智能体。
- 核心理念类似“System 2 规划 + System 1 执行”：VLM 负责高层组合推理，专用 agent 负责低层精确动作执行。

### 2.2 技能体系（Skill Taxonomy）

- 沿用并扩展了 NavNuances 中的技能分类，共定义 5 个可执行技能和 1 个规划技能：
  1. **Direction Adjustment（方向调整）**：转向、改变朝向。
  2. **Vertical Movement（垂直移动）**：上下楼梯、跨楼层移动。
  3. **Stop and Pause（停止与暂停）**：根据视觉/语言线索精确停止或临时暂停。
  4. **Landmark Detection（地标检测）**：识别并响应环境中特定物体。
  5. **Area and Region Identification（区域识别）**：识别房间或功能区并完成区域切换。
  6. **Temporal Order Planning（时序规划）**：处理条件即时性、持续时长、前后顺序、回指等时间关系。
- 技能被定义为**语义层面原子性**：一个完整导航意图对应一个技能；同一语义技能在模拟器中可由多个低层离散动作实现，但不视为多技能混合。

### 2.3 技能数据合成与智能体训练

- 针对每个技能构建**合成数据集**：从 Matterport3D 随机采样 4–7 步路径，使用技能相关启发式规则过滤（如垂直移动要求高度差 > ±2、方向调整要求明显角度变化等）。
- 使用 **GPT-4o** 根据轨迹视觉观测生成自然流畅、R2R 风格且强调目标技能的指令，避免人工标注成本。
- 训练采用**两阶段微调**：
  - **阶段一**：在 R2R + ScaleVLN/SRDF 增强数据 + Temporal 合成数据上微调 DUET，得到技能无关的骨干模型（Temporal DUET）。
  - **阶段二**：基于该骨干，分别在 5 个技能数据集上微调，得到 5 个专用专家：`π_da`、`π_vm`、`π_sp`、`π_ld`、`π_ar`。

### 2.4 VLM-based Action Router

路由器由三个阶段组成：

1. **Temporal Reordering Module（时序重排模块）**：仅输入原始指令，由 LLM（GPT-4o）将自然语言指令转换为按时间顺序排列的子目标列表 `I_reorder`。该列表只用于辅助子目标定位，技能智能体仍接收原始完整指令。
2. **Subgoal Localizer（子目标定位器）**：基于重排后的子目标、历史视觉观测和已完成子目标序列，输出当前应执行的子目标 `p*_t` 与推理轨迹 `r_t`。
3. **Skill Router（技能路由器）**：结合原始指令、当前子目标和推理轨迹，从 5 个技能智能体中选择唯一最合适的专家 `π*_t`，并由该专家执行当前导航动作。

公式化流程为：
- `I_reorder = LLM_TemporalReorder(I)`；
- `(p*_t, r_t) = Localize(I_reorder, H_{t-1}, G_{t-1})`；
- `π*_t = argmax_{π∈S} Router(I, p*_t, r_t)`；
- `a*_t = π*_t(I, O_t, M_t)`。

## 3. 实验设计

### 3.1 数据集与评测基准

- **R2R（Room-to-Room）**：主评测基准，包含 Val-Unseen 和 Test-Unseen 等标准划分。
- **GSA-R2R**：核心泛化评测基准，包含：
  - 住宅（Residential）与非住宅（Non-Residential）场景；
  - Basic 风格指令（类似 R2R）与 Scene 风格指令（对话式、导游式、口语化）；测试集包括 Test-R-Basic、Test-N-Basic、Test-N-Scene。
- **NavNuances**：细粒度技能评测数据集，用于独立验证各技能智能体的专项能力。
- **RxR-English**：额外零样本评测，用于验证密集、描述丰富长指令下的泛化能力。

### 3.2 对比方法

- **LLM-based 方法**：MapGPT、NavCoT、NavGPT-2、NaviLLM、DiscussNav。
- **监督 VLN 方法**：HAMT、DUET、BEVBERT、GR-DUET、SAME、ScaleVLN、SRDF。
- **SkillNav 变体**：
  - SkillNav（ScaleVLN-Aug）；
  - SkillNav（SRDF-Aug）；
  - 以及 Random router、不同 VLM 路由器（Qwen2.5-VL、GLM-4.1V、GPT-4o）等消融配置。

### 3.3 评价指标

- Navigation Error（NE）：导航误差。
- Oracle Success Rate（OSR）：路径上曾接近目标的比例。
- Success Rate（SR）：3 米内成功停止比例。
- SPL：考虑路径长度的加权成功率。
- nDTW：对路径偏离的惩罚指标（用于 RxR 评测）。

## 4. 资源与算力

论文在附录 F 中给出了较明确的训练配置：

- **GPU**：单个 NVIDIA A6000 GPU。
- **训练轮次/迭代**：
  - 阶段一：50,000 次迭代，batch size 32，学习率 5×10⁻⁵；
  - 阶段二：30,000 次迭代，batch size 16。
- **训练时长**：
  - SRDF 设置下，5 个技能微调累计约 **3,329 分钟（约 55.5 小时）**；
  - 对照：SRDF 基础训练约 2,521 分钟（约 42 小时）。
- **随机种子**：seed 0，评估采用确定性配置。
- **推理配置**：vLLM 框架、beam search 5 候选、Top-1 路由、temperature 0、最大上下文 40,960 tokens。
- 论文明确指出 SkillNav 的**训练成本略高于单一监督模型**，但属于一次性投入；**推理成本**显著低于纯 LLM 方法，但比纯监督模型慢（约 50 倍）。

## 5. 实验数量与充分性分析

### 实验覆盖范围较广

- 主实验：R2R（Val-Unseen、Test-Unseen）+ GSA-R2R（3 个测试子集）。
- 技能级评测：NavNuances 四个技能类别，并与 ScaleVLN、SRDF、Mixed Skills 对比。
- 零样本泛化：RxR-English Val Seen / Val Unseen。
- 消融实验：
  - Temporal Reordering 开关（两路由器 Qwen/GLM）；
  - 不同 VLM 路由器对比（Random/GLM/Qwen/GPT-4o）；
  - 技能集大小敏感度（2/3/4/5 个专家组合）；
  - Mixed Skills 单模型 vs 模块化多专家对比（表 15）。
- 附加分析：专家调用分布、技能间转移概率、合成数据交叉评测、keyword 覆盖率、数据泄漏分析、人工错误分析、效率/延迟分析等。

### 充分性评价

- **优点**：实验体系较为完整，兼顾**标准 benchmark 性能、跨数据集泛化、单技能专项能力、模块消融、效率分析、数据泄漏检验**和人工错误分析，证据链较全面。
- **潜在不足**：
  - 主实验主要在**离散模拟器**中进行，未涉及 VLN-CE 连续控制或真实机器人部署；
  - GSA-R2R 的优势在 ScaleVLN 变体上更明显，SRDF 变体提升幅度较小，说明方法对基础模型有一定依赖；
  - 人工错误分析样本量较小（17 个失败案例）；
  - 合成数据依赖 GPT-4o 生成，存在潜在的语言风格偏差，尽管论文做了泄漏检测和 keyword 覆盖分析，但长期影响仍需验证。

## 6. 主要结论与发现

- **SkillNav 在 GSA-R2R 上取得 SOTA 泛化性能**，尤其 Test-N-Scene 上显著超越基线和现有方法（如 SR 56.66% vs SRDF 52% 等）。
- **在 R2R 上保持竞争性**：ScaleVLN 变体相比基线 SPL 提升约 6.5%；SRDF 变体与 SOTA 基线持平（SPL 77%）。R2R 已接近人类水平（SR 0.84 vs 人类 0.86；SPL 0.77 vs 0.76），剩余提升空间有限。
- **模块化分解是泛化提升的关键**：消融实验表明，仅增加合成数据（Mixed Skills）不能带来同样的增益，真正的提升来自“技能分解 + 动态路由”的结构性设计。
- **Temporal Reordering 是必要结构支架**：关闭后 GSA-R2R Test-N-Scene SPL 下降约 2.5%。
- **专家调用表现出“精确优先”策略**：Stop and Pause 和 Direction Adjustment 合计占比近 60%，语义类技能（Landmark、Region）作为稀疏锚点使用。
- **错误分析显示主要瓶颈是视觉锚定不足**：路由器语言理解基本正确，但经常用 Region/Direction 替代更精细的 Landmark 技能，导致目标物未正确绑定。

## 7. 优点与亮点

- **创新性强的模块化框架**：将导航显式分解为原子技能并组合，突破端到端黑箱范式，兼具可解释性与泛化性。
- **免人工标注的数据合成管线**：借助 GPT-4o 合成技能导向的训练数据，成本低且语言多样。
- **VLM 路由器的三阶段设计**：将“时序规划—子目标定位—技能选择”分离，结构清晰，可实现零样本路由，无需额外训练。
- **训练-推理解耦**：高层推理用 VLM，低层执行用轻量专用策略，在效率和泛化之间取得较好平衡。
- **广泛而细致的实验体系**：包含跨数据集泛化、技能专项评测、消融、数据泄漏检测、效率分析、人工错误分析等多维度验证。
- **提升可解释性**：通过技能选择、子目标推理和定性案例分析，使智能体的决策过程更透明。

## 8. 不足与局限

- **模拟器局限**：仅在离散 VLN 环境中验证，未测试连续控制（VLN-CE）、真实机器人部署；低层技能执行器需要为不同动作空间重新适配。
- **技能库非穷尽**：当前 5 个技能主要覆盖室内导航常见情况，未包含物体操作、透明材质处理、人机交互导航等更专门域，需要扩展新执行器。
- **推理开销**：VLM 路由器的引入使推理速度比纯监督模型慢约 50 倍（吞吐约 0.49 inferences/s），在延迟敏感场景下受限；需要蒸馏、缓存或替换为轻量模型。
- **对路由模型的依赖**：路由性能与所选 VLM 能力相关，GPT-4o 表现最好，但开源模型（如 Qwen、GLM）存在一定差距。
- **合成数据潜在偏差**：尽管做了泄漏分析，GPT-4o 生成指令的语言风格与多样性仍可能与真实指令分布存在差距，且极小词汇覆盖（如 ScaleVLN 仅 208 个唯一 token）可能限制语义多样性。
- **错误模式依然存在**：初始朝向错位、子目标幻觉、密集指令下控制器瓶颈等问题尚未完全解决。
- **部分分析和样本量有限**：人工错误分析仅 17 个失败案例；R2R 性能接近人类水平后，方法在新基准上的增益能否转化为实际部署还需进一步验证。

（完）
