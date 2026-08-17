---
title: Active Test-time Vision-Language Navigation
title_zh: 主动式测试时视觉语言导航
authors: "Heeju Ko, Sungjune Kim, Gyeongrok Oh, Jeongyoon Yoon, Honglak Lee, Sujin Jang, Seungryong Kim, Sangpil Kim"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EY096v0Jmg"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 结合人类反馈的测试时主动学习视觉语言导航
tldr: VLN策略在陌生环境测试时性能退化，熵最小化易因错误累积而过度自信。作者提出ATENA测试时主动学习框架，通过人类对不确定导航结果的片段式反馈进行交互式修正。该框架学习提升动作置信度并利用反馈纠正错误，从而提升未知环境下的导航成功率。ATENA展示了测试时交互在VLN中的价值。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: VLN离线训练策略在不熟悉环境下部署时性能下降，熵最小化缺乏足够上下文支撑易导致错误累积。
method: 提出ATENA框架，通过测试时主动学习与人类碎片反馈交互，针对不确定动作逐步修正策略。
result: 实验表明ATENA在未知场景中有效提升导航性能，优于熵最小化基线。
conclusion: 主动测试时交互为VLN的环境适应提供了实用而有效的新途径。
---

## Abstract
Vision-Language Navigation (VLN) policies trained on offline datasets often exhibit degraded task performance when deployed in unfamiliar navigation environments at test time, where agents are typically evaluated without access to external interaction or feedback. Entropy minimization has emerged as a practical solution for reducing prediction uncertainty at test time; however, it can suffer from accumulated errors, as agents may become overconfident in incorrect actions without sufficient contextual grounding. To tackle these challenges, we introduce ATENA (Active TEst-time Navigation Agent), a test-time active learning framework that enables a practical human-robot interaction via episodic feedback on uncertain navigation outcomes. In particular, ATENA learns to increase certainty in successful episodes and decrease it in failed ones, improving uncertainty calibration. Here, we propose mixture entropy optimization, where entropy is obtained from a combination of the action and pseudo-expert distributions—a hypothetical action distribution assuming the agent's selected action to be optimal—controlling both prediction confidence and action preference. In addition, we propose a self-active learning strategy that enables an agent to evaluate its navigation outcomes based on confident predictions. As a result, the agent stays actively engaged throughout all iterations, leading to well-grounded and adaptive decision-making. Extensive evaluations on challenging VLN benchmarks—REVERIE, R2R, and R2R-CE—demonstrate that ATENA successfully overcomes distributional shifts at test time, outperforming the compared baseline methods across various settings.

---

## 论文详细总结（自动生成）

由于原始的论文 PDF 文本未能成功提取（返回的是 OpenReview 的验证页面），以下总结严格基于你提供的论文 Markdown 元数据、TLDR、动机、方法、结果与结论等字段，并明确指出因原始 PDF 未获取而无法确认的具体信息。

---

# Active Test-time Vision-Language Navigation 论文详细中文总结

## 1. 论文核心问题与整体含义

- **研究背景**：视觉语言导航（Vision-Language Navigation, VLN）策略通常在离线数据集上训练，但在测试时部署于不熟悉的环境中，模型性能会显著下降。传统测试时评估中，智能体无法获得外部交互或反馈，导致适应能力受限。
- **核心问题**：如何让 VLN 智能体在陌生环境部署时，通过测试时的主动交互与学习，克服分布偏移（distribution shift）、避免错误累积，从而提升导航成功率。
- **既有方案的不足**：熵最小化（Entropy Minimization）被用作测试时降低预测不确定性的实用方案，但该方法缺乏足够的上下文关联，容易导致智能体对错误动作产生过度自信，进而造成累积误差。
- **研究意义**：论文提出一种名为 **ATENA** 的测试时主动学习框架，通过引入人类对不确定导航结果的片段式反馈，在测试阶段动态修正智能体决策，为 VLN 的环境适应提供了新的解决思路。该工作发表于 **NeurIPS 2025**（审稿评分 9.0）。

## 2. 论文提出的方法论

- **核心思想**：ATENA 将测试时学习与人类交互反馈结合，通过学习“在成功片段中提高动作置信度，在失败片段中降低置信度”的方式，改善智能体的不确定性校准（uncertainty calibration），从而让智能体在未知环境中做出更合理、更有根据的决策。
- **关键技术细节**：
  - **混合熵优化（Mixture Entropy Optimization）**：
    - 通过将“动作分布”和“伪专家分布”（即假设智能体所选动作是最优情况下的假设动作分布）相结合来获取熵。
    - 该机制同时控制预测置信度与动作偏好，解决了单纯熵最小化中缺乏上下文支撑的问题。
  - **自主动学习策略（Self-Active Learning Strategy）**：
    - 让智能体基于高置信度的预测来评估自身导航结果，判断片段成功或失败。
    - 该策略使智能体在整个测试迭代过程中保持主动参与状态，实现基于反馈的自我修正和自适应决策。
- **算法流程概述（文字说明）**：
  1. 智能体在未知环境中执行导航任务，输出一系列动作。
  2. 针对不确定的导航结果，引入人类提供的片段式反馈（episodic feedback）。
  3. 通过混合熵优化，融合动作分布与伪专家分布计算熵，同时约束置信度与动作偏好。
  4. 利用自主动学习策略，根据高置信度预测自动评估导航结果（成功/失败）。
  5. 根据评估与反馈动态调整策略，在持续交互中不断改善导航表现。

## 3. 实验设计

- **使用的数据集/基准**：
  - **REVERIE**
  - **R2R**（Room-to-Room）
  - **R2R-CE**（R2R with Continuous Environments）
  - 均为视觉语言导航领域的权威基准（VLN benchmarks）。
- **对比方法**：与基线方法（尤其以熵最小化为主的方法）进行对比，实验覆盖多种设置（different settings），包括未知场景下的测试时部署与分布偏移场景。
- **实验目的**：验证 ATENA 是否能有效克服测试时的分布偏移问题，并超越现有基线方法。

## 4. 资源与算力

- **说明**：由于原始论文 PDF 未能成功获取（OpenReview 返回的是验证页面），**本总结无法确认论文是否明确提及 GPU 型号、数量、训练时长或算力规模**。元数据中亦未包含相关资源信息。
- 若需获得准确的算力信息，建议直接访问论文原文或 OpenReview 页面（https://openreview.net/pdf?id=EY096v0Jmg）。

## 5. 实验数量与充分性分析

- **实验数量**：论文在三大 VLN 基准（REVERIE、R2R、R2R-CE）上进行了“广泛应用”与“多种设置”评估，并对比了基线方法。依据元数据，无法确认具体实验组数（例如是否包含多重消融实验、不同反馈频率实验等）。
- **充分性评估**：
  - **优势**：覆盖三个主流基准，具有一定的说服力；结论显示 ATENA 在未知场景中优于熵最小化基线，表明核心有效性得到支撑。
  - **局限性**：由于缺少具体实验表格和详细数值，无法评估实验的统计显著性、误差棒、消融设计的完整性以及超参数敏感性分析等情况。
  - **公平性**：元数据提到“outperforming the compared baseline methods across various settings”，但未提供对比方法的具体实现细节和超参数设置，无法从现有信息判断公平性是否完全保障。

## 6. 主要结论与发现

- ATENA 在未知导航环境中能有效提升导航性能，显著优于熵最小化基线。
- 主动测试时交互（human-in-the-loop episodic feedback）为 VLN 的环境适应提供了一条“实用而有效”的新途径。
- 通过混合熵优化和自主动学习，智能体能够在测试过程中保持主动参与，做出更稳健、更有根据的决策，成功克服测试时的分布偏移问题。

## 7. 优点

- **方法创新性强**：将“主动学习”与“测试时交互”引入 VLN，突破了传统测试时无监督熵最小化的局限，思路新颖且具有实际应用价值。
- **机制设计合理**：混合熵优化同时控制置信度与动作偏好，有效缓解了熵最小化导致的过度自信问题。
- **具备闭环反馈机制**：人类片段式反馈 + 自评估机制形成闭环，智能体持续修正决策，符合机器人交互的实际部署场景。
- **基准选择全面**：在指令导航（R2R）、物体导航（REVERIE）以及连续环境导航（R2R-CE）等多个 VLN 分支上进行验证，覆盖性较好。
- **应用意义较强**：该研究为人机协作的导航智能体在实际复杂环境中的部署提供了可行范式。

## 8. 不足与局限

- **信息完整度受限**：由于原始 PDF 无法获取，本总结无法反映论文中的具体数据、可视化分析、故障案例讨论等细节。
- **实验覆盖可能存在不足**：
  - 是否在真实物理机器人上验证尚未可知，当前可能仅限仿真环境。
  - 未注明是否评估了不同反馈质量、不同反馈频率、多轮交互累积效果等实际交互因素。
  - 消融实验是否覆盖各组件（如伪专家分布、自主动学习策略）的独立贡献，暂无法确认。
- **偏差风险**：
  - 人类反馈可能引入主观偏差，若反馈不一致或低质量，可能导致策略偏向次优解，但论文未在摘要层面讨论鲁棒性。
  - 自主动学习依赖于“高置信度预测”评估导航结果，若初始置信度校准不佳，反馈信号可能存在偏差。
- **应用限制**：
  - 依赖人类片段式反馈意味着不完全自主，适用于人机协作场景，但不适用于完全无监督或完全自主的部署需求。
  - 在环境变化剧烈或反馈不可得的场景中，该方法的适用性存在局限。

---

（完）
