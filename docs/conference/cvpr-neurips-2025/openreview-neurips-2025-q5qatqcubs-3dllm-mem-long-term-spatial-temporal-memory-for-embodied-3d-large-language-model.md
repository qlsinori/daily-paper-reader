---
title: "3DLLM-Mem: Long-Term Spatial-Temporal Memory for Embodied 3D Large Language Model"
title_zh: 3DLLM-Mem：具身3D大语言模型的长期时空记忆
authors: "Wenbo Hu, Yining Hong, Yanjun Wang, Leison Gao, Zibu Wei, Xingcheng Yao, Nanyun Peng, Yonatan Bitton, Idan Szpektor, Kai-Wei Chang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=q5QaTQcUbS"
tags: ["query:vln-memory"]
score: 8.0
evidence: 面向具身3D大语言模型的长期时空记忆，与导航智能体的空间记忆需求直接对齐
tldr: 当前大语言模型在动态多房间3D环境中难以有效规划和行动，主要缺乏适当的3D空间-时间记忆建模。为此论文构建了包含2.6万条轨迹、2892个具身任务的3DMem-Bench基准，并提出3DLLM-Mem动态记忆管理与融合模型，用于具身空间-时间推理与动作。实验表明该模型在记忆驱动的具身任务上表现显著提升，为机器人导航等具身智能体的长期记忆机制提供了新范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 大语言模型缺少长期空间-时间记忆建模，难以在动态多房间环境中规划与行动。
method: 构建3DMem-Bench基准与3DLLM-Mem模型，采用动态记忆管理和融合机制实现具身空间-时间推理与动作。
result: 在超过2.6万条轨迹的具身任务上验证了模型有效提升长期记忆推理能力。
conclusion: 揭示了长期时空记忆对具身LLM的重要性，为后续导航等复杂任务提供基准与方法。
---

## Abstract
Humans excel at performing complex tasks by leveraging long-term memory across temporal and spatial experiences. In contrast, current Large Language Models (LLMs) struggle to effectively plan and act in dynamic, multi-room 3D environments. 
We posit that part of this limitation is due to the lack of proper 3D spatial-temporal memory modeling in LLMs. 
To address this, we first introduce 3DMem-Bench, a comprehensive benchmark comprising over 26,000 trajectories and 2,892 embodied tasks, question-answering and captioning, designed to evaluate an agent's ability to reason over long-term memory in 3D environments.
Second, we propose 3DLLM-Mem, a novel dynamic memory management and fusion model for embodied spatial-temporal reasoning and actions in LLMs. 
Our model uses working memory tokens, which represents current observations, as queries to selectively attend to and fuse the most useful spatial and temporal features from episodic memory, which stores past observations and interactions. Our approach allows the agent to focus on task-relevant information while maintaining memory efficiency in complex, long-horizon environments.
Experimental results demonstrate that 3DLLM-Mem achieves state-of-the-art performance across various tasks, outperforming the strongest baselines by 16.5\% in success rate on 3DMem-Bench's  most challenging in-the-wild embodied tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：人类能够借助长期记忆，在时间和空间经验中完成复杂任务；而当前大语言模型（LLM）在动态、多房间的三维（3D）环境中难以有效规划与行动。
- **核心问题**：论文认为，这种局限部分源于 LLM 缺乏合适的 **3D 空间-时间记忆建模**，即模型不能像人类一样跨时空调用过往经验来支持具身决策。
- **整体含义**：该工作旨在为具身智能体（如机器人导航）提供一种能够长期记忆并融合空间-时间信息的大语言模型机制，推动 LLM 从静态文本推理走向动态 3D 环境下的具身推理与动作执行。

## 2. 论文提出的方法论

- **两大核心贡献**：
  1. **3DMem-Bench 基准**：一个涵盖超过 **26,000 条轨迹**和 **2,892 个具身任务**的大规模基准，任务类型包括问答（question-answering）和描述生成（captioning），用于评估智能体在 3D 环境中基于长期记忆进行推理的能力。
  2. **3DLLM-Mem 模型**：一个新颖的动态记忆管理与融合模型，面向 LLM 的具身空间-时间推理与动作。

- **关键技术细节**：
  - 模型区分两类记忆：
    - **工作记忆（working memory tokens）**：表示当前观测信息。
    - **情景记忆（episodic memory）**：存储过去的观测与交互。
  - 机制流程：以工作记忆 token 作为查询（queries），有选择性地关注并融合情景记忆中**最有用的空间特征和时间特征**。
  - 设计目标：使智能体聚焦于任务相关信息，同时在复杂、长时程（long-horizon）环境中保持记忆效率。
  - 摘要中未给出具体公式或算法伪代码，但整体思路属于“查询驱动、动态读取记忆”的注意力融合范式。

## 3. 实验设计

- **数据集/场景**：基于论文自建的 **3DMem-Bench** 基准，覆盖大量具身任务，主要用于评估动态多房间 3D 环境下的长期空间-时间记忆推理能力。
- **Benchmark 构成**：
  - 26,000+ 条轨迹；
  - 2,892 个具身任务；
  - 包含问答和描述生成等任务类型。
- **对比方法**：摘要中提到对比了“最强的基线”（strongest baselines），但**未列出具体基线方法名称**。
- **主要结果**：在 3DMem-Bench 最具挑战性的“野外（in-the-wild）”具身任务上，3DLLM-Mem 的成功率比最强基线高出 **16.5%**，达到当前最优（state-of-the-art）性能。

## 4. 资源与算力

- **文中未明确说明**使用的 GPU 型号、数量、训练时长或推理资源。
- 由于提供材料限于摘要和元数据，无法得知具体算力开销；需要查看论文全文或附录才能获得该信息。

## 5. 实验数量与充分性

- **基于摘要可确认的实验信息有限**：仅提到在 3DMem-Bench 整体任务上的 SOTA 结果，以及野外任务上成功率提升 16.5%。
- **未提及**：
  - 具体分组实验数量；
  - 不同任务类型的详细结果；
  - 消融实验（如去掉空间记忆、时间记忆或融合机制分别会怎样）；
  - 与更广泛基线（如普通 LLM、无记忆模型）的对比细节。
- **总体评价**：从摘要看，实验覆盖了大规模基准并取得显著提升，方向明确、有说服力；但在没有全文信息的情况下，尚无法判断实验设计是否全面、公平，尤其是消融和基线选择方面。

## 6. 论文的主要结论与发现

- 当前 LLM 在动态 3D 环境中表现不佳的重要原因之一是**缺少长期时空记忆建模**。
- 构建专门的长期记忆基准 **3DMem-Bench**，能够有效评测具身智能体的记忆推理能力。
- 提出的 **3DLLM-Mem** 动态记忆管理和融合机制，可显著提升 LLM 在具身空间-时间推理与动作任务上的表现，尤其是在复杂野外场景中。
- 总体说明：长期空间-时间记忆对具身大语言模型至关重要，该研究为后续导航等复杂具身任务提供了基准和方法基础。

## 7. 优点

- **问题切入精准**：直指 LLM 在具身场景中欠缺时空记忆的核心痛点，与机器人导航等应用需求高度对齐。
- **提出专用基准**：3DMem-Bench 规模大（26k+轨迹、2.8k+任务），能够系统衡量长期记忆推理能力。
- **方法设计新颖**：动态区分工作记忆与情景记忆，并以当前观测为查询去融合历史时空特征，兼顾了**任务相关性**和**记忆效率**。
- **效果提升明显**：在最具挑战的任务上相对最强基线提升 16.5%，具有较强的实证说服力。
- **学术价值**：已被 NeurIPS 2025 接收，说明该方向得到领域认可，并为后续研究提供参考范式。

## 8. 不足与局限

- **摘要中实验细节有限**：没有列出具体基线、消融实验、各任务类型详细结果，难以全面评估方法的普适性和各个模块的独立贡献。
- **算力与训练成本未提及**：不便于判断该方法的资源可及性。
- **局限在基准环境**：3DMem-Bench 虽包含多房间动态环境，但仍可能是仿真或限定场景，真实世界机器人部署效果未知。
- **长期记忆管理挑战未深入讨论**：例如记忆的遗忘、冲突、隐私、容量上限等问题在摘要中未展开。
- **对比基线不明确**：“最强基线”具体是谁、是否充分调校、是否覆盖多样化的记忆增强方法，均需全文核实。
- **由于只能基于摘要和元数据，上述不足不等于论文本身缺陷，而是信息有限条件下的保守判断。**

（完）
