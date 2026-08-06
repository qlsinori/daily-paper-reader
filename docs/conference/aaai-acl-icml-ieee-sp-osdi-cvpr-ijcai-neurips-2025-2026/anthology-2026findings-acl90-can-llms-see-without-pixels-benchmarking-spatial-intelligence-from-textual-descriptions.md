---
title: Can LLMs See Without Pixels? Benchmarking Spatial Intelligence from Textual Descriptions
title_zh: 没有像素，LLM还能“看见”吗？——基于文本描述的空间智能基准
authors: "Zhongbin Guo, Zhen Yang, Yushan Li, Xinyue Zhang, Wenyu Gao, Jiacheng Wang, Chengzhi Li, Xiangrui Liu, Ping Jian (鉴萍)"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.90.pdf"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 包含自我中心导航等空间智能评测文本基准
tldr: 空间智能研究通常依赖视觉语言模型，但空间理解究竟来自视觉编码器还是底层推理能力仍待解答。本文提出SiT-Bench基准，将单/多视角场景转化为高保真带坐标的文本描述，不提供像素输入，直接测试大语言模型的空间智能，包含空间导航、视角变换和精细操作等17个子任务。基于3800余条专家标注的评测可为空间推理能力提供更纯净的评估方式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 422, \"height\": 225, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 398, \"height\": 231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 446, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1578, \"height\": 874, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1617, \"height\": 797, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 413, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 410, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 411, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 413, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 409, \"height\": 212, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 411, \"height\": 213, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 408, \"height\": 213, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 413, \"height\": 215, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 409, \"height\": 237, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 410, \"height\": 236, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 410, \"height\": 239, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 410, \"height\": 237, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 411, \"height\": 238, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 410, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 410, \"height\": 310, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 403, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl90/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 113, \"height\": 178, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1640, \"height\": 520, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1640, \"height\": 1035, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 805, \"height\": 2203, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1634, \"height\": 1440, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 631, \"height\": 967, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1639, \"height\": 1210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl90/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1635, \"height\": 630, \"label\": \"Table\"}]"
motivation: 当前空间智能评测多依赖视觉模型，难以判断空间理解是否源于文本推理而非视觉编码器。
method: 构建SiT-Bench基准，将场景转为坐标感知的文本描述，仅向LLM提供符号级空间信息，评测多个空间子任务。
result: 该基准包含3800多条专家标注和17个子任务，可系统评估LLM在无像素输入下的空间智能。
conclusion: 纯文本空间推理基准为解耦视觉编码与空间推理提供了重要评测工具。
---

## Abstract
Recent advancements in Spatial Intelligence (SI) have predominantly relied on Vision-Language Models (VLMs), yet a critical question remains: does spatial understanding originate from visual encoders or the fundamental reasoning backbone? Inspired by this question, we introduce **SiT-Bench**, a novel benchmark designed to evaluate the SI performance of Large Language Models (LLMs) without pixel-level input, comprises over 3,800 expert-annotated items across five primary categories and 17 subtasks, ranging from egocentric navigation and perspective transformation to fine-grained robotic manipulation. By converting single/multi-view scenes into high-fidelity, coordinate-aware textual descriptions, we challenge LLMs to perform symbolic textual reasoning rather than visual pattern matching. Evaluation results of state-of-the-art (SOTA) LLMs reveals that while models achieve proficiency in localized semantic tasks, a significant "spatial gap" remains in global consistency. Notably, we find that explicit spatial reasoning significantly boosts performance, suggesting that LLMs possess latent world-modeling potential. Our proposed dataset SiT-Bench serves as a foundational resource to foster the development of spatially-grounded LLM backbones for future VLMs and embodied agents.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：空间智能（Spatial Intelligence, SI）的近期进展主要依赖视觉语言模型（VLMs）。然而一个根本性问题尚未解答：模型的空间理解能力到底来源于视觉编码器，还是来源于底层大语言模型（LLM）的推理能力？
- **核心问题**：如果完全去除像素输入，仅提供文本描述，LLM 能否表现出空间智能？
- **整体含义**：本文旨在解耦“视觉感知”与“空间推理”，探究 LLM 作为通用推理引擎在纯文本条件下是否具备世界建模与空间理解的潜力，为未来 VLM 和具身智能体的空间感知能力发展提供理论基础与评测工具。

---

### 2. 论文提出的方法论

- **核心思想**：构建一个纯文本空间智能基准 **SiT-Bench**，彻底剥离像素信息，仅通过高保真、带坐标的文本描述向 LLM 提供符号级空间信息，迫使模型进行符号文本推理而非视觉模式匹配。
- **关键步骤**：
  - 将单视角/多视角场景转换为带坐标的文本描述（coordinate-aware textual descriptions）。
  - 设计涵盖 5 大主类、17 个子任务的任务体系，包括自我中心导航（egocentric navigation）、视角变换（perspective transformation）、精细机器人操作（fine-grained robotic manipulation）等。
  - 评测过程中**不向模型提供任何像素输入**，仅输入文本，要求模型完成空间推理任务。
- **技术细节**：文本描述需保持高保真度，确保空间关系、物体位置、方向等关键信息无损失；评测采用专家标注的正确答案，并设置了统一的评估标准。论文没有给出特定的数学公式，核心思路是“符号空间推理”。

---

### 3. 实验设计

- **数据集/基准**：**SiT-Bench**，包含 **3,800 余条专家标注样本**，覆盖 5 大主类、17 个子任务。
- **评测对象**：多种 SOTA 大语言模型（具体模型名称在摘要中未列出，需查阅原文）。
- **任务类型**：
  - 空间导航（如自我中心导航）
  - 视角变换
  - 精细操作任务
- **对比逻辑**：主要对比不同 LLM 在纯文本条件下的空间推理表现，观察不同任务类型上的能力差异，而不是与传统视觉模型直接对比。

---

### 4. 资源与算力

- **说明**：在提供的摘要和元数据文本中，**没有明确说明**使用了多少 GPU、训练/推理时长、算力规模等资源信息。需要查阅论文原文的实验设置部分才能获取更详细的信息。

---

### 5. 实验数量与充分性

- **实验数量**：从摘要来看，实验涵盖了 5 大类和 17 个子任务，每个任务有对应的专家标注样本，总计超过 3,800 条。
- **充分性与公平性**：
  - **优点**：多任务覆盖为评估提供了较全面的视角；专家标注保证了答案质量。
  - **不足**：摘要未提及是否进行了细致的消融实验（如文本表示方式对性能的影响、不同输入格式的敏感性等），也未提及不同模型参数的对比范围有多广。因此，实验的**横向广度较好，但纵向深度分析（如错误分析、消融）尚不明确**。

---

### 6. 论文的主要结论与发现

- **模型能力分层**：SOTA LLM 在局部语义任务上表现熟练，但在需要**全局一致性**的空间推理任务上存在显著的“**空间差距**”（spatial gap）。
- **显式推理的增益**：当模型被要求进行显式空间推理（即显式利用坐标和空间关系进行思考）时，性能显著提升。
- **潜在世界建模能力**：这一结果表明，LLM 内部可能已经具备**潜在的世界建模能力**，但默认情况下未被充分激发。
- **资源价值**：SiT-Bench 可作为评估和促进未来 VLM 与具身智能体空间感知能力的**基础性资源**。

---

### 7. 优点

- **问题设计新颖、关键**：直接戳中当前 VLM 空间智能研究中的痛点——区分“视觉感知”和“推理能力”的贡献。
- **纯文本基准的简洁性**：通过去除像素输入，提供了一种“干净”的评测方式，避免了视觉编码器带来的混淆变量。
- **覆盖范围广**：涵盖导航、视角变换、精细操作等多层次空间任务，有助于全面解析空间智能的内涵。
- **专家标注保证质量**：3,800 余条样本由专家标注，保障了评测的可靠性。
- **实用导向**：可作为未来空间推理基座模型（spatially-grounded LLM backbones）的评测标准。

---

### 8. 不足与局限

- **缺少视觉输入对照**：基准完全排除像素输入，虽然这是设计初衷，但也意味着它无法评估 VLM 在“像素+文本”混合条件下的实际表现，无法直接衡量视觉编码器的贡献。
- **文本描述的信息损耗**：将三维场景转换为二维文本描述的过程中，可能存在空间信息失真或丢失，特别是在复杂场景或多物体交互场景中。
- **任务覆盖有偏**：空间智能内涵广泛，17 个子任务虽然覆盖面较广，但仍难以覆盖所有真实世界空间任务（如物理交互中的动态空间变换）。
- **未提及算力和模型细节**：缺少对具体模型参数、计算成本和实验资源的信息，不利于复现与评估。
- **局限性风险**：基准可能对“擅长文本推理”的模型有利，而对那些更依赖感知模式但推理能力较弱的模型形成不公平劣势；此外，评测中未明确提及对抗性设置或文本描述的歧义性问题。

---

（完）
