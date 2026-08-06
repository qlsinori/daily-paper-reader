---
title: "MonoDream: Monocular Vision-Language Navigation with Panoramic Dreaming"
title_zh: MonoDream：基于全景梦境的单目视觉语言导航
authors: "Shuo Wang, Yongcai Wang, Zhaoxin Fan, Yucheng Wang, Maiyue Chen, Kaihui Wang, Zhizhong Su, Wanting Li, Xudong Cai, Yeying Jin, Deying Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37974/41936"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 单目视觉语言导航；统一导航表示；全景梦境
tldr: 针对视觉语言导航中全景RGB-D传感器成本高、单目模型性能不足的问题，提出轻量级VLA框架MonoDream。该方法通过全景梦境学习统一导航表示，联合对齐导航相关视觉语义与语言化动作意图，使单目智能体获得接近全景输入的导航性能。实验表明其在动作预测可靠性上取得显著提升，为低成本VLN部署提供了可行方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37974/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1797, \"height\": 758, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37974/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1491, \"height\": 905, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1835, \"height\": 849, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 850, \"height\": 385, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 769, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 783, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 584, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37974/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 831, \"height\": 213, \"label\": \"Table\"}]"
motivation: 全景RGB-D传感器成本高，现有单目VLA导航模型性能仍落后于全景方法。
method: 基于全景梦境模块，使单目智能体学习统一导航表示，对齐视觉语义与语言动作意图。
result: 在动作预测可靠性上明显改善，缩小了与全景RGB-D方法的差距。
conclusion: 统一导航表示和梦境机制可有效提升单目视觉语言导航性能。
---

## Abstract
Vision-Language Navigation (VLN) tasks often leverage panoramic RGB and depth inputs to provide rich spatial cues for action planning, but these sensors can be costly or less accessible in real-world deployments. Recent approaches based on Vision-Language Action (VLA) models achieve strong results with monocular input, yet they still lag behind methods using panoramic RGB-D information. We present MonoDream, a lightweight VLA framework that enables monocular agents to learn a Unified Navigation Representation (UNR). This shared feature representation jointly aligns navigation-relevant visual semantics (e.g., global layout, depth, and future cues) and language-grounded action intent, enabling more reliable action prediction. MonoDream further introduces Latent Panoramic Dreaming (LPD) tasks to supervise the UNR, which train the model to predict latent features of panoramic RGB and depth observations at both current and future steps based on only monocular input. Experiments on multiple VLN benchmarks show that MonoDream consistently improves monocular navigation performance and significantly narrows the gap with panoramic-based agents.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：视觉语言导航（VLN）任务要求智能体在真实 3D 环境中，依据自然语言指令导航到目标位置。现有高性能方法通常依赖全景 RGB-D 传感器（全景相机+深度传感器），以获得全局视野和显式几何信息，从而取得较高导航成功率（如 R2R-CE 上的 SR 可达 59%）。
- **核心问题**：全景相机和深度传感器在实际部署中带来**成本高、功耗大、重量增加、硬件集成复杂**等问题，限制了落地应用。虽然近年出现基于单目 RGB 相机的 VLA 模型，但其导航性能仍显著落后于使用全景 RGB-D 的方法。
- **根本挑战**：单目智能体的**视野狭窄**（仅前向视图），难以推断**全局空间布局**、**几何结构**和**未来场景动态**。例如，智能体在走廊中无法感知视线之外的侧门或楼梯，导致无法建立连贯的全局环境模型，也难以进行多步前瞻规划。
- **本文含义**：受神经科学启发（人脑可从局部视图推理全景场景、并基于意图内部模拟未来场景），论文提出 MonoDream，使单目智能体具备"想象"（Dreaming）能力，从有限的单目观测中推断并补全当前与未来的全景语义和几何信息，从而**显著缩小单目与全景 RGB-D 方法之间的性能差距**。

---

## 2. 方法论：核心思想、关键技术细节与公式

### 2.1 核心思想

MonoDream 是一个轻量级 VLA（Vision-Language-Action）框架，核心思想是让单目智能体学习一个**统一导航表示（UNR, Unified Navigation Representation）**——一个共享的潜空间，同时对齐以下信息：

- 隐式**动作意图**（语言化的导航行为）；
- **全景场景布局**（当前步骤的全景 RGB 特征）；
- **深度感知**（全景深度特征）；
- **未来动态**（未来步骤的全景 RGB-D 特征）。

该 UNR 可被解码为导航动作、指令文本，或直接作为导航相关特征使用。

### 2.2 关键技术细节

**（1）输入编码：**

- 语言指令 \(I\) 经文本编码器 \(\Phi_{text}\) 得到文本特征 \(E_{text} \in \mathbb{R}^{L \times d}\)；
- 视觉输入包含当前观测 \(o_t\) 和从历史观测中均匀采样 \(N=8\) 帧组成的 \(O_t = \{o_{p_0},...,o_{p_{N-1}}\}\)，各帧经视觉编码器 \(\Phi_{vis}\) 得到视觉特征 \(E_{vis}\)；
- 二者拼接为输入序列 \(S_t = [E_{text}, E_{vis}]\)，送入 LLM 骨干网络，输出隐藏状态 \(h_t\)，即为 **UNR**。

**（2）Latent Panoramic Dreaming（LPD）任务：**

LPD 是一组辅助监督任务，仅在训练阶段使用。其目标为：

- **当前步**：用 UNR \(h_t\) 预测当前步骤的全景 RGB 潜特征（\(H_t^{PI}\)）和全景深度潜特征（\(H_t^{PD}\)）；
- **未来步**：预测下一步的全景 RGB 潜特征（\(H_{t+1}^{PI}\)）和全景深度潜特征（\(H_{t+1}^{PD}\)）。

LPD 的损失函数为**均方误差（MSE）**：

\[
L_{Fea}^t(\theta) = \sum_{m \in M} \| h_t - H_t^m \|^2 + \sum_{m \in M} \| h_t - H_{t+1}^m \|^2
\]

其中 \(M = \{PI, PD\}\)。

监督信号由**共享权重的视觉编码器**（与单目输入编码器 \(\Phi_{vis}\) 相同）编码全景 RGB-D 获得，确保监督特征与 UNR 处于同一特征空间。

**（3）动作预测任务：**

模型基于 \(h_t\) 以自然语言形式预测接下来 3 个动作 \((a_t, a_{t+1}, a_{t+2})\)，损失为交叉熵：

\[
L_{Act}^t(\theta) = -\sum_{k=0}^{K} \log \pi_\theta(a_{t+k}^* | h_t)
\]

其中 \(K=3\)。

**（4）指令推理任务（Instruction Reasoning, IR）：**

在轨迹末端，基于 UNR \(h_T\) 用文本解码器重生成原始指令，损失为：

\[
L_{Ins}^\tau(\theta) = -\log \pi_\theta(I_\tau | h_T)
\]

**（5）总训练目标：**

\[
L = \sum_{\tau \in D} \left( \sum_{t}^{T_\tau} (L_{Act}^t(\theta) + \lambda L_{Fea}^t(\theta)) + L_{Ins}^\tau(\theta) \right)
\]

其中 \(D\) 为训练轨迹集合，\(\lambda\) 为 LPD 损失的权重超参数。

**（6）推理阶段：**

仅需单目 RGB 输入即可导航，LPD 模块全部关闭，不引入额外推理开销。

---

## 3. 实验设计

### 3.1 数据集与场景

- **数据集**：VLN-CE（连续环境视觉语言导航）基准下的 **R2R-CE** 和 **RxR-CE**；
- **训练数据**（均来自仿真环境）：
  - R2R-CE 训练划分：320K 步样本；
  - RxR-CE 训练划分：600K 步样本；
  - DAgger 策略收集的非 oracle 轨迹数据：500K 步样本；
  - 合计约 140 万步样本，**不使用任何外部数据**。
- **测试集**：R2R-CE Val-Unseen 与 RxR-CE Val-Unseen。

### 3.2 对比方法

- **全景 RGB-D 方法**（不依赖 LLM）：BEVBert、ETPNav、NP-ETPNav、Seq2Seq、CMA、LAW、CM2、WS-MGMap、sim2real、NavMorph；
- **单目 RGB 的 VLA 方法**：NaVid、Uni-NaVid、NaVILA、Aux-Think、NaVid-4D。

### 3.3 评估指标

- SR（成功率）、OSR（oracle 成功率）、SPL（按路径长度加权的成功率）、NE（导航误差）。

---

## 4. 资源与算力

- **GPU 型号与数量**：8 张 NVIDIA H20 GPU；
- **训练轮数**：5 epochs；
- **学习率**：1e-5，warm-up 比例 0.03；
- **Batch size**：80；
- **模型规模**：以 NVILA-lite-2B 为基础模型（约 2B 参数）。

---

## 5. 实验数量与充分性

### 5.1 实验组数

论文共包含 **4 大类实验**：

1. **主实验**：R2R-CE 与 RxR-CE 的 Val-Unseen 测试（表 1、表 2）；
2. **跨数据集评估**：仅在 R2R-CE 上训练，直接评测 RxR-CE Val-Unseen（表 3）；
3. **消融实验**（3 组）：
   - 辅助任务消融（IR 与 LPD 的有无，表 4）；
   - LPD 四个子任务消融（PI、PD、FPI、FPD，表 5）；
   - LPD 未来预测步数消融（1/2/3 步，表 6）；
4. **效率对比**：模型参数量与推理时间对比（表 7）。

### 5.2 充分性评估

**优点**：
- 消融实验设计较为系统，分别验证了每个 LPD 子任务的独立贡献；
- 跨数据集实验验证了泛化能力；
- 与主流方法在同设置下对比，对比基准较全面。

**不足之处**：
- 未在真实机器人平台上进行验证；
- 消融实验仅在 R2R-CE 上进行，未在 RxR-CE 上验证消融结论的普适性；
- 未报告多轮随机种子下的方差或显著性检验，无法判断性能提升的统计显著性；
- 对比表中部分方法（如 NaVid-4D）使用深度输入，分组标记清晰但未在讨论中详细分析差距来源。

---

## 6. 主要结论与发现

1. **MonoDream 显著提升单目导航性能**：在 R2R-CE Val-Unseen 上，SR 达 55.8%、SPL 达 49.1%，超越所有单目方法（如 NaVILA SR 54.0%、Uni-NaVid SR 47.0%、Aux-Think SR 55.7%），且**不使用任何外部训练数据**。
2. **大幅缩小与全景 RGB-D 方法的差距**：MonoDream 的 SPL（49.1%）与最佳全景方法 BEVBert（50.0%）几乎持平，SR 与 ETPNav（57.0%）接近，验证了"潜空间全景想象"的有效性。
3. **LPD 是性能提升的关键**：消融实验表明，移除 LPD 后 SR 下降约 11 个百分点（从 46.1% 降至 35.1%），说明全景 RGB-D 潜特征监督对单目导航至关重要。
4. **未来一步预测最优**：预测未来 1 步的 LPD 最佳，预测 2/3 步反而导致性能下降（因长程预测的不确定性累积）。
5. **模型效率优势**：MonoDream 模型仅 2B 参数、每步推理 0.8s，相比 NaVILA（8B、1.2s）更轻量、更快。
6. **跨数据集泛化能力强**：在未见过的 RxR-CE 上，SR 达 25.1%、SPL 达 21.6%，优于所有单目基线。

---

## 7. 优点

- **方法创新性强**：首次将"全景梦境"（Latent Panoramic Dreaming）作为潜空间监督引入单目 VLN，受神经科学启发，思路新颖；
- **无需外部数据**：仅用仿真环境数据即可取得 SOTA，数据效率高；
- **推理无额外开销**：LPD 仅在训练阶段使用，推理时完全裁剪，不增加部署成本；
- **模型精简高效**：2B 参数、0.8s/步，较 8B 模型更利于实际部署；
- **统一表示设计合理**：UNR 同时对齐视觉语义（布局、深度、未来）与语言动作意图，多任务联合训练互相增益；
- **消融实验较完整**：验证了每个设计选择的有效性。

---

## 8. 不足与局限

- **训练对全景 RGB-D 的依赖**：LPD 训练时需要获取全景 RGB-D 标签，限制了其在无此类传感器标注的真实场景数据上的扩展性；
- **未来预测视野有限**：仅预测未来 1 步，长时序规划能力受限；
- **缺少显式历史全景重建**：作者在 Limitations 中承认，模型未显式重建全景历史，仅依赖当前与下一步预测，引入记忆机制或可进一步提升；
- **未做真实世界验证**：所有实验均在仿真环境中完成，缺乏 Sim-to-Real 的部署验证；
- **消融实验范围局限**：仅基于 R2R-CE 训练集，未在 RxR-CE 上验证消融结论；
- **统计严谨性不够**：未报告多次运行的均值与方差、未做显著性检验；
- **性能提升幅度有限**：与最佳全景方法相比仍有差距（如 R2R-CE 上 SR 仍低于 BEVBert 的 59.0%），"缩小差距"而非"超越"全景方法。

---

（完）
