---
title: "NavA3: Understanding Any Instruction, Navigating Anywhere, Finding Anything"
title_zh: NavA3：理解任意指令、随处导航、找到任何目标
authors: "Lingfeng Zhang, Xiaoshuai Hao, Yingbo Tang, Haoxiang Fu, Xinyu Zheng, Pengwei Wang, Zhongyuan Wang, Wenbo Ding, Shanghang Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.37.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 长时间跨度导航，高层级指令理解，开放词汇目标导航
tldr: 该文指出现有导航任务局限于预定义物体或指令跟随，与真实开放场景需求差距较大。为此提出NavA3任务，要求智能体在真实环境中理解高层级人类指令并进行空间感知的开放词汇目标导航。作者还分析现有方法在此任务上的不足，推动具身导航向复杂开放场景发展。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long37/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1553, \"height\": 783, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long37/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1532, \"height\": 694, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long37/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1525, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long37/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1505, \"height\": 541, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long37/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1562, \"height\": 652, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long37/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1498, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long37/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 793, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long37/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 785, \"height\": 373, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long37/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 810, \"height\": 387, \"label\": \"Table\"}]"
motivation: 真实世界需要智能体理解高层级指令并定位开放词汇目标，而现有导航任务定义过于狭窄。
method: 提出NavA3长期导航任务与相应方法，结合高层级指令理解与开放词汇空间目标导航。
result: 揭示现有具身导航方法在高层指令和开放目标定位上的局限，并提供新任务促进研究。
conclusion: 面向真实开放场景的长期指令导航是具身智能的重大挑战，需要语义理解与目标定位协同。
---

## Abstract
Embodied navigation is a fundamental capability of embodied intelligence, enabling robots to move and interact within physical environments. However, existing navigation tasks primarily focus on predefined object navigation or instruction following, which significantly differs from human needs in real-world scenarios involving complex, open-ended scenes. To bridge this gap, we introduce a challenging long-horizon navigation task that requires understanding high-level human instructions and performing spatial-aware object navigation in real-world environments. Existing embodied navigation methods struggle with such tasks due to their limitations in comprehending high-level human instructions and localizing objects with an open vocabulary. In this paper, we propose NavA 3 , a hierarchical framework divided into two stages: global and local policies. In the global policy, we leverage the reasoning capabilities of Reasoning-VLM to parse high-level human instructions and integrate them with global 3D scene views. This allows us to reason and navigate to regions most likely to contain the goal object. In the local policy, we have collected a dataset of 1.0 million samples of spatial-aware object affordances to train the NaviAfford model (PointingVLM), which provides robust open-vocabulary object localization and spatial awareness for precise goal identification and navigation in complex environments. Extensive experiments demonstrate that NavA 3 achieves SOTA results in navigation performance and can successfully complete long-horizon navigation tasks across different robot embodiments in real-world settings, paving the way for universal embodied navigation. The dataset and code will be made available.

---

## 论文详细总结（自动生成）

# NavA3 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **现有导航任务的局限性**：当前具身导航研究主要分为两类——视觉语言导航（VLN）和目标导航（ObjectNav）。VLN 依赖逐步的详细指令（如“左转，出门，直走”），与人类自然交互习惯不符；ObjectNav 则仅需定位预定义类别（如“找到任意椅子”），忽略了空间上下文和具体需求。
- **真实世界需求与现有任务之间的鸿沟**：人类在实际场景中往往提出高层级意图指令，例如“我想喝一杯咖啡”或“我想吃茶室左边的水果”。这类指令不仅需要理解潜在目标，还涉及物体间的空间关系推理，而现有方法无法有效处理。
- **论文提出的新任务**：论文引入了一个**长时程（long-horizon）导航任务**，要求智能体在真实开放场景中理解高层级人类指令，并完成**开放词汇（open-vocabulary）的、具有空间感知的目标导航**。
- **核心意义**：这项工作试图弥合具身导航与人类真实需求之间的差距，推动具身智能从低层指令跟随向高层意图理解与复杂空间导航演进。

## 2. 论文提出的方法论

### 2.1 核心思想
- 论文提出 **NavA3** 框架，采用**层级式“全局-局部”两阶段策略**：
  - **全局策略**：使用 **Reasoning-VLM**（基于 GPT-4o）解析高层级人类指令，结合带注释的全局 3D 场景图，推理出目标物体以及最可能包含该物体的区域。
  - **局部策略**：使用 **NaviAfford 模型**（即 Pointing-VLM，基于 Qwen2.5-VL-7B 微调），在全景 RGB 观测和局部地图中搜索目标物体，输出目标点的像素坐标，并转换为机器人坐标系以完成精确导航。

### 2.2 关键技术与公式

**（1）3D 场景构建**
- 使用 LiDAR 传感器采集多视角 RGB 图像，通过 2D 到 3D 重建管线生成稠密点云 $P = \{p_i \in \mathbb{R}^3\}_{i=1}^{N}$。
- 将重建的 3D 场景转为俯视图（top-down view）。全局策略使用 MapNav 的注释方法添加房间级语义标注（如“茶室”“会议室”“阳台”），表示为 $S_{global} = \{R_j, A_j\}_{j=1}^{M}$；局部策略使用无标注的局部俯视图 $M_{local}$。

**（2）全局策略（Reasoning-VLM）**
- 通过结构化提示词模板引导 VLM 进行层次化推理：
  - 首先进行语义分解，推断目标物体 $O^* = f_{semantic}(I)$；
  - 然后分析空间语义关系，确定最有可能的目标区域 $R^* = \arg\max_{R_j \in S_{global}} P(O^* | R_j, A_j)$；
  - 最后在目标区域内随机采样一个航点，交由局部策略执行精确搜索。

**（3）局部策略（NaviAfford 模型）**
- **训练数据**：构建了约 5 万张图片、100 万组问答对的空间感知物体可供性数据集，来源包括 LVIS 和 Where2Place 数据集。将实例分割掩码转换为边界框坐标，并在每个框内采样 5–8 个代表性点以增强空间粒度。
- **两类可供性标注**：
  - **物体可供性（Object Affordance）**：计算方向关系（上下左右等），定位特定上下文中的目标物体；
  - **空间可供性（Spatial Affordance）**：识别满足约束条件的可用空间，用于导航与放置。
- **模型架构**：$Model(Q, V) = f_{LLM}(f_{text}(Q), f_{proj}(f_{vision}(V)))$，采用监督微调（SFT），损失函数为交叉熵：$L = -\sum_{i=1}^{N} \log P(t_i | t_{<i}, Q, V)$。
- **像素坐标到机器人坐标转换**：
  - 利用相机内参将像素坐标 $(u,v)$ 与深度 $d$ 转为相机坐标：$X = \frac{(u-c_x) \cdot d}{f_x}, Y = \frac{(v-c_y) \cdot d}{f_y}, Z = d$；
  - 再通过旋转矩阵和平移向量将相机坐标转换到世界/机器人坐标系：$[x_{world}; y_{world}] = R(\theta_r) [x_{robot}; y_{robot}] + [x_r; y_r]$，其中 $x_{robot} = Z_{cam}, y_{robot} = -X_{cam}$。
- **未检测到目标时的决策**：Reasong-VLM 分析局部 3D 场景和历史探索数据，决定继续探索当前区域或切换到新的房间/空间。

## 3. 实验设计

### 3.1 数据集与 Benchmark
- **导航任务 Benchmark**：包含 5 个真实场景——Meeting Room A、Meeting Room B、Tea Room、Workstation、Balcony，共 **50 个任务**（每个场景 10 个），每个任务执行 10 次 rollout 以降低随机性。人类专家定义高层级指令和唯一目标物体，并在 5 种不同起始位置下进行测试。
- **Pointing-VLM 评测**：使用 1,000 张未参与训练的图像进行可用性评估。

### 3.2 评估指标
- **导航误差（NE）**：智能体最终位置与目标的距离（米），越低越好。
- **成功率（SR）**：智能体到达目标 1 米范围内的导航事件百分比（Avg. SR）。
- **Pointing 指标**：预测点落在真实掩码内的比例（Acc）。

### 3.3 对比方法
- **闭源通用 VLM**：GPT-4o、Claude-3.5-Sonnet、Qwen-VL-Max；
- **开源通用 VLM**：Janus-Pro-7B、Qwen2.5-VL-7B、LLaVA-Next-7B；
- **导航专用方法**：NaVid、NaVILA、MapNav（对任务表述进行适配修改）；
- **Pointing 专用模型**：RoboPoint。

### 3.4 跨实体验证
- 系统部署于 **RealMan 轮式机器人**和 **Unitree Go2 四足机器人**，均配备 Intel RealSense D435i 相机进行 RGB-D 感知。

## 4. 资源与算力
- **GPU**：4 块 H100 GPU。
- **优化器**：AdamW，学习率 $10^{-5}$。
- **训练轮数**：1 个 epoch。
- **批大小**：每 GPU 4，梯度累积 2 步，有效批大小 32。
- **模型初始化**：NaviAfford 使用预训练的 Qwen2.5-VL-7B 权重、基于 LLaMAFactory 进行微调。
- **说明**：论文未披露具体训练时长。

## 5. 实验数量与充分性

### 5.1 实验组数
论文主要包含以下几组实验：
1. **主对比实验**：与 9 种基线方法在 5 个场景上的导航性能对比（表 1）；
2. **Annotation 消融**：4 种变体（w/o Map、w/o Annotation、w/o Room-level Annotation、Full Annotation）在 2 个场景上的对比（表 2）；
3. **Reasoning-VLM 消融**：7 种不同 VLM 作为全局策略的对比（表 3）；
4. **Pointing-VLM 消融**：9 种不同模型作为局部策略的对比（表 4）；
5. **定性分析**：包括 affordance 可视化和真实环境长时程导航及跨实体部署展示（图 5）。

### 5.2 充分性与客观性评估
- **优点**：消融设计比较系统，分别验证了 annotation 语义标注、Reasoning-VLM 推理能力和 Pointing-VLM 定位能力各自对整体性能的贡献；跨实体部署增强了结论的泛化性。
- **不足**：
  - 导航 benchmark 仅包含 5 个场景、50 个任务，规模相对有限，且场景类型偏向办公环境（会议室、茶室、工作台、阳台），缺乏住宅、商业等更多样化的场景覆盖；
  - 任务由“人类专家”定义，可能存在主观偏差；
  - 每个任务在不同起始位置进行 5 次测试、10 次 rollout，随机性控制较好，但总体测试次数（500 次导航）对于得出强统计结论而言仍有提升空间；
  - 缺少与真实人类表现或更多开源 SOTA 方法的对比。

## 6. 论文的主要结论与发现

- **NavA3 显著超越现有方法**：平均 SR 达到 66.4%，比最佳基线 MapNav（25.2%）提升 **41.2 个百分点**；NE 在各类场景中大幅下降（如会议室 A 从 7.21m 降至 1.23m）。
- **通用 VLM 在长时程导航任务上几乎失效**：GPT-4o（2.0%）、Claude-3.5-Sonnet（2.8%）等闭源模型和开源 7B 模型（0–0.4%）成功率极低，表明仅有强大语言推理能力不足以解决空间感知导航问题。
- **语义标注至关重要**：完整 annotation 比无标注变体平均 SR 提升 28–32%，说明区域级语义信息对高层推理有显著帮助。
- **Reasoning-VLM 的选择影响显著**：GPT-4o 作为推理器优于所有替代方案，而 7B 级开源模型的能力差距较大。
- **领域专用训练的 NaviAfford 优势明显**：在 affordance 理解上超过 RoboPoint 13.0%（70.8% vs. 55.9%），Nav SR 提高 10.5%；相比通用 VLM，优势更明显。
- **跨实体泛化能力初步验证**：系统在轮式机器人和四足机器人上均能完成任务，展示了一定的通用性。

## 7. 优点

- **问题定义具有现实意义**：将导航从低层指令跟随提升到高层意图理解与开放词汇目标定位，切中真实应用需求。
- **分层设计合理且清晰**：全局推理与局部定位解耦，兼具可解释性和模块化可替换性；每个模块可独立优化和替换。
- **大规模专用数据集贡献**：构建了 100 万组空间感知物体可供性问答对，为该方向后续研究提供了数据基础。
- **双维度 affordance 标注创新**：同时标注物体可供性和空间可供性，增强模型对空间关系的理解能力。
- **实验设计比较系统**：从主对比到三类消融再到跨实体部署，多层次验证了各组件贡献。
- **公式和方法描述具体**：坐标转换、损失函数、场景表示等关键环节均有明确的数学表达。

## 8. 不足与局限

- **对深度信息的依赖**：系统依赖 RGB-D 传感器的精确深度信息进行目标定位和坐标转换。在反光表面、透明物体或光线不佳的环境下，深度估计可靠性下降，可能影响导航精度。
- **模块化架构的延迟问题**：全局策略和局部策略相互独立而非端到端模型，高层推理与底层控制之间可能存在延迟，影响响应效率。
- **场景覆盖有限**：仅 5 个真实场景（50 个任务），缺乏大规模、多类型环境的基准测试，结论的外部效度有待验证；场景同质性较高，未涉及动态场景和未知环境。
- **动态环境适应性不足**：当前框架没有显式处理移动障碍物或环境布局变化的情况。
- **基线适配存在潜在偏差**：对于 NaVid、NaVILA、MapNav 等基线，需要修改任务表述以适应新任务，修改后的基线可能未达到最优性能，存在一定不公平比较风险。
- **Reasoning-VLM 依赖闭源模型**：GPT-4o 作为全局推理器取得了最好效果，但其闭源特性限制了系统的可复现性和完全自主部署。

## 附：论文元数据
- **标题**：NavA3: Understanding Any Instruction, Navigating Anywhere, Finding Anything
- **会议**：ACL 2026 Long Papers（第 64 届 ACL 年会，第 1 卷长文，第 868–878 页）
- **接收时间**：2026 年 7 月 2–7 日
- **作者单位**：清华大学深圳国际研究生院、北京智源人工智能研究院、新加坡国立大学、中科院自动化所、同济大学、小米汽车、北京大学多媒体信息处理国家重点实验室、鹏城实验室等

（完）
