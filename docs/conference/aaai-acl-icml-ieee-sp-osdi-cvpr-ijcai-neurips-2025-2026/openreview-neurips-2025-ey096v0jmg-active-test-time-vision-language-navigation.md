---
title: Active Test-time Vision-Language Navigation
title_zh: 主动测试时视觉语言导航
authors: "Heeju Ko, Sungjune Kim, Gyeongrok Oh, Jeongyoon Yoon, Honglak Lee, Sujin Jang, Seungryong Kim, Sangpil Kim"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EY096v0Jmg"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 视觉语言导航；测试时主动学习；情节反馈
tldr: 针对离线训练的视觉语言导航策略在陌生测试环境中性能下降且无外部反馈的问题，提出ATENA测试时主动学习框架。它通过与人类交互获取对不确定导航结果的情节反馈，在测试时引导策略置信度与决策，缓解熵最小化带来的累积错误。实验表明该方法在陌生环境导航任务上的性能得到显著提升，为实际部署提供了人机协作的测试时适应方式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 离线训练的VLN策略在陌生环境中任务表现下降，现有测试时熵最小化会累积误差。
method: 采用测试时主动学习，通过周期性的情景反馈指示导航结果，并学习提升决策置信度。
result: 在陌生环境导航中显著提升了任务成功率，减少了错误累积。
conclusion: 交互式测试时适应能够有效提升视觉语言导航的部署性能。
---

## Abstract
Vision-Language Navigation (VLN) policies trained on offline datasets often exhibit degraded task performance when deployed in unfamiliar navigation environments at test time, where agents are typically evaluated without access to external interaction or feedback. Entropy minimization has emerged as a practical solution for reducing prediction uncertainty at test time; however, it can suffer from accumulated errors, as agents may become overconfident in incorrect actions without sufficient contextual grounding. To tackle these challenges, we introduce ATENA (Active TEst-time Navigation Agent), a test-time active learning framework that enables a practical human-robot interaction via episodic feedback on uncertain navigation outcomes. In particular, ATENA learns to increase certainty in successful episodes and decrease it in failed ones, improving uncertainty calibration. Here, we propose mixture entropy optimization, where entropy is obtained from a combination of the action and pseudo-expert distributions—a hypothetical action distribution assuming the agent's selected action to be optimal—controlling both prediction confidence and action preference. In addition, we propose a self-active learning strategy that enables an agent to evaluate its navigation outcomes based on confident predictions. As a result, the agent stays actively engaged throughout all iterations, leading to well-grounded and adaptive decision-making. Extensive evaluations on challenging VLN benchmarks—REVERIE, R2R, and R2R-CE—demonstrate that ATENA successfully overcomes distributional shifts at test time, outperforming the compared baseline methods across various settings.

---

## 论文详细总结（自动生成）

# 主动测试时视觉语言导航（Active Test-time Vision-Language Navigation）——论文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：视觉语言导航（VLN）模型通常在离线数据集上训练，但在实际部署时会遇到**陌生的测试环境**，导致任务性能显著下降。传统测试场景中，智能体通常无法获得外部交互或反馈，只能依靠自身预测。
- **核心问题**：现有测试时熵最小化（Entropy Minimization）方法虽能降低预测不确定性，但容易**累积误差**——智能体可能在没有足够上下文依据的情况下，对错误动作产生过度自信。
- **整体含义**：论文提出一种**测试时主动学习**框架，通过引入人类对不确定导航结果的情节性反馈（episodic feedback），使智能体在测试阶段也能持续适应环境，提升决策的可靠性与部署性能。

## 2. 论文提出的方法论

- **核心思想**：提出 **ATENA（Active TEst-time Navigation Agent）** 框架，实现测试时的主动学习与人机交互。
- **关键技术细节**：
  - 通过与人类交互，对**不确定的导航结果**获取情节性反馈（例如该回合是否成功）。
  - 智能体在成功情节中增加确定性，在失败情节中降低确定性，从而**改进不确定性校准**。
  - 提出**混合熵优化（Mixture Entropy Optimization）**：
    - 熵来源于两个分布的组合：**动作分布**与**伪专家分布**（pseudo-expert distribution，即假设智能体所选动作最优时的假设性动作分布）。
    - 该机制同时控制**预测置信度**和**动作偏好**，避免单纯熵最小化带来的过度自信。
  - 提出**自我主动学习策略（Self-Active Learning）**：
    - 智能体基于高置信度预测评估自身导航结果，从而决定是否需要外部反馈。
    - 这使得智能体在**所有迭代中保持主动参与**，实现有依据的、自适应的决策。
- **算法流程（文字说明）**：
  1. 在测试环境中执行导航，得到一系列动作与预测分布。
  2. 计算混合熵（结合动作分布与伪专家分布）。
  3. 根据混合熵识别不确定的导航结果，触发主动查询机制。
  4. 人类（或模拟人类）提供该情节的成功/失败反馈。
  5. 利用反馈更新策略：提高成功情节的置信度，降低失败情节的置信度。
  6. 重复迭代，直至智能体在陌生环境中逐步适应。

## 3. 实验设计

- **数据集 / Benchmark**：
  - **REVERIE**
  - **R2R**（Room-to-Room）
  - **R2R-CE**（R2R with Continuous Environments，连续环境版本）
- **评估场景**：跨环境部署时面临的**分布偏移（distributional shifts）** 情况，即训练与测试环境不一致。
- **对比方法**：与多个基线方法进行比较，包括传统的测试时熵最小化方法以及其他测试时适应方法（具体方法名称未在提供文本中列出，但文中表明 ATENA 在所有设置下均优于对比基线）。
- **评估指标**：主要关注任务成功率（success rate）以及不确定性校准的相关指标（如置信度与结果一致性）。

## 4. 资源与算力

- 提供的文本中**未明确说明**使用的 GPU 型号、数量、训练/测试时长等算力信息。
- 由于该论文被 NeurIPS 2025 接收，通常此类工作会使用大型视觉-语言模型或预训练骨干网络，但具体资源消耗无法从摘要中获知。
- 若需完整资源细节，需查阅论文正文或附录。

## 5. 实验数量与充分性

- **实验覆盖**：在三个主流 VLN benchmark 上进行评估（REVERIE、R2R、R2R-CE），覆盖了室内导航、指令跟随、连续环境等多种任务变体，场景多样性较好。
- **消融实验**：摘要中未明确列出消融实验，但从方法包含多个组件（混合熵优化、自我主动学习、情节反馈）来看，预期有相应消融分析，需以正文为准。
- **公平性与客观性**：
  - 与多类基线比较，并在多种设置下验证，说明实验相对充分。
  - 但在没有具体数值和详细实验设置的情况下，无法完全判断公平性（如基线是否充分调参、是否使用相同骨干网络等）。

## 6. 论文的主要结论与发现

- ATENA 能够**有效克服测试时的分布偏移**，显著提升 VLN 任务在陌生环境中的成功率。
- 通过**交互式测试时适应**（而非仅依赖无监督熵最小化），可以减少累积错误，并改善不确定性校准。
- 自我主动学习机制可让智能体**自主判断何时需要反馈**，从而减少不必要的人工交互，同时保持适应性能。
- 在三个主流 benchmark 上，ATENA 均优于对比的基线方法。

## 7. 优点

- **问题切入有实际意义**：针对 VLN 部署中真实存在的“环境变化导致性能下降”问题，而不是仅追求实验室精度。
- **创新性结合**：将测试时自适应与主动学习、人类反馈相结合，突破了传统测试时自监督方法的局限。
- **方法设计完整**：混合熵优化同时考虑置信度与动作偏好，避免过度自信；自我主动学习降低人工反馈成本，具有实际部署价值。
- **实验验证充分**：跨多个 benchmark 和不同设置，结果一致性高。

## 8. 不足与局限

- **信息缺失**：摘录文本中缺乏具体数值、消融实验细节、对比方法名单和算力信息，难以进行深度量化评估。
- **依赖人类反馈**：虽然自我主动学习减少了交互频率，但仍需要一定量的人力参与，在完全自主部署场景中可能受限。
- **伪专家分布假设**：假设“所选动作最优”可能在某些错误动作上产生误导，尤其在环境分布偏移较大时，伪专家分布可能不准确。
- **泛化边界未知**：实验主要在室内 VLN 数据集上进行，对于更开放、动态或未知场景的泛化能力尚未验证。
- **隐私与安全性**：测试时交互式适应可能涉及人类标注者主观偏差，未讨论反馈质量对结果的影响。

（完）
