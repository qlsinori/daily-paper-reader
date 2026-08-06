---
title: "What You See Is What You Reach: Towards Spatial Navigation with High-Level Human Instructions"
title_zh: 所见即所达：面向高层人类指令的空间导航
authors: "Lingfeng Zhang, Haoxiang Fu, Xiaoshuai Hao, Shuyi Zhang, Qiang Zhang, Rui Liu, Long Chen, Wenbo Ding"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38258/42220"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 提出基于高层人类指令的空间导航任务，涵盖物体与区域目标导航
tldr: 针对现有具身导航任务难以整合高层人类指令与空间理解的问题，提出空间导航这一新任务，包含空间物体导航（SPON）与空间区域导航（SPAN）。SPON利用物体间的空间关系和上下文引导智能体到达指定物体，SPAN实现导航至指定区域，两者互补。该方法使智能体能够更好地解析高层语言指令并执行相应导航行为。实验表明其显著提升了指令跟随与空间导航的效果，缩小了现实导航需求与现有模型的差距，为语言引导具身导航提供了新任务框架。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38258/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1823, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38258/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1840, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38258/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1838, \"height\": 664, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38258/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 851, \"height\": 1072, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38258/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1836, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38258/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 880, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38258/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 490, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38258/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 293, \"label\": \"Table\"}]"
motivation: 现有具身导航任务难以整合高层人类指令与空间理解，智能体在真实复杂环境中执行能力受限。
method: 提出空间导航任务，包含空间物体导航（SPON）与空间区域导航（SPAN），利用空间关系和上下文引导智能体。
result: 实验表明该方法使智能体更有效地解析高层指令，并能完成指定物体与区域的导航目标。
conclusion: 弥合了高层自然语言指令与具身空间导航之间的鸿沟，为语言引导导航提供了新任务范式。
---

## Abstract
Embodied navigation is a fundamental capability that enables embodied agents to effectively interact with the physical world in various complex environments. However, a significant gap remains between current embodied navigation tasks and real-world requirements, as existing methods often struggle to integrate high-level human instructions with spatial understanding. To address this gap, we propose a new task of embodied navigation called spatial navigation, which encompasses two key components: spatial object navigation (SpON) for object-specific guidance and spatial area navigation (SpAN) for navigating to designated areas. Specifically, SpON guides agents to specific objects by leveraging spatial relationships and contextual understanding, while SpAN focuses on navigating to defined areas within complex environments. Together, these components significantly enhance agents’ navigation capabilities, enabling more effective interactions in real-world scenarios. To support this task, we have generated a spatial navigation dataset consisting of 10K trajectories within the simulator. This dataset includes high-level human instructions, detailed observations, and corresponding navigation actions, providing a comprehensive resource to enhance agent training and performance. Building on the spatial navigation dataset, we introduce SpNav, a hierarchical navigation framework. Specifically, SpNav employs vision-language model (VLM) to interpret high-level human instructions and accurately identify goal objects or areas within the observation range, achieving precise point-to-point navigation using a map and enhancing the agent’s ability to oper-
ate effectively in complex environments by bridging the gap between perception and action. Extensive experiments show that SpNav achieves state-of-the-art (SOTA) performance in spatial navigation tasks across both simulated and real-world environments, validating the effectiveness of our method.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与研究动机

现有具身导航研究主要集中于两条路线：
- **视觉语言导航（VLN）**：依赖逐步式的详细指令（如"左转→穿过门→继续走"），但这类指令不符合自然的人类交流习惯；
- **物体目标导航（ObjectNav）**：按预定物体类别导航（如"找一把椅子"），缺乏对上下文和特定用户需求的理解。

然而，现实中人类指令往往蕴含高度的抽象意图与空间关系推理需求，例如**"在门附近等我"**或**"帮我拿茶几左侧的水果"**，这要求智能体不仅具备基本导航能力，还需要理解物体/区域之间的空间语义关系。现有方法在这类任务上存在显著的能力鸿沟。为此，论文提出**空间导航（Spatial Navigation）**这一新任务，旨在弥合高层人类语言指令与具身空间导航之间的差距。

## 2. 方法论

### 2.1 任务定义

空间导航包含两个互补子任务：
- **空间物体导航（SpON）**：根据空间关系约束（如"把杯子放在更近的桌子上"）导航至特定物体；
- **空间区域导航（SpAN）**：导航至由空间关系定义的区域（如"去门前的空地"）。

形式化定义为：`(o_t, l_t, r_t) → a_{t+1}`，其中 `o_t` 为RGB-D观测，`l_t` 为自然语言指令，`r_t` 为机器人位姿。成功条件：执行 Done 动作且最终位置与目标的欧氏距离 ≤ 1.0 米。

### 2.2 数据集构造流程

1. 在 AI2THOR 模拟器 200 个室内场景中随机采样位姿，收集 50,000 组多模态观测（RGB、深度、分割、语义图）；
2. 通过几何关系提取空间关系三元组 `(oi, rij, oj)`，关系集合 R = {left of, right of, above, below, near, next to}；
3. 使用 GPT-4 将三元组转化为多样化自然语言指令（如"捡起冰箱右侧的壁画"）；
4. 采用 A* 算法规划最优专家轨迹，每条轨迹包含 10–30 时间步的状态-动作序列；
5. 最终生成 10,000 条轨迹（SpON 5,000 + SpAN 5,000）。

### 2.3 SpNav 分层框架

核心思想是**"所见即所达"（What You See is What You Reach）**，包含两大阶段：

**训练阶段**：构建 200,000 个空间关系问答对训练 **NaviPoint 模型**——基于 Qwen2.5-VL-7B 初始化，输入为图像和空间问题，输出为目标点的文本坐标序列，通过交叉熵损失进行监督微调：
`L_SFT = −Σ log P(yi | y<i, I, Q; θ)`

**推理阶段**：
1. **VLM 推理**：用 GPT-4o 解析高层指令，提取目标描述（如"去沙发左侧的空地"→"沙发左侧的空地"）；
2. **NaviPoint 指向**：将当前 RGB 观测与目标描述输入 NaviPoint，在自我中心视角中获得目标坐标；
3. **地图构建**：基于 RGB-D 观测与位姿，构建包含障碍物层、探索层、可通行层的多通道语义地图（480×480 网格，5cm 分辨率）；
4. **Map-to-Action**：通过坐标变换矩阵 `T_ego→global` 将图像坐标变换至全局地图坐标，再使用快速行进法（FMM）规划最优路径，最后将路径点转化为离散动作（前进/左转/右转/停止）。

## 3. 实验设计

### 3.1 Benchmark 数据集

在 AI2THOR 模拟器中额外构建了评估基准：**1,315 条轨迹**（SpON 713 条 + SpAN 602 条），使用与训练集完全不同的未见场景，每条轨迹包含高层指令与真实目标位置。

### 3.2 评估指标

采用四个标准指标：**NE**（导航误差）、**PL**（路径长度）、**SPL**（成功率加权路径长度）、**SR**（成功率）。

### 3.3 对比方法

- **闭源通用 VLM**：GPT-4o、Claude-3.5-Sonnet、Qwen-VL-Max；
- **开源通用 VLM**：Janus-Pro-7B、Qwen2.5-VL-7B、LLaVA-Next-7B；
- **导航专用方法**：NaVid、NaVILA、MapNav（将其任务形式适配为本任务，统一提示词格式以保证公平性）。

## 4. 资源与算力

文中在实现细节部分明确提及：**NaviPoint 模型在 4 张 A100 GPU 上训练**，AdamW 优化器，学习率 10⁻⁵，每卡 batch size 为 4，梯度累积 2 步，有效 batch size 为 32。但**未说明具体训练时长**（如迭代轮数或总训练时间）。

## 5. 实验数量与充分性

论文共包含 **1 组主实验 + 3 组消融实验 + 1 组定性分析**：

| 实验 | 目的 |
|------|------|
| 主实验（Table 1） | 与三类 SOTA 方法对比整体性能 |
| 消融：推理 VLM 替换（Table 2） | 验证 GPT-4o 作为推理模块的有效性 |
| 消融：指向 VLM 替换（Table 3） | 验证 NaviPoint 相比通用 VLM 和 RoboPoint 的优势 |
| 消融：Map-to-Action（Table 4） | 与 Random、Direct-and-Avoid、PointNav 对比 |
| 定性分析（Figure 4） | 模拟器 + 真实环境零样本迁移展示 |

**充分性评估**：整体实验设计较为全面，覆盖了模块级消融和端到端对比，且在主实验中对所有对比方法统一了提示词格式，确保了公平性。不足之处在于：缺少与更多近期工作（如 InstructNav、VoroNav）的对比，且未报告多次运行的标准差或显著性检验，消融实验的结果差异是否具有统计意义待验证。

## 6. 主要结论

1. **SpNav 在主实验中全面超越所有基线**：相比最佳闭源模型 Claude-3.5-Sonnet，SR 提升 661%（41.1% vs 5.4%），NE 降低 73%；相比最佳导航专用模型 MapNav，SR 提升 95%（41.1% vs 21.1%）。
2. **分层设计有效**：消融实验证明 GPT-4o 推理 + NaviPoint 指向 + Map-to-Action 导航三模块各自均优于替代组件；
3. **任务特定训练至关重要**：通用开源 VLM 在本任务上 SR 为 0%，而经过空间数据微调的 7B NaviPoint 甚至超越 13B RoboPoint；
4. **具备从仿真到真实的零样本迁移能力**：在真实室内环境中可直接处理空间关系指令并导航至目标。

## 7. 优点

- **任务定义新颖且务实**：精准指向了现有导航任务与真实应用需求之间的关键缺口，将空间关系推理融入导航任务设计；
- **数据构造流程严谨**：利用模拟器语义图提取空间三元组、VLM 生成多样化指令、A* 规划专家轨迹，形成可扩展的数据生产管线；
- **分层框架设计清晰**：将"指令理解—目标定位—路径规划"解耦为三个独立可替换的模块，便于逐一优化与消融分析；
- **实验对比公平**：对基线方法统一适配提示词与动作空间，降低不公平比较的风险；
- **跨领域验证**：不仅限于模拟器，还展示了真实环境的零样本迁移能力，增强了说服力；
- **论文写作规范**：动机论证充分、相关工作梳理清晰、方法论展示完整。

## 8. 不足与局限

- **基于仿真器数据**：训练与评估均在 AI2THOR 中进行，虽有真实场景定性展示，但定量评估缺乏真实环境数据，泛化性说服力不足；
- **绝对成功率偏低**：SR 最高仅 41.1%，意味着近 60% 任务失败，离实际部署仍有较大距离；
- **依赖模拟器位姿真值**：Map-to-Action 使用模拟器的实时位姿进行坐标变换，在真实环境中需要可靠的里程计或 SLAM 系统替代；
- **GPT-4o 闭源依赖**：推理模块依赖闭源 API，存在成本、延迟与可复现性问题（尽管消融中展示了替换为开源模型的折中方案）；
- **对比公平性的潜在局限**：闭源 VLM 基线未经微调直接进行端到端预测，而 SpNav 的 NaviPoint 经过了任务特定训练，比较起点不完全对等；
- **缺少统计显著性与多场景扩展**：未报告多次运行的方差，也未见在更复杂场景（如多楼层、动态障碍物）中的测试；
- **缺少人类指令的多样性验证**：数据集中的指令由 GPT-4 基于空间三元组生成，风格可能相对单一，与真实人类指令的分布差异未作分析。

（完）
