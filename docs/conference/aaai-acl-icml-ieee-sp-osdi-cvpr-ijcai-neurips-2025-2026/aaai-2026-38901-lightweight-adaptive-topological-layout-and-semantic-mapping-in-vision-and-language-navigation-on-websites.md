---
title: Lightweight Adaptive Topological Layout and Semantic Mapping in Vision-and-Language Navigation on Websites
title_zh: 网站视觉语言导航中的轻量级自适应拓扑布局与语义映射
authors: "Pingrui Lai, Zihao Xie, Hua Yang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38901/42863"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 在网站上根据人类指令进行视觉语言导航，并构建自适应语义映射
tldr: 针对网站视觉语言导航中导航图结构开放且网页布局动态变化的问题，本文提出ATLAS框架，自适应构建时变、无界的拓扑布局并融合语义映射。该方法用统一机制更新跨网页的全局地图，使智能体在依据人类指令导航时能同时提升准确率和推理速度。实验表明ATLAS能有效处理动态网页环境，为网页智能体导航提供了轻量级且可扩展的解决方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38901/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 882, \"height\": 816, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38901/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1670, \"height\": 739, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38901/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 883, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38901/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 872, \"height\": 788, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38901/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 876, \"height\": 231, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38901/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38901/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1833, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38901/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 873, \"height\": 543, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38901/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38901/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 873, \"height\": 211, \"label\": \"Table\"}]"
motivation: 现有网页智能体依赖大语言模型但导航性能受限、推理慢，全局地图构建面临开放动态网页结构的挑战。
method: 提出ATLAS框架，自适应构建时变无界拓扑图并融合语义映射，以轻量方式维护跨页面全局地图。
result: 在网站VLN任务上提升了导航准确率与效率，验证了自适应拓扑语义映射的有效性。
conclusion: 自适应拓扑布局与语义映射可显著增强网页智能体的指令导航能力，并兼顾计算开销。
---

## Abstract
Vision-and-Language navigation on websites requires agents to navigate target webpages and answer questions based on human instructions. Current web agents primarily leverage Large Language Models (LLMs) for semantic understanding and reasoning, but still suffer from limited navigation performance and slow inference speed. Constructing a global map across webpages can effectively enhance both navigation accuracy and efficiency, however, this is challenged by the open structure of web navigation graphs and the dynamic nature of web layouts. In this paper, we propose ATLAS: Adaptive Topological Layout And Semantic mapping, a framework that adaptively constructs a time-varying, unbounded topological map across webpages and unifies heterogeneous elements through semantic representation. This enables both global path planning and local element selection for web-based navigation and question answering. As a lightweight approach, ATLAS significantly outperforms existing state-of-the-art methods on the WebVLN benchmark with a 10% improvement in success rate, and achieves the highest average task success rate on both the Mind2Web and WebArena benchmarks.

---

## 论文详细总结（自动生成）

# 网站视觉语言导航中的轻量级自适应拓扑布局与语义映射——论文总结

## 1. 核心问题与整体含义

- 论文关注**网站上的视觉语言导航（Vision-and-Language Navigation on Websites）**任务：智能体需根据人类自然语言指令，在真实网页中导航至目标页面并回答问题。
- 现有主流方法严重依赖大型语言模型（LLM）进行语义理解与推理，存在两大核心瓶颈：
  - **导航性能有限**：LLM 缺乏显式的环境状态表示和动作选择模块，难以稳定完成多步网页操作；
  - **推理速度慢**：LLM 逐 token 生成导致高延迟，影响实际使用效率。
- 本文受机器人导航中 SLAM 构建全局地图思想的启发，提出在网页环境中构建**全局拓扑地图**来提升导航精度与效率。
- 然而，该思路面临两个关键挑战：
  - **导航图结构开放**：网页元素（按钮、超链接、内容块）导致连接图可无限扩张，难以穷举探索；
  - **网页布局动态变化**：同一网站在不同用户或不同时间访问时结构可能不同，导致理论可达节点与实际可操作节点不一致。
- 为此，论文提出 **ATLAS（Adaptive Topological Layout And Semantic mapping）** 框架，自适应构建时变、无界的拓扑语义地图，统一异构网页元素表示，实现全局路径规划与局部元素选择的结合。

## 2. 方法论

ATLAS 将任务建模为部分可观测马尔可夫决策过程（POMDP），主要由五个组件组成：

1. **状态与上下文初始化**
   - 使用预训练 BERT 初始化 `[CLS]` 状态向量和语言 token；
   - 语言 token 仅生成一次，后续作为 Transformer 的 key/value。

2. **自适应拓扑布局构建（ATL）**
   - **动态节点添加**：维护图 G_t，节点包括已访问节点、可访问节点以及当前节点，每个节点用语义表示 hi 编码（根据节点类型取均值、邻居信息或最新观察）。
   - **Web 感知边构建**：边权重结合“是否存在超链接”与节点语义余弦相似度，公式为 e_ij = 1_link + α·cos(h_i, h_j)。
   - **自适应图更新**：每访问新页面，将当前节点、邻居节点和新边加入图，实现无界、时变的图扩展。

3. **语义映射模块（SM）**
   - 将 HTML 元素（按钮等）编码为统一表示 fi，融合视觉特征（CNN 提取包围框区域）、类型特征（tag 嵌入 + 属性 MLP）和文本特征（MLP 编码文本内容）；
   - 通过多层 Transformer（SemanticEncoder）对元素间关系进行语义融合，并可与指令 token 做交叉注意力。

4. **图引导的导航规划（GP）**
   - **全局规划**：用 NodeEncoder 编码图中节点，再通过图注意力网络（GAT）聚合全局上下文，输出全局动作分数 a_global；
   - **局部选择**：用 Transformer 解码器（ActionDecoder）基于当前页元素语义特征输出局部分数 a_local；
   - **特征融合**：计算融合权重 β，加权组合全局与局部动作得到最终策略，平衡探索与利用。

5. **Web 感知答案生成**
   - 将最终导航状态与全局拓扑图上下文拼接，通过 QAEncoder 编码，再由 QADecoder 生成答案文本。

- **训练策略**：总损失 = 导航监督损失 + 答案生成损失 + 语义损失（类型分类、元素关系、布局一致性），采用多任务联合优化。

## 3. 实验设计

### 数据集与 Benchmark

- **WebVLN**：14,825 个任务，导航 + 问答联合评测；指标包括 SR（成功率）、OSR、SPL、TL 以及 WUPS@0.0 / WUPS@0.9（答案相似度）。
- **Mind2Web**：2,350 个任务，137 个网站、31 个领域；评价跨任务、跨网站、跨域的成功率（SR）。
- **WebArena**：812 个任务，涵盖搜索、导航、操作等；离线评测任务成功率，在线评测还关注每步平均耗时（AT）。

### 对比方法

- **导航式方法**：VLNBERT、WebGUM、WebVLN-Net。
- **LLM 方法**：AgentBench、NavGPT（含 GPT-4 版本）、ActionVerse、GPT-3.5-Turbo、GPT-4、Flan-T5-XL、LLaMA2-7B/70B、AutoWebGLM、CogAgent、Qwen2.5、Llama3.1、GPT-4o、OpenAI-o3/o4-mini、DigiRL、Filtered BC 等。
- **消融实验**：分别移除系统架构中的 ATL、SM、GP、F（特征融合）模块，以及逐步添加五种训练损失（Lnav、Ltype、Lrel、Lcoh、Lans）。

## 4. 资源与算力

- 文中仅说明使用 **NVIDIA Tesla A100 和 NVIDIA RTX 3090 GPU** 进行训练与推理。
- 未明确给出 GPU 数量、训练时长、显存占用等具体资源信息。

## 5. 实验数量与充分性

- **主实验规模**：在 WebVLN 上进行验证集和测试集评测；在 Mind2Web 上报告跨任务、跨网站、跨域三种设置；在 WebArena 上报告离线任务成功率并给出在线效率对比图。
- **补充实验**：两组消融实验（系统架构、训练损失）、一个定性案例分析（ATLAS vs WebVLN-Net 的状态转移图）。
- **充分性评估**：
  - 数据集覆盖三个主流基准，对比方法包含传统导航模型和多种 LLM 方案，维度较全面；
  - 消融实验验证了每个关键模块和损失项的贡献，结论较可靠；
  - 但部分对比实验（如 WebArena 在线）仅给出平均指标，缺少分项统计和方差分析；且未提供失败案例分析。
  - 总体而言，实验数量较为充分，设计基本客观公平，但细节可进一步丰富。

## 6. 主要结论与发现

- 在 WebVLN 上，ATLAS 相比 SOTA 方法成功率显著提升：验证集 SR 提升 12.5%，测试集 SR 提升 17.03%；相比 LLM 方法，轨迹长度更短。
- 在 QA 指标上，ATLAS 在 WUPS@0.9 和 WUPS@0.0 上均大幅超过 WebVLN-Net，说明不仅能到达目标页，还能正确组织信息回答问题。
- 在 Mind2Web 上，ATLAS 以 61.0% 的平均成功率超越所有基线（包括 AutoWebGLM 的 59.5%），跨任务和跨网站表现最佳。
- 在 WebArena 离线评测中，ATLAS 平均成功率 41.0%，超过全部对比模型（如 OpenAI-o4-mini 36.9%、DigiRL 30.3%）。
- 推理速度方面，ATLAS 比开源小模型快 2 倍以上，比闭源专有 LLM 管线的速度快 10 倍以上，同时保持较高成功率。
- 定性分析显示，ATLAS 能有效利用图结构进行“探索-回退”，避免线性导航导致的答非所问。

## 7. 优点

- **轻量高效**：无需大规模 LLM，即可实现比 LLM 方法更高的导航成功率，且推理速度显著更快。
- **自适应拓扑建模**：能应对网页图结构开放与布局动态变化，构建无界、时变的地图，是核心创新点。
- **全局 + 局部协同决策**：图引导的全局规划与页面内局部元素选择相融合，平衡探索与利用。
- **语义统一表示**：将多模态异构 HTML 元素映射为统一语义向量，提升模型对网页结构的理解能力。
- **实验覆盖多基准**：在 WebVLN、Mind2Web、WebArena 上均取得 SOTA 或最高平均成绩，泛化性有说服力。
- **模块化设计**：各组件可独立消融验证，便于分析与改进。

## 8. 不足与局限

- **特定场景性能欠佳**：在信息整合（如 Reddit 多帖推理）和工具使用（如 Map 多软件交互）任务上，ATLAS 仍存在明显不足，说明其在复杂长期任务中泛化能力有限。
- **轨迹长度增加**：相比导航式方法，ATLAS 的轨迹长度略长（约 +5.12%），原因是图构建过程中的额外探索开销。
- **依赖 HTML 元素可点击性**：方法假设可访问到的按钮子集可被准确提取，对于动态渲染或非标准页面可能存在误差。
- **资源信息不透明**：未报告 GPU 数量、训练时间等关键资源指标，影响复现和效率评估。
- **对比公平性存疑**：部分 LLM 基线（如 GPT-4）为 zero-shot 或 few-shot，而 ATLAS 经过特定任务训练，比较虽有意义但并非完全同等条件下进行。
- **未提供错误分析**：缺少对失败案例的系统性分析，无法充分诊断导航错误的根本原因。
- **模型容量限制**：基于 BERT 的轻量架构在复杂推理和长上下文理解上可能弱于大规模 LLM，未来或需结合更强语义模型提升上限。

（完）
