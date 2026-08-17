---
title: "CityWalker: Learning Embodied Urban Navigation from Web-Scale Videos"
title_zh: CityWalker：从网络规模视频中学习具身城市导航
authors: "Liu, Xinhao, Li, Jintong, Jiang, Yicheng, Sujay, Niranjan, Yang, Zhicheng, Zhang, Juexiao, Abanes, John, Zhang, Jing, Feng, Chen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_CityWalker_Learning_Embodied_Urban_Navigation_from_Web-Scale_Videos_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 从网络规模视频学习动态城市环境的具身视觉导航
tldr: 城市动态环境的无地图与非道路区域导航仍是具身智能体的难点。CityWalker 提出从网络海量行走与驾驶视频中提取动作监督的规模化数据流水线，以模仿学习训练城市导航策略，无需昂贵人工标注。模型习得复杂的空间推理与常识性导航行为，在无地图或非道路设定下展现类人导航能力，为最后一公里配送等自主智能体提供了可扩展的视觉导航训练范式。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1781, \"height\": 563}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 838}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 853, \"height\": 462}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 331}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1691, \"height\": 847}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 774, \"height\": 478}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 743, \"height\": 454}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 748}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 253}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 692, \"height\": 355}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 223}]"
motivation: 现有视觉导航方法在无地图或非道路的城市环境中表现不佳，限制了末端配送等自主智能体应用。
method: 从网络视频自动提取动作监督，构建大规模模仿学习流水线，训练类人城市导航模型。
result: 模型学习了复杂的空间推理与常识导航行为，在无地图及非道路设定下具备更接近人的导航能力。
conclusion: 规模化网络视频数据驱动是解决开放城市环境视觉导航泛化难题的有效途径。
---

## Abstract
Navigating dynamic urban environments presents significant challenges for embodied agents, requiring advanced spatial reasoning and adherence to common-sense norms. Despite progress, existing visual navigation methods struggle in map-free or off-street settings, limiting the deployment of autonomous agents like last-mile delivery robots. To overcome these obstacles, we propose a scalable, data-driven approach for human-like urban navigation by training agents on thousands of hours of in-the-wild city walking and driving videos sourced from the web. We introduce a simple and scalable data processing pipeline that extracts action supervision from these videos, enabling large-scale imitation learning without costly annotations. Our model learns sophisticated navigation policies to handle diverse challenges and critical scenarios. Experimental results show that training on large-scale, diverse datasets significantly enhances navigation performance, surpassing current methods. This work shows the potential of using abundant online video data to develop robust navigation policies for embodied agents in dynamic urban settings.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：在动态城市环境中，具身智能体（如末端配送机器人、机器人出租车）需要在无高清地图或非道路（off-street）条件下安全、高效地导航。现有视觉导航方法大多依赖仿真环境或受控场景，难以应对城市空间中复杂、动态、充满不确定性的真实情况，例如多变地形、密集行人、交通信号、突发障碍等，同时还需遵守常识性社会规范（如走人行道、保持社交距离等）。
- **核心问题**：如何利用大规模、易获取的网络视频数据，训练出能像人类一样在真实城市环境中导航的具身智能体，从而突破传统方法在数据规模、标注成本与泛化能力上的瓶颈。
- **整体含义**：作者提出 **CityWalker**，一种完全数据驱动、可扩展的城市导航训练范式——从超过 2000 小时的网络城市行走和驾驶视频中自动提取动作监督，无需昂贵的人工标注，即可学习类人的城市导航策略。实验表明，大规模数据预训练显著提升真实世界导航性能，展示了“网络视频 → 具身导航策略”的可行性。

## 2. 方法论

- **核心思想**：将城市导航问题形式化为**真实世界中的点目标导航（point-goal navigation, PGN）**。智能体在每一步接收 RGB 观测、当前位置（GPS）和子目标路点，学习策略 \(\pi(a_t | o_{(t-k):t}, p_{(t-k):t}, w_t)\)，输出未来若干步的动作路点。
- **数据流水线**：
  - 从互联网收集 **2000+ 小时**第一视角城市行走视频 + 驾驶视频；
  - 使用现成的**视觉里程计（VO，如 DPVO）** 提取帧间相对位姿，作为动作标签；
  - 针对 VO 的累积误差和尺度歧义，**只使用短时间窗口内的相对位姿**，并将每个动作按轨迹平均步长进行归一化，得到一致、抽象的动作空间；
  - 该流水线可扩展到任意带自运动的视频（如驾驶视频），支持跨域、跨形态学习。
- **模型架构**：
  - 输入：过去 \(k=5\) 帧图像、过去 5 步位置、当前目标位置；
  - 图像用冻结的 **DINOv2** 编码，坐标用可训练的编码器；
  - 一个 **Transformer** 处理输入 token 序列，输出未来 token；
  - 动作头（action head）和到达头（arrival head）分别预测未来 5 步动作和是否到达目标；
  - 训练时引入**特征幻觉（feature hallucination）** 辅助损失：让预测的未来 token 与真实未来帧的 DINOv2 特征做 MSE 损失，促使模型生成更具信息量的未来表征。
- **损失函数**：
  \[
  \mathcal{L} = \omega_{l1}\mathcal{L}_{l1} + \omega_{ori}\mathcal{L}_{ori} + \omega_{arr}\mathcal{L}_{arr} + \omega_{feat}\mathcal{L}_{feat}
  \]
  - 其中 \(\mathcal{L}_{ori}\) 为负余弦相似度（方向误差），\(\mathcal{L}_{l1}\) 为动作 L1 损失，\(\mathcal{L}_{arr}\) 为到达状态 BCE 损失，\(\mathcal{L}_{feat}\) 为特征幻觉 MSE 损失；各项权重按同量级设定。
- **核心创新**：不再依赖昂贵的 VLM 提示或人工标注，而是用带噪的 VO 伪标签在超大规模视频上做模仿学习，证明了噪声标签在大数据下依然有效且可扩展。

## 3. 实验设计

- **数据集与场景**：
  - **网络视频数据**：2000+ 小时城市行走视频 + 数量不等的驾驶视频（涵盖不同地理位置、天气、时间段）；
  - **专家微调数据**：使用 Unitree Go1 四足机器人（配备 Livox Mid-360 LiDAR 和网络摄像头）在纽约市采集 15 小时遥操作数据，其中 6 小时用于微调，9 小时用于离线测试；
  - **真实部署测试**：在新场景中部署，目标距离约 50–100 m，分**直行、左转、右转**三类场景。
- **Benchmark 与关键场景**：定义了六类关键场景（可重叠）：转弯（Turn）、路口穿越（Crossing）、绕行（Detour）、近距离行人（Proximity）、拥挤人群（Crowd）以及其他（Other），分别统计指标。
- **评估指标**：
  - **AOE（平均方向误差）**：预测动作与真实动作的夹角；
  - **MAOE（最大平均方向误差）**：所有时间步中最大 AOE 的均值，避免小误差步低估整体错误；
  - 同时报告 **L2 距离** 和 **到达准确率（Arrival）**。
- **对比方法**：GNM、ViNT（零样本和微调）、NoMaD（零样本），以及 CityWalker 的零样本和微调版本；同时提到与 CoNVOI 类似方法因无开源代码未测试。
- **实验组成**：
  1. **离线基准测试**（表 1）：按关键场景对比 L2、MAOE、Arrival；
  2. **真实世界导航**（表 2）：对比各方法的成功率；
  3. **数据规模效应**（图 6）：训练数据小时数与 MAOE 的关系；
  4. **特征幻觉损失效益**（图 7）：有无该损失的训练曲线对比；
  5. **跨域/跨形态实验**：仅驾驶视频 vs 驾驶+行走混合视频；
  6. **组件消融**（表 3）：方向损失、特征幻觉、微调的影响；
  7. **分步时间步长 AOE**（表 4）：AOE(1)–AOE(5) 与 MAOE 对比。

## 4. 资源与算力

- 论文正文**未明确说明**使用的 GPU 型号、数量、训练时间、显存等具体算力信息。
- 仅在致谢中提及使用“NYU IT 高性能计算资源、服务和专家支持”，但无量化细节。
- 数据流水线方面，作者强调使用视觉里程计处理 2000 小时视频**所需墙钟时间可忽略不计**，且易于并行化，但未给出具体 GPU 时数或机器规模。

## 5. 实验数量与充分性

- **实验数量较丰富**：包括离线评估（表 1）、真实世界部署（表 2）、数据规模曲线（图 6）、训练损失分析（图 7）、组件消融（表 3）、时间步误差分析（表 4）等，基本覆盖了方法有效性的核心论证。
- **充分性与客观性分析**：
  - 优点：既有标准离线指标又有真实部署成功率；关键场景分类细致；消融实验覆盖损失函数和微调；数据规模实验有力支撑“可扩展性”主张。
  - 不足：
    1. **真实部署规模较小**：每个方向仅 8–14 次试验，统计显著性有限；
    2. **专家数据仅来自纽约市**，地域多样性不足；
    3. **消融实验差异不大**（MAOE 15.16–17.03），部分改进在误差范围内，作者自己也承认“marginal”；
    4. **未测试 CoNVOI**（近期相关工作），削弱了与 SOTA 的全面对比；
    5. **关键场景定义依赖启发式规则**（如行人检测框大小、人数阈值），可能不够精确；
    6. 离线测试中“到达率”与真实部署成功率的定义不一致（离线为二分类预测 vs 实部署为 5m 距离判断），可能影响可比较性。

## 6. 主要结论与发现

- **CityWalker 在真实城市环境中显著优于现有方法**：离线基准（表 1）中，微调模型在大多数场景和指标上达到最好；真实部署（表 2）中总体成功率 77.3%，远高于微调 ViNT 的 57.1%、零样本 ViNT 的 37.7% 和零样本 NoMaD 的 42.9%。
- **零样本 CityWalker 也表现优异**：在离线任务中可与微调后的基线相当或更好，证明大规模预训练的有效性，也说明人类行走视频与四足机器人之间存在领域间隙但可迁移。
- **数据规模定律成立**：训练数据从 250 小时增加到 2000 小时，MAOE 持续下降；超过 1000 小时训练后，零样本模型性能已超过微调 ViNT。
- **跨域数据融合有增益**：仅用 250 小时驾驶+行走混合数据几乎达到 1000 小时行走数据的性能，说明多样性和跨域数据能带来更强的泛化能力。
- **特征幻觉损失在微调阶段有益**：虽然纯预训练零样本时该损失可能因领域差距造成轻微负面效果，但在微调后不再存在问题，且训练损失曲线显示其能加速收敛、降低最终误差。
- **时间步预测稳定性好**：CityWalker 的多步预测误差不随步数增长而明显退化（而 ViNT 会），这有助于真实导航中平稳执行。

## 7. 优点

- **数据驱动、可扩展**：直接从网络视频提取动作标签，避免人工标注，且 VO 方案可并行化，成本极低，适合扩展到任意规模数据。
- **跨域跨形态泛化**：统一归一化动作空间使同一策略可同时从行走和驾驶视频学习，并能迁移到四足机器人，展示了显著的跨 embodiment 能力。
- **方法简洁高效**：无需 VLM、无需仿真、无需强化学习，仅用冻结视觉编码器 + 轻量 Transformer + 辅助特征预测损失即可实现优越性能。
- **评估细致**：提出 AOE/MAOE 指标并针对关键场景（转弯、穿越、绕行、拥挤等）分别评估，比单一 L2 或成功率更能反映导航质量。
- **真实部署验证**：不仅做离线评估，还在真实纽约市街道上部署四足机器人，对比基线，证明实际可行性。

## 8. 不足与局限

- **算力细节缺失**：未报告 GPU 型号、数量、训练时长，影响可复现性和成本评估。
- **真实测试规模有限**：每个转向类型仅 8–14 次试验，样本量较小，误差范围可能较大，结论的统计稳健性有待加强。
- **传感器与硬件依赖**：当前实现依赖 iPhone 的 GPS 定位（噪声大），且需要 VO/LiDAR 真值辅助；在 GPS 信号差的场景（城市峡谷、室内）可能失效。
- **场景覆盖仍有限**：专家数据仅来自纽约市，网络视频虽多样但主要以北美城市为主，对完全不同的道路结构、文化交通规范可能泛化不足。
- **特征幻觉损失存在两面性**：在跨 domain 预训练时可能引入误导信号，需要依赖微调来修正，说明该方法对训练阶段较为敏感。
- **消融效果微弱**：方向损失和特征幻觉损失的增益较小（MAOE 差异 < 0.1°），其单独贡献难以确认，需要更大规模或更精细的消融验证。
- **基线对比不完整**：未与 CoNVOI 等工作比较；且基线模型原本面向的目标设定（image-goal）与本任务的 waypoint-goal 不完全一致，虽然作者进行了适配，仍可能存在不公平因素。
- **到达率预测作为指标的偏差**：离线“到达率”是模型预测是否到达，而真实部署的成功率由距离阈值判定，两者并不完全对应，可能导致离线结果与实部署结论存在细微差异。

（完）
