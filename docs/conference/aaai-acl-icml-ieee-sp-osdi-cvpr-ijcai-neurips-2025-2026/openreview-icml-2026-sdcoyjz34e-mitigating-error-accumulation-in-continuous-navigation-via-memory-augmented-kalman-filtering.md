---
title: Mitigating Error Accumulation in Continuous Navigation via Memory-Augmented Kalman Filtering
title_zh: 通过记忆增强卡尔曼滤波缓解连续导航中的误差累积
authors: "Yin Tang, Jiawei Ma, Jinrui Zhang, Alex Jinpeng Wang, Deyu Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/711857fd38004509b173ac1ca4148cf32ab031d1.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 基于记忆增强卡尔曼滤波的连续视觉语言导航误差累积抑制
tldr: 连续视觉语言导航通常采用递推航位推算方式逐步预测路径，导致位置误差随时间累积和状态漂移。本文借鉴经典控制理论，将连续预测建模为递归贝叶斯状态估计问题，并提出记忆增强的卡尔曼滤波来修正累积误差。该方法能缓解内部信念与客观坐标的错位，提高后续轨迹预测的准确性。针对无人机等连续导航场景，该机制显著降低了轨迹漂移并保持实时性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 连续视觉语言导航中的航位推算会逐步累积位置误差，导致状态漂移。
method: 将连续预测建模为递归贝叶斯状态估计，并引入记忆增强的卡尔曼滤波进行误差修正。
result: 有效抑制轨迹预测中的误差累积，提升连续导航定位一致性。
conclusion: 控制理论启发的状态估计方法可为连续VLN提供鲁棒的误差修正机制。
---

## Abstract
Continuous prediction in complex environments is critical for Unmanned Aerial Vehicle (UAV). However, the existing Vision-Language Navigation (VLN) models follows the dead-reckoning, which iteratively predicts the next waypoint and updates its position, thereby constructing the complete trajectory. Then, such stepwise manner will inevitably lead to accumulated errors of position over time, resulting in misalignment between internal belief and objective coordinates, which is known as ``state drift'' and ultimately compromises the subsequent trajectory prediction. Drawing inspiration from classical control theory, we propose to correct for errors by formulating the continuous prediction as a recursive Bayesian state estimation problem. In this paper, we design NeuroKalman, a novel framework that decouples navigation into two complementary processes: a Prior Prediction, based on motion dynamic,s and a Likelihood Correction, from historical observation. We first mathematically associate Kernel Density Estimation of the measurement likelihood with the attention-based retrieval mechanism, which then allows the system to rectify the latent representation using retrieved historical anchors without gradient updates. Comprehensive experiments on TravelUAV benchmark demonstrate that, with only 10\% of the full training data fine-tuning, our method clearly outperforms strong baselines and regulates drift accumulation.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：连续视觉语言导航（Continuous Vision-Language Navigation, VLN）对无人机（UAV）在复杂环境中的自主飞行至关重要。现有VLN模型通常采用**航位推算（Dead-reckoning）**方式：模型逐步预测下一个航点并据此更新自身位置，逐步拼接出完整轨迹。
- **核心问题**：这种逐步递推的方式不可避免地导致**位置误差随时间累积**，使得模型内部的信念状态与客观世界坐标产生错位，即“**状态漂移（State Drift）**”。状态漂移会进一步损害后续轨迹预测的准确性，形成恶性循环。
- **整体意义**：论文从**经典控制理论**中寻求解决方案，将连续导航中的误差修正建模为**递归贝叶斯状态估计问题**，旨在从方法论层面系统性抑制误差累积，提升无人机长程连续导航的鲁棒性与一致性。

## 2. 论文提出的方法论：核心思想与技术细节

- **核心思想**：借鉴卡尔曼滤波（Kalman Filtering）中“先验预测 + 观测修正”的闭环框架，将导航过程解耦为两个互补环节：
  1. **先验预测（Prior Prediction）**：基于运动动力学（Motion Dynamics）模型，预测下一时刻的状态（如位置、速度）。
  2. **似然修正（Likelihood Correction）**：基于历史观测（Historical Observation），对先验预测结果进行修正，校准累积误差。
- **技术细节**：
  - 将**测量似然（Measurement Likelihood）的核密度估计（Kernel Density Estimation, KDE）**与**基于注意力的检索机制（Attention-based Retrieval Mechanism）**进行数学关联。
  - 通过这种关联，系统无需任何梯度更新，即可利用从历史数据中检索到的“锚点（Anchors）”来修正当前的潜在状态表示。
  - 这种设计使得误差修正过程轻量化、可即时执行，并保持导航任务的实时性。
- **算法流程（文字描述）**：
  1. 利用运动动力学模型给出状态先验估计；
  2. 通过注意力机制检索历史观测中相似的“锚点”状态；
  3. 用KDE对当前观测似然进行估计，并将检索结果转化为修正量；
  4. 将先验与修正结合，输出校准后的状态估计，用于下一步轨迹预测。

## 3. 实验设计：数据集、基准与对比方法

- **数据集/Benchmark**：论文使用了**TravelUAV**基准，这是一个面向无人机连续视觉语言导航的专用大规模评测平台，包含多种真实复杂环境与导航指令。
- **训练策略**：论文采用了一种极具挑战性的设置——仅使用**完整训练数据的 10%** 进行微调（fine-tuning），在此低数据条件下检验模型性能。
- **对比方法**：与多个**强基线（Strong Baselines）** 进行了对比。论文摘要中提到“clearly outperforms strong baselines”，但具体基线方法名称（如经典的VLN模型、现有连续导航方法等）在摘要中未逐一列出，详细列表需查阅论文正文。
- **评测指标**：主要围绕**轨迹漂移抑制（Drift Accumulation Regulating）** 与**导航定位一致性（Position Consistency）** 等指标进行评估。

## 4. 资源与算力

- **论文未在摘要和元数据中明确说明**训练所用的具体 GPU 型号、GPU 数量、训练总时长或 FLOPs 等算力信息。
- 根据论文只使用 10% 数据微调的描述，可以推断其训练开销可能相对较低，且方法本身强调实时性（保持实时导航能力），但具体的硬件资源细节需要查阅**论文全文的实验设置或补充材料**才能获知。

## 5. 实验数量与充分性

- **实验组数**：论文在摘要层面主要呈现了在 TravelUAV 基准上的核心对比实验，以及“10%数据微调”这一关键设置下的性能表现。元数据“evidence”和“result”均指向单一的基准验证。
- **是否充分**：
  - **客观性**：TravelUAV 是公认的无人机 VLN 基准，使用该基准验证具有一定客观性与可比性。
  - **充分性评估**：仅凭摘要信息，论文未明确展示以下内容：
    - 多数据集交叉验证（如室内导航、仿真环境等）；
    - 详细的消融实验（如分别验证 KDE 与注意力检索的贡献、不同历史锚点数量影响等）；
    - 不同数据量（如 1%、5%、50%、100%）的敏感度分析。
  - **总体判断**：核心结论有基准数据支撑，但实验维度的开放性信息不足，全面充分的验证需要依赖论文全文的消融与扩展实验。

## 6. 论文的主要结论与发现

- 将连续 VLN 建模为递归贝叶斯状态估计、并用记忆增强的卡尔曼滤波进行误差修正，能够**有效抑制轨迹预测中的误差累积**。
- 在 TravelUAV 基准上，所提出的方法在**仅使用 10% 训练数据微调**的条件下，**明显优于强基线模型**，并能够有效调控漂移累积。
- 结论表明，**控制理论启发的状态估计机制**可为连续视觉语言导航提供一种鲁棒、高效的误差修正范式，兼具性能优势与实时性。

## 7. 优点：方法与实验设计的亮点

- **理论创新性强**：将经典控制理论（卡尔曼滤波）引入连续 VLN，与现有纯深度学习航位推算方法形成鲜明差异，开辟了交叉学科解决导航漂移问题的新思路。
- **方法设计优雅**：将 KDE 与注意力检索机制进行数学关联，实现了**无需梯度更新的误差修正**，计算开销低，有利于实时部署。
- **低数据依赖优势突出**：仅用 10% 训练数据微调即可超越强基线，说明方法对数据效率有显著增益，尤其适合数据采集困难的真实无人机场景。
- **问题定位精准**：正视了连续 VLN 中“状态漂移”这一核心痛点，而非仅停留在算法层面的叠加优化。

## 8. 不足与局限

- **实验信息可见性有限**：摘要中未列出具体对比方法名称、完整消融实验、更多数据集的泛化验证，导致实验充分性的外部评估存在局限。
- **算力资源未披露**：论文未提供训练资源成本（GPU型号/数量/时长），若后续可补充模型效率的量化指标，将更有说服力。
- **潜在偏差风险**：
  - 只报告了 10% 数据微调下的结果，若 100% 数据下优势缩小，则需如实报告以避免高数据量场景下的误导性结论；
  - 检索式历史锚点机制可能受历史数据分布偏差影响，在分布外环境中的泛化能力有待验证。
- **应用限制**：
  - 方法依赖历史观测的有效检索，在无先验地图或极少历史数据的陌生环境中，记忆增强机制可能面临冷启动问题；
  - 框架设计主要针对无人机连续导航场景，迁移到足式机器人或地面车辆等不同动力学模型时，需要重新适配运动动力学先验。

（完）
