---
title: "PhysVLM: Enabling Visual Language Models to Understand Robotic Physical Reachability"
title_zh: PhysVLM：让视觉语言模型理解机器人物理可达性
authors: "Zhou, Weijie, Tao, Manli, Zhao, Chaoyang, Guo, Haiyun, Dong, Honghui, Tang, Ming, Wang, Jinqiao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhou_PhysVLM_Enabling_Visual_Language_Models_to_Understand_Robotic_Physical_Reachability_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向具身视觉推理的物理可达性空间映射
tldr: 视觉语言模型在具身推理中常忽略机器人自身的物理可达性，产生不可行的响应。本文提出统一的空间物理可达性图（S-P Map），将不同机器人的可达范围抽象为通用空间表征，并整合进视觉语言模型PhysVLM。实验显示该模型在具身视觉推理任务中能更准确地判断可执行区域，为后续导航与操作提供更可靠的物理约束。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 689, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1807, \"height\": 861, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1698, \"height\": 661, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1754, \"height\": 517, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 888, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 781, \"height\": 343, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 758, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 755, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 702, \"height\": 185, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhou-physvlm-enabling-visual-language-models-to-understand-robotic-physical-reachability-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 784, \"height\": 265, \"label\": \"Table\"}]"
motivation: 视觉语言模型缺乏对机器人物理可达性的理解，导致具身推理结果不切实际。
method: 提出统一的空间物理可达性图，将机器人可达范围编码进视觉语言模型。
result: 在具身视觉推理中提升了响应可行性与准确性。
conclusion: 为视觉语言模型在机器人任务中的物理感知提供了新的空间表示方法。
---

## Abstract
Understanding the environment and a robot's physical reachability is crucial for task execution. While state-of-the-art vision-language models (VLMs) excel in environmental perception, they often generate inaccurate or impractical responses in embodied visual reasoning tasks due to a lack of understanding of robotic physical reachability. To address this issue, we propose a unified representation of physical reachability across diverse robots, i.e., Space-Physical Reachability Map (S-P Map), and PhysVLM, a vision-language model that integrates this reachability information into visual reasoning. Specifically, the S-P Map abstracts a robot's physical reachability into a generalized spatial representation, independent of specific robot configurations, allowing the model to focus on reachability features rather than robot-specific parameters. Subsequently, PhysVLM extends traditional VLM architectures by incorporating an additional feature encoder to process the S-P Map, enabling the model to reason about physical reachability without compromising its general vision-language capabilities. To train and evaluate PhysVLM, we constructed a large-scale multi-robot dataset, Phys100K, and a challenging benchmark, EQA-phys, which includes tasks for six different robots in both simulated and real-world environments. Experimental results demonstrate that PhysVLM outperforms existing models, achieving a 14% improvement over GPT-4o on EQA-phys and surpassing advanced embodied VLMs such as RoboMamba and SpatialVLM on the RoboVQA-val and OpenEQA benchmarks. Additionally, the S-P Map shows strong compatibility with various VLMs, and its integration into GPT-4o-mini yields a 7.1% performance improvement.

---

## 论文详细总结（自动生成）

# PhysVLM：让视觉语言模型理解机器人物理可达性——论文详细总结

## 1. 论文的核心问题与整体含义

**研究动机与背景：**
- 视觉语言模型（VLM）在环境感知方面表现出色，但在具身智能任务（如机器人抓取、任务规划）中，往往忽略机器人自身的**物理可达性**（Physical Reachability），从而生成不准确或不切实际的响应。
- 例如，GPT-4o 在被问到“机器人能否拿起碗”时，会回答“可以”，但实际上碗可能位于机器人手臂的物理可达范围之外，导致执行失败（见论文图1）。
- 人类在执行任务时，会根据自身身体条件和环境约束调整行为，而现有 VLM 缺乏这种对机器人自身物理约束的建模能力。

**要解决的两个关键挑战：**
1. **统一表示问题**：不同机器人在尺寸、关节类型、自由度等方面差异巨大，VLM 难以直接学习这些机器人特定的参数差异。
2. **能力兼容问题**：如何在提升 VLM 物理可达性理解能力的同时，不损害其原有的通用视觉语言能力。

**核心贡献概述：**
- 提出 **S-P Map（Space-Physical Reachability Map，空间物理可达性图）**，将不同机器人的物理可达性抽象为统一的、与机器人配置无关的空间表示。
- 提出 **PhysVLM**，通过额外的约束编码器将物理可达性信息集成到传统 VLM 架构中，在不损害通用视觉语言能力的前提下增强物理推理能力。
- 构建大规模多机器人数据集 **Phys100K** 和挑战性基准 **EQA-phys**。

---

## 2. 论文提出的方法论

### 2.1 核心思想

PhysVLM 的核心思想是：**将机器人物理可达性从机器人特定的参数空间抽象为通用的空间表示（S-P Map），使模型只需理解“哪些区域可达”，而无需关心机器人具体是哪种型号或配置**。

### 2.2 S-P Map 编码方法

S-P Map 的生成公式为：

```
S-P Map = F(P_raw, {θ_min^i, θ_max^i}, DH, E)
```

其中：
- **P_raw**：机器人 RGB-D 相机获取的原始点云数据
- **{θ_min^i, θ_max^i}**：各关节 i 的运动范围
- **DH**：Denavit-Hartenberg 参数，描述各关节的几何结构
- **E**：相机坐标系到机器人坐标系的外参标定矩阵

**生成流程（文字描述）：**

1. **正向运动学计算可达到工作空间**：
   - 对具有 n 个自由度的机械臂，每个关节 i 有 DH 参数 {θᵢ, dᵢ, aᵢ, αᵢ}
   - 通过齐次变换矩阵 Tᵢ = G(θᵢ, dᵢ, aᵢ, αᵢ) 描述每个关节
   - 将各关节变换矩阵连乘得到从基座到末端执行器的变换矩阵 T = T₁T₂...Tₙ
   - 在关节运动范围内采样大量关节配置，代入正运动学方程，计算对应的末端位置，将工作空间离散为体素网格 W_voxel（离线预计算并存储）

2. **点云变换与可达性过滤**：
   - 原始点云 P_raw 通过外参矩阵 E 变换到机器人坐标系：P = E · P_raw
   - 通过体素网格查找，筛选出位于可达工作空间内的有效点云：P_valid = {p ∈ P | p ∈ W_voxel}（公式6）

3. **S-P Map 生成**：
   - 将有效点云 P_valid 变换回相机坐标系，利用相机内参投影到图像平面
   - 在原始深度图上标记符合物理可达性的区域；对不可达区域施加灰色遮罩并勾勒边界
   - 最终得到清晰突出不可达区域的 S-P Map，实现与机器人具体配置无关的通用可达性表示

### 2.3 模型架构

PhysVLM 采用**双分支架构**：

| 分支 | 功能 | 技术细节 |
|------|------|----------|
| **视觉分支** | 提取 RGB 图像的高层视觉特征 | 预训练 ViT（SigLip-400M）+ 最大池化 + 两层 MLP 投影 |
| **物理可达性约束分支** | 处理 S-P Map | 同样使用 SigLip-400M + 最大池化 + 特征融合层 + 两层 MLP |
| **语言解码器** | 生成文本响应 | Qwen-2.5-Instruct-3B + Qwen-2.5 tokenizer |

**设计特点**：
- 视觉分支和约束分支**独立运行**，各自提取特征后再融合，送入统一解码器
- 这种设计使模型能够融合视觉、可达性和文本三模态信息，同时保持通用视觉推理能力不受损害

### 2.4 训练流程

**两阶段训练策略：**
1. **第一阶段（对齐阶段）**：使用 LLaVA-Pretrain 和 OpenX-Embodiment 数据集，仅训练投影层，建立视觉输入和物理可达性的基础理解。
2. **第二阶段（微调阶段）**：解冻所有参数，使用 Phys100K、ShareGPT4V 和 RoboVQA 数据联合训练全模型，增强复杂场景下的物理约束推理能力。

**训练数据构造（Phys100K）：**
- RoboVQA：20K 样本
- ScanNet：10K 样本
- OpenX-Embodiment：60K 样本
- PyBullet 仿真新增：10K 样本（使用 UR5、FR5、CR5、FRANKA 四种机械臂）
- 缺失深度图的数据集使用 DepthAnything-v2 生成深度图
- 使用 Grounding DINO 和 SAM2 获取物体 2D 边界框和分割结果
- 问答对分两类：**具身 QA**（覆盖功能推理、世界知识、物体识别等8类）和**物理可达性任务**（基于可达性标签用5个固定模板生成）

---

## 3. 实验设计

### 3.1 评估基准与数据集

| 基准/数据集 | 内容 | 规模 |
|-------------|------|------|
| **EQA-phys**（自建） | 模拟器：PyBullet 中 UR5、FR5、CR5、FRANKA 四种机械臂；真实：UR3、XArm6 两种机械臂 | 模拟 200 样本 / 1000 问题；真实 60 样本 / 300 问题（专家标注） |
| **RoboVQA-val** | 机器人视觉问答验证集 | 标准基准 |
| **OpenEQA** | 具身问答基准 | ScanNet 和 HM3D 子集 |
| **真实任务规划** | “Pick A into B” 等真实任务 | 每类任务执行 10 次取平均成功率 |

### 3.2 对比方法

**API 类 VLM：**
- GPT-4o、GPT-4o-mini、Claude-3.5
- 以及这三个模型在输入中加入 S-P Map 的变体（验证 S-P Map 的通用兼容性）

**具身 VLM：**
- SpatialVLM（3B）
- SpatialBot（3B）
- 3D-VLA（引用报告结果）
- RoboMamba（引用报告结果）

### 3.3 评估指标
- **EQA-phys**：LLM 评分制（满分 5 分，1-5 分制，换算为百分比）
- **RoboVQA-val**：BLEU-1 到 BLEU-4
- **OpenEQA**：EM-EQA（精确匹配）
- **任务规划**：平均成功率

---

## 4. 资源与算力

论文中明确提到：
- **GPU 型号与数量**：8 块 A800 GPU
- **训练时长**：48 小时
- **模型规模**：PhysVLM-3B（约 30 亿参数）
- **训练轮数**：两阶段各训练 1 个 epoch
- **超参数**：第一阶段 batch size 128、学习率 1e-3；第二阶段 batch size 64、学习率 1e-5

---

## 5. 实验数量与充分性

### 实验组数统计

论文共报告了 **4 大类实验**，包含 **7 个正式表格**：

| 表格编号 | 实验内容 | 对比方法数 |
|----------|----------|------------|
| 表1 | EQA-phys（含真实机器人和模拟器，6种机器人） | 8 种方法 + 3 种 S-P Map 增强变体 |
| 表2 | RoboVQA-val（BLEU 1-4） | 5 种方法 |
| 表3 | OpenEQA（ScanNet / HM3D） | 5 种方法 |
| 表4 | 真实任务规划（全在范围内 / 部分在范围内） | 5 种方法 |
| 表5 | S-P Map 消融（S-P Map vs Depth Map vs 无输入） | 3 组对照 |
| 表6 | 特征编码器消融（独立 vs 共享权重） | 2 组对照 |
| 表7 | 训练数据消融（移除 PyBullet / 移除其他数据集） | 3 组对照 |

### 充分性与客观性评估

**充分性较高的方面：**
- 覆盖了模拟器和真实机器人的**零样本泛化评估**（UR3、XArm6 未见过的机器人）
- 消融实验从**输入表示**（S-P Map vs Depth Map vs 无）、**架构设计**（独立 vs 共享编码器）、**数据组成**（去掉不同数据源）三个维度展开，较为全面
- S-P Map 的**通用兼容性**通过 GPT-4o、GPT-4o-mini、Claude-3.5 三组增强实验验证

**可能存在的不足：**
- 真实机器人评估规模相对有限（60 样本 / 300 问题）
- 任务规划实验中每类任务仅执行 10 次，统计显著性可能不足
- 3D-VLA 和 RoboMamba 无法直接运行，仅引用报告结果，对比不完全公平
- API 模型（GPT-4V）在 OpenEQA 上仅测试了前 200 个样本

---

## 6. 论文的主要结论与发现

1. **PhysVLM 显著优于现有模型**：
   - 在 EQA-phys 上平均得分 71.0%，比 GPT-4o（57.0%）**高出 14 个百分点**
   - 在 RoboVQA-val 上 BLEU-4 达 43.5%，超越 RoboMamba（36.3%）7.2 个百分点
   - 在 OpenEQA 上排名第二（57.4%），超越所有具身 VLM 和 GPT-4V，仅次于 GPT-4o

2. **S-P Map 具有强通用兼容性**：
   - GPT-4o-mini + S-P Map 提升 7.1%
   - Claude-3.5 + S-P Map 提升 3.4%
   - GPT-4o + S-P Map 提升 4.1%
   - 验证了 S-P Map 作为机器人无关抽象表示的有效性

3. **零样本真实机器人泛化能力**：
   - 对未见过的 UR3 和 XArm6 机器人，PhysVLM 得分均超过 63%
   - 归因于 S-P Map 的统一抽象和双分支独立编码架构

4. **任务规划的实用性提升**：
   - 当部分物体超出可达范围时，PhysVLM 的任务成功率（48.4%）显著高于 GPT-4o（35.8%）和 Claude-3.5（32.1%）
   - 表明模型能正确规划“先移动再操作”的步骤

5. **消融验证**：
   - 移除 S-P Map 导致模拟器性能下降 16 个百分点、真实性能下降 9.3 个百分点
   - 用深度图替代 S-P Map 性能明显下降（证实仅靠深度信息不足以理解物理可达性）
   - 独立约束编码器优于共享权重的编码器（EQA-phys 71.0% vs 68.2%）

---

## 7. 优点

### 方法设计亮点
1. **统一的机器人类无关表示**：S-P Map 巧妙地将不同机器人的物理参数（DH 参数、关节范围、外参矩阵）抽象为统一的空间图，极大降低了 VLM 学习物理可达性的难度，并实现了跨机器人泛化。
2. **模块化架构扩展**：在不改变原有 VLM 架构的前提下，通过附加约束编码器集成新模态，保持了通用视觉语言能力，设计简洁、可复用性强。
3. **任务驱动的问题定义**：明确指出“物理可达性”是 VLM 具身推理的盲点，并将抽象概念转化为可计算、可训练、可评估的具体形式。
4. **S-P Map 的即插即用性**：不仅服务自身模型，还能增强现有 API 模型（GPT-4o 系列、Claude-3.5），具备广泛的应用价值。

### 实验设计亮点
5. **数据集规模可观**：Phys100K 包含约 10 万样本，涵盖仿真和真实、简单和复杂场景。
6. **真实机器人零样本评估**：对未参与训练的 UR3 和 XArm6 进行测试，增强了结论的说服力。
7. **多维度消融**：从输入模态、架构选择、训练数据组成三个层面验证了设计决策的合理性。
8. **多基准验证**：不仅测试物理可达性任务，还在通用具身 QA 基准（RoboVQA、OpenEQA）上验证了模型没有顾此失彼。

---

## 8. 不足与局限

### 实验覆盖局限
1. **真实机器人评估规模有限**：仅 2 种真实机器人（UR3、XArm6）、60 个样本、300 个问题，相对于模拟器的 200 样本 / 1000 问题，真实场景覆盖明显偏少。
2. **任务类型单一**：真实任务规划仅评估了“Pick A into B”一类任务，缺乏移动操作、多步操作、避障等更复杂场景的验证。
3. **任务规划统计量薄弱**：每类任务仅执行 10 次，偶然性较高，缺乏置信区间或显著性检验。

### 对比公平性风险
4. **部分基线方法不可复现**：3D-VLA 和 RoboMamba 由于可执行版本不可用，仅引用其论文报告结果，与直接运行实验的方法之间的公平性可能存在偏差。
5. **OpenEQA 上 GPT-4o 仅测 200 个样本**（用 * 标注），对比不完全一致。

### 方法内在局限
6. **零样本真实性能与模拟仍有差距**：论文自认真实机器人上的表现（63-64%）低于模拟器（71-78%），领域差距（domain gap）仍然明显。
7. **对深度图和标定的依赖**：S-P Map 的生成依赖 RGB-D 相机、精确的外参标定矩阵和机器人 DH 参数，这些在实际部署中可能存在噪声或标定误差。
8. **2D 图像空间的投影局限**：S-P Map 本质上将 3D 可达性压缩到 2D 图像平面，可能丢失部分空间信息（如遮挡区域的深度歧义）。

### 偏差风险
9. **伪标签依赖启发式方法**：对于缺乏精确机器人参数的公开数据集（如 ScanNet、RoboVQA），可达性标签通过分割结果和深度值近似生成，可能引入噪声标签。
10. **数据来源不平衡**：OpenX-Embodiment 占 Phys100K 的 60%，可能使模型偏向该数据集的任务分布。

---

## 总结

PhysVLM 通过提出统一的 S-P Map 表示，成功地为视觉语言模型注入了机器人物理可达性理解能力，在 EQA-phys 上以 71.0% 的得分较 GPT-4o 提升 14 个百分点，同时不损害通用视觉推理表现。这项工作为 VLM 在机器人具身任务中的“物理常识”建模提供了一个简洁有效的方向，其开源的数据集和基准（Phys100K、EQA-phys）也将推动领域后续研究。不过，真实场景性能、数据规模覆盖和评估公平性等方面仍有进一步提升空间。

（完）
