---
title: "RoboSense: Large-scale Dataset and Benchmark for Egocentric Robot Perception and Navigation in Crowded and Unstructured Environments"
title_zh: RoboSense：面向拥挤非结构化环境中机器人第一视角感知与导航的大规模数据集与基准
authors: "Su, Haisheng, Song, Feixiang, Ma, Cong, Wu, Wei, Yan, Junchi"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Su_RoboSense_Large-scale_Dataset_and_Benchmark_for_Egocentric_Robot_Perception_and_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 7.0
evidence: 面向复杂环境的机器人第一视角感知与导航数据集与基准
tldr: 拥挤非结构化环境下的第一视角感知与自主导航是智能移动机器人的关键挑战，现有数据受遮挡和截断影响较大。本文搭建多传感器数据采集平台，构建了面向此类环境的RoboSense大规模数据集与基准，支持拥挤场景下的感知和导航研究。该工作为评估和提升复杂环境下移动机器人的具身感知与导航能力提供了新的评测基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 876, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 721, \"height\": 333, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 486, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1793, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1818, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 874, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 871, \"height\": 210, \"label\": \"Table\"}]"
motivation: 现有机器人在拥挤非结构化环境中的第一视角感知能力不足，缺少相应大规模数据与评测基准。
method: 搭建多传感器采集平台，构造RoboSense数据集和基准，覆盖复杂环境的感知与导航任务。
result: 提供大规模真实环境数据和标准评测，为该场景下的自主导航研究建立重要基础。
conclusion: RoboSense有助于推动拥挤非结构化环境下移动机器人的感知与导航技术发展。
---

## Abstract
Reliable embodied perception from an egocentric perspective is challenging yet essential for autonomous navigation technology of intelligent mobile agents. With the growing demand of social robotics, near-field scene understanding becomes an important research topic in the areas of egocentric perceptual tasks related to navigation in both crowded and unstructured environments. Due to the complexity of environmental conditions and difficulty of surrounding obstacles owing to truncation and occlusion, the perception capability under this circumstance is still inferior. To further enhance the intelligence of mobile robots, in this paper, we setup an egocentric multi-sensor data collection platform based on 3 main types of sensors (Camera, LiDAR and Fisheye), which supports flexible sensor configurations to enable dynamic sight of view from ego-perspective, capturing either near or farther areas. Meanwhile, a large-scale multimodal dataset is constructed, named RoboSense, to facilitate egocentric robot perception. Specifically, RoboSense contains more than 133K synchronized data with 1.4M 3D bounding box and IDs annotated in the full 360^ \circ view, forming 216K trajectories across 7.6K temporal sequences. It has 270xand 18xas many annotations of surrounding obstacles within near ranges as the previous datasets collected for autonomous driving scenarios such as KITTI and nuScenes. Moreover, we define a novel matching criterion for near-field 3D perception and prediction metrics. Based on RoboSense, we formulate 6 popular tasks to facilitate the future research development, where the detailed analysis as well as benchmarks are also provided accordingly. Data desensitization measures have been conducted for privacy protection.

---

## 论文详细总结（自动生成）

# RoboSense 论文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：自动驾驶领域已取得显著进展，但面向**社交移动机器人**（如清扫车、配送机器人、零售机器人等）在**拥挤且非结构化环境**（如校园、公园、广场、人行道、景区等）中的自主导航仍面临巨大挑战。现有感知数据集（如 KITTI、nuScenes、Waymo）均针对自动驾驶场景采集，数据来源于结构化道路，缺少面向机器人在复杂社会环境中第一视角（egocentric）感知的大规模数据集与评测基准。
- **核心问题**：在拥挤非结构化环境中，障碍物密集、频繁出现截断（truncation）与遮挡（occlusion），且移动机器人速度低、近场感知需求高，现有感知方法在近场障碍物定位方面表现不足，缺乏针对性的数据支撑和评测手段。
- **整体含义**：论文构建了 RoboSense——首个面向拥挤非结构化环境中机器人第一视角感知与导航的大规模多模态数据集与基准，填补了该领域的研究空白，为具身感知、导航与预测技术发展提供标准化评测平台。

## 2. 方法论

### 2.1 数据采集平台

- 采用**社交移动机器人**（清扫机器人）作为采集平台，安装 3 类主传感器：
  - **相机（Camera）**：4 台针孔相机（RGB，25Hz，1920×1080）
  - **鱼眼相机（Fisheye）**：4 台（RGB，25Hz，1280×720，180° FOV）
  - **激光雷达（LiDAR）**：1 台 Hesai Pandar40M（360°，10Hz）+ 3 台 Zvision ML30s + 1 台 Livox Horizon
  - 另配备 GPS/IMU、超声波传感器（3 个 LRU + 8 个 SRU）
- 通过 NTP 协议进行时间同步，生成 10 FPS 的同步多模态数据。

### 2.2 数据集规模与标注

- 在上海滴水湖区域采集 **42 小时**数据，覆盖 **22 个地点**、**6 类场景**（景区、公园、广场、校园、街道、人行道）。
- 手动筛选出 **7,619 段 20 秒的代表性序列**。
- 共包含 **133K+ 同步帧**、**1.4M 个 3D 边界框**（Vehicle/Cyclist/Pedestrian 三类）、**216K 条轨迹**。
- 标注频率为 **1Hz**（因机器人速度低于 1 m/s）。
- 近场（≤5m）障碍物标注数量是 KITTI 的 **270 倍**、nuScenes 的 **18 倍**，对象距离分布峰值约在 5m 处。
- 除 3D 框和轨迹外，还提供**占用标签（Occupancy）**，包含动态物体与静态场景分割。

### 2.3 坐标系定义

定义了 5 种坐标系：**Ego-Vehicle 坐标系**（用于感知/预测/规划）、**全局坐标系**（北-东-上）、**LiDAR 坐标系**、**相机坐标系**（针孔与鱼眼定义不同）、**像素坐标系**。

### 2.4 新增评估准则：CCDP

- 提出 **Closest Collision-point Distance Proportion（CCDP）** 匹配准则，以障碍物最近碰撞点到自车的距离作为匹配基准，并使用相对比例（5%/10%）而非绝对距离，更贴合低速近场导航的安全需求。
- 相比传统 3D IoU 或中心距离（CD）准则，CCDP 更能反映模型对近距离障碍物碰撞点定位的能力。

### 2.5 基准任务

论文定义了 **6 个标准化任务**：
1. 多视角 3D 检测（Multi-view 3D Detection）
2. LiDAR 3D 检测
3. 多模态 3D 检测
4. 多目标 3D 跟踪（3D MOT）
5. 运动预测（Motion Forecasting）
6. 占用预测（Occupancy Prediction）

## 3. 实验设计

### 3.1 数据集划分

- 训练集 50%、测试集 40%、验证集 10%。
- 6 类场景中 **S-6（街道）被完全划分为测试集**（具有 78% 夜间数据），实现场景级域分离测试；其余场景在各划分间共享。

### 3.2 对比方法

| 任务 | 对比方法 |
|------|---------|
| LiDAR 3D 检测 | PointPillar、SECOND、PV-RCNN、Transfusion-L |
| 多视角 3D 检测 | BEVDet、BEVDet4D、BEVDepth、BEVFormer |
| 3D 跟踪 | AB3DMOT（基于 BEVDepth/PointPillar 检测结果） |
| 运动预测 | ViP3D、PnPNet、Constant Pos/Vel 基线 |
| 占用预测 | BEVDepth 扩展版 |

### 3.3 传感器布局消融

对比 4C（仅相机）、4F（仅鱼眼）、4C+4F、4L（仅 LiDAR）、8V+4L（多模态）五种传感器布局在不同距离范围（0-5m、5-10m、10-30m）下的检测与跟踪性能。

### 3.4 评估指标

- 检测：mAP（含 3D AP、AOS、ASE）
- 跟踪：sAMOTA、AMOTP、MT、ML
- 预测：minADE、minFDE、MR、EPA
- 占用：mIoU-3D、mIoU-BEV（分距离范围）

## 4. 资源与算力

- **论文未明确说明**使用的 GPU 型号、数量或训练时长。
- 仅提及实现细节：图像输入统一缩放至 640×352，LiDAR 点云范围设置为 x∈[-45m, 45m]、y∈[-45m, 45m]、z∈[-1m, 4m]，使用 ResNet18 作为图像骨干网络，模型在 FCOS3D 上预训练。
- 算力相关信息需参阅补充材料或联系作者获取。

## 5. 实验数量与充分性

### 实验数量

- **LiDAR 检测**：4 种方法，2 种匹配准则（CP/CCP），3 类物体。
- **多视角检测**：4 种方法，2 种匹配准则。
- **传感器布局对比**：5 组布局，3 个距离范围，涵盖检测与跟踪。
- **跟踪实验**：5 组传感器配置下的 sAMOTA/AMOTP/MT/ML。
- **运动预测**：4 组方法对比。
- **占用预测**：4 个不同距离范围下的 mIoU 结果。
- 总体实验矩阵较为丰富。

### 充分性评估

- **优点**：对比方法覆盖了当前主流检测框架（pillar-based、voxel-based、point-voxel、transformer-based），评估维度全面（检测+跟踪+预测+占用），且包含传感器布局消融和距离分层分析，实验设计较为系统。
- **局限性**：
  - 占用预测仅使用 BEVDepth 一种基线，缺乏多种占用预测方法的横向对比。
  - 运动预测仅对比两种端到端方法，未包含基于 HD-map 的经典预测方法（如 DenseTNT、MultiPath++）。
  - 跟踪仅使用 AB3DMOT，未对比更先进的 3D tracker。
  - 未提供多任务联合训练 vs 独立训练的对比实验（论文称支持多任务端到端训练但未给出相应结果）。

## 6. 主要结论与发现

- **数据集填补空白**：RoboSense 是首个面向拥挤非结构化环境中机器人第一视角感知与导航的大规模多模态数据集，近场障碍物标注量远超现有自动驾驶数据集。
- **CCDP 更具挑战性**：使用 CCP 匹配准则的检测 AP 显著低于 CP（如 Transfusion-L 的 Vehicle 类 AP 下降 18.5%，Pedestrian 类下降 29.5%），表明近场碰撞点定位是当前模型的短板，对导航安全至关重要。
- **传感器互补性明显**：鱼眼相机在近场（<10m）表现更优，针孔相机在远场（10-30m）更优，两者融合可实现全距离范围的性能提升；LiDAR 在远场和 CCP 定位上优势明显，但近场（<5m）性能反而不如视觉融合方案。
- **多模态融合显著提升近场感知**：8V+4L 多模态方案将 5m 内 CCP 3D AP 从 20.5%（视觉）提升至 36.9%。
- **近场感知仍是开放难题**：即便使用多传感器融合，5m 内 CCP AP 仍不足 37%，说明近距障碍物因大视角遮挡与截断带来的感知挑战仍亟待解决。
- **运动预测**：PnPNet 优于 ViP3D，端到端方法明显优于常速/常加速度基线。

## 7. 优点

- **填补数据空白**：首个面向拥挤非结构化环境的机器人第一视角感知数据集，场景选择贴合社交机器人实际应用需求。
- **大规模高质量标注**：1.4M 3D 框、216K 轨迹、360° 无盲区覆盖，近场标注密度远超现有数据集。
- **多模态多传感器**：相机+鱼眼+LiDAR 多类型传感器配合柔性配置，支持不同布局的对比研究。
- **创新的评估准则**：CCDP 匹配准则更贴合低速近场导航的安全需求，比传统 IoU/CD 准则更具实际意义。
- **场景级域分离**：测试集完全采用独立场景（S-6），有效评估模型泛化能力。
- **多样化基准任务**：覆盖检测、跟踪、预测、占用等 6 项任务，支持多任务联合优化。
- **隐私保护措施**：对采集数据进行了人脸、车牌、路牌等脱敏处理。

## 8. 不足与局限

- **数据集覆盖有限**：全部数据采集自上海滴水湖区域（22 个地点），地理多样性不足；场景以户外/半封闭为主，未涵盖室内场景。
- **标注频率较低**：1Hz 的标注频率可能限制高动态场景下的模型训练与评估精度。
- **仅支持 3 类移动目标**：未标注摩托车、滑板车等其他常见交通参与者类别。
- **在线评估依赖**：测试集仅提供数据，需通过提交到在线 benchmark 进行评测，增加了使用门槛。
- **算力信息披露不足**：未报告训练所需 GPU 资源与时长，复现成本不明确。
- **部分任务基线不够全面**：占用预测和运动预测的对比方法较少，不足以全面反映各领域最先进水平。
- **未提供多任务联合训练结果**：论文声称支持端到端多任务训练，但缺乏与独立训练的实验对比验证。
- **应用限制**：数据集基于特定机器人平台（清扫机器人）和传感器配置，向其他类型移动平台迁移时需重新标定。

---

（完）
