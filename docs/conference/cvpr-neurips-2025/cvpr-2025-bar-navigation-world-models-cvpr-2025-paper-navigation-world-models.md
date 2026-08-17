---
title: Navigation World Models
title_zh: 导航世界模型
authors: "Bar, Amir, Zhou, Gaoyue, Tran, Danny, Darrell, Trevor, LeCun, Yann"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Bar_Navigation_World_Models_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 面向导航的可控视频生成模型，通过模拟未来观测规划轨迹，直接针对具身导航任务
tldr: 针对导航智能体在复杂环境中规划轨迹的需求，提出导航世界模型NWM，利用条件扩散Transformer基于过去观测和动作预测未来视觉观测。该模型在人类与机器人第一视角视频上扩展至十亿参数规模，并可通过模拟轨迹评价目标达成度来规划，支持动态约束，实验表明能从头规划有效轨迹。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 1110}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 645, \"height\": 1047}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 876, \"height\": 288}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1812, \"height\": 375}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 848, \"height\": 640}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1803, \"height\": 393}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1798, \"height\": 369}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 858, \"height\": 333}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 863, \"height\": 302}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 878, \"height\": 388}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 683, \"height\": 108}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 730, \"height\": 233}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 185}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1662, \"height\": 165}]"
motivation: 传统监督导航策略行为固定，难以动态融入约束，且需要大量标注演示。
method: 提出条件扩散Transformer训练的可控视频生成模型NWM，根据历史观测和导航动作预测未来观测。
result: 在多样第一视角视频上训练至十亿参数，能通过仿真规划达成目标的导航轨迹并动态施加约束。
conclusion: 生成式世界模型为导航规划提供了一种可约束、可泛化的能力，优于固定监督策略。
---

## Abstract
Navigation is a fundamental skill of agents with visual-motor capabilities. We introduce a Navigation World Model (NWM), a controllable video generation model that predicts future visual observations based on past observations and navigation actions. To capture complex environment dynamics, NWM employs a Conditional Diffusion Transformer (CDiT), trained on a diverse collection of egocentric videos of both human and robotic agents, and scaled up to 1 billion parameters. In familiar environments, NWM can plan navigation trajectories by simulating them and evaluating whether they achieve the desired goal. Unlike supervised navigation policies with fixed behavior, NWM can dynamically incorporate constraints during planning. Experiments demonstrate its effectiveness in planning trajectories from scratch or by ranking trajectories sampled from an external policy. Furthermore, NWM leverages its learned visual priors to imagine trajectories in unfamiliar environments from a single input image, making it a flexible and powerful tool for next-generation navigation systems.

---

## 论文详细总结（自动生成）

# 《Navigation World Models》论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：导航是具身智能体（如机器人、动物）的基本能力，视觉在导航中起核心作用。传统监督式导航策略（如 NoMaD、GNM）在训练后行为固定，难以动态引入新约束（如“禁止左转”“避开悬崖边缘”），也无法根据问题难度动态分配算力。
- **核心问题**：能否构建一个可泛化、可控制、可规划的“世界模型”，通过模拟未来视觉观测来评估和规划导航轨迹，而不是直接学习固定的策略映射？
- **核心回答**：论文提出**导航世界模型（Navigation World Model, NWM）**——一个基于条件扩散 Transformer 的可控视频生成模型，根据历史观测和导航动作自回归地预测未来视觉帧，并利用该预测能力进行轨迹规划、轨迹排序以及未知环境中的想象生成。
- **整体含义**：NWM 将视频生成、视觉导航和基于模型的规划结合起来，提供了一种可动态施加约束、可扩展、可泛化的导航规划新范式，为下一代自监督导航系统奠定了基础。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 2.1 核心思想
- 将导航问题建模为**条件视频预测问题**：给定过去的视觉观测（编码后的潜变量）和动作指令，学习一个随机映射 `F(s_{t+1} | s_t, a_t)` 来预测未来视觉状态。
- 与仅学习策略不同，世界模型模拟环境动态，可通过“想象”多种轨迹来评估是否达到目标，并在规划时灵活加入各种约束。

### 2.2 状态与动作表示
- 视觉观测通过预训练的 **VAE（Stable Diffusion tokenizer）** 编码为潜变量 `s`，支持解码回像素空间进行可视化。
- 动作 `a = (u, ω)`，其中 `u ∈ R²` 控制前后/左右平移，`ω ∈ R` 控制偏航角变化；可扩展至 6 DoF。
- 额外引入**时间偏移 `k`** 作为动作的一部分，允许模型预测未来或过去 `k` 步的状态，从而学习环境的时间动态。
- 对于无标注数据（如 Ego4D），仅使用时间偏移作为动作，省略显式动作条件。

### 2.3 条件扩散 Transformer（CDiT）
- **架构**：CDiT 改进了 DiT 的注意力机制：
  - 第一个注意力块仅对当前待去噪目标帧的 token 进行自注意。
  - 通过**交叉注意力层**，让当前帧的每个 query 关注过去上下文帧的 key/value。
  - 计算复杂度从 DiT 的 `O(m²n²d)`（二次于上下文长度）降低到`O(mn²d)`（线性于上下文长度）。
- **条件注入**：将导航动作、时间偏移、扩散时间步分别编码为向量后求和，通过 AdaLN（自适应层归一化）调制网络。
- **扩散训练**：使用标准扩散前向加噪/反向去噪流程，损失函数包括简单均方误差和变分下界损失，预测噪声并学习协方差矩阵。
- **可扩展性**：CDiT 在 1B 参数规模下比标准 DiT 节省约 4 倍 FLOPs，同时预测精度更高。

### 2.4 基于世界模型的规划
- **能量函数**（式 4）：`E = -similarity(s_T, s_goal) + 状态约束惩罚 + 动作约束惩罚`。
  - 相似度通过解码最后状态和目标图像后用 LPIPS/DreamSim 等感知度量计算。
  - 约束以指示函数形式加入，例如非法动作或危险状态。
- **规划优化**：使用**交叉熵方法（CEM）** 优化动作序列，最小化能量函数，即模型预测控制（MPC）。
- **轨迹排序**：假设存在外部策略（如 NoMaD），采样多个轨迹后用 NWM 模拟并打分，选择能量最低者作为最终输出。

## 3. 实验设计：数据集、基准与对比方法

### 3.1 数据集
- **域内（in-domain）机器人数据集**：
  - **SCAND**：社交合规导航视频。
  - **TartanDrive**：越野驾驶视频。
  - **RECON**：开放世界导航。
  - **HuRoN**：社交交互导航。
- **无标注数据**：**Ego4D**（人类第一视角视频，仅时间标签）。
- **未知环境评估**：**Go Stanford** 数据集作为模型从未见过的环境，用于测试泛化能力。

### 3.2 评估指标
- **轨迹精度**：ATE（绝对轨迹误差）和 RPE（相对位姿误差）。
- **图像/视频质量**：LPIPS、DreamSim、PSNR（预测帧与真值相似度），FID、FVD（生成分布质量）。

### 3.3 对比方法
- **DIAMOND**：基于 UNet 的扩散世界模型（离线强化学习）。
- **GNM**：通用目标条件导航策略。
- **NoMaD**：基于扩散策略的导航模型。

### 3.4 核心实验概览
| 实验 | 内容 |
|---|---|
| 消融实验 | 模型规模（CDiT vs DiT）、目标数量、上下文长度、时间/动作条件的作用 |
| 视频预测 | 单步/多步预测（1–16秒），与 DIAMOND 对比 FID/LPIPS/FVD |
| 独立规划 | 用 NWM + CEM 从零规划轨迹，对比 GNM、NoMaD |
| 约束规划 | 在三种动作约束下测试规划能力 |
| 轨迹排序 | 用 NWM 对 NoMaD 采样的 16/32 条轨迹排序，验证导航提升 |
| 未知环境泛化 | 加/不加 Ego4D 无标注数据，在 Go Stanford 上评估预测质量 |

## 4. 资源与算力

- 论文明确提到 CDiT-XL（1B 参数）模型在 **8 台 H100 机器（每台 8 张 GPU，共 64 张 H100）** 上训练，但**未给出具体训练时长（步数/天数）**。
- 默认设置：上下文 4 帧，总 batch size 1024，4 个不同目标，等效 batch size 4096。优化器 AdamW，学习率 `8e-5`。
- 其他细节（如模型变体的训练代价）未完全披露。

## 5. 实验数量与充分性

- **实验数量**：相对丰富，包括 4 组消融、1 组视频预测对比、1 组生成质量对比、1 组独立规划、1 组约束规划、1 组轨迹排序、1 组未知环境泛化。每组均有定量指标和定性可视化。
- **充分性**：
  - **优点**：消融设计较全面，覆盖架构、条件设计、上下文长度、目标数量；对比方法覆盖了当前主流策略和世界模型；在多个机器人数据集上评测。
  - **客观性**：报告了多次采样的均值和标准差；使用了标准轨迹误差指标和感知相似度指标。
  - **潜在不足**：
    - 主要定量评估集中于 RECON 和 Go Stanford，域内其他数据集（SCAND、TartanDrive、HuRoN）的详细结果仅部分报告（规划实验表 2 提到“all in-domain datasets”，但具体数据未展示）。
    - 与真实机器人部署的差距未涉及；没有在物理机器人上验证规划结果。
    - 无标注数据 Ego4D 的加入在已知环境（RECON）上反而导致预测指标下降（见表 4），论文解释为泛化性提升但牺牲了域内精度，缺乏更深入的权衡分析。

## 6. 论文的主要结论与发现

- **CDiT 优于 DiT**：在相同甚至更少 FLOPs 情况下，CDiT 获得更好的未来预测精度，证明线性复杂度注意力的有效性。
- **更多的目标状态和更长的上下文有助于预测**：4 个目标、4 帧上下文在 LPIPS/DreamSim/PSNR 上均最优。
- **时间和动作条件缺一不可**：仅时间条件会导致性能大幅下降（LPIPS 从 0.295 升至 0.760），仅动作条件也有小幅下降。
- **NWM 可独立规划**：NWM + CEM 在 RECON 上的 ATE/RPE（1.13/0.35）显著优于 GNM（1.87/0.73）和 NoMaD（1.93/0.52）。
- **NWM 可改进外部策略**：对 NoMaD 采样的轨迹进行排序（32 条）后，ATE/RPE 分别从 1.93/0.52 改善至 1.78/0.48。
- **约束规划可行**：在“先前进后转向”“先左右转后前进”等约束下，最终位姿偏差较小。
- **无标注数据提升未知环境泛化**：加入 Ego4D 后，Go Stanford 上的 LPIPS/DreamSim/PSNR 均改善（LPIPS 从 0.658 降至 0.652，PSNR 从 11.031 升至 11.083），说明预训练视觉先验有助于想象未知环境。
- **模型仍存在模式崩溃和动态模拟困难**。

## 7. 优点

- **新颖的架构**：CDiT 以线性复杂度处理长上下文，解决了 DiT 在视频预测中计算量过大的问题，且扩展至 1B 参数仍高效。
- **统一多种数据源**：同时利用机器人视频（有动作）和人类视频（无动作），提升了世界模型的泛化能力。
- **灵活规划范式**：世界模型天然支持动态约束（禁止动作、禁止区域等），克服了硬编码策略的局限。
- **无需真实交互**：纯离线训练，规划时只依赖模型模拟，不与环境交互。
- **可解释中间产物**：能解码预测帧为像素，可视化轨迹模拟过程，便于分析失败原因。
- **实验较扎实**：包含从预测、生成到规划、排序的完整评估链条，并给出定量统计。

## 8. 不足与局限

- **模式崩溃**：在未知环境中，模型长时间预测会逐渐退化到训练数据的分布，丢失当前场景上下文。
- **动态实体建模弱**：难以准确模拟行人等动态对象的运动，影响复杂社会环境的模拟。
- **动作维度有限**：仅支持 3 DoF 导航动作（平移+偏航），未扩展到 6 DoF 或机械臂控制（作者声称可扩展但未验证）。
- **域内性能与泛化的权衡**：引入无标注数据虽然提升了未知环境性能，但显著降低了已知环境（RECON）的预测精度（LPIPS 从 0.295 恶化到 0.368），论文未能给出较好的平衡方案。
- **规划效率与规模**：CEM 优化需要多次前向模拟，计算开销大；1B 模型训练资源需求高，未报告具体训练时长和成本。
- **实验范围局限**：主要在室内/越野数据集上验证，未在真实机器人上部署；与强化学习或 SLAM 方法的系统对比不足。
- **相似度度量依赖**：用 LPIPS 等作为目标函数可能偏向感知平滑而非精确几何，是否能泛化到更复杂的导航任务（如动态避障）存疑。

---

（完）
