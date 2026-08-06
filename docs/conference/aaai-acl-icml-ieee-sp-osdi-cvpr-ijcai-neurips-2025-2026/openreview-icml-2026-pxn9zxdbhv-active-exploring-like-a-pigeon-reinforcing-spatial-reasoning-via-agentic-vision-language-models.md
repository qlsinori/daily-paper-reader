---
title: "Active Exploring like a Pigeon: Reinforcing Spatial Reasoning via Agentic Vision-Language Models"
title_zh: 像鸽子一样主动探索：通过智能体视觉语言模型强化空间推理
authors: "Wei Deng, Xianlin Zhang, Mengshi Qi"
date: 2026-04-30
pdf: "https://openreview.net/pdf/54cb4a4f37805d2dff8e5b522a2c4800c77b3abd.pdf"
tags: ["query:semantic-map"]
score: 8.0
evidence: 提出动态认知地图与持久空间记忆，用于智能体空间推理，受鸽类导航启发。
tldr: 现有的视觉语言模型在进行空间推理时往往只是被动观察，难以应对真实世界的复杂空间关系；且强化学习常因稀疏奖励而训练困难。该文借鉴鸽子利用认知地图导航的行为，提出智能体式探索管线，将场景布局参数化为动态认知地图并作为持久记忆，同时引入空间断言代码以程序化描述空间关系。通过主动探索与强化学习，该方法显著提升了模型的空间推理能力，展示了认知地图式记忆机制在智能体空间理解中的潜力。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: VLM空间推理依赖被动观察，缺乏主动探索与持久空间记忆。
method: 用动态认知地图编码场景布局，结合空间断言代码和强化学习进行主动探索。
result: 在复杂空间推理任务上取得显著提升，证明记忆机制的有效性。
conclusion: 为智能体空间推理提供了认知启发式的记忆与探索范式。
---

## Abstract
Enabling Vision-Language Models (VLMs) to perform spatial reasoning remains challenging.
Existing approaches treat VLMs as passive observers, which is difficult for real-world applications.
Moreover, reinforcement learning methods rely on sparse rewards, limiting their effectiveness for complex reasoning tasks.
Inspired by pigeons' building and exploiting cognitive maps for navigation, we propose a novel agentic pipeline for spatial reasoning.
First, we introduce a new \emph{dynamic cognitive map} parameterizing scene layout as object positions and orientations, serving as persistent memory for new observations.
Second, we propose a novel \emph{Spatial Assertion Codes (SAC)}, Python expressions programmatically describing spatial relationships.
By collaborating with the dynamic cognitive map, SAC enables verification of intermediate reasoning steps, providing dense reward signals.
We optimize the model via supervised and reinforcement finetuning.
Experiments on the MindCube benchmark demonstrate state-of-the-art performance with \emph{80.5\%} overall accuracy, outperforming the best current method by \emph{29.5} accuracy points (a relative improvement of \emph{53.2\%}) on the challenging \textsc{Rotation} subset. Our code and data are open-sourced at \url{https://github.com/dw-dengwei/active-spatial-reasoning.git}.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：使视觉语言模型（VLM）具备真正的空间推理能力。现有方法将 VLM 视为被动观察者，只能静态处理输入信息，难以应对真实世界中需要主动探索和动态适应的复杂空间场景。
- **背景与动机**：
  - 当前 VLM 在空间推理上依赖被动观察，面对新场景时缺乏主动获取信息的能力，导致空间理解不完整。
  - 强化学习（RL）方法在空间推理任务上常面临稀疏奖励问题，即模型只在最终结果时获得反馈，中间推理过程缺乏监督信号，训练效率低且效果有限。
  - 受鸽子利用认知地图进行导航的生物学行为启发，论文提出构建动态认知地图作为持久空间记忆，并结合程序化空间描述实现密集奖励的主动探索式空间推理。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将空间推理建模为主动探索过程，模仿鸽子构建和利用认知地图导航的行为。模型通过持续观察、记忆更新和推理验证三个环节协同工作，实现复杂的空间理解。
- **关键技术细节**：
  - **动态认知地图（Dynamic Cognitive Map）**：
    - 将场景布局参数化为物体位置与朝向，形成结构化空间表示。
    - 作为持久记忆存储历史观察信息，每当模型收到新观察时，更新地图以保持环境认知的时效性和一致性。
  - **空间断言代码（Spatial Assertion Codes, SAC）**：
    - 用 Python 表达式程序化描述空间关系（如“物体 A 在物体 B 左侧”）。
    - 与动态认知地图配合，可验证中间推理步骤的正确性，为强化学习提供密集奖励信号，缓解稀疏奖励问题。
  - **训练方法**：采用监督微调（Supervised Finetuning）与强化微调（Reinforcement Finetuning）两阶段优化。监督阶段学习基础空间推理能力，强化阶段通过密集奖励策略进一步优化主动探索策略。

### 3. 实验设计

- **Benchmark**：MindCube 基准，包含复杂空间推理任务，其中 Rotation 子集被特别强调为挑战性较高的场景。
- **数据集/场景**：以 MindCube 中的各类空间推理任务为主，涵盖需要多步观察和空间关系推断的复杂场景。
- **对比方法**：与当前最优（State-of-the-Art）的已有空间推理方法对比。摘要中未逐一列出对比方法名称，但明确提及其表现优于最佳现有方法。

### 4. 资源与算力

- 摘要中**未提及**任何关于 GPU 型号、数量、训练时长等算力资源的信息。
- 论文在代码开源链接中提供了代码和数据的公开访问，但算力详情需查阅论文全文或仓库说明。

### 5. 实验数量与充分性

- 摘要中报告的实验包括：在 MindCube 基准上的整体性能测试（80.5% 准确率）以及 Rotation 子集上的专项评估。
- **充分性与客观性**：
  - 尚无消融实验（如去除动态认知地图或 SAC 的对比）的明确信息，无法判断各组件的独立贡献。
  - 实验场景集中在 MindCube 基准，缺乏对其他空间推理数据集（如室内导航、机器人操作等）的泛化验证。
  - 与现有方法的对比数量有限，对比方法的选取标准未明确，公平性难以全面评估。
- 总体而言，摘要展示的结果显著，但实验覆盖面和详细程度不足，需查看论文全文才能全面评判。

### 6. 论文的主要结论与发现

- 提出的主动探索式智能体空间推理方法在 MindCube 基准上取得 **80.5%** 的整体准确率，达到当前最优水平。
- 在最具挑战性的 Rotation 子集上，该方法比最佳现有方法高出 **29.5 个百分点**（相对提升 **53.2%**），证明动态认知地图与空间断言代码的组合在处理复杂空间变换推理上具有显著优势。
- 验证了认知地图式记忆机制的有效性，表明持久空间记忆和主动探索是提升 VLM 空间推理能力的关键方向。

### 7. 优点

- **生物学启发**：借鉴鸽子认知地图导航机制，为空间推理引入创新性的认知框架，具有跨学科理论价值。
- **方法创新**：
  - 动态认知地图将场景布局结构化并持续更新，解决被动观察的局限性。
  - 空间断言代码（SAC）将空间关系程序化，使推理过程可验证，从而提供密集奖励信号，有效缓解稀疏奖励问题。
- **性能提升显著**：在挑战性最强的 Rotation 子集上实现 53.2% 的相对提升，结果具有说服力。
- **开放共享**：代码与数据已开源，有利于复现和后续研究。

### 8. 不足与局限

- **实验覆盖有限**：仅在 MindCube 单一基准上验证，缺乏跨领域泛化评估（如真实机器人环境、室内导航等），结论普适性有待证明。
- **消融分析缺失**：摘要未展示各组件（动态地图 vs. SAC vs. 主动探索策略）的独立消融实验，无法确定每项创新的具体贡献度。
- **对比方法不透明**：未列出具体对比方法及其配置，消费者难以判断对比的公平性和基线强弱。
- **算力成本不明**：未披露训练所需 GPU 资源、时间等关键信息，影响可复现性和实际部署评估。
- **应用限制**：当前方法依赖程序化断言代码，对非结构化或开放式真实环境的适应能力尚不明确；主动探索策略在未知动态场景中的鲁棒性未验证。

（完）
