---
title: "PanoNav: Mapless Zero-Shot Object Navigation with Panoramic Scene Parsing and Dynamic Memory"
title_zh: PanoNav：基于全景场景解析与动态记忆的无地图零样本物体导航
authors: "Qunchao Jin, Yilin Wu, Changhao Chen"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38899/42861"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 零样本物体目标导航，全景场景解析与动态记忆
tldr: 零样本物体导航在未知环境中对家庭机器人具有挑战性。现有方法依赖深度传感器或预建地图，限制多模态大模型的空间推理；无地图方法又常因缺乏历史上下文而陷入局部死锁。为此提出PanoNav，一种纯RGB的无地图零样本目标导航框架，通过全景场景解析模块释放多模态大模型的空间解析潜力，并结合动态记忆提供历史上下文，从而缓解短视决策问题。实验表明该方法能有效提升未知环境下的目标导航成功率。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1831, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1807, \"height\": 735, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 881, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 536, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 535, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 537, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 530, \"height\": 357, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 744, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 536, \"height\": 359, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38899/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 536, \"height\": 356, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38899/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1794, \"height\": 650, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38899/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 806, \"height\": 209, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38899/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1741, \"height\": 304, \"label\": \"Table\"}]"
motivation: 现有零样本物体导航依赖深度传感器或预建地图，且无地图方法缺乏历史上下文导致局部死锁。
method: 提出PanoNav框架，包含全景场景解析模块以充分利用多模态大模型的空间解析能力，以及动态记忆机制提供历史上下文。
result: 在未知环境中相比现有无地图方法显著提升目标导航成功率，减少局部死锁。
conclusion: 纯RGB、无地图的零样本物体导航可由全景解析与动态记忆有效支撑，为家庭机器人导航提供新思路。
---

## Abstract
Zero-shot object navigation (ZSON) in unseen environments remains a challenging problem for household robots, requiring strong perceptual understanding and decision-making capabilities. While recent methods leverage metric maps and Large Language Models (LLMs), they often depend on depth sensors or prebuilt maps, limiting the spatial reasoning ability of Multimodal Large Language Models (MLLMs). Mapless ZSON approaches have emerged to address this, but they typically make short-sighted decisions, leading to local deadlocks due to a lack of historical context. We propose PanoNav, a fully RGB-only, mapless ZSON framework that integrates a Panoramic Scene Parsing module to unlock the spatial parsing potential of MLLMs from panoramic RGB inputs, and a Memory-guided Decision-Making mechanism enhanced by a Dynamic Bounded Memory Queue to incorporate exploration history and avoid local deadlocks. Experiments on the public navigation benchmark show that PanoNav significantly outperforms representative baselines in both SR and SPL metrics.

---

## 论文详细总结（自动生成）

# PanoNav 论文详细中文总结

## 1. 论文的核心问题与整体含义

**研究动机与背景：**
- 零样本物体目标导航（Zero-Shot Object Navigation, ZSON）要求家庭机器人在未预先探索的环境中，仅根据自然语言指令（如"找到沙发"）自主规划路径并到达目标物体，是智能体自主决策、移动操作与人机交互的重要前置能力。
- 现有方法存在三类主要局限：
  - **依赖深度传感器或预建地图**：如 VLFM、ESC、VoroNav 等方法依靠 RGB-D 传感器构建 2.5D 或度量地图，增加了硬件负担，且在动态/噪声环境下鲁棒性不足；
  - **受限于预定义物体类别**：部分基于模仿学习或强化学习的方法只能在有限类别上泛化，难以应对开放词汇（open-vocabulary）场景；
  - **无地图方法缺乏历史上下文**：ZSON、PixNav 等仅基于当前观测做决策，容易产生"短视"行为，导致机器人反复回到已探索区域、陷入局部死锁（local deadlock）。
- **论文的核心论点**：纯 RGB、无地图的零样本物体导航可以由"全景场景解析 + 动态记忆引导决策"有效支撑，从而在不依赖深度传感器和地图的前提下显著提升导航成功率。

## 2. 论文提出的方法论

**核心思想：** 提出 PanoNav 框架，包含两大核心模块——全景场景解析（Panoramic Scene Parsing）与动态记忆引导的决策机制（Dynamic Memory-Guided Decision-Making），实现纯 RGB、无地图、开放词汇的零样本物体导航。

**关键技术细节：**

1. **全景场景解析（Panoramic Scene Parsing）**：
   - 每个时间步采集 6 个方向（间隔 60°）的 RGB 全景观测 V_t = {V^1_t, ..., V^6_t}；
   - **局部方向解析（Local Directional Parsing）**：对每个方向的图像，使用 Scaffold（SCA）方法生成对应的点阵图（dot matrix image）M^i_t = SCA(V^i_t)，将原始 RGB 图像与点阵图同时输入多模态大语言模型 MLLM（Qwen-2.5-VL），在隐空间构建空间关系图 G^i_t = P(Ψ(V^i_t), Φ(V^i_t, M^i_t))，其中 Ψ(·) 提取几何距离关系、Φ(·) 解析平面位置关系、P(·) 聚合两者。输出内容包括：物体清单、物体间空间关系、房间类型、目标似然度、信息丰富度等文本描述；
   - **全局全景摘要（Global Panoramic Summary）**：对整体环境进行高层语义分析，输出场景中一般存在的物体、当前所处房间/场景类型，提供隐式的自定位感知，作为动态记忆的输入。

2. **动态记忆引导的决策机制（Dynamic Memory-Guided Decision-Making）**：
   - 引入**动态有界记忆队列（Dynamic Bounded Memory Queue）** Q，最大长度为 n；
   - 每个时间步将全局摘要 gs_t 存入队列，当队列满时将最老的元素出队，保持长度恒定；
   - 决策函数：队列未满时 r_t = F(ld_t, gs_t)；队列已满时 r_t = F(ld_t, gs_t, Q_t)，其中 F(·) 为决策 LLM（DeepSeek-V3）；
   - 输出包括决策方向和目标是否被找到的标志位；
   - 使用 PixNav 作为底层运动控制器执行具体动作（动作空间含 Stop、MoveAhead、TurnLeft、TurnRight、LookUp、LookDown 六个离散指令）。

3. **解决的问题**：无记忆时 LLM 容易过度依赖"物体-房间"先验（如在客厅找沙发时反复停留在已搜索过的厅室区域）；记忆机制让 LLM 可以结合历史探索信息，引导机器人前往未探索但可能相关的区域（如走廊），避免局部死锁。

## 3. 实验设计

**数据集与 Benchmark：**
- 使用 **Habitat 模拟器**在 **HM3D（Habitat-Matterport 3D Research Dataset）** 上进行评估，该数据集包含 20 个完整建筑的高保真重建；
- 从验证集中随机选取 **200 个 episode**；
- 评估指标：**Success Rate（SR）** 和 **Success-weighted Path Length（SPL）**。

**对比方法：**

| 类别 | 方法 |
|------|------|
| 闭集 + 基于地图 | FBE（RGB-D）、SemExp（RGB-D） |
| 闭集 + 无地图 | Habitat-Web、OVRL（均需 RGB-D + GPS+Compass） |
| 开放词汇 + 基于地图 | VLFM、ESC、VoroNav、L3MVN（均需 RGB-D + GPS+Compass） |
| 开放词汇 + 无地图 | ImagineNav（需 RGB-D）、ZSON（RGB）、PixNav（RGB） |
| 本文方法 | **PanoNav（RGB Only, Mapless, Open-Set）** |

**主要实验结果：**
- PanoNav 达到 **SR 43.5%、SPL 23.7%**；
- 相比同设置基线 PixNav（SR 37.9%、SPL 20.5%），SR 提升 14.76%，SPL 提升 15.61%；
- 相比 ZSON（SR 25.5%、SPL 12.6%）提升显著；
- 甚至超越了多个闭集/基于地图的方法（FBE、SemExp、Habitat-Web、ESC、VoroNav）。

**额外实验：**
1. **死锁规避测试（Deadlock Avoidance Test）**：选取 5 个高欺骗性 episode（如"在客厅出发找沙发但客厅没有沙发"、"在走廊出发找马桶"），进行 10 次重复实验，使用 SR、SPL、DTS(f)（失败时距目标的距离）、ER（逃逸率）四个指标。
2. **消融实验（Ablation Study）**：四组配置对比——三视角 vs 全景六视角、一步式端到端决策 vs 解耦式解析+决策、有记忆 vs 无记忆。

## 4. 资源与算力

**论文未明确说明算力资源**。文中没有提及使用的 GPU 型号、数量、训练时长（实际上该方法是零训练/无训练范式，主要依赖预训练 MLLM 和 LLM 的推理），也未报告单次导航的推理时延或 API 调用成本等计算开销信息。

## 5. 实验数量与充分性

**实验组数：**
- 主实验：1 个数据集（HM3D）、200 个 episode，对比 11 种方法；
- 死锁规避测试：5 个 episode × 10 次重复；
- 消融实验：4 组配置。

**充分性评估：**
- **优点**：对比基线覆盖全面，横跨闭集/开放词汇、地图/无地图、RGB/RGB-D 多种设置；死锁测试具有针对性，消融实验对三个关键设计（全景视角、解耦架构、记忆机制）均有验证。
- **不足**：单一数据集（HM3D）、200 episodes 规模相对较小；死锁测试仅 5 个 episode（虽然有重复实验），样本量有限；未报告方差/置信区间；未在真实机器人上验证；缺少失败案例分析。整体实验设计较规范，但覆盖广度与统计严谨性尚有提升空间。

## 6. 论文的主要结论与发现

- PanoNav 在纯 RGB、无地图、开放词汇设置下显著优于同设置的 ZSON 和 PixNav，SR 和 SPL 分别达到 43.5% 和 23.7%，甚至超过部分依赖深度传感器和地图的强基线方法；
- **动态有界记忆队列是解决局部死锁的关键**：带记忆的 SR 为 48.0%（无记忆仅 12.0%），逃逸率 ER 从 32.0% 提升至 82.0%；
- **全景六视角明显优于受限三视角**（SR 43.5% vs 19.5%），说明宽视野对空间感知至关重要；
- **解耦式"解析→决策"优于一步式端到端决策**（SR 43.5% vs 35.0%），表明显式分离感知与推理可降低 MLLM 的认知负担；
- 轨迹可视化显示，在存在"欺骗性"区域的环境中，PanoNav 能在陷入局部循环后主动识别死锁并逃离，继续搜索目标。

## 7. 优点

- **方法设计新颖性**：首次提出纯 RGB、无地图、开放词汇 ObjectNav 框架同时解决"空间解析能力不足"和"局部死锁"两个问题；
- **点阵图辅助空间推理巧妙**：通过 SCA 方法生成的点阵图与原始 RGB 图像配对输入 MLLM，有效激活了多模态大模型对平面位置与几何距离关系的解析能力，成本低、可操作性强；
- **动态有界记忆队列设计简洁高效**：只存储全局摘要文本而非图像/特征，内存开销可控；有界设计避免历史信息无限累积，符合实际部署需求；
- **无需训练、即插即用**：框架完全基于预训练模型（Qwen-2.5-VL + DeepSeek-V3 + PixNav 控制器）的推理，零训练成本；
- **实验对比客观**：与同设置基线对比时保持公平条件，且结果优于多个假设更强的方法，说服力较强。

## 8. 不足与局限

- **基准覆盖有限**：仅在 HM3D 一个数据集上评估，未在 Gibson、MP3D 等其他常见 ObjectNav 基准上验证泛化性；
- **实验规模偏小**：200 个验证 episodes 在标准 ObjectNav 评测中属于较小规模；死锁测试仅 5 个场景，统计功效有限；
- **缺少统计显著性检验**：未报告多次运行的标准差、置信区间或显著性测试结果；
- **依赖闭源 LLM 服务**：决策模块使用 DeepSeek-V3，存在 API 成本、时延和隐私问题，且更换模型后的鲁棒性未验证；
- **无真实世界验证**：仅在仿真环境中评估，未考虑真实机器人的感知噪声、执行误差和动态干扰；
- **未报告推理开销**：每步调用 MLLM+LLM 的计算/时间成本未量化，实际部署可行性存疑；
- **记忆机制较简单**：当前记忆队列仅存储全局摘要文本，丢失了细粒度的方向级历史信息（论文也在未来工作中承认将探索多模态记忆）；
- **运动控制器依赖外部方法**：使用 PixNav 作为控制器，PanoNav 自身的决策上限受底层控制器质量制约。

（完）
