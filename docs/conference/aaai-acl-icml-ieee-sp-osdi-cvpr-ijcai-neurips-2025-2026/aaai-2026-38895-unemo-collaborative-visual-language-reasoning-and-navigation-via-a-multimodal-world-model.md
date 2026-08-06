---
title: "UNeMo: Collaborative Visual-Language Reasoning and Navigation via a Multimodal World Model"
title_zh: UNeMo：基于多模态世界模型的视觉-语言协同推理与导航
authors: "Changxin Huang, Lv Tang, Zhaohuan Zhan, Lisha Yu, Runhao Zeng, Zun Liu, Zhengjie Wang, Jianqiang Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38895/42857"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 联合优化视觉推理与导航策略的视觉语言导航框架
tldr: 论文针对现有基于大语言模型的视觉语言导航推理局限于语言模态、且推理模块与导航策略分离优化的问题，提出UNeMo框架。该框架通过多模态世界模型协同优化视觉状态推理与导航策略，使推理和行动目标一致。实验验证了联合优化能有效提升语言引导导航的成功率，为VLN中的多模态推理与策略对齐提供了新方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38895/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 868, \"height\": 366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38895/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1823, \"height\": 808, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38895/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1720, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38895/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1745, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38895/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1069, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38895/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 776, \"height\": 339, \"label\": \"Table\"}]"
motivation: 现有VLN方法用LLM做语言推理但缺乏视觉推理，且推理与策略优化目标冲突。
method: 通过多模态世界模型统一视觉状态推理与导航策略，实现端到端联合优化。
result: 实验表明UNeMo在多个VLN基准上显著提升导航成功率和路线准确率。
conclusion: 视觉-语言推理与策略的协同优化是提升具身导航性能的有效途径。
---

## Abstract
Vision-and-Language Navigation (VLN) requires agents to autonomously navigate complex environments via visual images and natural language instructions—remains highly challenging. Recent research on enhancing language-guided navigation reasoning using pre-trained large language models (LLMs) has shown promising prospects. However, the reasoning of such methods is limited to the linguistic modality, lacking visual reasoning capabilities. Moreover, existing reasoning modules are optimized separately from navigation policies, leading to incompatibility and potential conflicts in optimization objectives.  To tackle these challenges, we introduce UNeMo, a novel framework designed for the collaborative optimization of visual state reasoning and navigational decision-making. It introduces a Multimodal World Model (MWM) that takes visual features, language instructions, and navigational actions as inputs to jointly predict subsequent visual states, enabling cross-modal reasoning. Via a Hierarchical Prediction-Feedback (HPN) mechanism, MWM collaborates with navigation policies: the first layer generates actions using current vision-and-language features; MWM then infers post-action visual states to guide the second layer’s fine-grained decisions. This forms a dynamic bidirectional promotion mechanism where MWM reasoning optimizes navigation policies, while policy decisions feedback to improve MWM’s reasoning accuracy. Experiments on R2R and REVERIE datasets show UNeMo outperforms state-of-the-art methods by 2.1% and 0.7% in navigation accuracy for unseen scenes, validating its effectiveness.

---

## 论文详细总结（自动生成）

# UNeMo：基于多模态世界模型的视觉-语言协同推理与导航

## 1. 核心问题与整体含义

视觉-语言导航（Vision-and-Language Navigation, VLN）要求智能体依据视觉观察和自然语言指令在未知环境中自主导航。现有基于大语言模型（LLM）的方法存在两个关键缺陷：
- **推理模态受限**：推理过程局限于语言模态，缺乏视觉状态推理能力，无法对环境的动态变化进行预判。
- **优化目标脱节**：推理模块与导航策略分离训练，导致两者优化目标不兼容，甚至互相冲突，限制了整体导航性能。

论文提出 **UNeMo** 框架，通过引入多模态世界模型（Multimodal World Model, MWM）将视觉状态推理与导航决策统一到协作优化框架中，实现“推理指导行动，行动反馈推理”的双向促进机制，为 VLN 中的多模态协同推理与策略对齐提供了新思路。

## 2. 方法论

### 核心思想
UNeMo 基于 NavGPT2 构建，在 LLM 编码的视觉/语言特征之上，增加一个**多模态世界模型**来预测执行动作后的未来视觉状态，并通过**层级预测-反馈导航器（HPFN）** 将该预测状态注入导航策略，实现联合优化。

### 多模态世界模型（MWM）
- 采用条件变分自编码器（CVAE）架构，输入为当前节点局部视图特征、语言指令特征和导航动作，输出下一时刻的视觉状态嵌入。
- 具体流程：
  1. 导航策略先选出得分最高的候选节点 \( j \)。
  2. 该节点的局部视图嵌入 \( E_{o_j} \) 与指令特征 \( F_x \) 经多层交叉注意力融合（式 4），得到跨模态嵌入。
  3. 通过两个 MLP 估计未来状态的分布参数（均值 \( \mu \) 和方差 \( \sigma^2 \)）。
  4. 重参数化采样潜变量 \( z \)，与节点 \( j \) 的固有嵌入拼接后由 MLP 解码出预测的未来视觉状态 \( \hat{S}_{t+1}^{o} \)（式 5）。

### 层级预测-反馈导航器（HPFN）
- **第一层（粗粒度）**：基于当前拓扑图节点嵌入 \( V_t \) 预测初步动作 \( a'_t \)。
- **MWM 预测**：对初步动作指向的节点进行未来视觉状态推理。
- **第二层（细粒度）**：通过交叉注意力将预测状态 \( \hat{S}_{t+1}^{o} \) 与节点嵌入融合（式 6），更新后的节点嵌入经策略网络输出最终动作 \( a''_t \)（式 7）。
- 训练损失沿用 NavGPT2 的**行为克隆 + DAgger** 组合（式 3），但增加了对层级动作的双向监督。

## 3. 实验设计

### 数据集与基准
- **R2R（Room-to-Room）**：路径指令跟随任务，指令平均 32 词，需逐步导航。
- **REVERIE**：高层级目标导向导航任务，指令平均 21 词，需同时定位远端目标物体。
- 评估指标：SR（成功率）、SPL（路径加权成功率）、TL、NE、OSR，以及 REVERIE 的 RGS 和 RGSPL。

### 对比方法
- **R2R**：NavCoT、LangNav、NaviLLM、NavGPT2（1.5B/5B）等 LLM 导航方法。
- **REVERIE**：RecBERT、AirBert、HAMT、DUET（含复现版本 DUET*）。
- 同时验证 UNeMo 可适配不同基础策略（NavGPT2 和 DUET）。

### 消融实验
- **状态推理方法对比**：拓扑图状态（TopoState）、视觉条件解码（Cond2Vis）、视觉世界模型（Vis-WM）、完整 UNeMo。
- **HPFN 策略消融**：仅 MWM 辅助训练、仅第一层动作 \( a' \)、仅第二层动作 \( a'' \)、联合 \( a' \) 与 \( a'' \)。

## 4. 资源与算力

文中明确说明：
- 实验运行于 **Ubuntu 22.04，单张 NVIDIA RTX 4090 GPU**。
- UNeMo 使用 **FlanT5-1.5B** 作为 LLM 骨干（为 NavGPT2 的 30% 参数量），显存占用约 **12GB**，远低于 NavGPT2-5B 的 27GB。
- **未报告具体训练时长**，也未提及 batch size、训练轮数等超参数细节。

## 5. 实验数量与充分性

- **主实验**：R2R 的 val-unseen 和 test-unseen 两个划分；REVERIE 的 val-unseen 和 test-unseen 两个划分，共 4 组结果。
- **消融实验**：两组，分别讨论状态推理方法（4 种变体）和 HPFN 内部策略（4 种变体），共 7 组额外实验。
- **充分性评估**：
  - 优点：覆盖了两种场景、多类基线、不同 LLM 规模，并对关键模块进行了细致消融，结论整体客观。
  - 不足：缺少与更多最新方法的系统对比（如 DUET 原始结果在部分指标上优于 UNeMo 的 SPL）；未提供误差分析或失败案例；未在不同随机种子下报告方差，难以判断显著性。

## 6. 主要结论与发现

- UNeMo 在 R2R val-unseen 上 SR/SPL 相对 NavGPT2-1.5B 提升 **2.1%**；在更难的 test-unseen 上提升 1.5%/1.3%。
- 在 REVERIE test-unseen 上 SR 相对 DUET 提升 **0.7%**，远程定位指标 RGS 也略有优势。
- **长路径导航提升更显著**：R2R val-seen 中，长路径 SR 从 64.2% 提升至 69.8%（+5.6%），短路径仅 +1.2%，说明未来状态推理对复杂长程导航帮助更大。
- **高效性**：用 1.5B 参数模型即可超越 5B 模型，显存节省超过一半。
- 消融验证了 MWM 和 HPFN 的必要性，其中仅使用第二层动作监督（\( a'' \)）效果最佳。

## 7. 优点

- **创新性**：首次将 CVAE 形式的“世界模型”引入 LLM 导航框架，使语言引导的导航具备视觉前瞻能力。
- **协作优化设计**：通过 HPFN 将世界模型与导航策略纳入同一优化闭环，解决了传统方法中推理与决策目标冲突的问题。
- **即插即用**：作为通用框架可适配不同基础导航策略（NavGPT2、DUET），且仅在微调阶段引入，便于复用预训练模型。
- **实用性强**：在保持高性能的同时大幅降低计算资源需求，有利于实际部署。
- **实验较扎实**：在两种 benchmark、多个划分、多种消融下验证了方法有效性，并特别分析了长路径场景。

## 8. 不足与局限

- **路径效率代价**：在 REVERIE 上 SPL/RGSPL 相比 DUET 略有下降，说明额外的前瞻推理增加了探索行为，牺牲了路径最优性。
- **依赖基础模型**：强依赖 NavGPT2 的拓扑编码和 LLM 蒸馏特征，若基础策略改变，框架的适配成本未充分分析。
- **基准覆盖有限**：仅在 R2R 和 REVERIE 两个数据集上验证，未涉及更连续化的 VLN-CE 或真实机器人环境。
- **缺乏部署验证**：论文提及未来将部署到物理机器人，目前仍限于仿真环境。
- **训练细节缺失**：未给出训练时长、随机种子、超参数敏感性等，复现难度较大。
- **对比公平性**：与 DUET 对比时并未使用相同的基础特征提取设置（DUET 用传统预训练，UNeMo 用 LLM 蒸馏），可能引入额外变量。

（完）
