---
title: "STRIDER: Navigation via Instruction-Aligned Structural Decision Space Optimization"
title_zh: STRIDER：基于指令对齐结构化决策空间优化的导航
authors: "Diqi He, Xuehao Gao, Hao Li, Junwei Han, Dingwen Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=w0xm9oG8im"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 使用自然语言指令在连续环境中进行零样本视觉语言导航
tldr: 零样本VLN-CE要求智能体在没有场景训练的情况下依据自然语言指令在未知3D环境中导航。论文指出现有方法缺乏结构化决策与反馈整合，故提出STRIDER框架，通过集成空间布局信息并利用历史动作反馈优化决策空间，使动作与空间结构及任务意图对齐。实验显示STRIDER在连续环境VLN基准上显著提升导航成功率。该框架为长程决策中的指令对齐提供了新的优化思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 零样本VLN-CE中现有方法缺少结构化决策和对动作反馈的整合，难以在长程导航中保持指令一致性。
method: 提出STRIDER，整合空间布局与动作反馈优化决策空间，使动作与空间结构和任务意图对齐。
result: 在VLN-CE基准上实现优越的导航成功率，优于现有零样本方法。
conclusion: 验证了结构化决策空间优化对零样本连续环境导航的有效性，可推广到其他长程具身任务。
---

## Abstract
The Zero-shot Vision-and-Language Navigation in Continuous Environments (VLN-CE) task requires agents to navigate previously unseen 3D environments using natural language instructions, without any scene-specific training. A critical challenge in this setting lies in ensuring agents’ actions align with both spatial structure and task intent over long-horizon execution. Existing methods often fail to achieve robust navigation due to a lack of structured decision-making and insufficient integration of feedback from previous actions. To address these challenges, we propose STRIDER (Instruction-Aligned Structural Decision Space Optimization), a novel framework that systematically optimizes the agent’s decision space by integrating spatial layout priors and dynamic task feedback. Our approach introduces two key innovations: 1) a Structured Waypoint Generator that constrains the action space through spatial structure, and 2) a Task-Alignment Regulator that adjusts behavior based on task progress, ensuring semantic alignment throughout navigation. Extensive experiments on the R2R-CE and RxR-CE benchmarks demonstrate that STRIDER significantly outperforms strong SOTA across key metrics; in particular, it improves Success Rate (SR) from 29\% to 35\%, a relative gain of 20.7\%. Such results highlight the importance of spatially constrained decision-making and feedback-guided execution in improving navigation fidelity for zero-shot VLN-CE.

---

## 论文详细总结（自动生成）

## STRIDER：基于指令对齐结构化决策空间优化的导航（中文总结）

### 1. 核心问题与整体含义（研究动机与背景）

- **任务背景**：零样本连续环境视觉语言导航（Zero-shot VLN-CE）要求智能体在**未经过场景特定训练**的情况下，仅依据自然语言指令在未知的三维连续环境中完成导航。
- **核心挑战**：在长时程（long-horizon）执行过程中，智能体的动作需要同时与**空间结构**（如墙壁、障碍物、可行走区域）和**任务意图**（指令语义）保持一致。
- **现有方法不足**：已有方法缺乏**结构化决策**——即没有显式利用空间布局来约束动作候选；同时缺乏对**历史动作反馈**的整合，导致导航过程中容易偏离指令语义或陷入无效探索。
- **研究意义**：该问题直接关系到具身智能体在真实环境中的部署能力，是视觉语言导航从仿真走向实际应用的关键瓶颈。

### 2. 方法论：核心思想、关键技术细节与流程

- **总体框架**：提出 STRIDER（Instruction-Aligned Structural Decision Space Optimization，指令对齐结构化决策空间优化），其核心思想是**将空间布局先验和动态任务反馈同时纳入决策空间的优化过程**，从而让动作选择与空间结构及任务语义对齐。
- **两个关键创新模块**：
  1. **结构化航点生成器（Structured Waypoint Generator）**
     - 作用：利用环境的空间结构（如可通行区域、障碍物边界、拓扑关系）对动作空间进行约束。
     - 效果：过滤掉不符合空间结构约束的动作，缩小候选动作集合，使决策只能在物理可行且结构合理的航点之间进行。
  2. **任务对齐调节器（Task-Alignment Regulator）**
     - 作用：根据任务执行进度动态调整智能体的导航行为。
     - 机制：持续收集来自之前动作的反馈信号，判断当前状态与指令目标的语义距离和进度，从而修正下一步决策，确保语义对齐不随步数增加而漂移。
- **算法流程简化描述**：
  1. 接收自然语言指令和当前感知到的视觉/空间观测；
  2. 结构化航点生成器根据空间布局生成候选航点集合（约束动作空间）；
  3. 任务对齐调节器结合历史动作反馈与任务进度，对候选动作进行语义评分和重排序；
  4. 选择综合得分最高的动作执行；
  5. 更新反馈状态，循环直至到达目标或终止条件。

### 3. 实验设计：数据集、基准与对比方法

- **数据集/场景**：
  - **R2R-CE**：基于 Matterport3D 场景的连续环境版本，指令来自 R2R 数据集，是 VLN-CE 最常用的基准。
  - **RxR-CE**：来自 RxR 数据集，包含更多样化、更长的指令，对长程语义对齐要求更高。
- **Benchmark**：两者均属于 VLN-CE 连续环境导航基准，测试智能体在未见过的场景中的零样本泛化能力。
- **对比方法**：论文声称与“强基线/当前最优方法”（strong SOTA）进行了对比，但摘要中未列出具体方法名称；通常此类工作会对比如 Sim2Sim、Sim2Real 零样本 VLN 方法（如 VLN-CE 上的零样本基线、基于预训练视觉语言模型的方法等）。
- **主要指标**：成功率和导航效率相关指标，重点报告了 **Success Rate (SR)**。

### 4. 资源与算力

- **文中未明确说明**训练所需的 GPU 型号、数量、训练时长或推理成本等算力信息。
- 由于论文正文未提供实验设置细节（如 batch size、训练轮数、硬件配置），因此无法评估其计算资源需求。这在摘要型内容中较为常见，但若为全文则应在实验部分补充。

### 5. 实验数量与充分性

- **从摘要可见的实验覆盖**：
  - 两个数据集：R2R-CE 和 RxR-CE；
  - 展示了主实验的 SR 指标提升（29% → 35%）。
- **未明确提及的实验**：
  - 缺少消融实验的具体描述（例如验证两个模块各自的贡献是否分别做了移除测试）。
  - 缺少不同训练/推理策略对比、超参数敏感性、跨场景泛化稳定性等分析。
- **充分性评估**：
  - 仅凭摘要信息，实验设计看似覆盖了**核心基准**，但**公开证据有限**。若正文包含消融实验和更多指标（如 SPL、nDTW、路径长度等），则更为充分。
  - 实验公平性无法从摘要判断——需要确认对比方法是否同样为零样本设置、是否使用相同的视觉骨干和指令编码器、是否在相同评估协议下进行。

### 6. 主要结论与发现

- STRIDER 在零样本 VLN-CE 任务上**显著超越现有 SOTA**：
  - 成功率（SR）从 29% 提升到 35%，相对提升 **20.7%**。
- 结论强调：
  - **空间约束的决策空间**（结构化航点生成）能有效避免无效动作，提高物理可行性和导航精度；
  - **反馈引导的任务对齐执行**（任务对齐调节器）能在长程导航中维持指令语义一致性；
  - 该框架证明了结构化决策空间优化在零样本连续环境导航中的有效性，并具有推广到其他长程具身任务的潜力。

### 7. 优点

- **方法论创新性强**：将“空间结构约束”和“动作反馈整合”同时纳入决策空间优化，针对零样本 VLN-CE 的痛点较为精准。
- **模块化设计**：两个模块分工明确，分别解决“物理可行性”和“语义一致性”问题，便于理解和扩展。
- **性能提升显著**：在 SR 上的相对增益达到 20.7%，在连续环境导航中属于较大幅度的提升。
- **任务意义明确**：零样本、无场景训练的特性使其更贴近真实应用，具备较强的实用价值。

### 8. 不足与局限

- **实验细节缺失**：当前摘要未提供具体消融实验、模块贡献分解、不同场景类型（如室内 vs. 室外）的表现，难以全面验证方法的泛化能力。
- **对比方法不明确**：未列出具体 SOTA 方法名称，无法确认比较的公平性和全面性。
- **算力信息缺失**：未提及训练成本，不利于复现和效率评估。
- **潜在偏差风险**：
  - 只报告 SR 为主，可能忽略了路径效率（SPL）等关键指标；若 SR 提升但路径更长，实际部署效果可能打折扣。
  - 零样本设置下，预训练模型的选择可能对结果影响较大，文中未说明是否对骨干网络做了针对性调优。
- **应用限制**：
  - 方法仍依赖室内 3D 场景数据集，对复杂动态场景或真实机器人平台的适应能力未知；
  - 结构化航点生成可能需要额外的空间拓扑信息，在未知且无先验的环境中获取这些信息可能受限。

---

（完）
