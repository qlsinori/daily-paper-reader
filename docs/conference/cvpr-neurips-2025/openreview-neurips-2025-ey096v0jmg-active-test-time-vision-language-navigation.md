---
title: Active Test-time Vision-Language Navigation
title_zh: 主动测试时视觉语言导航
authors: "Heeju Ko, Sungjune Kim, Gyeongrok Oh, Jeongyoon Yoon, Honglak Lee, Sujin Jang, Seungryong Kim, Sangpil Kim"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EY096v0Jmg"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 主动测试时自适应方法，用于视觉语言导航
tldr: VLN策略在陌生测试环境中容易性能下降，现有熵最小化方法会因过度自信产生累积误差。本文提出ATENA，一个测试时主动学习框架，通过episodic人类反馈实现人机交互，在不确定的导航结果上主动请求帮助并学习提高置信度。该方法能有效缓解陌生环境下的决策漂移，为VLN的测试时适应提供了实用的人机协同范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLN模型在陌生测试环境中任务表现退化，熵最小化等测试时方法易累积误差和过度自信。
method: 提出ATENA主动测试时学习框架，在不确定导航结果上引入人类反馈，通过episodic交互逐步提升模型置信度。
result: ATENA能够增强不熟悉环境中的导航决策，降低错误累积，提升测试时导航表现。
conclusion: 表明主动人机反馈是测试时VLN适应中应对不确定性的有效手段，拓展了VLN的实用部署能力。
---

## Abstract
Vision-Language Navigation (VLN) policies trained on offline datasets often exhibit degraded task performance when deployed in unfamiliar navigation environments at test time, where agents are typically evaluated without access to external interaction or feedback. Entropy minimization has emerged as a practical solution for reducing prediction uncertainty at test time; however, it can suffer from accumulated errors, as agents may become overconfident in incorrect actions without sufficient contextual grounding. To tackle these challenges, we introduce ATENA (Active TEst-time Navigation Agent), a test-time active learning framework that enables a practical human-robot interaction via episodic feedback on uncertain navigation outcomes. In particular, ATENA learns to increase certainty in successful episodes and decrease it in failed ones, improving uncertainty calibration. Here, we propose mixture entropy optimization, where entropy is obtained from a combination of the action and pseudo-expert distributions—a hypothetical action distribution assuming the agent's selected action to be optimal—controlling both prediction confidence and action preference. In addition, we propose a self-active learning strategy that enables an agent to evaluate its navigation outcomes based on confident predictions. As a result, the agent stays actively engaged throughout all iterations, leading to well-grounded and adaptive decision-making. Extensive evaluations on challenging VLN benchmarks—REVERIE, R2R, and R2R-CE—demonstrate that ATENA successfully overcomes distributional shifts at test time, outperforming the compared baseline methods across various settings.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：视觉语言导航（VLN）模型通常在离线数据集上训练，但部署到陌生导航环境时，由于环境分布偏移，任务性能会明显下降。
- **核心问题**：在测试阶段，智能体通常无法获得外部交互或反馈；现有常用的熵最小化方法虽能降低预测不确定性，却容易导致智能体在缺乏上下文依据的情况下对错误动作过度自信，从而产生累积误差。
- **整体含义**：论文旨在解决 VLN 在测试时面对分布偏移的适应问题，提出一种通过人类反馈进行主动测试时学习的人机协作范式，提升智能体在未知环境中的导航鲁棒性和决策可靠性。

## 2. 论文提出的方法论

- **总体框架**：提出 ATENA（Active TEst-time Navigation Agent），一种测试时主动学习框架。
- **核心思想**：通过「情节式反馈」（episodic feedback）让人类对不确定的导航结果进行干预，智能体学习在成功情节中提高置信度、在失败情节中降低置信度，从而改善不确定性校准。
- **关键技术细节**：
  - **混合熵优化（Mixture Entropy Optimization）**：熵的计算来自「动作分布」与「伪专家分布」（假设智能体所选动作为最优时的假想动作分布）的组合；通过同时控制预测置信度和动作偏好，避免单纯熵最小化带来的过度自信问题。
  - **自我主动学习策略（Self-Active Learning Strategy）**：智能体基于高置信度预测自行评估导航结果，从而在整个迭代过程中保持主动参与，实现有依据且自适应的决策，不依赖被动等待反馈。
- **算法流程（文字描述）**：智能体在测试环境中执行导航 → 对不确定结果触发人类反馈 → 根据成功/失败反馈调整混合熵目标 → 通过主动学习策略更新自身不确定性估计 → 持续迭代优化导航决策。

## 3. 实验设计

- **数据集 / Benchmark**：
  - REVERIE
  - R2R
  - R2R-CE（连续环境版本）
- **对比方法**：与多种基线方法进行了比较，尤其包括基于熵最小化的测试时适应方法。
- **实验设置**：涵盖不同场景和设定下的测试时分布偏移评估，以验证 ATENA 在未知环境中的泛化能力。

## 4. 资源与算力

- 论文提供的摘要和元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力资源信息。
- 因此，无法基于现有内容判断实验的计算成本；若需进一步了解，应查阅论文全文的实验设置部分。

## 5. 实验数量与充分性

- 从摘要可见，论文在 **3 个主流 VLN benchmark** 上进行了广泛评估，并对比了多种基线方法。
- 由于仅有摘要内容，**无法获知具体的实验组数**（例如消融实验数量、反馈预算变化、不同模型规模等）。
- 总体而言，多 benchmark 验证表明实验覆盖面较广，但**客观性和公平性**需要看到完整实验设置（如人类反馈模拟方式、基线调参细节、随机种子等）后才能充分评估。

## 6. 论文的主要结论与发现

- ATENA 能够有效克服测试时的分布偏移，在陌生环境中提升导航决策能力，优于所对比的基线方法。
- 主动引入人类反馈比完全无反馈的熵最小化方法更稳健，能够减少错误累积。
- 研究表明，主动人机反馈是测试时 VLN 适应中应对不确定性的有效手段，拓展了 VLN 的实用部署可能性。

## 7. 优点

- **问题切入点好**：直击 VLN 测试时分布偏移和熵最小化过度自信的痛点。
- **方法具有实用性**：采用情节式人类反馈，符合真实人机协作场景，为测试时适应提供了可行范式。
- **创新性**：混合熵优化结合伪专家分布，兼顾置信度与动作偏好，缓解了传统熵最小化的缺陷；自我主动学习减少了对人工反馈的过度依赖。
- **实验验证充分**：在三大 VLN 基准（含离散与连续环境）上进行评估，覆盖多样场景，增加了结论的可信度。

## 8. 不足与局限

- **人类反馈成本与模拟方式未在摘要中说明**：实际部署中，人类反馈的获取成本、延迟和噪声会影响方法的实用性。
- **计算资源信息缺失**：无法评估方法在训练和测试阶段的计算开销。
- **实验细节不足**：摘要未给出消融实验、超参数敏感性、失败案例分析等信息，限制了方法的深入理解。
- **潜在偏差风险**：人类反馈可能带有主观性，若反馈策略偏向简单场景，可能导致评估结果偏乐观；同时，伪专家分布的假设是否在所有环境下都成立需要进一步验证。
- **应用限制**：针对视觉语言导航，是否推广到其他具身智能任务（如操作、多智能体协作）尚不明确。

（完）
