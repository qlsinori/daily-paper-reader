---
title: "CityWalker: Learning Embodied Urban Navigation from Web-Scale Videos"
title_zh: CityWalker：从大规模网络视频学习具身城市导航
authors: "Liu, Xinhao, Li, Jintong, Jiang, Yicheng, Sujay, Niranjan, Yang, Zhicheng, Zhang, Juexiao, Abanes, John, Zhang, Jing, Feng, Chen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_CityWalker_Learning_Embodied_Urban_Navigation_from_Web-Scale_Videos_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 利用网络视频学习具身城市导航
tldr: 现有视觉导航方法在无地图或离路场景中表现受限，制约了自主代理的实际部署。本文提出CityWalker，通过从大规模网络城市行走与驾驶视频中提取动作监督，以模仿学习训练具身导航代理，无需人工标注。在真实与模拟环境中实验验证了其在复杂动态场景下的导航能力，为免地图城市导航提供了一条可扩展的数据驱动路线。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1781, \"height\": 563}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 838}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 853, \"height\": 462}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 331}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1691, \"height\": 847}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 774, \"height\": 478}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 743, \"height\": 454}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1444, \"height\": 748}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 253}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 692, \"height\": 355}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-citywalker-learning-embodied-urban-navigation-from-web-scale-videos-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 223}]"
motivation: 现有视觉导航方法在无地图或离路环境中表现不佳，限制了城市自主代理的部署。
method: 从互联网城市视频中提取动作监督，构建无需标注的大规模模仿学习流程训练导航模型。
result: 在真实世界与模拟环境中验证了方法有效性，实现了类人的城市导航行为。
conclusion: 提供了一种数据驱动的可扩展免地图城市导航范式。
---

## Abstract
Navigating dynamic urban environments presents significant challenges for embodied agents, requiring advanced spatial reasoning and adherence to common-sense norms. Despite progress, existing visual navigation methods struggle in map-free or off-street settings, limiting the deployment of autonomous agents like last-mile delivery robots. To overcome these obstacles, we propose a scalable, data-driven approach for human-like urban navigation by training agents on thousands of hours of in-the-wild city walking and driving videos sourced from the web. We introduce a simple and scalable data processing pipeline that extracts action supervision from these videos, enabling large-scale imitation learning without costly annotations. Our model learns sophisticated navigation policies to handle diverse challenges and critical scenarios. Experimental results show that training on large-scale, diverse datasets significantly enhances navigation performance, surpassing current methods. This work shows the potential of using abundant online video data to develop robust navigation policies for embodied agents in dynamic urban settings.

---

## 论文详细总结（自动生成）

# CityWalker：从大规模网络视频学习具身城市导航（CVPR 2025）中文总结

## 1. 论文的核心问题与整体含义
- **问题背景**：在城市动态环境中进行具身导航（Embodied Urban Navigation）极具挑战性，移动代理（如最后一公里配送机器人、无人出租车）需要在无地图或离路场景下具备空间推理能力和遵守常识规范（如走人行道、等红绿灯、保持社交距离）的能力。
- **现有方法的不足**：传统 SLAM+模块化方法依赖地图；基于模拟器的强化学习难以处理真实世界的动态障碍物与行人；基于遥操作数据的模仿学习受限于数据规模和多样性，难以泛化。
- **核心思路**：利用互联网上大规模的城市步行和驾驶视频（2000+ 小时），通过视觉里程计提取动作监督，以模仿学习方式训练导航策略，无需人工标注，实现可扩展的数据驱动解决方案。
- **整体含义**：该工作证明“网络视频数据”可以作为训练具身导航策略的高效来源，为免地图的复杂城市导航提供了一条可扩展的路线。

## 2. 方法论
- **核心思想**：构建一个端到端导航策略模型，输入过去 5 帧 RGB 观测、过去 5 个位置和当前目标路点，输出未来 5 步动作和到达状态。
- **动作标签生成**：使用现成的视觉里程计（DPVO）从网络视频中提取相对位姿，作为模仿学习的伪标签；通过“按轨迹平均步长归一化”克服尺度歧义，统一了步行与驾驶视频的动作空间。
- **模型架构**：
  - 图像编码器：冻结的 DINOv2（提取视觉特征）。
  - Transformer：处理图像 token 和坐标 token 的时间序列。
  - 动作头与到达头：MLP 解码出预测动作和到达概率。
  - 特征幻觉辅助损失（Feature Hallucination）：将 Transformer 输出的未来 token 与真实未来帧的 DINOv2 特征做 MSE 回归，促进信息性未来表征的学习。
- **损失函数**：总损失为 L1 动作损失、方向损失（负余弦相似度）、到达状态 BCE 损失和特征幻觉损失的加权和。
- **关键设计**：仅使用短时间窗口内的相对位姿，规避 VO 全局累积漂移问题；训练时依赖大规模视频数据，微调时仅需少量专家数据即可在目标机器人上落实。

## 3. 实验设计
- **训练数据**：
  - 网络来源的 2000+ 小时城市行走视频，覆盖不同地区、天气和时段。
  - 另加入驾驶视频进行跨域/跨本体训练。
- **专家数据（离线测试/微调）**：在纽约多个区域通过 Unitree Go1 四足机器人采集 15 小时遥操作数据，其中 6 小时用于微调，9 小时用于离线测试；使用 LiDAR-SLAM（FAST-LIO）获得真值动作，手机获取 GPS。
- **关键场景定义**（不互斥）：
  - Turn：动作方向变化 >20°。
  - Crossing：检测到红绿灯（置信度 >0.5）。
  - Detour：动作方向与目标方向偏差 >45°。
  - Proximity：检测到的最大人体框占图像面积 >25%。
  - Crowd：检测到 ≥5 个人。
- **对比方法**：GNM、ViNT、NoMaD（部分方法进行微调），以及本文模型的 zero-shot 和 fine-tuned 版本；另外提及 CoNVOI（因未开源不能测试）和 VLM-based 方法见附录。
- **评估方式**：
  - 离线：平均方向误差（AOE）、最大平均方向误差（MAOE）、L2 距离、到达准确率，按场景均值统计。
  - 真实部署：在未见过环境中的导航成功率（目标距离 50–100m，5m 内判定到达），分为直行、左转、右转案例。

## 4. 资源与算力
- 论文**未明确说明**使用的 GPU 型号、数量或具体训练时长。
- 仅在图表说明中提到：所有模型训练 10 个 epochs；不同数据量使用的 batch size 不同。
- 作者强调数据处理管线可并行化，处理 2000 小时视频仅需“可忽略的墙钟时间”（相对成本极低），但未给出具体硬件/算力数字。

## 5. 实验数量与充分性
- **实验组数量**：
  - 离线基准测试：5 个方法 × 6 个场景 × 3 个指标。
  - 真实部署：3 类转向场景 × 多个试验（每类 8–14 次）。
  - 数据规模实验：不同视频小时数（250/1000/2000 等）的 zero-shot 曲线。
  - 消融研究：方向损失、特征幻觉损失、微调三项的贡献。
  - 跨域实验：仅驾驶视频、驾驶+行走视频混合训练的对比。
  - 不同预测时间步（1–5）的 AOE 分析。
- **充分性与客观性**：
  - 实验设计较为全面，涵盖了性能、数据规模、跨本体、消融和真实部署。
  - 但离线测试数据仅来自纽约市，场景多样性有限；特征幻觉和方向损失的消融增益很小，作者承认在误差范围内。
  - 与最强基线 ViNT 的对比在同一环境中进行，但未与 CoNVOI 等近期相关工作比较（因开源限制），公平性受到一定影响。

## 6. 主要结论与发现
- 大规模网络视频训练显著提升了城市导航性能：微调后的 CityWalker 在离线基准和真实部署中均优于 GNM、ViNT、NoMaD。
- 真实部署成功率：CityWalker 77.3%，优于 ViNT fine-tuned（57.1%）和 NoMaD zero-shot（42.9%）。
- 数据规模效应：超过 1000 小时视频训练后，zero-shot 模型即可超过微调后的 ViNT，说明数据规模的重要性。
- 跨域/跨本体：仅用驾驶视频训练的模型性能接近 zero-shot 基线；混合驾驶+行走视频显著提升性能，250 小时混合数据几乎达到 1000 小时步行数据的水平，体现出通用性和鲁棒性。
- 特征幻觉损失：zero-shot 时反而略降，但微调后带来正向收益，并降低了训练损失（尤其是方向损失）。
- 多步预测能力：CityWalker 的 AOE 在各预测步上更稳定，而 ViNT 的误差随时间步增加而增大，这解释了真实部署中的优势。

## 7. 优点
- **数据驱动、免标注**：使用视觉里程计从网络视频中自动生成动作标签，避免了昂贵的遥操作或 VLM 提示成本，具有良好的扩展性。
- **统一动作空间**：通过步长归一化，使步行与驾驶视频可协同训练，支持跨域、跨本体迁移（如驾驶视频用于四足机器人）。
- **放大性能**：清晰展示了“数据量 → 性能”的规模律，为后续研究提供了有力证据。
- **面向真实场景**：设计了关键场景（转弯、过街、绕行、近人、人群）及相应评价指标，更贴近复杂城市导航的实际需求。
- **真实部署验证**：使用四足机器人在纽约市区进行多场景导航测试，结果表明在转弯等动态难点场景中优势明显。

## 8. 不足与局限
- **环境覆盖有限**：离线测试和真实部署均局限于纽约市，网络视频虽“多地区”但未明确分析地域/天气/时段覆盖是否均衡，泛化性存在疑问。
- **GPS 噪声敏感**：作者指出当前实现受 iPhone 定位噪声影响较大，限制了实际应用的稳定性。
- **关键场景定义依赖检测器**：红绿灯、行人检测的阈值设定可能引入偏差，且场景互有重叠、比例不均衡。
- **消融增益有限**：方向损失和特征幻觉损失在离线指标上的贡献边际化，作者仅以训练损失趋势作为补充依据，说服力有限。
- **基线覆盖不足**：未能与同期的 CoNVOI 等上下文感知方法进行比较（因代码未开源），削弱了对比完整性。
- **未提供算力细节**：缺少 GPU 型号、数量、训练耗时等可重复性信息，不利于复现。
- **无安全/失败分析**：真实部署中将所有人类干预（碰撞风险或超时）视为失败，但未提供失败模式分析或安全性保障机制。

（完）
