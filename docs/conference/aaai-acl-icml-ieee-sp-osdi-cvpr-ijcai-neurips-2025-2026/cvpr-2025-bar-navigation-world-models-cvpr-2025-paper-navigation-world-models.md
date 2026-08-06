---
title: Navigation World Models
title_zh: 导航世界模型
authors: "Bar, Amir, Zhou, Gaoyue, Tran, Danny, Darrell, Trevor, LeCun, Yann"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Bar_Navigation_World_Models_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 通过视频生成进行轨迹规划的导航世界模型
tldr: 导航是具身智能体的基础技能。本文提出导航世界模型（NWM），一种可控视频生成模型，基于过去观察与导航动作预测未来视觉观察。模型采用条件扩散Transformer，在人类与机器人的大规模第一视角视频上训练至10亿参数规模。在熟悉环境中，NWM可通过模拟未来轨迹并评估是否达成目标来直接规划路径，还能在规划中灵活融入各种约束。实验表明其能从零开始规划有效轨迹，展现出超越固定策略的泛化能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 1110, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 645, \"height\": 1047, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 876, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1812, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 848, \"height\": 640, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1803, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1798, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 858, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 863, \"height\": 302, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 878, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 683, \"height\": 108, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 730, \"height\": 233, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1662, \"height\": 165, \"label\": \"Table\"}]"
motivation: 现有监督导航策略行为固定，难以灵活利用环境动力学进行规划。
method: 训练条件扩散Transformer作为世界模型，基于历史观测与动作生成未来视频，并用模拟轨迹评估规划。
result: 在熟悉环境中可从零规划有效导航轨迹，并动态融入目标约束，验证了视频生成用于规划的可行性。
conclusion: 可控视频生成可作为一种通用导航规划器，为具身智能体提供新的决策范式。
---

## Abstract
Navigation is a fundamental skill of agents with visual-motor capabilities. We introduce a Navigation World Model (NWM), a controllable video generation model that predicts future visual observations based on past observations and navigation actions. To capture complex environment dynamics, NWM employs a Conditional Diffusion Transformer (CDiT), trained on a diverse collection of egocentric videos of both human and robotic agents, and scaled up to 1 billion parameters. In familiar environments, NWM can plan navigation trajectories by simulating them and evaluating whether they achieve the desired goal. Unlike supervised navigation policies with fixed behavior, NWM can dynamically incorporate constraints during planning. Experiments demonstrate its effectiveness in planning trajectories from scratch or by ranking trajectories sampled from an external policy. Furthermore, NWM leverages its learned visual priors to imagine trajectories in unfamiliar environments from a single input image, making it a flexible and powerful tool for next-generation navigation systems.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前的视觉导航策略（如 GNM、NoMaD）通常以监督方式训练，行为是“硬编码”的，训练完成后很难动态引入新的约束（如“禁止左转”“禁止进入危险区域”），也无法根据问题难度灵活分配计算资源。作者希望设计一种新型模型，能够克服这些限制，实现更灵活、可扩展的导航规划。
- **整体含义**：论文提出将“世界模型”（World Model）的思想引入视觉导航任务——即通过学习环境动力学，使智能体能够在“想象”中模拟未来的视觉观测，并据此规划行动。这与人类规划时常在脑海中预演未来轨迹的认知方式相契合。
- **核心主张**：可控视频生成可以作为一种通用的导航规划器，为具身智能体提供一种新的决策范式——从“学习固定策略”转向“学习环境模拟器 + 规划算法”的组合。

## 2. 论文提出的方法论

### 2.1 核心思想

- 训练一个**可控视频生成模型**（Navigation World Model, NWM），以过去（若干帧）观测和导航动作作为条件，自回归地预测未来帧。
- 训练完成后，NWM 不仅可用于视频预测，还可用于**规划**：通过模拟多条候选轨迹并评估其到达目标的可能性，选择最优轨迹。

### 2.2 公式化表述

- 给定第一视角视频数据集 `D = {(x_0, a_0, ..., x_T, a_T)}`，其中 `x_i` 为图像，`a_i = (u, ω)` 为导航动作（`u` 控制平移，`ω` 控制偏航角旋转）。
- 世界模型 `F_θ` 定义为随机映射：`s_{t+1} ~ F_θ(s_{t+1} | s_t, a_t)`，其中 `s_t = enc_φ(x_t)` 是预训练 VAE 编码的潜表示。
- 论文引入**时间偏移（time shift）** 输入 `k`，使动作表示为 `a_t = (u, ω, k)`，其中 `k` 控制预测未来（或过去）多少步。相应的导航动作可从时间 t 到 m=t+k-1 累加近似。
- 为了鼓励动作与时间的**解耦**（避免模型只依赖时间而忽略动作，或反之），训练时为每个状态采样多个（最多 4 个）目标状态。

### 2.3 Conditional Diffusion Transformer (CDiT)

- 采用扩散 Transformer 架构，但提出一种高效的 **CDiT 块**，其关键设计是：
  - 第一个注意力块仅对**目标帧（被去噪的帧）** 的 token 进行自注意力；
  - 通过**交叉注意力层**，使当前帧的每个 query token 关注**过去帧**的 tokens（作为 key/value）；
  - 整体计算复杂度为 `O(mn²d)`，**与上下文帧数 m 呈线性关系**；相比之下，标准 DiT 的复杂度为 `O(m²n²d)`，与上下文长度呈二次关系。

- **条件嵌入**：将导航动作 `a`、时间偏移 `k`、扩散时间步 `t` 分别通过正弦-余弦特征提取和 MLP 映射为嵌入向量，三者求和后送入 AdaLN 层生成调制系数。
- **扩散训练**：使用标准去噪扩散目标（`L_simple`），并附加变分下界损失；噪声调度遵循 DiT 的设置。
- **无标签数据**：训练无标签数据（如 Ego4D）时，省略显式动作条件即可。

### 2.4 规划方法

- **能量函数**：定义 `E(s_0, a_0, ..., a_{T-1}, s_T) = -S(s_T, s_g) + ΣI(a_t ∉ A_valid) + ΣI(s_t ∉ S_safe)`。
  - `S(s_T, s_g)` 表示最终预测状态与目标图像的感知相似度（用 LPIPS 计算）；
  - 约束可以通过有效动作集合 `A_valid` 和安全状态集合 `S_safe` 灵活编码。
- **优化**：使用**交叉熵方法（CEM）** 进行模型预测控制（MPC），是一种无导数的基于种群的优化方法。
- **轨迹排序**：当存在外部导航策略（如 NoMaD）时，可从中采样多条轨迹，用 NWM 逐条模拟，选择能量最低（即最接近目标）的轨迹执行。

## 3. 实验设计

### 3.1 数据集

| 数据集 | 用途 | 说明 |
|--------|------|------|
| SCAND | 已知环境训练/评估 | 社会合规导航，多样环境 |
| TartanDrive | 已知环境训练/评估 | 越野驾驶 |
| RECON | 已知环境训练/评估 | 开放世界导航 |
| HuRoN | 已知环境训练/评估 | 社交交互导航 |
| Ego4D | 额外无标签预训练 | 人类第一视角视频，仅使用时间偏移动作 |
| GO Stanford | 未知环境评估 | 仅作测试，模型未见过的环境 |

- 所有机器人数据集带有位置/旋转信息，可推断相对动作；对不同智能体的步长做了标准化处理。

### 3.2 评估指标

- **轨迹准确性**：ATE（绝对轨迹误差）、RPE（相对位姿误差）
- **感知相似度**：LPIPS、DreamSim
- **像素质量**：PSNR
- **生成分布质量**：FID、FVD

### 3.3 对比方法

- **DIAMOND**：基于 UNet 的扩散世界模型（离线强化学习设定）
- **GNM**：通用目标条件导航策略（全连接轨迹预测网络）
- **NoMaD**：基于扩散策略的导航模型（GNM 的扩展）
- **标准 DiT**：自注意力覆盖所有上下文 tokens 的扩散 Transformer

### 3.4 主要实验场景

1. **消融实验**（RECON 上 4 秒未来预测）：模型规模 vs. 计算量、目标数量（1/2/4）、上下文长度（1/2/4）、时间与动作条件的贡献。
2. **视频预测与生成**：在 RECON 上预测 1–16 秒未来帧，比较 FID/LPIPS 随时间的衰减；生成 16 秒视频并比较 FVD。
3. **独立规划**：在 RECON 上评估目标条件导航，轨迹长度 8，时间偏移 k=0.25。
4. **带约束规划**：施加三种动作约束（先前进后转向、先左/右转后前进、直线后前进），衡量与无约束基线的位置/偏航差异。
5. **轨迹排序**：采样 NoMaD 的 16/32 条轨迹，用 NWM 排序，评估 ATE/RPE 提升。
6. **未知环境泛化**：在 GO Stanford 上评估加入 Ego4D 无标签数据前后的视频预测性能。

## 4. 资源与算力

- 论文明确指出：**XL 规模模型在 8 台 H100 机器上训练，每台 8 张 GPU（共 64 张 H100）**。
- 默认配置为 CDiT-XL（1B 参数）、上下文 4 帧、总 batch size 1024（配合 4 个目标，等效 batch 4096）、使用 AdamW 优化器（学习率 8e-5）。
- 论文**未明确说明**具体训练时长（如多少天/多少步），也未给出总 FLOPs 的绝对数值，仅对比了 CDiT vs. DiT 的相对 FLOPs（CDiT 节省 2–4 倍）。

## 5. 实验数量与充分性

- **实验组数**：论文包含 6 大类实验（消融、视频预测/生成、独立规划、约束规划、轨迹排序、未知环境泛化），子实验较多。消融覆盖了模型结构（CDiT vs. DiT）、规模（Small/Base/Large/XL）、目标数、上下文长度、时间/动作条件五组变量；对比基线包括 DIAMOND、GNM、NoMaD 三个代表性方法。
- **充分性评价**：
  - **积极方面**：实验层次清晰，从预测质量到规划性能再到泛化能力，形成了较完整的证据链；同时报告了多次采样的均值和标准差，具有统计规范性。
  - **不足方面**：
    - 规划实验仅在 RECON 一个已知环境上报告 ATE/RPE 结果，缺乏多环境（如 SCAND、TartanDrive）的规划结果对比；
    - 约束规划实验仅报告了相对于无约束基线的偏移量，未与端到端策略在相同约束下的表现做对比；
    - 未知环境泛化实验只评估了视频预测质量，**没有评估在该环境中的实际规划性能**；
    - 与 GNM/NoMaD 的数据集分布存在交集（NoMaD 也使用部分相同数据集），可能存在基准偏差。

## 6. 论文的主要结论与发现

- **CDiT 架构高效且可扩展**：在最高 1B 参数规模下，CDiT 比标准 DiT 计算量少 2–4 倍，预测精度反而更好；更大的模型带来更好的性能。
- **多目标训练有益**：每个状态使用 4 个随机目标训练，显著提升预测质量（LPIPS 从 0.312 降到 0.296，PSNR 提升约 0.3）。
- **更长上下文有帮助**：从 1 帧增加到 4 帧上下文，预测准确度持续提升。
- **时间与动作条件缺一不可**：仅用时间条件性能严重退化（LPIPS 0.760），仅用动作条件也有小幅下降。
- **NWM 可作为独立规划器**：在 RECON 上，NWM 规划（ATE 1.13）大幅优于 GNM（1.87）和 NoMaD（1.93），达到 SOTA 水平。
- **NWM 可提升外部策略**：用 NWM 对 NoMaD 采样的 32 条轨迹排序，ATE 从 1.93 降至 1.78，RPE 从 0.52 降至 0.48。
- **约束规划可行**：NWM 能在施加动作约束时依然有效规划，性能损失相对较小。
- **无标签数据提升泛化**：加入 Ego4D 无标签视频后，在未知环境 GO Stanford 上的预测指标全面改善（LPIPS 0.658→0.652，DreamSim 0.478→0.464，PSNR 11.031→11.083），表明模型能利用无动作标注的数据学到的视觉先验。

## 7. 优点

- **范式创新**：将视频生成模型作为导航世界模型，跳出“端到端策略学习”的固定范式，支持规划时动态添加约束（如禁止某些动作、禁止进入某些区域），这是传统监督策略不具备的灵活性。
- **架构设计精巧**：CDiT 在保持 Transformer 表达能力的同时，将注意力复杂度从二次降为线性（关于上下文帧数），使长上下文和更大模型成为可行选择；论文提供了清晰的计算复杂度分析和实验验证。
- **数据多样性**：在跨环境（室内/越野/社交）、跨本体（机器人/人类）的大规模数据上训练，并验证了无标签 Ego4D 数据对未知环境泛化的收益，符合 LeCun 一贯的“世界模型+自监督”研究路线。
- **实验规范**：多次采样报告均值和标准差，指标选取得当（既有轨迹指标 ATE/RPE，也有感知指标 LPIPS/DreamSim，还有生成质量 FID/FVD）。
- **落地价值**：NWM 既可作为独立规划器，也可提升现有策略（轨迹排序），展示了实际应用的两种路径。

## 8. 不足与局限

- **模式崩溃（Mode Collapse）**：在未知环境中，模型会逐渐丢失输入上下文，生成的帧逐渐趋同于训练数据的分布模式，长时预测失真（论文在 Figure 10 中给出了示例）。
- **动态场景建模弱**：模型难以准确模拟行人等动态物体的运动时序，虽然偶有成功案例。
- **动作空间受限**：目前仅支持 3 自由度（平面平移+偏航），未扩展到 6 自由度或机械臂关节等更复杂的动作空间。
- **规划实验范围有限**：独立规划仅在 RECON 单一环境上评估，缺少在多个已知环境中的系统评估；约束实验也仅在单一场景下测试。
- **需要大量计算资源**：1B 参数模型需要 64 张 H100 GPU 训练，具体时长未披露，复现门槛较高。
- **未见明确的失败分析**：论文虽提及局限，但未对模式崩溃的发生条件、何时动态建模失败、数据分布差异如何影响性能做系统的量化分析。
- **规划时长较短**：评估的规划轨迹长度为 8 步、单步 0.25 秒（合计约 2 秒），实际导航通常需要更长的时间范围。

（完）
