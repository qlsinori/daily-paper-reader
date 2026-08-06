---
title: "EvoEmpirBench: Dynamic Spatial Reasoning with Agent-ExpVer"
title_zh: EvoEmpirBench：基于Agent-ExpVer的动态空间推理
authors: "Pukun Zhao, Longxiang Wang, Miaowei Wang, Chen Chen, Fanqing Zhou, Haojian Huang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40979/44940"
tags: ["query:semantic-map"]
score: 7.0
evidence: 包含迷宫导航与经验记忆机制的动态空间推理基准，涉及空间记忆编取
tldr: 针对现有空间推理基准多关注静态全局可见环境、难以评估动态部分可观测条件下长程推理和记忆利用的问题，提出EvoEmpirBench动态空间推理基准。基准包含局部可观测的迷宫导航和消除类任务，每次动作都会触发环境结构变化，要求智能体持续更新认知与策略。进一步提出基于主观经验的记忆机制，实现跨任务经验迁移与验证。实验表明该基准和机制能有效评测并提升模型的空间理解与自适应规划能力，为空间记忆研究提供了标准化测试平台。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40979/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 872, \"height\": 609, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40979/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1827, \"height\": 1111, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40979/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 705, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40979/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 705, \"height\": 766, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40979/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1848, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40979/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1881, \"height\": 780, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40979/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1839, \"height\": 823, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40979/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 895, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40979/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 885, \"height\": 378, \"label\": \"Table\"}]"
motivation: 现有空间推理基准多假设静态或全局可见环境，难以评估局部可观测与动态变化下的长程推理和记忆利用能力。
method: 构建两个动态空间基准（迷宫导航与消除类任务），并提出基于主观经验的记忆机制实现跨任务经验迁移。
result: 实验显示所提基准与机制能有效评测并提升模型在动态部分可观测环境中的空间理解和自适应规划能力。
conclusion: 为动态空间推理与空间记忆研究提供了新基准与方法，可推动复杂环境下具身智能体的导航能力。
---

## Abstract
Most existing spatial reasoning benchmarks focus on static or globally observable environments, failing to capture the challenges of long-horizon reasoning and memory utilization under partial observability and dynamic changes. We introduce two dynamic spatial benchmarks—locally observable maze navigation and match-2 elimination—that systematically evaluate models' abilities in spatial understanding and adaptive planning when local perception, environment feedback, and global objectives are tightly coupled. Each action triggers structural changes in the environment, requiring continuous update of cognition and strategy. We further propose a subjective experience-based memory mechanism for cross-task experience transfer and validation. Experiments show that our benchmarks reveal key limitations of mainstream models in dynamic spatial reasoning and long-term memory, providing a comprehensive platform for future methodological advances.

---

## 论文详细总结（自动生成）

## EvoEmpirBench：基于Agent-ExpVer的动态空间推理——详细总结

### 一、核心问题与整体含义（研究动机与背景）

- **现有空间推理基准的缺陷**：绝大多数空间推理基准依赖静态数据集或全局可见环境，无法有效评估模型在局部可观测、环境动态变化条件下所需的长程推理能力与记忆利用能力。静态基准还面临数据污染、性能快速饱和等问题。
- **动态评估的缺失**：虽然已有一些动态评估方法（如Chatbot Arena、GameArena、Agent-Pro等），但存在主观偏差、场景单一、交互结构浅、信息复杂度有限等问题，难以迁移到真实复杂任务。
- **核心研究问题**：如何在部分可观测、动态变化的环境中，系统性地评估和提升大语言模型（LLM）的空间理解、自适应规划与长期记忆能力？
- **论文的总体回应**：构建了一个动态空间推理基准 **EvoEmpirBench（EEB）**，包含两个动态游戏环境——**局部可观测迷宫导航**与**消消乐（Match-2）**——并提出了一种受人类认知启发的在线学习框架 **Agent-ExpVer**，使智能体能够在持续交互中抽象经验、提炼规则并实现参数无关的自适应学习。

### 二、方法论：核心思想与关键技术细节

**2.1 动态推理基准：EvoEmpirBench（EEB）**

- **迷宫导航游戏（Maze Navigation）**：9×9网格世界，智能体在局部可观测条件下探索地图、收集金币、抵达终点。三个难度等级：
  - Easy：简单地图，5枚金币，无怪物；
  - Medium：引入2只移动怪物，威胁生命值；
  - Hard：保留2只怪物，额外增加4种交互道具（镐、铁剑、磁铁、钥匙），每种道具以不同方式改变环境结构。
- **消消乐游戏（Match-2 Elimination）**：8×8棋盘，通过消除至少2个同色方块得分，方块消除后下落、顶部生成新方块，目标是在有限步数内达成各颜色的消除配额。三个难度等级逐步收紧步数限制并提高目标配额。
- 两个游戏均提供了3个难度等级 × 30个实例 = 90个任务片段/游戏，总计180个片段。难点在于：每个动作都会触发环境结构性变化，要求智能体持续更新认知和策略。

**2.2 在线学习框架：Agent-ExpVer**

Agent-ExpVer由三个协作智能体组成，模拟人类"从经验中学习"的认知过程：

- **GeoLink Agent（环境交互代理）**：与环境进行迭代交互，在每个时间步 \( t \)，根据当前策略 \( \pi_t \) 选择动作 \( a_t \)，观测下一状态 \( s_{t+1} \) 和奖励 \( r_t \)，并记录完整的交互历史 \( H_{0:T} \)。
- **InsightForce Agent（经验抽象代理）**：在每局结束后，将交互历史 \( H_{0:T} \) 和最终指标 \( m \) 总结为**主观经验** \( e = f_{sum}(H_{0:T}, m) \)，存入经验记忆模块 \( M_{exp} \)。随后通过重放该回合来验证经验的有效性——如果关卡通过且分数提升，则该经验升级为**可复用的真相（truth）**，存入真相库 \( M_{truth} \)。
- **TruthWeaver Agent（真相管理代理）**：负责真相库的维护，执行三类操作——**合并**（语义相似的真相结合）、**删除**（冗余真相去重）、**插入**（新增独立真相）。
- **策略演化机制**：当前策略 \( \pi_t \) = 基础提示 \( \pi_0 \) ∪ 所有已验证的真相。若新策略的性能增量 \( \Delta < 0 \)，则回滚最新更新并重新进行经验抽象，确保策略只朝着改进方向演化。

### 三、实验设计

**3.1 Benchmark 与场景**

- 使用论文自建的 **EvoEmpirBench**（含迷宫导航与消消乐两个游戏），每个游戏包含3个难度等级、每等级30个实例，共90个实例/游戏。
- 每个游戏设置了多维评估指标：
  - 迷宫导航：成功率（Suc.Rate）、平均分（A.Score）、平均步数（A.Steps）、探索率（A.Explor）、金币收集率（A.Gold）、剩余生命（Rem.HP）、击杀数（A.Kills）、破坏障碍数（A.Barr）；
  - 消消乐：成功率、平均分、剩余/最大步数比（R/M.S）、每步得分（Score/Step）、每步消除数（Clear/Step）、API有效率（API Eff.）。

**3.2 对比模型**

- **专有模型**：GPT-4、GPT-4.1、Gemini-2.0-flash、Gemini-2.5-flash-preview、Claude-3-5-sonnet、Claude-3-7-sonnet、Grok-3；
- **开源模型**：Deepseek-V3、Llama-3.1-8B-instruct、Llama-3.1-70B-instruct、Qwen2.5-7B/14B/32B/72B-instruct、Qwen3-30B-a3B；
- **人类基线**：对同一任务进行了人类参与者的基准测试；
- **Agent-ExpVer增强版**：对GPT-4.1、Gemini-2.5-flash-preview、Claude-3-7-sonnet、Qwen2.5-32B-instruct四个模型应用了Agent-ExpVer框架，对比增强前后性能。

### 四、资源与算力

- 论文**未明确说明**所使用的GPU型号、GPU数量、训练时长或API调用总成本等算力资源信息。
- 这可能是由于该框架采用参数无关的在线学习方式（通过提示词级别的经验注入，不进行梯度更新），因此训练算力开销相对较低。但具体的实验基础设施投入在文中没有任何描述。

### 五、实验数量与充分性

- **总体实验量**：每组模型在每项任务上运行90个任务片段（3个难度 × 30实例 × 2个任务），覆盖了约15个基线模型 + 4个增强变体 + 人类基线，实验总量不可谓不大。
- **消融实验**：
  - **TruthWeaver消融**（表4）：在Qwen2.5-32B和GPT-4.1上移除TruthWeaver Agent，对比完整框架，验证其必要性；
  - **约束条件消融**（表5）：迷宫任务中移除部分可观测性（Full-Vision），消消乐中禁用道具（NoProps），验证EEB设计对任务难度的影响。
- **进一步分析**：展示了Agent-ExpVer学习过程中成功率/分数随迭代轮次的变化曲线，以及学习前后完成迷宫所需步数的分布变化。
- **充分性与客观性评估**：
  - **优点**：模型覆盖广泛（专有+开源+人类基线），指标多维，消融设计合理；
  - **不足**：每个配置仅测试90个实例，统计稳定性有待提升；未提供多次运行的方差/置信区间；人类基线仅90个样本，代表性有限；Agent-ExpVer仅应用于4个模型，普适性结论的支撑稍显不足。此外，"样本数量90"是否等价于90局完整游戏也需进一步澄清（论文中同时提到"120个任务片段"，这个数字存在歧义）。

### 六、主要结论与发现

- **主流模型在动态空间推理中表现欠佳**：迷宫任务中，多数模型成功率低于50%（最优GPT-4.1为73.33%，人类为90%）；消消乐任务更具挑战，基线LLM平均成功率仅33.7%（最优Grok-3为42.22%，人类为86.67%），与人类差距悬殊。
- **Agent-ExpVer带来一致性能提升**：应用后，迷宫任务成功率平均提升+5.6%、平均分提升+9.5%；消消乐任务成功率平均提升+13.3%。GPT-4.1-ours达到78.89%成功率，逼近人类水平。
- **TruthWeaver是必要组件**：移除后两个任务上性能均显著下降（Qwen成功率-6.1%，GPT-4.1成功率-8.3%），证实真相管理机制对缓解知识遗忘和稳定策略信念至关重要。
- **部分可观测性与道具使用显著增加任务难度**：全可见条件下GPT-4.1成功率从73.33%升至93.33%，表明EEB的设计确实对模型推理提出了更高要求。
- **学习过程中的"先降后升"现象**：经验归纳初期出现性能短暂下降（策略过泛化），经过3–4轮迭代后稳步提升，反映了模型的自我修正能力。

### 七、优点

- **基准设计新颖且紧扣现实**：部分可观测性 + 动态环境变化 + 多维度目标权衡，比静态或全局可见的基准更贴近真实应用场景；
- **跨任务通用框架**：Agent-ExpVer不依赖于特定游戏规则，是一种通用的在线学习机制，支持参数无关的持续适应；
- **认知启发性强**：经验提炼→验证→真相沉淀→策略更新的流程，模拟了人类"从实践中学习"的过程；
- **评估指标全面**：从成功率到资源管理、生存能力、交互效率等多个维度刻画智能体能力，避免了单一指标带来的片面结论；
- **对模型能力差异具有良好区分度**：实验显示不同规模模型在EEB上的表现梯度清晰，能有效反映模型推理能力的实际差异。

### 八、不足与局限

- **算力信息缺失**：未报告任何GPU/API成本、训练时长等关键资源细节，降低了实验的可复现性参考价值；
- **统计严谨性不足**：未提供多次运行的方差、标准误或置信区间；90个实例的测试量对于高方差动态任务而言可能不够稳定；
- **人类基线有限**：90个人类试次不足以代表人类整体水平，且未说明参与者背景（是否熟悉该类游戏）与实验条件；
- **Agent-ExpVer的可扩展性存疑**：仅对4个模型进行了增强实验，对更大规模或不同架构模型的适用性未知；经验抽象完全依赖LLM自身能力，低能力模型可能提炼出低质量真相，导致误差累积；
- **缺少与其他持续学习方法的直接对比**：未与Reflexion、Voyager、AutoManual等已有方法进行横向比较，无法明确Agent-ExpVer的相对优势；
- **文本内容中"120个任务片段"与"90个实例/游戏"存在数字不一致**，影响基准规模的准确理解；
- **应用范围仍然有限**：两个游戏环境虽具代表性，但尚不足以覆盖真实世界空间推理的全部复杂度（如三维空间、物理交互、多智能体协作等）。

（完）
