---
title: "CityWalker: Learning Embodied Urban Navigation from Web-Scale Videos"
title_zh: CityWalker：从网络规模视频学习具身城市导航
authors: "Liu, Xinhao, Li, Jintong, Jiang, Yicheng, Sujay, Niranjan, Yang, Zhicheng, Zhang, Juexiao, Abanes, John, Zhang, Jing, Feng, Chen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_CityWalker_Learning_Embodied_Urban_Navigation_from_Web-Scale_Videos_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 具身城市导航；从网络规模视频学习；模仿学习
tldr: 针对具身智能体在无地图或非道路场景下难以导航的问题，提出从网络大规模行走和驾驶视频中学习导航策略的数据驱动方法。通过可扩展的视频处理流程提取动作监督，无需昂贵标注即可进行大规模模仿学习，使智能体学会类人的城市导航行为。该工作为户外具身导航提供了低成本、规模化的训练途径。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1781, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 838, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 853, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1691, \"height\": 847, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 774, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 743, \"height\": 454, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 748, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 692, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 223, \"label\": \"Table\"}]"
motivation: 现有视觉导航方法在无地图或非道路的城市场景中表现不佳，且标注成本高。
method: 利用大规模网络视频，通过可扩展流程提取动作监督，进行模仿学习训练导航模型。
result: 模型在动态城市环境中学习到复杂的导航行为，无需地图即可泛化。
conclusion: 大规模网络视频数据可为具身城市导航提供高效、低成本的学习范式。
---

## Abstract
Navigating dynamic urban environments presents significant challenges for embodied agents, requiring advanced spatial reasoning and adherence to common-sense norms. Despite progress, existing visual navigation methods struggle in map-free or off-street settings, limiting the deployment of autonomous agents like last-mile delivery robots. To overcome these obstacles, we propose a scalable, data-driven approach for human-like urban navigation by training agents on thousands of hours of in-the-wild city walking and driving videos sourced from the web. We introduce a simple and scalable data processing pipeline that extracts action supervision from these videos, enabling large-scale imitation learning without costly annotations. Our model learns sophisticated navigation policies to handle diverse challenges and critical scenarios. Experimental results show that training on large-scale, diverse datasets significantly enhances navigation performance, surpassing current methods. This work shows the potential of using abundant online video data to develop robust navigation policies for embodied agents in dynamic urban settings.

---

## 论文详细总结（自动生成）

## CityWalker 论文详细总结

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：具身智能体（如四足机器人、配送机器人）如何在**无地图（map-free）或非道路（off-street）** 的**动态城市环境**中实现安全、类人的导航。
- **研究动机**：
  - 城市环境具有动态、不可预测的特点，包含多样地形、密集行人、复杂障碍物和交通信号；导航不仅需要空间推理，还需要遵守常识性社会规范（如走人行道、遵守交通信号、保持人际距离）。
  - 现有视觉导航方法在**静态室内环境**或**仿真器**中表现优异，但在真实城市环境中泛化能力不足。
  - 通过遥操作收集专家轨迹数据的方法受限于**数据规模小、多样性不足**，难以覆盖复杂城市场景。
  - 受语言、视觉和机器人领域**规模定律（scaling law）** 的启发，作者探索是否可以利用**互联网上大量现成的城市行走/驾驶视频**来训练导航策略。
- **整体含义**：该工作验证了"利用网络规模视频数据训练具身导航策略"这一范式的可行性，为户外具身导航提供了低成本、可扩展的学习路径。

---

### 2. 方法论

#### 2.1 核心思想

- 从互联网收集**2000+小时的户外城市行走和驾驶视频**（第一人称视角），利用**视觉里程计（Visual Odometry, VO）** 自动提取动作标签，无需繁琐的人工标注，即可进行大规模模仿学习。
- 任务建模为**真实城市场景下的点目标导航（point-goal navigation）**：智能体在相邻两个路点之间自主导航，路点由导航工具（如 Google Maps）提供，智能体需判断何时到达当前子目标并规划局部动作。

#### 2.2 关键公式

- **问题形式化**：学习策略 π(aₜ | o₍ₜ₋ₖ₎:ₜ, p₍ₜ₋ₖ₎:ₜ, wₜ)，其中 o 为 RGB 观测，p 为 GPS 位置，w 为子目标路点，a 为动作（欧氏空间中的一系列动作路点）。通常取 k=5，同时预测未来 5 步动作。
- **平均方向误差（AOE）指标**：
  - AOE(k) = (1/n) Σᵢ θᵢₖ = (1/n) Σᵢ arccos(⟨âᵢₖ, aᵢₖ⟩ / (‖âᵢₖ‖‖aᵢₖ‖))
  - 最大平均方向误差（MAOE）= (1/n) Σᵢ maxₖ θᵢₖ
- **方向损失函数（Orientation Loss）**：
  - L_ori = −(1/k) Σᵢ₌₁ᵏ ⟨âᵢ, aᵢ⟩ / (‖âᵢ‖‖aᵢ‖)
- **总损失函数**（四个损失的加权和）：
  - L = ω_l1·L_l1 + ω_ori·L_ori + ω_arr·L_arr + ω_feat·L_feat

#### 2.3 关键技术细节

- **数据标签提取**：使用 DPVO 等视觉里程计工具从视频中提取相对位姿。针对 VO 的两个问题——全局累积误差和尺度歧义——提出解决方案：
  - 仅使用**短时间窗口内的相对位姿**（预测 5 帧历史 + 5 帧未来），规避累积误差；
  - 将每个动作按**轨迹内平均步长归一化**，解决尺度不一致（步行 vs 驾驶）问题。
- **模型架构**（基于 ViNT/NoMaD 的框架）：
  - 核心为 **Transformer**，处理时间序列输入 token（5 帧图像特征 + 1 个坐标嵌入）；
  - 图像编码器使用**冻结的 DINOv2**；
  - Action Head 预测动作，Arrival Head 预测是否到达目标；
  - **特征幻觉（Feature Hallucination）**：计算未来帧 token 与直接从未来帧提取的 DINOv2 特征的 MSE 损失，引导 Transformer 生成更具信息量的未来 token，作为辅助训练信号。
- **可扩展性与跨域性**：
  - 数据管线可并行化，处理 2000 小时视频的耗时可忽略不计，成本极低；
  - 可扩展到任意带自我运动的视频（如驾驶视频）；支持跨域、跨具身零样本部署或微调。

---

### 3. 实验设计

#### 3.1 数据集

| 数据集 | 来源 | 用途 | 规模 |
|---|---|---|---|
| 城市行走视频 | 互联网（不同地理位置、天气、光照） | 预训练 | 2000+ 小时 |
| 驾驶视频 | 互联网 | 跨域训练/消融 | 与行走视频混合使用时数据量显著下降 |
| 专家遥操作数据 | 纽约市多区域（Unitree Go1 四足机器人 + Livox Mid-360 LiDAR + 网络摄像头） | 微调与离线测试 | 15 小时（6 小时微调 + 9 小时测试） |

#### 3.2 基准（Benchmark）

- **离线评估**（基于遥操作数据的真实轨迹）：在以下**关键场景（Critical Scenarios）** 中计算 L2 距离、MAOE（最大平均方向误差）、Arrival 成功率：
  - Turn（转弯）：动作方向变化 > 20°
  - Crossing（过路口）：检测到红绿灯
  - Detour（绕行）：动作角与目标角偏差 > 45°
  - Proximity（近距离）：最近的检测行人边界框 > 图像面积 25%
  - Crowd（人群）：检测到 ≥ 5 人
  - Other（其他场景）
- **真实世界部署**：在未见过的城市区域，目标距离起点 50–100m，分为**直行、左转、右转**三类，以距离目标 5m 内是否到达判定成功。

#### 3.3 对比方法

- **GNM**（General Navigation Model，微调）
- **ViNT**（Visual Navigation Transformer，零样本 + 微调）
- **NoMaD**（零样本）
- **CityWalker（Ours）**：零样本 + 微调

---

### 4. 资源与算力

- **论文未明确报告**使用的 GPU 型号、数量或具体训练时长。
- 仅作者提到在 NYU IT 高性能计算资源下完成实验。
- 关于数据处理的算力成本有相关说明：由于采用视觉里程计（VO）而非 VLM 提示，数据处理管线可高度并行化，"处理 2000 小时视频数据所需的墙钟时间可忽略不计"，这暗示训练数据扩展的计算成本极低，但训练所需的 GPU 资源未披露。

---

### 5. 实验数量与充分性

#### 实验组数（论文中的实证研究）

| 实验 | 内容 | 目的 |
|---|---|---|
| 离线基准测试（Table 1） | 3 个基线 + Ours（零样本/微调）在 6 类场景、3 个指标上的完整对比 | 回答 Q1：能否在城市环境成功导航 |
| 真实世界部署（Table 2） | ViNT（零样本/微调）、NoMaD（零样本）、Ours（微调）在直行/左转/右转的成功率（每类 8–14 次试验） | 验证真实环境性能 |
| 数据规模扩展（Fig. 6） | 不同训练数据量（约 250–2000 小时）下的 MAOE 曲线 | 回答 Q2：数据规模的影响 |
| 跨域/跨具身（Fig. 6） | 仅驾驶视频、驾驶+行走混合视频的零样本表现 | 验证管线通用性 |
| 特征幻觉损失消融（Fig. 7 + Table 3） | 有无特征幻觉损失的训练曲线对比 + 完整消融（方向损失/特征幻觉/微调各组件） | 回答 Q3：各组件贡献 |
| 不同预测时步 AOE 分析（Table 4） | AOE(1)–AOE(5) 及 MAOE 的逐步分析 | 分析多步预测稳定性 |

#### 充分性与公平性评估

- **优点**：实验层次较为完整，覆盖了离线→真实部署、单体→跨域扩展、整体性能→组件消融，形成了较为完整的技术验证链条。
- **不足**：
  - 真实世界部署试验次数较少（每类约 10 次），统计显著性有限；
  - 关键场景分类依赖检测器的阈值，可能存在分类噪声；
  - 离线评估与真实部署之间存在 gap，真实部署仅报告了成功率，缺少 MAOE 等更细粒度的指标；
  - 基线方法的帧率、相机标定等实现细节未在正文中披露（可能在附录），公平性存在一定不确定性；
  - 作者承认未与 CoNVOI 等 VLM 方法直接对比（因缺开源代码）。

---

### 6. 主要结论与发现

1. **训练规模效应显著**：在 1000+ 小时视频上训练的零样本模型，其性能已超过微调后的 ViNT 基线，表明"网络规模数据可以部分替代专家微调"。
2. **性能全面领先**：CityWalker（微调）在离线基准的所有场景和指标上均优于现有基线（仅 Detour 场景稍弱），真实部署成功率 77.3%，远超第二名 ViNT 微调模型的 57.1%。
3. **跨域/跨具身泛化**：仅用驾驶视频训练的模型已达到与零样本基线相当的水平；混合行走+驾驶数据后性能大幅提升——仅 250 小时混合数据即可接近 1000 小时纯行走数据的效果。
4. **多步预测更稳定**：与 ViNT 的 AOE 随预测步长递增不同，CityWalker 在 2–5 步预测中保持较稳定的 AOE，有助于真实导航中的稳定动作执行。
5. **微调带来增益**：由于专家数据与预训练数据域差异较大（行人视角 vs 四足视角），微调对最终部署性能提升明显。
6. 特征幻觉损失在零样本推理中反而略损性能，但在微调后恢复正向作用；训练曲线显示该损失可降低总损失和方向损失。

---

### 7. 优点

- **数据可扩展性突出**：提出使用低成本的视觉里程计（VO）生成伪标签，无需昂贵的 VLM 提示或人工标注；2000 小时视频的处理对墙钟时间几乎无压力，相比 VLM 手段大大降低了规模化门槛。
- **问题选择有价值**：准确定位了"路点间导航"这一痛点——准确路点已由导航工具提供，难点在于智能体在两路点间的实时决策，该问题定义清晰且紧贴真实应用。
- **关键场景导向的评估体系**：定义了 Turn、Crossing、Detour、Proximity、Crowd 等关键场景，并引入 **MAOE** 指标替代传统 L2 距离，更能反映对导航成败影响重大的方向性错误。
- **跨域、跨具身验证**：通过驾驶视频→四足机器人的跨域实验，展示出数据管线的通用性；混合数据后的性能增益进一步验证了跨领域数据融合的价值。
- **方法简洁实用**：遵循了"大规模数据 + 简单管线 + 少量微调"的范式，模型架构本身基于成熟的 ViNT 框架，聚焦点在于数据，而非复杂的算法设计。

---

### 8. 不足与局限

- **GPS 定位噪声敏感**：作者明确指出，在实际部署中，iPhone 定位服务的读数噪声较大，系统对位置噪声敏感，可通过更好的 GPS 硬件改善——这说明系统的鲁棒性尚未完全解决。
- **部分场景覆盖不足**：Detour（绕行）场景的表现最弱，作者将其归因于训练视频中此类数据比例偏低，显示数据分布的偏差会直接影响模型能力。
- **真实世界实验规模有限**：仅在纽约市特定区域部署，未覆盖不同的城市、交通文化和地理环境；单类试验数量约 10 次，统计意义有限。
- **特征幻觉损失存在域适配问题**：零样本阶段，该辅助损失因行人视角与机器人视角的域差异而略微有害；这表明辅助任务的损失设计需随预训练数据与部署域的适配程度调整。
- **基线对比条件不完美**：基准设置本来是"图像目标导航"任务，而本文是点目标导航，可能需要改造适配；ViNT 等基线在不同任务设定下的公平性仍有讨论空间。
- **缺少与最相关工作的直接比较**：作者承认无法与 CoNVOI 对比（开源缺失），也未与同期的 LeLaN 等方法进行定量对比，削弱了对比的全面性。
- **训练算力信息缺失**：未报告 GPU 型号、数量和训练时长，不利于复现和衡量方法的经济成本。

---

（完）
