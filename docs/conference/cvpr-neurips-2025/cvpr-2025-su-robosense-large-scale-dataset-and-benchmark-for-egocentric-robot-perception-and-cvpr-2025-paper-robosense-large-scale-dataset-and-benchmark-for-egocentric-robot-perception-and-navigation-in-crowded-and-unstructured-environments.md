---
title: "RoboSense: Large-scale Dataset and Benchmark for Egocentric Robot Perception and Navigation in Crowded and Unstructured Environments"
title_zh: RoboSense：以自我为中心的拥挤非结构化环境机器人感知与导航大规模数据集与基准
authors: "Su, Haisheng, Song, Feixiang, Ma, Cong, Wu, Wei, Yan, Junchi"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Su_RoboSense_Large-scale_Dataset_and_Benchmark_for_Egocentric_Robot_Perception_and_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 大规模以自我为中心的机器人导航数据集与基准
tldr: 本文构建了大规模以自我为中心的机器人感知与导航数据集RoboSense，覆盖拥挤和非结构化环境。数据采集平台集成多传感器，聚焦近场场景理解中的截断、遮挡等难题，提供感知与导航评测基准。该数据集能支持低成本、高置信度的障碍物检测与碰撞避免评估，为移动机器人在复杂社会场景中的导航研究提供重要数据基础。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 539, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 876, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 721, \"height\": 333, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 486, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1793, \"height\": 368, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 419, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1818, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1820, \"height\": 497, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 874, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-robosense-large-scale-dataset-and-benchmark-for-egocentric-robot-perception-and-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 871, \"height\": 210, \"label\": \"Table\"}]"
motivation: 拥挤非结构化环境中机器人近场感知受截断和遮挡限制，缺少大规模评测数据。
method: 搭建多传感器以自我为中心的数据采集平台，构建数据集与导航评测基准。
result: 基准支持近场障碍物检测与碰撞避免等导航任务的低成本评估。
conclusion: 为复杂环境下的机器人感知与导航研究奠定数据基础。
---

## Abstract
Reliable embodied perception from an egocentric perspective is challenging yet essential for autonomous navigation technology of intelligent mobile agents. With the growing demand of social robotics, near-field scene understanding becomes an important research topic in the areas of egocentric perceptual tasks related to navigation in both crowded and unstructured environments. Due to the complexity of environmental conditions and difficulty of surrounding obstacles owing to truncation and occlusion, the perception capability under this circumstance is still inferior. To further enhance the intelligence of mobile robots, in this paper, we setup an egocentric multi-sensor data collection platform based on 3 main types of sensors (Camera, LiDAR and Fisheye), which supports flexible sensor configurations to enable dynamic sight of view from ego-perspective, capturing either near or farther areas. Meanwhile, a large-scale multimodal dataset is constructed, named RoboSense, to facilitate egocentric robot perception. Specifically, RoboSense contains more than 133K synchronized data with 1.4M 3D bounding box and IDs annotated in the full 360^ \circ view, forming 216K trajectories across 7.6K temporal sequences. It has 270xand 18xas many annotations of surrounding obstacles within near ranges as the previous datasets collected for autonomous driving scenarios such as KITTI and nuScenes. Moreover, we define a novel matching criterion for near-field 3D perception and prediction metrics. Based on RoboSense, we formulate 6 popular tasks to facilitate the future research development, where the detailed analysis as well as benchmarks are also provided accordingly. Data desensitization measures have been conducted for privacy protection.

---

## 论文详细总结（自动生成）

# RoboSense：拥挤非结构化环境中以自我为中心的机器人感知与导航大规模数据集与基准

## 1. 核心问题与整体含义（研究动机与背景）

随着自动驾驶技术的成熟，社会移动机器人的感知/导航日益受到关注。本文聚焦于此前的数据集（如 KITTI、nuScenes、Waymo等）所忽视的复杂、拥挤、非结构化的近场社交场景下的感知问题：

- **以自我为中心（Egocentric）感知的挑战**：在面向交通参与者（如行人、非机动车、车辆）时常遇到严重的截断与遮挡，尤其是近场目标，物体大面积占据视野、频繁被遮挡，感知能力远低于开放道路上的自动驾驶场景。
- **现有数据集的局限性**：
  - 现有基准（KITTI、nuScenes、Waymo、Argoverse、H3D、Lyft L5等）均针对**结构化道路上的自动驾驶**采集，传感器视角多为俯视车顶安装，目标距离较远。
  - 社交机器人（如清扫车、配送车、零售车等）的导航场景在**光照、人车流密度、目标距离和场景复杂度**上与驾驶场景差异极大，不能直接沿用。
  - 缺乏覆盖近场、360°全视角、多传感器同步的社交机器人导航数据集。
- **本文的核心目标**：构建首个面向拥挤、非结构化环境中以自我为中心的机器人感知公共数据集 **RoboSense**，提出新的评估准则，并建立 6 个标准化基准任务，填补这一领域的空白。

## 2. 提出的方法论

### 2.1 数据采集平台

- 以实际社交移动机器人（RoboSweeper）为采集平台，在上海滴水湖区域持续采集 42 小时，覆盖 22 个不同地点。
- 传感器配置（支持灵活组合）：
  - **Camera**：4 台针孔相机（25Hz, 1920×1080，FOV 111.78°×63.16°）
  - **Fisheye**：4 台鱼眼相机（25Hz, 1280×720，FOV 180°×180°）
  - **LiDAR**：1 台 Hesai Pandar40M（64 线，360°）+ 3 台 Zvision ML30s + 1 台 Livox Horizon（用于拼接点云获取全向覆盖）
  - **Ultrasonic**：3 个远距 + 8 个近距超声波传感器（用于自由空间检测与安全保障）
  - **GPS/IMU**：RTK 定位、1000Hz 更新率
- 所有传感器通过 NTP 时间同步，以 100ms 为全局时间戳，输出同步多模态数据，帧率为 10 FPS。

### 2.2 标注方案

- **3D 物体框**：对三个可移动类别（“Vehicle”、“Cyclist”、“Pedestrian”）在 LiDAR 坐标系与 Camera 坐标系中分别标注，每帧用 `[x, y, z, w, l, h, θ, cls]` 表示，含位置、尺寸、朝向与类别。
- **轨迹**：在 BEV 视角下为每个agent分配唯一 Track ID，跨连续帧关联形成全局轨迹。
- **占据标签**：将 3D 空间体素化，基于标注的 3D 框和轨迹沿时间维度进行动态/静态分割，生成稠密的占据状态标签（"occupied"、"free"、"unknown"）及语义标签。
- **隐私保护**：对所有人脸、车牌和路牌进行了脱敏处理。

### 2.3 核心创新：CCDP 匹配准则

- 针对低速、近场场景，提出**最近碰撞点距离比例（Closest Collision-point Distance Proportion, CCDP）**作为新的匹配准则，而非 nuScenes 的中心距离（CD）或 KITTI 的 3D IoU。
- CCDP 将匹配阈值定义为相邻障碍物最近碰撞点到自车的距离的一个相对比例 p（取 5%、10%、20%），更关注**近场障碍物碰撞点的定位精度**，这是低速导航安全的核心。
- 评估指标包括：mAP、AOS（航向角精度）、ASE（尺度误差）、sAMOTA、AMOTP、minADE、minFDE、MR、EPA、IoU 等。

### 2.4 基准任务定义

提出 6 个标准化任务：
1. **多视角 3D 检测**（Multi-view 3D Detection，4 Camera/鱼眼）
2. **LiDAR 3D 检测**
3. **多模态 3D 检测**（Camera + LiDAR 融合）
4. **多目标跟踪**（3D MOT）
5. **运动预测**（Motion Forecasting，预测未来 3 秒、K 条轨迹）
6. **占据预测**（Occupancy Prediction，3D 体素状态与语义）

## 3. 实验设计与 Benchmark

### 3.1 数据集划分与场景构成

- 共 7.6K 个时序序列（每个 20 秒）、133K+ 帧同步数据、1.4M 个 3D 框、216K 条轨迹，覆盖 6 类场景：**公园、景区、广场、校园、人行道、街道**。
- 标注频率为 1Hz（因机器人速度 <1m/s），时间跨度为42小时。
- 训练/测试/验证集划分比例为 50%/40%/10%，测试集（S-6 街道场景）数据完全隔离，仅提供数据不提供标注，通过线上评测获取结果。
- 场景多样性：包含白天/夜间（65%/35%）、不同光照与天气条件。

### 3.2 各任务对比方法

**LiDAR 3D 检测**：
- PointPillar（基于 pillar）、SECOND（基于体素）、PV-RCNN（两阶段 point-voxel）、Transfusion-L（Transformer 融合方法）。

**多视角 3D 检测（仅图像）**：
- BEVDet（LSS-based）、BEVDet4D（时序扩展）、BEVDepth（深度预测分支）及 BEVFormer（Transformer query-based）。

**3D 多目标跟踪**：
- 采用 Tracking-by-Detection 范式，分别使用 BEVDepth（图像检测）和 PointPillar（LiDAR 检测）作为输入，AB3DMOT 作为跟踪器。

**运动预测**：
- ViP3D（视觉端到端）、PnPNet（LiDAR 端到端），以及 Constant Position / Constant Velocity 作为参考基线。

**占据预测**：
- 以 BEVDepth 为基础，替换检测解码器为占据重建层，用 4F（鱼眼）输入。

**传感器布局对比实验**：
- 视觉配置：4C、4F、4C+4F
- LiDAR配置：4L（拼接）
- 多模态配置：8V+4L（后期融合）

### 3.3 核心实验结果

**3D 检测**：
- LiDAR 检测中，Transfusion-L 综合最优（Vehicle 3D AP 83.6%/65.1%）。
- 图像多视图检测中，BEVDepth 与 BEVFormer 相当，均优于 BEVDet。
- 使用 CCP 匹配时，所有方法性能显著低于 CP 匹配（如 Transfusion-L 的 Vehicle 3D AP 下降 18.5%，Pedestrian 下降 29.5%），说明近场碰撞点定位是当前方法的薄弱环节。

**传感器布局**：
- 4F 在近场（0–5m、5–10m）表现优于 4C；4C 在远场（10–30m）更优；组合 4C+4F 可全面提升。
- 多模态 8V+4L 的 CCP AP 在 5m 内从 20.5%（视觉）提升至 36.9%，AOS 也一致提升，验证了多传感器互补价值。

**多目标跟踪**：
- 4C+4F 的 sAMOTA（51.16）超过 4L（44.77），多模态方案在 AMOTP、MT、ML 上最优。

**运动预测**：
- PnPNet（LiDAR）优于 ViP3D（视觉）：minADE 0.89 vs 1.31；两者均远优于 Constant 基线。

**占据预测**：
- 2m 内 mIoU-3D=39.6，5m 降至 30.7，12.8m 时仅 16.1——近场占据预测仍有很大提升空间。

## 4. 资源与算力

论文**未明确报告**训练所用的 GPU 型号、数量或训练时长等算力信息。仅在实现细节中说明：视觉骨干使用 ResNet18、输入图像缩放为 640×352、voxel size 设置为 0.16m（pillar-based）/0.05m（voxel-based）。这些配置暗示其实验可在常规学术级 GPU 资源下复现，但具体算力需求无法从文中确认。

## 5. 实验数量与充分性

- 实验覆盖 6 大任务、多个方法族（CNN、Transformer、端到端、tracking-by-detection、LSS、query-based），共报告 7 张主表。
- 检测任务：4 种 LiDAR 方法 + 4 种视觉方法 + 2 种匹配准则（CP/CCP）× 2 种阈值（5%/10%）。
- 传感器布局消融：4C、4F、4C+4F、4L、8V+4L 五组对比，覆盖 3 个距离范围。
- 运动预测：2 种端到端方法 + 4 组参考基线。
- 占据预测：4 个距离范围、3D 与 BEV 两种度量。

**充分性评价**：
- 优点：任务覆盖全面（感知前端→跟踪→预测→占据），多传感器组合对比极具参考价值，CCDP 与 CP 的对照实验有效验证了指标设计的合理性。
- 不足：数据集全部来自上海滴水湖单一地理区域，场景多样性可能不够；运动预测缺少单独基于 GT 轨迹的模块化评估（与端到端评价混合）；占据预测仅用简化的 BEVDepth 扩展作为基线，缺少与 SparseOcc 等专用 SOTA 方法的对比。

## 6. 主要结论与发现

1. **近场感知仍是瓶颈**：所有当前先进方法在近场（0–5m）的碰撞点定位精度显著低于中心点精度，说明截断与遮挡对导航安全构成实质威胁。
2. **多传感器互补性明确**：鱼眼与针孔相机在远近场互补，LiDAR 与相机的后融合可显著提升近场 CCP 精度（5m 内提升 80%+ 相对）。
3. **CCDP 是更合适的匹配准则**：相比 CD 与 IoU，CCDP 能更好地反映模型在低速近场场景中定位最近碰撞点的能力。
4. **视觉方法在拥挤场景可达 LiDAR 级跟踪性能**：4C+4F 的 sAMOTA 超过 4L，说明多视角视觉在近距离场景潜力巨大。
5. **端到端预测方法有效但仍有差距**：PnPNet 在运动预测上优于 Constant 基线和 ViP3D，但整体精度距离落地要求还有显著距离。

## 7. 优点与亮点

- **填补领域空白**：首个面向拥挤/非结构化环境中以自我为中心的机器人感知数据集，与自动驾驶数据集差异明显。
- **近场标注规模空前**：5m 内的 3D 框数量是 KITTI 的 270 倍、nuScenes 的 18 倍，为近场感知研究提供了数据基础。
- **灵活的传感器配置**：支持纯视觉、纯 LiDAR、多模态等多种传感器布局评估，为实际系统的传感选型提供参考。
- **指标创新**：提出 CCDP 匹配准则，更贴合低速导航的安全需求。
- **360° 全覆盖无盲区**：4 Camera+4 Fisheye+5 LiDAR+11 超声波，传感器冗余度高。
- **任务完整性好**：从感知、跟踪到预测、占据，形成相对完整的导航感知评测体系。
- **隐私保护到位**：对人脸、车牌、路牌等进行脱敏处理，合规性强。

## 8. 不足与局限

- **地理与场景偏差风险**：全部数据采集自上海滴水湖（单一城市、单一区域），场景类型有限（6 类），可能无法完全代表其他地区或极端天气的社交机器人部署环境。
- **标注频率低**：1Hz 的标注频率限制了高动态目标跟踪与预测任务的时间分辨率，相比 Waymo（10Hz）差距明显。
- **运动预测与感知耦合**：运动预测指标只在感知 TP 上计算，但 ViP3D/PnPNet 的端到端预测同时包含感知误差与预测误差，无法剥离感知和预测各自的贡献。
- **占据预测基线过简**：仅用修改的 BEVDepth 作为基线，未与 SparseOcc、Occ3D 等先进占据网络对比，标杆性能参考价值有限。
- **未提供 HD-map 标注**：运动预测任务不包含车道/地图信息，对依赖地图先验的方法不友好。
- **算力信息缺失**：未报告训练资源，影响复现成本评估。
- **测试集不可得性**：测试集（S-6）需通过线上提交获取结果，训练与测试场景分布差异（S-6 为夜间为主且独占测试集）可能引入跨场景泛化偏差。

（完）
