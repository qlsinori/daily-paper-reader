---
title: "HeLa-Mem: Hebbian Learning and Associative Memory for LLM Agents"
title_zh: HeLa-Mem：面向LLM智能体的赫布学习与联想记忆
authors: "Jinchang Zhu, Jindong Li, Cheng Zhang, Jiahong Liu, Menglin Yang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.625.pdf"
tags: ["query:semantic-map"]
score: 9.0
evidence: 基于赫布学习与联想记忆的LLM智能体长期记忆架构
tldr: 该论文指出当前LLM智能体长期记忆以非结构化嵌入向量检索为主，缺乏人类记忆的联想与巩固机制。受认知神经科学启发，提出HeLa-Mem记忆架构，实现联想、巩固和扩散激活三大机制。该架构使智能体能够在长程交互中保持连贯性并按关联强度提取记忆，为持续学习与记忆回调提供了神经形态的计算模型。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long625/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 722, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long625/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 805, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long625/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1631, \"height\": 636, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long625/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 740, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long625/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1637, \"height\": 696, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long625/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 727, \"height\": 664, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 824, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 804, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1647, \"height\": 956, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 728, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 786, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 719, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long625/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 380, \"label\": \"Table\"}]"
motivation: 现有LLM智能体长期记忆只靠向量相似检索，无法体现记忆联想和巩固结构。
method: 受生物学记忆启发，构建具有联想、巩固和扩散激活机制的HeLa-Mem记忆架构。
result: 实验表明HeLa-Mem在长程对话任务中显著提升记忆提取准确率和连贯性。
conclusion: 联想式记忆架构能有效增强LLM智能体的长期记忆能力。
---

## Abstract
Long-term memory is a critical challenge for Large Language Model agents, as fixed context windows cannot preserve coherence across extended interactions. Existing memory systems represent conversation history as unstructured embedding vectors, retrieving information through semantic similarity. This paradigm fails to capture the associative structure of human memory, wherein related experiences progressively strengthen interconnections through repeated co-activation. Inspired by cognitive neuroscience, we identify three mechanisms central to biological memory: association, consolidation, and spreading activation, which remain largely absent in current research. To bridge this gap, we propose HeLa-Mem, a bio-inspired memory architecture that models memory as a dynamic graph with Hebbian learning dynamics. HeLa-Mem employs a dual-level organization: (1) an episodic memory graph that evolves through co-activation patterns, and (2) a semantic memory store populated via Hebbian Distillation, wherein a Reflective Agent identifies densely connected memory hubs and distills them into structured, reusable semantic knowledge. This dual-path design leverages both semantic similarity and learned associations, mirroring the episodic-semantic distinction in human cognition. Experiments on LoCoMo demonstrate superior performance across four question categories while using significantly fewer context tokens. Code is available on GitHub: https://github.com/ReinerBRO/HeLa-Mem

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大语言模型（LLM）智能体受限于固定上下文窗口，无法在长时间跨度的多轮交互中维持连贯性。传统记忆系统将对话历史视为静态文本，通过嵌入向量的语义相似度进行检索，导致“记住事实但缺乏关系连续性”的问题。
- **关键洞察**：论文指出，人类记忆并非静态数据库，而是通过反复共激活逐步形成联想结构的动态系统。现有研究在三个生物记忆核心机制上存在明显缺失：
  - **联想（Association）**：相关经验通过重复共激活逐渐强化联结；
  - **巩固（Consolidation）**：情景记忆被逐步浓缩为稳定、可复用的语义知识；
  - **扩散激活（Spreading Activation）**：回忆某一条记忆时会沿着联想通路自然激活相关概念，支持多跳推理。
- **整体含义**：论文主张将认知神经科学中的赫布学习原理引入LLM智能体记忆设计，将静态的“存储—检索”模式升级为动态演化的“联想—巩固—检索”框架，使智能体具备类似于生物记忆的连续性与适应性，为长期记忆研究提供了一个神经形态的计算范例。

## 2. 方法论

### 2.1 核心思想
HeLa-Mem将对话历史建模为**动态赫布图**（Dynamic Hebbian Graph），通过三条生物学原则驱动设计：
1. **联想优于孤立**：共现的记忆应建立联结，形成超越语义相似性的潜在通路；
2. **主动巩固**：频繁访问的记忆簇应固化为稳定知识（模拟睡眠巩固机制）；
3. **扩散检索**：回忆一个记忆应自然触发相关联的概念。

### 2.2 关键模块与技术细节

- **双级存储结构**：
  - **情景记忆图（Episodic Memory Graph）**：对话轮次以节点形式存储，节点包含原文、稠密嵌入、时间戳、关键词和说话人角色；边表示联想强度，随赫布学习动态演化。
  - **语义记忆库（Semantic Memory Store）**：存储三类蒸馏知识——用户模型（用户特征及置信度）、事实性记忆（带绝对时间戳的事件）、智能体知识（人格与行为模式）。

- **在线编码与联想（Online Encoding & Association）**：
  - 通过赫布学习规则动态更新边权重，核心公式为：

    w(t+1)ij = (1 − λ)·w(t)ij + η·I(vi, vj ∈ Kt)

    其中 λ 为衰减率，η 为学习率，I(·) 为共激活指示函数。频繁共激活的记忆边权重增强，不使用的连接随时间衰减。

- **反思性巩固（Reflective Consolidation）**：
  - **中枢检测（Hub Detection）**：节点总关联强度超过阈值 δhub 时触发蒸馏：
    
    D(vi) = Σ w(i,j) > δhub
    
  - **赫布蒸馏（Hebbian Distillation）**：LLM综合中枢节点及其强连接邻居，提炼共同主题与因果关系，抽象为语义条目存入语义记忆库。
  - **自适应遗忘（Adaptive Forgetting）**：同时满足三个条件（边权重低于 δprune、非活跃时长超过 δage、零近期访问）的节点被移除，实现有选择地清理噪声而非一刀切丢弃。

- **双路检索（Dual-Path Retrieval）**：
  - **基础激活**：结合嵌入相似度、时间衰减和关键词重叠计算初始得分：

    Sbase(vi) = (sim(q, ei) + α·keyword_match)·γ(vi)

  - **扩散激活**：高分节点沿赫布边传播激活：

    S(vj) = Sbase(vj) + β·Σ Sbase(vi)·wij

  - **最终排序**：基础路径取 Top-k，翻转路径补充 Top-m 个未被选中但扩散得分高的节点，合并形成最终上下文。

### 2.3 生命周期
系统通过“在线编码→赫布学习→中枢检测→蒸馏→遗忘→双路检索”的连续认知循环，实现类似生物记忆系统的自动维护与管理。

## 3. 实验设计

- **主基准（LoCoMo）**：
  - 数据集：10个超长对话（平均约300轮，约9K token/对话），共1,986个问答对；
  - 问题类别：多跳（Multi-hop）、时间性（Temporal）、开放域（Open Domain）、单跳（Single-hop）四类；
  - 评估指标：F1与BLEU-1分数；
  - 骨干模型：GPT-4o-mini、GPT-4o、Qwen2.5-14b、Qwen2.5-3b；
  - 对比方法：LoCoMo（Native）、ReadAgent、MemoryBank、MemGPT、A-Mem、MemoryOS、Mem0、LightMem等。

- **额外基准（LongMemEval-S）**：
  - 500项长期对话记忆基准，使用GPT-4o-mini作为骨干和LLM评判，对比LangMem、MemoryOS、Mem0、FullText、NaiveRAG、A-MEM等方法。

- **消融实验**（GPT-4o-mini上）：去除反思性智能体、去除扩散激活、去除自适应遗忘三种变体对比。

- **案例研究**：多跳查询“你在哪里初次遇见影响你职业选择的人？”的检索链路追踪。

## 4. 资源与算力

- **原文未明确说明**使用的GPU型号、数量和训练时长。
- 论文仅提及评估了四种骨干LLM（GPT-4o-mini、GPT-4o、Qwen2.5-14b、Qwen2.5-3b），这些属于推理/评估阶段的开销。文章未报告API调用量、分布式训练配置或消融实验的计算总成本。
- 此外，论文在附录E中声明使用LLM工具进行语法检查与少量句子润色，但这不涉及实验算力。

## 5. 实验数量与充分性评估

- **实验数量较为充分**：
  - 主实验覆盖4个骨干模型×4类问题×多种对比方法（表1）；
  - 平均排名统计（表2）；
  - 3组消融实验（表3）；
  - 额外的LongMemEval-S基准评测（表6、表7）；
  - 可视化分析（赫布边权重矩阵）与案例追踪（图5、图6）；
  - 附录包含了数据集统计与问题类型分布（表4、表5）。

- **充分性与公平性分析**：
  - **优点**：跨模型规模验证说明了方法的鲁棒性；消融实验验证了各模块的贡献；额外基准增强了结果的可信度。
  - **注意点**：
    - MemoryOS部分结果由作者复现（标注†），可能引入复现偏差；
    - Qwen2.5-14b实验中对比基线数量较少（A-Mem、MEM0、MemoryOS、LightMem），且缺少如MemGPT等方法的对比；
    - 消融实验仅在单一骨干（GPT-4o-mini）上执行，未覆盖不同规模模型；
    - 缺少检索质量（如Hit@K）的独立评估，主要通过下游QA指标间接反映。

## 6. 主要结论与发现

- **性能领先**：在LoCoMo上，HeLa-Mem以最少上下文token（约1,010 token）实现了四类问题的最佳或接近最佳性能，平均排名1.25，显著优于MemoryOS（2.25）。
- **多跳推理显著增强**：GPT-4o-mini上Multi-hop达到40.14%，远超MemoryOS（38.39%）和A-Mem（27.02%），验证了赫布联想对跨信息桥接的有效性。
- **时间推理优势明显**：Temporal类别达到47.29%（GPT-4o-mini），得益于蒸馏期间保留绝对时间戳。
- **反思性巩固最重要**：消融显示，去除反思性智能体导致最大性能下降（34.74%→29.87%），确认了元认知组件对知识消化的关键作用。
- **扩散激活不可或缺**：去除扩散激活使多跳推理降幅显著（36.04%→33.88%），说明联想通路对复杂推理的价值。
- **自适应遗忘的价值**：在短对话（约300轮）中遗忘机制影响微弱，但对长期扩展性与检索噪声控制至关重要。
- **跨场景验证**：LongMemEval-S上准确性达65.40%，在时间性、跨会话、知识更新三个推理密集型类别上均为最佳。

## 7. 优点

- **理论创新性强**：将生物学中的赫布学习、睡眠巩固和扩散激活有机整合为统一的记忆架构，理论映射清晰。
- **双路检索设计巧妙**：语义路径与联想路径互补，有效规避了“语义陷阱”（即高相似性掩盖关键关联信息的问题）。
- **生命周期自动管理**：中枢检测—蒸馏—遗忘形成完整闭环，实现无需人工标注的记忆维护。
- **token效率突出**：在保证性能的同时显著压缩上下文长度（约1,010 token vs. 传统全量约16,910 token），实用价值高。
- **跨模型泛化良好**：在4种不同规模/来源的骨干模型上均表现稳定。
- **实验可视化直观**：边权重热力图和案例检索追踪清晰揭示了方法的内部工作机制。

## 8. 不足与局限

- **冷启动问题**：赫布权重需要足够交互历史才能积累，早期会话中联想检索优势不明显。论文建议未来可用语义相似度初始化赫布边以加速引导。
- **对骨干LLM的依赖**：语义蒸馏和中枢检测的质量依赖于底层LLM的推理能力；若LLM产生幻觉或推理错误，错误可能传播至长期存储并影响后续检索准确性。
- **遗忘机制缺乏长程验证**：LoCoMo约300轮对话不足以饱和记忆容量，自适应遗忘在更长对话中的实际效益尚未得到充分验证。
- **消融覆盖不足**：仅在GPT-4o-mini上进行消融实验，未显示不同规模骨干下各模块贡献的差异。
- **未开源详细复现细节**：虽然声明代码在GitHub上，但正文未说明具体的数据预处理、蒸馏调用次数和延迟开销（如反思性代理的推理开销）。
- **部分实验公平性受限**：MemoryOS结果由作者复现而非原始数据，可能引入偏差；Qwen2.5-14b下对比基线较少。
- **伦理与偏见风险**：论文虽简要提及长期记忆可能强化既有偏见，但未对记忆偏差的累积效应进行实验分析或提出缓解策略。

（完）
