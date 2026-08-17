---
title: "3DLLM-Mem: Long-Term Spatial-Temporal Memory for Embodied 3D Large Language Model"
title_zh: "3DLLM-Mem: 具身三维大语言模型的长期空间-时间记忆"
authors: "Wenbo Hu, Yining Hong, Yanjun Wang, Leison Gao, Zibu Wei, Xingcheng Yao, Nanyun Peng, Yonatan Bitton, Idan Szpektor, Kai-Wei Chang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=q5QaTQcUbS"
tags: ["query:vln-memory"]
score: 9.0
evidence: 面向具身三维大模型的长时空间-时间记忆建模与评测基准
tldr: 针对大语言模型在动态多房间三维环境中缺乏长期时空记忆的问题，论文提出3DLLM-Mem动态记忆管理与融合模型，并构建含2.6万轨迹与2892任务的大型评测基准3DMem-Bench。模型在具身问题回答、描述和动作任务中利用长期记忆进行推理与规划。实验表明，显式的三维空间-时间记忆显著增强大模型在复杂具身场景中的表现，为记忆增强型导航提供基础。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有大语言模型缺少三维空间-时间记忆建模，难以在动态多房间环境中规划和行动。
method: 提出动态记忆管理与融合模型，并构建3DMem-Bench基准评测长期记忆。
result: 在具身推理与行动任务上显著提升，验证了长期空间-时间记忆的价值。
conclusion: 为具身大模型提供长期记忆建模和评测基准，支持记忆增强导航。
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

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：当前大语言模型（LLM）在动态、多房间 3D 环境中进行规划与行动的能力明显不足，难以像人类一样利用跨时间和空间的经验进行长期记忆推理。
- **关键假设**：现有 LLM 缺乏合适的三维空间-时间（spatial-temporal）记忆建模，是其无法在复杂具身场景中高效行动的重要原因。
- **研究目标**：通过引入长期记忆建模，提升 LLM 在 3D 具身环境中的推理与决策能力，同时提供评测基准以促进该方向的发展。

## 2. 方法论

- **核心思想**：提出 3DLLM-Mem，一种动态记忆管理与融合模型，用于 LLM 的具身空间-时间推理和动作。
- **技术细节**：
  - 将**当前观测**表示为**工作记忆令牌（working memory tokens）**，作为查询（queries）。
  - 利用这些查询从**情景记忆（episodic memory）**中存储的过去观测与交互中，**选择性注意并融合**最有用的空间和时间特征。
  - 这种机制使智能体能够在复杂、长时程环境中**聚焦任务相关信息**，同时维持**记忆效率**。
- **公式或算法流程**：所提供内容中未给出具体公式或伪代码；模型流程大致为：当前观测 → 工作记忆令牌 → 选择性检索/融合情景记忆中的时空特征 → 输出推理或动作。

## 3. 实验设计

- **数据集与场景**：
  - 新提出的 **3DMem-Bench**，包含 **超过 26,000 条轨迹** 和 **2,892 个具身任务**。
  - 任务类型涵盖 **具身问答（question-answering）** 和 **描述（captioning）**，并涉及具身动作任务。
- **Benchmark 目的**：评测智能体在 3D 环境中基于长期记忆进行推理的能力，尤其是复杂或“野外（in-the-wild）”场景。
- **对比方法**：与“最强基线”进行比较，但所提供的摘要中未列出具体基线名称。
- **核心结果**：3DLLM-Mem 在 3DMem-Bench 最具挑战性的具身任务上取得 state-of-the-art 表现，成功率达到 16.5% 的绝对提升（相对于最强基线）。

## 4. 资源与算力

- **提供的材料中未明确说明**使用了多少 GPU、训练时长或算力规模。
- 仅凭摘要和元数据无法获得训练资源的具体信息。

## 5. 实验数量与充分性

- **实验数量**：摘要提到“across various tasks”（多个任务），但未详细列出所有实验组；也未提及消融实验的数量。
- **充分性与公平性**：
  - 从现有信息看，实验设计覆盖了多种具身任务（问答、描述、动作），并使用了大规模基准，具备一定充分性。
  - 但**缺乏基线方法的具体细节**，也**没有消融实验**说明各组件（如情景记忆、查询机制）的贡献，因此难以完整评估实验的客观性与公平性。

## 6. 主要结论与发现

- 显式的三维空间-时间记忆建模能显著增强 LLM 在复杂具身场景中的表现。
- 3DLLM-Mem 在多个任务上达到 state-of-the-art，尤其在最具挑战性的 in-the-wild 具身任务中优势明显（成功率提升 16.5%）。
- 长期记忆（情景记忆 + 工作记忆查询融合）是记忆增强型导航与具身智能的重要基础。

## 7. 优点

- **大规模基准**：3DMem-Bench 提供超过 2.6 万条轨迹和近 3 千个任务，覆盖面广，具有资源价值。
- **新颖的记忆机制**：以工作记忆令牌作为查询、从情景记忆中选择性融合时空特征，设计直接且有效。
- **任务多样性**：同时评测问答、描述和动作任务，能够较全面评估模型能力。
- **显著实证增益**：在最具挑战性的任务上大幅超过强基线，验证了方法实用价值。
- **开放基础**：为长期记忆增强的具身导航和 3D LLM 研究提供了新的评测与建模框架。

## 8. 不足与局限

- **信息不完整**：所提供内容仅有摘要和元数据，缺乏方法细节、具体实验设置、消融分析等，限制深入评估。
- **基线不明**：未说明与哪些具体模型对比，无法判断比较的全面性与公平性。
- **实验覆盖不足**：未给出不同数据集、场景或任务的具体实验结果，也未见记忆容量、记忆效率与性能的权衡分析。
- **适用范围**：3DMem-Bench 的具体环境和真实世界迁移性尚不明确；in-the-wild 任务的定义也需进一步说明。
- **潜在偏差风险**：长期记忆查询机制可能过度依赖早期观测，或在极长轨迹中产生累积误差，已有内容未讨论。

**（完）**
