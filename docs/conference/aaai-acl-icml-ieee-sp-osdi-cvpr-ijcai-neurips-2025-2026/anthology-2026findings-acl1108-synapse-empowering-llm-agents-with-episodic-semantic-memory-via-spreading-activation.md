---
title: "Synapse: Empowering LLM Agents with Episodic-Semantic Memory via Spreading Activation"
title_zh: 突触：通过激活扩散赋予LLM代理情景-语义记忆
authors: "Hanqi Jiang, Junhao Chen, Yi Pan, Ling Chen, Weihang You, Yifan Zhou, Ruidong Zhang, Yohannes Abate, Tianming Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1108.pdf"
tags: ["query:semantic-map"]
score: 9.0
evidence: 长期智能体记忆；情景-语义记忆；激活扩散；动态图
tldr: 针对标准检索增强方法无法处理长时智能体记忆的割裂性问题，提出Synapse统一记忆架构，借鉴认知科学中的激活扩散机制，将记忆建模为动态图。通过侧抑制和时间衰减动态突出相关子图并过滤干扰，融合几何嵌入与基于激活的图检索实现三重混合检索。该架构提升了LLM代理在长时任务中的记忆利用能力，为长期记忆建模提供了新思路。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1108/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1594, \"height\": 762, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1108/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 794, \"height\": 553, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1655, \"height\": 674, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1659, \"height\": 1212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1660, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1666, \"height\": 1132, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 688, \"height\": 1004, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 771, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 409, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 797, \"height\": 333, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1663, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1660, \"height\": 640, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1108/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1655, \"height\": 843, \"label\": \"Table\"}]"
motivation: 标准检索增强方法难以解决长期智能体记忆中知识片段割裂、无法形成连贯记忆的问题。
method: 构建动态图记忆，采用激活扩散机制，结合侧抑制与时间衰减，并设计三重混合检索策略。
result: 动态地突出相关子图并过滤干扰，提升了长时记忆的检索准确性。
conclusion: 基于激活扩散的记忆架构能有效弥补静态向量检索的局限，加强LLM代理的长时记忆能力。
---

## Abstract
While Large Language Models (LLMs) excel at generalized reasoning, standard retrieval-augmented approaches fail to address the disconnected nature of long-term agentic memory. To bridge this gap, we introduce Synapse (Synergistic Associative Processing Semantic Encoding), a unified memory architecture that transcends static vector similarity. Drawing from cognitive science, Synapse models memory as a dynamic graph where relevance emerges from spreading activation rather than pre-computed links. By integrating lateral inhibition and temporal decay, the system dynamically highlights relevant sub-graphs while filtering interference. We implement a Triple Hybrid Retrieval strategy that fuses geometric embeddings with activation-based graph traversal. Extensive evaluations on the LoCoMo benchmark show that Synapse significantly outperforms state-of-the-art methods in complex temporal and multi-hop reasoning tasks, offering a robust solution to the "Contextual Tunneling" problem.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大语言模型（LLM）在有限上下文窗口内表现出卓越的推理能力，但作为自主智能体（Agent）时，缺乏对长期经验的积累与叙事连贯性的保持能力。
- **核心问题**：现有的检索增强生成（RAG）方法将记忆视为静态向量库，基于语义相似度进行检索，无法应对需要**因果推理或传递性推理**的场景。作者将此问题归纳为 **Contextual Isolation（上下文隔离）**，其根源是 **Search Assumption（搜索假设）**——即假设记忆的相关性完全由与当前查询的语义接近度决定。
- **典型例子**：用户问“我今天为什么感到焦虑？”，向量检索可能找到最近关于“焦虑”的对话，却遗漏了几周前记录的时间冲突——后者才是根本原因，但与前者的词法和嵌入均无重叠。
- **核心洞察**：人类记忆检索不是“搜索”，而是**能量传播过程**——认知科学中的 **Spreading Activation（激活扩散）理论**（Collins & Loftus, 1975; Anderson, 1983）。访问一个概念会自然激活语义、时间或因果上相关联的概念，无需显式提示。
- **论文主张**：记忆不应被建模为静态可索引的库，而应被建模为可推理的动态网络。

## 2. 论文提出的方法论

### 2.1 总体框架：SYNAPSE（Synergistic Associative Processing & Semantic Encoding）

SYNAPSE 包含三大核心组件：**统一情景-语义图（Unified Episodic-Semantic Graph）**、**认知动力学（Cognitive Dynamics）**、以及**三重混合检索（Triple Hybrid Retrieval）**，外加**不确定性感知拒绝（Uncertainty-Aware Rejection）**机制。

### 2.2 统一情景-语义图

- **情景节点（Episodic Nodes, VE）**：封装每一交互轮次，表示为元组 (ci, hi, τi)，分别对应文本内容、稠密嵌入（由 all-MiniLM-L6-v2 生成）、时间戳。
- **语义节点（Semantic Nodes, VS）**：由 LLM 每 N=5 轮通过提示词提取的抽象概念（实体、偏好等），重复检测采用嵌入相似度阈值 τdup=0.92。
- **三类边**：
  - **时间边（Temporal Edges）**：连接时序相邻的轮次；
  - **抽象边（Abstraction Edges）**：在同一个合并窗口内双向连接情景节点与相关概念节点；
  - **关联边（Association Edges）**：建模概念之间的潜在关联。
- **图维护与可扩展性**：
  - 边剪枝：每个节点最多保留 Top-K（默认 K=15）入边；
  - 节点垃圾回收：激活值持续低于休眠阈值 ϵ=0.01 达 W=10 轮后归档至磁盘，保证活跃图节点数 ≤10,000。

### 2.3 认知动力学：激活扩散

- **初始化（双触发器）**：
  - **词法触发器**：BM25 稀疏检索，捕获精确实体匹配（如专有名词）；
  - **语义触发器**：稠密检索，捕获概念相似性（如“Ski Trip”）；
  - 两者 Top-k 节点的并集构成锚点集 T，按公式 (1) 注入初始能量。
- **扇出效应传播（Fan Effect）**：遵循 ACT-R 理论，能量按公式 (2) 传播。传播因子 S=0.8，时间衰减 ρ=0.01，激活按出度稀释，建模注意力稀释。
- **侧抑制（Lateral Inhibition）**：按公式 (3)，高激活节点抑制竞争节点（Top-M=7），实现注意力选择与稀疏性。
- **Sigmoid 非线性激活**：按公式 (4) 将抑制后的势能转换为最终发放率。迭代顺序严格为：传播→侧抑制→非线性激活，T=3 步内稳定。

### 2.4 三重信号混合检索

综合打分函数（公式 5）：

S(vi) = λ1 · sim(hi, hq) + λ2 · a(T)i + λ3 · PageRank(vi)

- 默认权重 λ = {0.5, 0.3, 0.2}（语义、激活、结构）；
- 三者角色正交：**PageRank** 提供与查询无关的全局结构先验（突出重要枢纽节点），**激活值**提供查询特定的局部上下文信号；
- 检索 Top-k（默认 k=30）后按拓扑序重排。

### 2.5 不确定性感知拒绝

- 受“知晓感”（Feeling of Knowing）启发，采用双重认知门控：
  - **置信度门控**：若最高排名节点的激活能量 Cret < τgate=0.12，则触发否定确认协议，预先拒绝回答；
  - **显式验证提示**：对临界情况，强制 LLM 判断“是否被明确提及？如果没有，输出‘未提及’”，区分参数知识幻觉与有依据的检索。

## 3. 实验设计

### 3.1 数据集与 Benchmark

- **LoCoMo benchmark**（Maharana et al., 2024）：长时对话记忆测试集，对话平均约 16K tokens，最多 35 个会话；
- 分为五类认知任务：**Single-Hop（C1）、Temporal（C2）、Open-Domain（C3）、Multi-Hop（C4）、Adversarial（C5）**；
- 主指标为 **F1 和 BLEU-1**，另以加权平均（排除对抗类别）衡量整体性能。

### 3.2 对比方法

涵盖四种范式的 **10 种以上基线**：

- 系统级：MemGPT、MemoryOS、Mem0
- 图结构：AriGraph、GraphRAG、Zep
- 检索式：MemoryBank、ENGRAM、LangMem
- 智能体/压缩型：ReadAgent、LoCoMo、A-Mem

公平性处理：可复现的基线统一使用 GPT-4o-mini（temperature 0.1）重新运行；固定专有后端的基线则报告其默认强模型结果。

### 3.3 主要实验矩阵

| 实验类型 | 内容 |
|---------|------|
| 主实验 | LoCoMo 五类任务，GPT-4o-mini 骨干，F1/BLEU-1 |
| 消融（机制级） | 不确定性门控、侧抑制、扇出效应、节点衰减逐一去除 |
| 消融（系统级） | 去除激活动力学、去除图结构、仅向量 |
| 效率分析 | 令牌数、延迟、API 成本、成本效率（F1/$） |
| 敏感性分析 | Top-k 参数、各超参数（S、δ、γ、θ、β、T、M） |
| 门控校准 | τgate 扫描（0.00–0.20）+ 假拒绝率 FRR |
| 统计稳定性 | 3 个随机种子，标准差 ≤0.5 |
| 低相似度子集 | 语义相似度低于 0.5 / 0.3 的子集表现 |
| LLM-as-a-Judge | 语义正确性评分（0–100） |
| 跨骨干模型 | GPT-4o、Qwen-1.5b、Qwen-3b |
| 定性分析 | 指标发散案例、失败模式（认知隧道） |

## 4. 资源与算力

- 论文**未明确给出训练/微调的总算力**（GPU 数量、训练时长、总计算预算等）；
- 仅提及：延迟在**单张 NVIDIA A100 GPU** 上测量（平均 100 次查询），SYNAPSE 平均延迟 1.9 秒；
- 图构建成本在智能体生命周期内摊销，每次查询成本可忽略；
- 每 1,000 次查询的 API 成本为 $0.24（GPT-4o-mini）。

## 5. 实验数量与充分性

- **覆盖面广**：主实验 + 12 组以上补充实验（消融、敏感性、效率、跨骨干、语义评估等），在多组实验维度上相当充分。
- **公平性举措**：
  - 统一骨干（GPT-4o-mini）重跑可复现基线；
  - 排除对抗类别计算加权平均，防止因自身拒绝机制导致分数虚高；
  - 报告“门控禁用”时的性能（F1 40.3），证明优势不依赖拒绝模块。
- **统计验证**：实例级配对 t 检验（N=500），p<0.05 验证显著优于 Zep。
- **可复现性**：3 个随机种子的标准差 ≤0.5，稳定性良好。
- **仍需注意的偏差**：
  - 主实验集中在单一 benchmark（LoCoMo）；
  - LLM-as-a-Judge 虽与生成器分离，仍可能偏好特定风格；
  - 对抗类别权重在整体排名中可能影响任务排名的直观解释。

## 6. 论文的主要结论与发现

1. **新 SOTA**：SYNAPSE 在 LoCoMo 上实现加权平均 F1=40.5（排除对抗类别），比第二强 Zep（39.7）高 0.8 点，比 A-Mem（33.3）高 7.2 点；任务排名第一。
2. **多跳推理显著提升**：35.7 vs. A-Mem 27.0（+23% 相对提升），验证激活扩散能跨中间节点桥接语义脱节的事实。
3. **对抗鲁棒性卓越**：96.6 F1 的拒绝率，远超 LoCoMo（69.2），归功于置信度门控与验证提示。
4. **效率优势突出**：约 814 tokens/查询，较全上下文方法（16,910 tokens）减少约 95%；成本效率（F1/$）达 167.3，远高于其他基线。
5. **机制互补性**：消融实验显示侧抑制、扇出效应、节点衰减各自承担不可替代的认知功能；缺少任意一项都会在相应任务类别产生显著退化。
6. **结构优于暴力**：SYNAPSE 在 k=30 时已超越 A-Mem，证明结构精度比单纯增大上下文体积更高效。

## 7. 优点

- **理论创新扎实**：从认知科学（ACT-R、激活扩散、侧抑制、时间衰减、元认知监控）到计算架构的映射逻辑清晰，不只是修辞性类比，而是落实到具体公式与机制。
- **解决真实痛点**：针对“上下文隔离”问题给出了精确的工程化方案（图结构 + 传播动力学），非简单的向量模式扩展。
- **效率与性能兼顾**：以 95% 的 token 缩减换取约 2 倍性能提升，建立了新的帕累托前沿。
- **鲁棒性设计**：不确定性感知拒绝机制有效控制幻觉；横向抑制的稀疏化防止“枢纽爆炸”问题。
- **实验完整**：11 组以上的实验矩阵覆盖机制级、系统级、效率、敏感性、稳定性、跨骨干等多个维度，消融设计有针对性，与理论主张一一对应。
- **诚实披露局限**：明确了冷启动问题、认知隧道风险、模态限制、对基础模型能力的依赖等，增强了工作可信度。

## 8. 不足与局限

- **冷启动问题（Cold Start）**：激活扩散依赖足够稠密的图拓扑。在历史对话稀疏的初始阶段，图维护的计算开销相比简单线性缓冲区没有优势。
- **认知隧道（Cognitive Tunneling）**：侧抑制在强枢纽存在时可能过度抑制低度细节（如在机场高激活背景下丢失“绿色夹克”这样的细节），导致简单查询上的性能退化。
- **模态限制**：当前仅在文本模态验证；尚未扩展至多模态记忆（图像、音频等），限制了在具身智能体中的应用。
- **对底层 LLM 的依赖**：
  - 上游依赖 LLM 提取语义节点的质量——小型开源模型可能无法稳定遵守提取模式，导致错误传播；
  - 下游依赖 LLM-as-a-Judge 评估，虽与生成器分离，仍存在风格偏见风险。
- **隐私与伦理风险**：长期场景记忆的持续存储天然涉及敏感用户信息；作者虽提出本地存储与“被遗忘权”设计，但尚未实现/验证端到端的隐私保护方案。
- **评估基准单一**：全部实验

。全部实验集中在 **LoCoMo 单一 benchmark** 上，未在 LongMemEval、MemGPT 长期对话集等其他长时记忆基准上交叉验证；因此，结论的泛化性（尤其在不同对话长度、用户规模、领域分布下）仍有待检验。

---

## 9. 总结评述

总体而言，SYNAPSE 是一篇**理论驱动、机制完整、实验扎实**的论文。其核心贡献不在于提出某一种更强的检索算法，而在于对“长期记忆应当如何组织与访问”这一根本问题给出了一个认知科学层面自洽、工程层面可落地的回答：**将记忆从静态向量库重构为动态网络，并用激活扩散模拟人类记忆的联想式提取**。

值得强调的是，本文的启发价值超越了具体的 F1 数字：它把“记忆检索”这一通常被简化为 top-k 近邻搜索的问题，重新界定为**图上的能量传播 + 注意力抑制 + 元认知门控**三者协同的过程。这种视角转换，可能为后续多轮对话智能体、终身学习系统乃至个性化助手提供新的设计范式。

与此同时，我们也应看到其局限：实验仅在单一基准、单一语言（英文）上验证；对冷启动、认知隧道等失效模式的应对仍是启发式的；隐私与遗忘机制尚未端到端落地。这些不足恰好勾勒出未来研究的方向——如何让记忆系统在更多模态、更多场景、更严格隐私约束下，持续接近人类记忆的灵活性与鲁棒性。

（完）
