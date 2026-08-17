---
title: "Towards Long-Horizon Vision-Language Navigation: Platform, Benchmark and Method"
title_zh: 迈向长程视觉语言导航：平台、基准与方法
authors: "Song, Xinshuai, Chen, Weixing, Liu, Yang, Chen, Weikai, Li, Guanbin, Lin, Liang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Song_Towards_Long-Horizon_Vision-Language_Navigation_Platform_Benchmark_and_Method_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 长程视觉语言导航，包含平台、基准和方法
tldr: 针对现有视觉语言导航方法局限于单阶段、难以处理复杂动态环境中的多阶段任务，论文提出长程视觉语言导航任务LH-VLN，强调连续子任务间的长期规划与决策一致性。为支持该任务开发了自动化数据生成平台NavGen，并构建长程规划与推理基准LHPR-VLN，同时给出相应方法。相关工作为VLN的长期规划研究提供平台和基准支撑。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1546, \"height\": 641, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1540, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 705, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1625, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1658, \"height\": 385, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1309, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1756, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 821, \"height\": 201, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-towards-long-horizon-vision-language-navigation-platform-benchmark-and-method-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 202, \"label\": \"Table\"}]"
motivation: 现有VLN方法缺乏多阶段与长程任务规划能力，难以应对复杂动态环境。
method: 提出LH-VLN任务、数据生成平台NavGen与长程规划推理基准LHPR-VLN。
result: 构建复杂任务数据集并验证任务设计与方法的有效性。
conclusion: 为长程VLN研究提供数据平台与评测基准，推动长期规划能力提升。
---

## Abstract
Existing Vision-Language Navigation (VLN) methods primarily focus on single-stage navigation, limiting their effectiveness in multi-stage and long-horizon tasks within complex and dynamic environments. To address these limitations, we propose a novel VLN task, named Long-Horizon Vision-Language Navigation (LH-VLN), which emphasizes long-term planning and decision consistency across consecutive subtasks. Furthermore, to support LH-VLN, we develop an automated data generation platform NavGen, which constructs datasets with complex task structures and improves data utility through a bidirectional, multi-granularity generation approach. To accurately evaluate complex tasks, we construct the Long-Horizon Planning and Reasoning in VLN (LHPR-VLN) benchmark consisting of 3,260 tasks with an average of 150 task steps, serving as the first dataset specifically designed for the long-horizon vision-language navigation task. Furthermore, we propose Independent Success Rate (ISR), Conditional Success Rate (CSR), and CSR weight by Ground Truth (CGT) metrics, to provide fine-grained assessments of task completion. To improve model adaptability in complex tasks, we propose a novel Multi-Granularity Dynamic Memory (MGDM) module that integrates short-term memory blurring with long-term memory retrieval to enable flexible navigation in dynamic environments. Our platform, benchmark and method supply LH-VLN with a robust data generation pipeline, comprehensive model evaluation dataset, reasonable metrics, and a novel VLN model, establishing a foundational framework for advancing LH-VLN.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 现有视觉语言导航（VLN）研究大多聚焦于**单阶段、短时程**的导航任务，指令简单、动作序列有限，难以反映真实世界中**多阶段、长时程**的复杂需求。
- 真实场景中，智能体需要执行跨多个子任务的连续指令，要求具备**持续决策、动态重规划、跨时间步的连贯推理**能力，这对服务机器人、自主助手等应用至关重要。
- 针对上述缺口，论文首次提出**长程视觉语言导航（LH-VLN）**任务，强调在连续子任务序列中保持**长期规划与决策一致性**。
- 为支撑该任务，论文从三个层面给出系统解决方案：**数据生成平台（NavGen）**、**评测基准（LHPR-VLN）与新指标**，以及**专用导航模型（MGDM）**。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 2.1 NavGen 数据生成平台
- 采用**双向、多粒度**生成机制：
  - **正向生成**：利用 GPT-4 结合场景资产（HM3D）与机器人配置（Spot、Stretch），生成复杂多阶段指令及对应轨迹，并由 Habitat3 模拟器执行得到轨迹数据。
  - **反向生成**：将复杂任务轨迹拆分为子轨迹段，通过轨迹分割算法得到“前进”“左转”等动作标签，结合 RAM 图像标注，再交给 GPT-4 生成逐步（step-by-step）VLN 指令。
- 公式表达：生成轨迹  
  \(D_{traj} = \text{Sim}(D_{ins}, S, A, \text{OR}(M, E))\)，其中 M 为导航模型，E 为专家模型。

### 2.2 LHPR-VLN 基准与新指标
- 基准任务格式为“在某处找到某物，并将其带到某处，然后……”；每个复杂任务包含 2–4 个连续子任务。
- 关键设置：子任务成功需满足目标物体在**1 米测地距离**内，且位于**水平 60°视场**中；智能体动作空间为“前进、左转、右转、停止”。
- 提出三个细粒度指标：
  - **ISR（独立成功率）**：各子任务独立完成的成功率；
  - **CSR（条件成功率）**：考虑子任务间的顺序依赖关系；
  - **CGT（基于真值路径加权的CSR）**：按子任务路径长度占整条任务路径的比例加权，更能反映不同难度子任务上的表现。
- 另有 TAR（目标接近率）等补充指标。

### 2.3 MGDM 导航模型
- 基础架构：采用 ViT（EVA-CLIP-Large）编码多方向 RGB 观测，Transformer 进行多视角融合，并以 LLM（Vicuna 7B）作为决策器。
- **CoT 反馈模块**：定期接收指令、当前观测与历史记忆，让 GPT-4 生成链式思考（Chain-of-Thought），提升任务理解与行动规划，减少幻觉。
- **自适应记忆集成与更新（AMIU）**：
  - **短期记忆**：对历史观测编码序列，使用基于置信度熵的“模糊+遗忘”池化操作压缩记忆，避免长任务下记忆过度累积。
  - **长期记忆**：从数据集检索与当前观测最匹配的历史观测-动作对，加权影响当前决策。
- 动作决策公式：最终动作由模型当前预测与检索到的历史动作加权平均得到；训练采用交叉熵损失与专家动作对齐。

## 3. 实验设计：数据集 / 场景、benchmark、对比方法

- **场景与平台**：主要使用 **Habitat3** 模拟器，场景资产来自 **HM3D** 的 216 个大尺度室内场景；另使用 HSSD 场景进行生成能力测试。
- **机器人配置**：Hello Robot 的 Stretch 与 Boston Dynamics 的 Spot。
- **Benchmark**：LHPR-VLN，共 **3,260 个任务**，平均 **150 个任务步骤**，平均指令长度 18.17，包含多阶段与逐步导航任务。
- **对比方法**：
  - 随机（Random）
  - GLM-4v prompt（零样本）
  - NaviLLM（预训练 + 微调）
  - GPT-4 + NaviLLM（GPT-4 分解任务后由 NaviLLM 顺序执行）
  - ETPNav（图基方法，文中提及但因无法适应三视角设置未能出结果）
  - MGDM（本文方法）
- **主实验**：在 LH-VLN 任务上按“2–3 子任务”和“3–4 子任务”两组长度进行对比；另外在“逐步导航任务”上进行测试。

## 4. 资源与算力

- 论文**未明确说明**训练所使用的 GPU 型号、数量或训练时长。
- 仅提及训练设置：LLM 为 Vicuna 7B，视觉编码器为 EVA-CLIP-02-Large（冻结），优化器为 Adam，学习率 3e-5，采用模仿学习与轨迹监督学习交替训练。
- 因此无法从论文文本中获知具体算力资源规模，这是论文在可复现性方面的一个信息公开不足。

## 5. 实验数量与充分性

- 实验组数较为有限，主要包括：
  1. 主实验（Table 2）：在两类任务长度（2–3 子任务、3–4 子任务）上对比 6 种方法，共 5 个指标（SR、NE、ISR、CSR、CGT）；
  2. 逐步任务实验（Table 3）：对比 Random、GLM-4v、NaviLLM、MGDM 在逐步导航上的 SR/OSR/SPL/NE；
  3. 消融实验（Table 4）：对 MGDM 分别移除自适应记忆（Adap Mem）、长期记忆（LT Mem）、CoT 模块，共 4 组；
  4. 另有基准统计（子任务数量分布、机器人类型比例等）和可视化案例分析。
- **充分性评价**：
  - 优点：主实验覆盖了单阶段与多阶段、不同任务长度，以及多种基线（零样本、微调、任务分解组合），能基本回答论文提出的三个研究问题（现有模型能否完成复杂任务、任务分解的作用、记忆的重要性）。
  - 不足：**对比方法较少**，未包含近期更强的大模型导航方法（如 NaviD、ETPNav 的具体数值未列出）；消融实验仅验证了模块去除后的整体影响，缺少对短期记忆池化窗口、长期记忆检索数量等超参数的敏感性分析；实验场景主要为 HM3D，未在 HSSD 上提供完整评测结果。总体实验数量偏少，但面向新任务的首个基准，属于可接受的初始验证。

## 6. 论文的主要结论与发现

- 现有 VLN 模型（包括预训练和微调的 NaviLLM、GPT-4 组合方法）在 LH-VLN 任务上表现普遍很差，**在 2–3 子任务设置下所有非本文方法的 SR/ISR/CSR/CGT 均为 0**，说明现有方法难以理解并完成多阶段复杂任务。
- 使用 GPT-4 做任务分解能够提升单阶段模型在复杂任务中的**子任务独立成功率（ISR）**，但整体任务连贯性（CSR、CGT）提升有限，甚至出现 CGT 下降，说明“分解+顺序执行”模式缺少全局理解与连贯记忆。
- **记忆是长程导航的关键**：模型在更长任务（3–4 子任务）上的 ISR/CSR/CGT 反而优于较短任务，可能因为前序阶段积累的记忆有助于后续子任务执行；消融实验也证实移除自适应记忆后 NE 大幅恶化（从 1.23 升至 4.44）。
- 本文提出的 MGDM 在 LH-VLN 任务上取得了相对最优的综合表现，尤其在 N E 上显著降低（1.23），表明其在复杂长程导航中具有较大潜力。
- 在逐步任务上，MGDM 的 SR 仍为 0，暴露出其对“停止”时机的判断不够准确，有待进一步改进。

## 7. 优点

- **任务定义具有前瞻性**：首次明确提出 LH-VLN，填补了长程、多阶段 VLN 任务的空缺，贴近真实应用需求。
- **平台自动化程度高**：NavGen 采用双向生成机制，无需大量人工标注即可产出复杂多阶段指令和轨迹，且可移植到不同模拟器和场景。
- **评测体系更细粒度**：提出的 ISR/CSR/CGT 指标能区分“独立完成能力”“条件依赖能力”和“按路径难度加权”的不同维度，优于传统 SR 的粗粒度评价。
- **模型设计有创新**：MGDM 结合 CoT 反馈、短期记忆熵最小化模糊/遗忘与长期记忆检索，在动态环境和长时程任务中表现出更强的适应性和决策连贯性。
- **消融设计对应明确研究问题**，并给出可视化案例，直观展示记忆长度对行为质量的影响。

## 8. 不足与局限

- **算力信息缺失**：未提供 GPU 型号、数量、训练时间，复现成本未知。
- **实验规模有限**：主实验场景仅 HM3D，缺少跨数据集泛化评估；HSSD 仅用于生成平台展示，未做完整导航评测。
- **基线覆盖不足**：未包含近期更多强基线（如 NaViD、MultiPLY、InstructNav 等），也缺少 ETPNav 在对应设置下的具体结果。
- **识别“停止”能力弱**：MGDM 在逐步任务中 SR 为 0，说明其目标到达判断有缺陷，这会影响实际部署的可靠性。
- **新指标可能存在偏置**：CSR 和 CGT 的定义中包含子任务顺序依赖权重，但未深入分析不同子任务数量/难度分布对指标稳定性的影响；CGT 依赖真值路径长度，而路径长度与场景结构、机器人运动模式有关，可能引入场景偏差。
- **依赖 GPT-4 生成指令与数据**，其生成质量、多样性和潜在偏见未被系统验证；同时使用 GPT-4 生成 CoT 会增加推理成本与不确定性。
- **长期记忆来源**主要来自 LHPR-VLN 数据集本身，在线导航时如何动态构建和维护长期记忆在真实环境中的适用性有待进一步讨论。

（完）
