---
title: "IndoorUAV: Benchmarking Vision-Language UAV Navigation in Continuous Indoor Environments"
title_zh: IndoorUAV：连续室内环境中视觉语言无人机导航的基准测试
authors: "Xu Liu, Yu Liu, Hanshuo Qiu, Yang Qirong, Zhouhui Lian"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39562/43523"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向室内无人机的视觉语言导航基准
tldr: 论文针对室内无人机视觉语言导航这一未被充分研究的任务，构建了IndoorUAV基准，包含从Habitat模拟器收集的1000余个多样3D室内场景，并模拟真实无人机飞行动力学。该基准和方法专门为室内无人机VLN设计，填补了地面机器人与室外无人机研究之间的空白。实验验证了基准的可用性和方法的有效性，为仓库检查、送货、搜救等应用提供了评测平台。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39562/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 856, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39562/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1841, \"height\": 861, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39562/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 884, \"height\": 720, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39562/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1780, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39562/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1837, \"height\": 813, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39562/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1831, \"height\": 649, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39562/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1741, \"height\": 415, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39562/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1673, \"height\": 419, \"label\": \"Table\"}]"
motivation: 室内无人机VLN具有重要应用价值但缺乏专门基准和方法。
method: 构建大规模室内3D场景数据集并模拟真实无人机动力学，提出匹配的VLN方法。
result: 提供了超过1000个场景的基准，验证了所提方法的有效性。
conclusion: 推动室内无人机视觉语言导航的研究与实际应用。
---

## Abstract
Vision-Language Navigation (VLN) enables agents to navigate in complex environments by following natural language instructions grounded in visual observations. Although most existing work has focused on ground-based robots or outdoor Unmanned Aerial Vehicles (UAVs), indoor UAV-based VLN remains underexplored, despite its relevance to real-world applications such as inspection, delivery, and search-and-rescue in confined spaces. 
To bridge this gap, we introduce IndoorUAV, a novel benchmark and method specifically tailored for VLN with indoor UAVs. We begin by curating over 1,000 diverse and structurally rich 3D indoor scenes from the Habitat simulator. Within these environments, we simulate realistic UAV flight dynamics to collect diverse 3D navigation trajectories manually, further enriched through data augmentation techniques. Furthermore, we design an automated annotation pipeline to generate natural language instructions of varying granularity for each trajectory. This process yields over 16,000 high-quality trajectories, comprising the IndoorUAV-VLN subset, which focuses on long-horizon VLN. 
To support short-horizon planning, we segment long trajectories into sub-trajectories by selecting semantically salient keyframes and regenerating concise instructions, forming the IndoorUAV-VLA subset. Finally, we introduce IndoorUAV-Agent, a novel navigation model designed for our benchmark, leveraging task decomposition and multimodal reasoning.
We hope IndoorUAV serves as a valuable resource to advance research on vision-language embodied AI in the indoor aerial navigation domain.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：视觉语言导航（VLN）旨在让智能体通过视觉观察和自然语言指令在复杂环境中导航。已有工作主要集中在两类场景：(1) 室内地面机器人（轮式或四足）导航；(2) 室外无人机导航。**室内无人机 VLN** 这一具有重要实际应用价值的领域（如室内巡检、物资配送、搜救）长期被忽视。
- **核心挑战**：室内无人机导航与地面导航有本质区别——需要垂直方向推理、自由 3D 机动、细粒度空间理解以及高精度避障；与室外无人机导航也不同——室内空间密集、狭窄、结构复杂。现有数据集（如 R2R、SOON、RxR 等）基于 2D 导航图，难以支持 3D 空间推理。
- **论文定位**：首次提出专门针对室内无人机 VLN 的大规模基准数据集 **IndoorUAV**，同时提出配套的导航模型 **IndoorUAV-Agent**，填补室内空中 VLN 研究的空白。

---

## 2. 论文提出的方法论

### 2.1 数据采集与标注管线

- **环境来源**：从 Habitat 模拟器兼容的 Matterport3D（MP3D）、Gibson、HM3D、Replica 四个 3D 场景数据集中人工筛选了 **1075 个高保真室内场景**，覆盖住宅、办公、公共空间等多种布局。
- **动作空间设计**：定义 4 自由度（4 DoF）UAV 动作空间，包括：(1) 前向移动、(2) 垂直平移（上/下）、(3) 横向平移（左/右）、(4) 偏航旋转。同时设计了细粒度双尺度动作（如 `fly forward small` 为 0.15m，`fly forward large` 为 0.9m；`turn left small` 为 3°，`turn left large` 为 15°），以支持室内狭窄空间中的精确机动。
- **轨迹收集**：在去除 navmesh 约束的模拟环境中，由经验丰富的操作员手动遥控无人机，从采样的起点飞至目标点，记录自然、平滑的 3D 飞行轨迹。
- **数据增强**：对每条轨迹进行反向（起点与终点互换）和子轨迹重组，在不损失质量的前提下加倍数据量。
- **自动指令标注管线**：
  1. 基于运动变化（急转弯 >45°、垂直爬升 >1m、长直线飞行等）提取关键帧；
  2. 为每个关键帧标注对应动作类型；
  3. 使用 GPT-4o 描述关键帧图像（位置 + 近/中/远、左/中/右的物体结构）；
  4. 将描述拼接后由 GPT-4 生成**详细长指令**和**简短目标描述**两种粒度的导航指令。

### 2.2 两个子数据集

- **IndoorUAV-VLN**（长时程 VLN）：包含 **16,040** 条高质量轨迹，平均路径长度 21.6 米，平均指令长度 112 词，要求智能体理解并执行多步、语义丰富的指令。
- **IndoorUAV-VLA**（短时程 VLA）：从 VLN 子集中将长轨迹分割为子轨迹，每条仅包含 **1–3 个动作**（如"飞过柜子"、"在桌子附近下降"），重新生成简洁指令（平均 14.5 词），共 **34,925** 条短轨迹，侧重细粒度低层动作执行。

### 2.3 IndoorUAV-Agent 模型架构

- **短时程 VLA 任务**：直接使用微调后的 **π0 模型**（基于视觉-语言-动作流模型），输入当前第一人称视觉观测 + 简短指令，输出未来 h 步的连续状态序列（3D 坐标 + 偏航角）。
- **长时程 VLN 任务**：采用**任务分解管线**——先用 GPT-4o 将长指令分解为 n 个 VLA 风格的子指令（每条包含 1–3 个动作），然后依次调用 π0 VLA 模型执行每个子任务。第 i 个子任务的输入参考帧使用第 (i−1) 个子任务执行结束后的观测图像，保证时序连续性并减少误差累积。

---

## 3. 实验设计

### 3.1 评价指标

- **Success Rate (SR)**：VLA 任务中，终点位置误差 <0.5m 且偏航角差 <π/4；VLN 任务中，终点位置误差 <2m。
- **Normalized Dynamic Time Warping (NDTW)**：衡量预测轨迹与参考轨迹的对齐程度。VLA 任务中综合三维坐标 NDTW 和偏航角 NDTW（按路径长度和累计旋转角加权）；VLN 任务中仅用三维坐标 NDTW。
- **Navigation Error (NE)**：预测终点与目标点的距离。
- **Oracle Success Rate (OSR)**：轨迹上任意一点满足 SR 条件即视为成功。

### 3.2 对比基线

- **VLA 模型**：π0、π0-FAST、OpenVLA
- **VLN 模型**：Seq2Seq、CMA、NaVid、OpenFly-Agent
- **LLM 基线**：GPT-4o
- 在 VLA 实验中，基线模型均在数据集上进行微调（标 * 号）。

### 3.3 主要实验结果

- **IndoorUAV-VLA 测试集**：微调后的 π0 表现最佳（Full SR 27.16%，NDTW 9.44%）；Easy 子集 SR 达 46.58%，Medium 21.64%，Hard 7.55%。传统 VLN 回归模型（Seq2Seq、CMA）SR 均低于 3%。
- **IndoorUAV-VLN 测试集**：提出的 IndoorUAV-Agent 在全部指标上最佳——Seen SR 7.29%、Unseen SR 5.06%、NDTW 17.19%/15.65%。相比不分解任务的 π0 基线，SR 在 seen/unseen 上分别提升 +4.37%/+2.23%。NaVid 虽有较高 OSR（14.70%/16.21%），但常因无法预测"停止"动作导致 SR 很低。

---

## 4. 资源与算力

- **论文中未明确说明**使用的 GPU 型号、数量、训练时长、参数量等算力信息。
- 数据收集依赖人工操作员在模拟器中手动遥控无人机，以及 GPT-4/GPT-4o API 驱动的自动指令生成管线（具体调用次数和成本未披露）。
- 模型部分仅提及微调 π0 和对比模型，但未报告微调所需的计算资源。

---

## 5. 实验数量与充分性

### 实验数量

- 两个主要实验组：IndoorUAV-VLA（表 2）和 IndoorUAV-VLN（表 3）。
- VLA 实验按难度（Easy/Medium/Hard）细分，共 8 个模型 × 4 个难度类别；VLN 实验含 seen/unseen 两个测试集划分，共 7 个模型 × 4 个指标。
- 未进行消融实验（如：指令分解模块的有效性、数据增强策略的贡献、不同动作空间粒度的影响等）。
- 部分定性结果可视化展示（图 5），但样例数量有限。

### 充分性与公平性评价

- **优点**：基准覆盖 1075 个场景、50,000+ 轨迹，远超市面其他 VLN 数据集；对比基线涵盖 VLA 和 VLN 两类主流方法，且多数经过微调，较为公平。
- **不足**：
  - 缺乏消融实验，无法清晰归因各组件的贡献；
  - 所有模型在 IndoorUAV 上的绝对性能都很低（最优 SR 仅 27.16% 和 7.29%），缺少对失败模式的深入分析（除 NaVid 的停止问题外）；
  - 没有针对指令标注质量的量化评估（如人工评测 GPT-4 生成指令的自然度和准确性）。

---

## 6. 论文的主要结论与发现

1. **室内无人机 VLN 是一个极具挑战性的任务**：即使是最先进的方法（微调 π0）在 VLA 子集上 SR 仅 27.16%，VLN 子集上最优 SR 不足 10%，表明与真实应用需求仍有巨大差距。
2. **任务分解策略有效**：IndoorUAV-Agent 通过 GPT-4o 将长指令分解为短子指令，显著优于直接端到端执行长指令的基线方法，验证了层次化"语言理解 + 低层控制"框架的可行性。
3. **现有地面 VLN 模型难以直接迁移到无人机场景**：NaVid 等模型在室内空中导航中表现不佳，说明该任务需要专门的模型设计。
4. **双粒度数据集设计合理**：VLA（短时程精细控制）和 VLN（长时程目标导向）在同一环境下互补，为不同层次的导航能力评测提供了统一平台。
5. **IndoorUAV 可作为未来研究的基准资源**：为室内空中视觉语言具身智能研究提供了大规模、多样化的评测环境。

---

## 7. 优点

- **填补空白**：首个大规模室内 UAV VLN 基准，弥补了地面与室外空中 VLN 之间的研究缺口。
- **真实感强**：基于 Habitat 模拟器，结合真实 UAV 飞行动力学和 4-DoF 动作空间，支持自由 3D 运动；1075 个多样场景在数量和多样性上显著超越既有数据集。
- **双粒度设计**：同时覆盖长时程 VLN 和短时程 VLA，支持高阶语义理解与低层运动控制的联合研究。
- **自动化标注管线**：利用 GPT-4/GPT-4o 实现关键帧提取、场景描述、指令生成的自动化流程，具备可扩展性。
- **细粒度动作空间**：双尺度动作定义（small/large）更贴合室内狭窄空间中对精确控制的需求。
- **Agent 设计有启发性**：任务分解 + VLA 执行的模块化架构，在多步长时程任务中展现出明显优势，且具备可解释性。

---

## 8. 不足与局限

- **模拟器与真实环境的差距**：数据集完全基于 Habitat 模拟，未在真实室内环境中验证。模拟中的物理特性、光照、传感器噪声与真实世界存在偏差，模型迁移到实机的有效性存疑。
- **指令质量依赖 LLM**：导航指令完全由 GPT-4/GPT-4o 自动生成，未与人工标注进行对比或质量评估，可能存在语言模式单一、指令与轨迹对齐不精确等问题。
- **缺乏消融实验**：未对数据增强策略、关键帧选择方法、双尺度动作设计、GPT-4o 分解模块等核心设计逐一进行消融验证，因果归因不足。
- **绝对性能过低**：所有模型在基准上表现不佳（VLN SR <10%），虽然证明了任务难度，但也可能反映基准存在某些系统性困难（如指令粒度过细、轨迹过长、动作空间过复杂），论文未对此深入分析。
- **无真实世界验证**：没有在实体无人机上部署实验，限制了工作的实际应用说服力。
- **算力与成本信息缺失**：未报告训练资源、API 调用成本、数据收集人力投入等，降低了可复现性和工程参考价值。
- **未讨论失败案例**：除 NaVid 停止动作问题外，未系统分析其他模型（如 π0）的典型失败模式，不利于后续研究的针对性改进。

---

（完）
