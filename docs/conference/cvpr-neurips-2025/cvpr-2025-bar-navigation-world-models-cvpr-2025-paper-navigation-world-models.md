---
title: Navigation World Models
title_zh: 导航世界模型
authors: "Bar, Amir, Zhou, Gaoyue, Tran, Danny, Darrell, Trevor, LeCun, Yann"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Bar_Navigation_World_Models_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 可控视频生成模型，用于模拟环境中的导航规划
tldr: 导航是世界模型在视觉运动智能体中的核心能力，但现有监督策略无法灵活融入约束。本文提出Navigation World Models（NWM），采用条件扩散Transformer（CDiT）预测未来视觉观测，通过模拟并评估轨迹是否达成目标来完成规划。NWM可动态加入约束，训练数据来自人类和机器人第一视角视频，规模达十亿参数。实验证明其在熟悉环境中能从零开始规划出有效导航轨迹，展示了生成式世界模型用于导航规划的潜力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 1110}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 645, \"height\": 1047}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 876, \"height\": 288}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1812, \"height\": 375}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 848, \"height\": 640}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1803, \"height\": 393}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1798, \"height\": 369}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 858, \"height\": 333}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 863, \"height\": 302}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 878, \"height\": 388}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 683, \"height\": 108}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 730, \"height\": 233}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 185}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-bar-navigation-world-models-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1662, \"height\": 165}]"
motivation: 现有导航策略行为固定，难以动态融入新约束，需要可泛化的世界模型来支撑轨迹规划。
method: 提出NWM模型，利用条件扩散Transformer基于历史观测和动作预测未来视觉观测，并通过模拟轨迹评估目标达成度来规划。
result: 实验表明NWM能规划有效轨迹，且支持动态约束，优于固定策略的导航方法。
conclusion: 生成式世界模型为导航规划提供了可扩展的新范式，具备在熟悉环境中从零规划的能力。
---

## Abstract
Navigation is a fundamental skill of agents with visual-motor capabilities. We introduce a Navigation World Model (NWM), a controllable video generation model that predicts future visual observations based on past observations and navigation actions. To capture complex environment dynamics, NWM employs a Conditional Diffusion Transformer (CDiT), trained on a diverse collection of egocentric videos of both human and robotic agents, and scaled up to 1 billion parameters. In familiar environments, NWM can plan navigation trajectories by simulating them and evaluating whether they achieve the desired goal. Unlike supervised navigation policies with fixed behavior, NWM can dynamically incorporate constraints during planning. Experiments demonstrate its effectiveness in planning trajectories from scratch or by ranking trajectories sampled from an external policy. Furthermore, NWM leverages its learned visual priors to imagine trajectories in unfamiliar environments from a single input image, making it a flexible and powerful tool for next-generation navigation systems.

---

## 论文详细总结（自动生成）

# 导航世界模型（Navigation World Models）——中文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- 导航是具身智能体（含视觉-运动能力的智能体）的基本能力，智能体需要依赖视觉构建环境表征、评估距离、捕捉地标，并进行路径规划。
- 现有最先进的机器人导航策略（如 NoMaD、GNM）是“硬编码”的监督式策略，存在两大局限：
  - **行为固定**：训练完成后难以动态引入新约束（例如“禁止左转”）。
  - **算力固定**：无法针对困难问题动态分配更多计算资源。
- 作者提出 **Navigation World Model（NWM）**，即可控视频生成模型，通过学习历史观测和导航动作来预测未来视觉观测。
- 在**已知环境**中，NWM 可通过“先模拟后评估”的方式规划轨迹（独立规划或对外部策略采样的轨迹排序）；在**未知环境**中，可从单张图像想象轨迹。
- 核心愿景：以生成式世界模型取代固定策略，为下一代导航系统提供更灵活、可扩展的范式。

## 2. 方法论：核心思想、关键技术细节与公式

### 2.1 整体框架

- 输入：一段以自我为中心的（egocentric）视频数据，以及对应的导航动作序列 `D = {(x₀, a₀, ..., x_T, a_T)}`。
- 动作定义：`a_i = (u, ω)`，其中 `u ∈ R²` 控制前后/左右平移，`ω ∈ R` 控制偏航角变化（在平面导航假设下为 3 自由度）。
- 学习目标：学习一个随机映射 `F_θ`，从过去 m 个潜变量观测 `s_t` 和动作 `a_t` 预测未来潜状态 `s_{t+1}`：
  - `s_i = enc_φ(x_i)`
  - `s_{t+1} ~ F_θ(s_{t+1} | s_t, a_t)`
- 使用预训练 VAE（Stable Diffusion tokenizer）将图像压缩为潜变量，便于计算和解码回像素空间。
- 该形式化可自然跨环境共享，并可扩展到更复杂的动作空间（如机械臂控制）。

### 2.2 时间控制扩展

- 在动作中加入时间偏移 `k ∈ [T_min, T_max]`，即 `a_t = (u, ω, k)`，表示模型需要往前/往后运动多少步。
- 导航动作可通过从当前时刻 t 到下一时刻 m = t + k - 1 的累计来计算：
  - `u_{t:m} = Σ_{r=t}^{m} u_r`
  - `ω_{t:m} = Σ_{r=t}^{m} ω_r mod 2π`
- 允许最大 ±16 秒的时间偏移。
- 为了缓解“动作-时间纠缠”（即模型可能只依赖时间而忽略动作或反过来），训练时对每个状态采样多个目标（goals），引入自然反事实（同一区域在不同时间到达）。

### 2.3 Conditional Diffusion Transformer（CDiT）架构

- **设计动机**：标准的 DiT 对全部上下文 token 做自注意力，复杂度为 `O(m²n²d)`（m 帧数，n 每帧 token 数），随上下文长度呈二次增长。
- **CDiT 模块**：
  - 第一个注意力块仅对当前去噪目标帧的 token 进行自注意力。
  - 通过**交叉注意力层**将来自过去帧的 token 作为 key/value 注入，使当前帧 token 可以感知上下文。
  - 交叉注意力复杂度为 `O(mn²d)`，**随上下文帧数线性扩展**，支持更长上下文。
- **条件注入**：
  - 导航动作 a、时间偏移 k、扩散时间步 t 分别通过正弦余弦特征和 2 层 MLP 映射为嵌入，然后求和：
    - `ρ = ψ_a + ψ_k + ψ_t`
  - ρ 输入 AdaLN 模块，生成 scale/shift 系数调制 LayerNorm 和注意力输出。
  - 对无标签数据，直接省略动作嵌入。

### 2.4 扩散训练

- 前向过程：向目标状态加入高斯噪声，`s^{(t)}_{t+1} = √α_t s_{t+1} + √(1-α_t) ε`。
- 反向过程：学习去噪网络 `F_θ(s_{t+1} | s_t, a_t, t)`。
- 训练损失：
  - 简化损失：`L_simple = E[ || s_{t+1} - F_θ(s^{(t)}_{t+1} | s_t, a_t, t) ||² ]`
  - 并预测噪声协方差矩阵，使用变分下界损失 `L_vlb`。
- 采样采用与 DiT 一致的 noise schedule 和超参数。

### 2.5 规划与轨迹评估

- **能量函数**（得分越低越好）：
  - `E(s₀, a₀, ..., a_{T-1}, s_T) = -S(s_T, s_goal) + Σ I(a_t ∉ A_valid) + Σ I(s_t ∉ S_safe)`
  - `S` 为感知相似度分数（将 s_T 和 s_goal 用 VAE 解码到像素空间，再计算 LPIPS / DreamSim 相似度）。
  - 约束项通过指示函数施加：非法动作进入无效集合，不安全状态进入不安全集合。
- **优化**：采用**交叉熵方法（CEM）**作为无梯度、基于种群的优化器，视作 Model Predictive Control（MPC）问题。
- **轨迹排序**：可用外部策略（如 NoMaD）采样 n 条轨迹，用 NWM 模拟每条轨迹并根据能量函数排序，选出最优轨迹。

## 3. 实验设计

### 3.1 数据集与场景

- **有标签机器人数据集**（含位姿和旋转，可推断相对动作）：
  - **SCAND**：社交合规导航视频。
  - **TartanDrive**：越野驾驶。
  - **RECON**：开放世界导航。
  - **HuRoN**：社交交互导航。
- **无标签数据**：Ego4D 视频（仅使用时间偏移动作）。
- **未知环境评估**：Go Stanford（GO Stanford）数据集。

### 3.2 Benchmark 与评估指标

- **轨迹预测精度**：绝对轨迹误差（ATE）、相对位姿误差（RPE）。
- **图像/视频质量**：LPIPS、DreamSim（感知相似度）、PSNR（像素级）、FID、FVD（生成分布质量）。
- **单步/多步预测**：在 RECON 数据集上评估 1 到 16 秒的未来预测。

### 3.3 对比方法

- **DIAMOND**：基于 UNet 的扩散世界模型，作为离线强化学习世界模型基线。
- **GNM**：通用目标条件导航策略（数据集汤训练）。
- **NoMaD**：扩展 GNM 的扩散策略，支持导航和探索。
- **NWM（规划）**：独立使用 NWM + CEM 规划。
- **NWM + NoMaD(排序)**：用 NWM 对 NoMaD 采样的 16/32 条轨迹排序。

### 3.4 主要实验配置

- 默认模型：CDiT-XL，10 亿参数，上下文 4 帧，总 batch size 1024 × 4 个目标 = 4096。
- 使用 Stable Diffusion VAE tokenizer、AdamW（lr=8e-5）。
- 采样 5 次报告均值±标准差。

## 4. 资源与算力

- 论文提到：XL 规模模型在 **8 台 H100 机器（每台 8 张 H100 GPU）** 上训练，即共 **64 张 H100 GPU**。
- **未明确提及**具体训练时长、总 GPU-hours 或单次训练耗时。
- 计算效率对比：CDiT 相比标准 DiT 在相同参数量下减少约 4 倍 FLOPs，同时性能更好。

## 5. 实验数量与充分性

- **消融实验**（RECON 上 4 秒未来预测）：
  - 目标数量（1/2/4）：4 目标最优。
  - 上下文长度（1/2/4）：更长上下文更好。
  - 时间/动作条件消融：仅时间退化严重，仅动作略有下降，两者联合最优。
- **架构对比**：CDiT-L vs DiT-XL（等参数量）及不同规模（S/B/L/XL），CDiT 始终在更低 FLOPs 下获得更低 LPIPS。
- **视频预测与生成**：与 DIAMOND 在 1 FPS/4 FPS 下对比 16 秒生成，NWM 在 FVD 上显著更优（200.969 vs 762.734），并在长时间预测上优于 DIAMOND。
- **导航规划**：
  - 独立规划（NWM planning）ATE/RPE 显著优于 GNM/NoMaD。
  - 排序外部策略（NWM + NoMaD）在 16/32 采样下提升 NoMaD 性能，且 32 样本更好。
  - 约束规划实验（三种动作约束）表明 NWM 能有效满足约束，代价较小。
- **未知环境泛化**：加入 Ego4D 无标签数据后，Go Stanford 上 LPIPS/DreamSim/PSNR 均改善，但 RECON 上略有下降（可能的域转移代价）。
- 总体而言，实验数量较充分，覆盖预测、生成、规划、排序、泛化和消融，对比基线合理（DIAMOND、GNM、NoMaD），但部分实验仅在单一数据集（RECON）上报告消融，跨数据集消融较少。

## 6. 主要结论与发现

- NWM 作为大规模条件扩散世界模型，能在已知环境中通过模拟轨迹实现从零规划，达到甚至超过现有监督导航策略的效果。
- NWM 能动态融入导航约束（如转向顺序），这是固定策略难以实现的。
- 在轨迹排序模式下，NWM 可以提升外部策略（NoMaD）的导航精度，且采样越多排序效果越好。
- CDiT 架构在大规模（10 亿参数）下计算效率远高于标准 DiT，且预测质量更好。
- 加入无标签、无动作的 Ego4D 视频数据能改善 NWM 在未知环境中的预测和生成能力，支持“自监督数据 + 世界模型”的扩展路径。
- 生成式世界模型有望成为下一代导航系统的灵活基础组件。

## 7. 优点

- **方法新颖**：将可控视频生成模型用于导航规划，摆脱固定策略局限，支持在规划时动态施加约束。
- **架构高效**：CDiT 将注意力复杂度从上下文的二次方降为线性，支撑更长上下文和更大规模。
- **跨域多智能体训练**：混合机器人（越野、社交、室内）和人类第一视角视频，提升泛化性。
- **即插即用式增强**：能以“ranking”方式与现有策略组合，直接提升 SOTA 方法性能，实用性强。
- **无标签数据利用**：展示了 Ego4D 自然视频对未知环境预测的正向迁移，有自监督潜力。
- **实验全面**：覆盖预测、视频合成、规划、排序、约束、泛化和消融，且有直观可视化和定性结果。

## 8. 不足与局限

- **分布外模式坍缩**：在未知或分布外环境中，模型会逐渐失去上下文，生成结果向训练数据靠拢（mode collapse），导致长期预测失真。
- **动态时序模拟不足**：难以准确模拟移动物体（如行人）的时序动态，与真实环境仍有差距。
- **动作维度有限**：目前仅支持 3 自由度平面导航（平移+偏航），未扩展到 6 自由度或机械臂控制。
- **约束求解依赖简单优化**：采用 CEM 作为规划器，在高维动作空间或复杂约束下可能效率不足。
- **泛化实验牺牲已知环境性能**：加入 Ego4D 后未知环境指标提升，但 RECON 上有所下降，说明域间存在权衡。
- **消融范围有限**：主要在 RECON 上做消融，未在全部数据集上系统评估。
- **算力信息不完整**：只说明 64 张 H100 训练，未报告训练时长、总能耗等可复现细节。
- **无显式空间记忆**：模型未构建结构化的环境地图，长期规划能力的内在机制尚不完全明确，依赖隐式表示驱动。

（完）
