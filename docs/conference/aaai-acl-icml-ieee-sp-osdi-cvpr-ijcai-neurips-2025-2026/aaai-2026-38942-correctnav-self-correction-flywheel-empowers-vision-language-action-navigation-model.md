---
title: "CorrectNav: Self-Correction Flywheel Empowers Vision-Language-Action Navigation Model"
title_zh: CorrectNav：自修正飞轮赋能视觉-语言-动作导航模型
authors: "Zhuoyuan Yu, Yuxing Long, Zihan Yang, Chengyan Zeng, Hongwei Fan, Jiyao Zhang, Hao Dong"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38942/42904"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 视觉语言导航，基于自修正的执行指令方法
tldr: 现有视觉语言导航模型在执行指令时常常偏离正确轨迹，且缺乏有效的纠错能力。针对该问题提出自修正飞轮（Self-correction Flywheel）后训练范式，将训练集中的错误轨迹视为有价值的数据来源，识别偏差并自动生成用于感知和动作的自修正数据，支撑模型持续训练。实验表明该方法能显著提升视觉语言导航模型在偏离轨迹后的恢复能力，进而提高指令跟随导航的成功率。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38942/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1373, \"height\": 717, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38942/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1696, \"height\": 796, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38942/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 885, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38942/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 884, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38942/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 680, \"height\": 502, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38942/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1299, \"height\": 674, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38942/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 793, \"height\": 744, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38942/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1562, \"height\": 805, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38942/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38942/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 232, \"label\": \"Table\"}]"
motivation: 现有视觉语言导航模型在执行指令时易偏离轨迹且缺乏错误恢复能力。
method: 提出自修正飞轮后训练范式，从错误轨迹中自动生成自修正数据并用于感知与动作训练。
result: 在视觉语言导航基准上显著减少轨迹偏差，提升模型从错误中恢复的成功率。
conclusion: 将错误轨迹转化为训练数据可有效增强导航模型的自修正能力，提升指令跟随鲁棒性。
---

## Abstract
Existing vision-and-language navigation models often deviate from the correct trajectory when executing instructions. However, these models lack effective error correction capability, hindering their recovery from errors. To address this challenge, we propose Self-correction Flywheel, a novel post-training paradigm. Instead of considering the model’s error trajectories on the training set as a drawback, our paradigm emphasizes their significance as a valuable data source. We have developed a method to identify deviations in these error trajectories and devised innovative techniques to automatically generate self-correction data for perception and action. These self-correction data serve as fuel to power the model’s continued training. The brilliance of our paradigm is revealed when we re-evaluate the model on the training set, uncovering new error trajectories. At this time, the self-correction flywheel begins to spin. Through multiple flywheel iterations, we progressively enhance our monocular RGB-based VLA navigation model CorrectNav. Experiments on R2R-CE and RxR-CE benchmarks show CorrectNav achieves new state-of-the-art success rates of 65.1% and 69.3%, surpassing prior best VLA navigation models by 8.2% and 16.4%. Real robot tests in various indoor and outdoor environments demonstrate \method's superior capability of error correction, dynamic obstacle avoidance, and long instruction following.

---

## 论文详细总结（自动生成）

# CorrectNav：自修正飞轮赋能视觉-语言-动作导航模型——论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：视觉-语言导航（Vision-and-Language Navigation, VLN）任务要求智能体根据自然语言指令在未知环境中导航至目标位置，是具身智能的基础能力之一。已有 VLN 模型主要聚焦于增强视觉感知和多模态推理能力（如改进特征表示、扩充训练数据），试图让模型在每一步都尽可能正确。
- **核心问题**：现实情况是，模型在导航过程中不可避免地会预测错误动作，导致偏离正确路径。偏差一旦产生，环境与指令之间就会出现错位，而现有模型**缺乏有效的自我纠错能力**，难以从错误中恢复并回到正确轨迹。这种缺陷成为制约 VLN 模型整体性能进一步提升的关键瓶颈。
- **研究问题**：作者提出一个核心问题——**能否教会机器人在导航过程中自我纠错？** 具体而言，需要回答两件事：① 纠什么错（即错误来源）；② 如何教会模型纠错。
- **核心洞察**：作者观察到，即使是在**训练集**上评估性能良好的导航模型，仍然会产生错误轨迹。传统视角将这些错误视为训练不充分的缺陷，而本文的创新视角在于——**将这些错误轨迹视为宝贵的数据资源**，用于生成自修正训练数据，驱动模型持续改进。

## 2. 论文提出的方法论

### 2.1 总体范式：Self-correction Flywheel（自修正飞轮）

- 这是一种**后训练（post-training）范式**，以四步闭环迭代运行：
  1. **模型评估**：在训练集上评估当前模型，收集错误轨迹。
  2. **偏差检测**：自动检测错误轨迹偏离正确路径的位置。
  3. **数据创建**：从感知和动作两个维度自动生成自修正数据。
  4. **持续训练**：用自修正数据继续训练模型。
- 完成上述四步即为一轮飞轮迭代；在新一轮中重新评估模型，又会出现**新的错误轨迹**，生成全新的自修正数据，形成闭环，实现多轮性能提升。

### 2.2 CorrectNav 模型结构

- **输入**：仅使用单目 RGB 视频和语言指令，不依赖深度、全景图或里程计等多传感器。
- **组成**：
  - 视觉编码器：SigLIP，提取采样帧的视觉特征；
  - 投影器：2-layer MLP，将视觉特征映射到 LLM 语义空间；
  - 大语言模型（LLM）：Qwen2，以自回归方式预测动作。
- **初始化**：基于 LLaVA-Video 7B 预训练权重初始化。

### 2.3 导航微调策略

1. **导航动作预测**：从 R2R 和 RxR 训练集收集 oracle 轨迹（共 210 万+逐步动作数据，其中 R2R 52.7 万、RxR 158 万），让模型基于指令和 RGB 观测预测 m 步动作块（action trunk）。
2. **域随机化**：随机化相机高度、视场角（FoV）、分辨率、光照条件，增强视觉多样性。
3. **轨迹级指令生成**：基于完整 oracle 轨迹，让模型根据 RGB 观测历史生成语言格式的导航指令（R2R 1 万条 + RxR 2 万条轨迹）。
4. **通用多模态数据召回**：从 LLaVA-Video 178K 数据集中采样 24 万条 ActivityNet-QA 和 NextQA 实例，防止导航微调导致通用多模态能力遗忘。

### 2.4 自修正飞轮的关键技术细节

#### ① 偏差检测（DeviDetect）
- **原理**：通过计算模型轨迹与 oracle 轨迹之间的距离来判断偏差。
- **数学定义**：
  - 对 oracle 轨迹参考点进行均匀插值，形成密集点序列 $T'_g$；
  - 对模型轨迹上每个位置 $M_i$，计算其到 $T'_g$ 的最短距离 $h_i = \min_{x \in T'_g} \|M_i - x\|_2$；
  - 定义 $M_i$ 在 $T'_g$ 上的正交足迹 $P_i = \arg\min_{P \in T'_g} \|M_i - P\|_2$；
  - 若存在时刻 $t$ 使 $h_t > S$ 且此前所有时刻 $h_i \le S$（$S$ 为预设距离阈值），则判定模型在 $M_t$ 处开始偏离。

#### ② 错误修正轨迹（动作纠正数据）
- 基于检测到的偏离点 $M_t$ 和其正交足迹 $P_t$，利用轨迹规划器 $\Gamma$ 生成一条新的错误修正轨迹：
  \[
  T_e = (M_t, G_{k+1}, \dots, G_n)
  \]
  即从偏离点出发，依次经过后续参考点，最终到达目的地。
- **训练方式**：只在修正轨迹段 $T_e$ 上进行动作学习，偏离前的轨迹仅作为观测历史输入，确保模型聚焦于"纠错行为"学习。

#### ③ 关键帧感知数据（感知纠正数据）
- **动机**：不仅要教模型"做什么"，还要教它"为什么"。
- **数据生成方法**：选取偏离点 $M_t$ 及其前后帧作为修正关键帧 $\{K_1, K_2, K_3\}$，使用多模态大模型 Qwen-VL-Plus 生成两类感知数据：
  - **地标描述**（captioning）：描述帧中可能出现的导航地标（家具、装饰、建筑结构等）；
  - **视觉问答对**（QA）：围绕目标相对位置、物体颜色、机器人当前朝向等生成问答对。
- **训练方式**：输入观测视频 $\{I_1, I_2, \dots, K_i\}$，分别以描述文本为生成目标（训练场景理解），以及以问答对形式让模型基于当前观测回答问题（激活纠错行为理解）。

#### ④ 数据采样与多轮迭代
- 每轮飞轮训练时，从新生成数据中**随机采样一半**错误修正轨迹及其关键帧感知数据，同时混合等量（采样量的一半）的原始 oracle 轨迹以维持训练稳定性。
- 多轮迭代持续进行，直至模型性能不再提升或出现下降（实验中第四轮开始下降，遂停止）。

## 3. 实验设计

### 3.1 模拟实验

- **数据集/基准**：
  - **R2R-CE**（Room-to-Room in Continuous Environments）：基于 MP3D 室内场景；
  - **RxR-CE**（Room-across-Room in Continuous Environments）：同样基于 MP3D；
  - 评估均采用官方 **Val-Unseen** 划分，模拟器为 Habitat 3.0。
- **评估指标**：导航误差（NE）、Oracle 成功率（OS）、成功率（SR）、成功路径加权长度（SPL）、归一化动态时间扭曲（nDTW）。
- **对比方法**：
  - **基于 waypoint predictor 的模型**：BEVBert、ETPNav、HNR、DreamWalker、GridMM、Ego2-Map 等；
  - **导航大模型（VLA）**：NaVid、Uni-NaVid、NaVILA、StreamVLN；
  - **其他基线**：CMA、Seq2Seq、RGB-CMA、InstructNav、LAW 等。

### 3.2 真实机器人实验

- **平台**：AgiBot Lingxi D1 四足机器人，配备单目 RGB 相机及运动 API。
- **部署方式**：机器人将 RGB 观测上传至远程服务器（NVIDIA A100 GPU），CorrectNav 预测 4 步动作块并调用运动 API 执行。
- **场景**：办公室、家庭、校园（分别包含室内外环境）。
- **指令设置**：每个场景 20 条简单指令和 20 条复杂指令（涉及长轨迹、复杂建筑结构、拥挤障碍物、动态场景变化）。
- **对比模型**：NaVid 和 NaVILA，评估指标为 SR 和 NE。

## 4. 资源与算力

- **训练硬件**：8 块 NVIDIA A100 GPU。
- **训练时长**：
  - 导航微调阶段：约 80 小时；
  - 每轮自修正飞轮迭代：约 20 小时；
- **推理配置**：输入 16 帧采样 RGB 帧，预测包含 4 个有效动作的动作块。
- **备注**：论文对训练资源的使用有明确交代，但未详细披露数据生成（MLLM 推理）环节的算力成本细节。

## 5. 实验数量与充分性

### 实验数量
1. **两大模拟基准评测**（R2R-CE 与 RxR-CE Val-Unseen），对比 20+ 种基线方法；
2. **消融实验**：逐项移除三大关键技术（轨迹修正、关键帧感知、数据采样策略），在两个基准上分别验证；
3. **飞轮迭代分析**：追踪 4 轮迭代的性能变化（SR 和 NE 曲线）；
4. **定性案例分析**：对比有无飞轮后训练的轨迹纠正行为差异；
5. **真实机器人实验**：3 类场景 × 2 种复杂度 × 3 个模型对比，共 360 条指令测试。

### 充分性与客观性评估
- **充分**：模拟评测覆盖了 VLN-CE 领域两个最权威的 benchmark，对比基线全面（包含多传感器方法和单目 RGB 方法），评估指标多样（5 个标准指标）；消融实验覆盖了所有关键模块。
- **公平性**①：与同类单目 RGB VLA 方法严格对比；对使用深度、全景、里程计等额外传感器输入的模型，仍实现了超越，说明提升不依赖传感器冗余。
- **公平性风险②**：训练与评估均基于**训练集本身**产生错误轨迹来生成自修正数据，存在潜在的过拟合评估集风险（后文在局限中进一步说明）；真实实验中简单/复杂任务的划分标准未详细说明，可能存在主观性。

## 6. 论文的主要结论与发现

1. **模拟基准大幅 SOTA**：CorrectNav 在 R2R-CE 和 RxR-CE Val-Unseen 上分别取得 65.1% 和 69.3% 的成功率，比此前最优 VLA 导航模型分别高 **8.2% 和 16.4%**；甚至超过使用额外传感器（深度/全景/里程计）的最优 waypoint 模型（比 HNR 高 4.1% / 13.0%）。
2. **飞轮迭代有效**：前三轮自修正飞轮迭代中，模型在两个基准上持续提升，验证了多轮迭代的有效性；第四轮开始下降后停止训练。
3. **三大技术缺一不可**：消融实验证实，移除任何一项技术（轨迹修正、关键帧感知、数据采样策略）都会导致性能下降，其中移除**轨迹修正**影响最大。
4. **真实世界优势显著**：CorrectNav 在办公室、家庭和校园三类环境中，无论简单还是复杂指令，均大幅优于 NaVid 和 NaVILA（如在复杂办公室指令中 SR 为 0.75 对比 NaVid 的 0.30 和 NaVILA 的 0.20）。
5. **纠错能力显现**：定性案例显示，飞轮后训练的模型能够在误入错误路径后主动掉头回到正确路线，或在进入错误门口后退出并转向正确入口，而未训练的模型无法做到。

## 7. 优点

- **新颖的问题视角**：将模型在训练集上的错误轨迹从"训练不充分的缺点"重新定义为"宝贵的数据资源"，提出了自修正飞轮的闭环训练范式，思想具有原创性和通用性。
- **自动化的数据生成管线**：无需人工标注即可自动完成偏差检测、纠错轨迹生成和关键帧感知数据创建，具有良好的可扩展性。
- **隐式纠错、零额外推理开销**：与 SmartWay、EnvolveNav 等需要额外模型或链式思考推理的方法不同，自修正能力通过训练直接内化于模型参数中，部署时无需增加模块或推理步骤，有利于实时机器人应用。
- **单目 RGB 输入**：去除了对深度、全景、里程计等多传感器的依赖，显著降低了硬件门槛，实验证明其性能仍能超越多传感器方法。
- **工程实现完整**：包含域随机化、轨迹级指令生成、通用多模态数据召回等系统性微调策略，兼顾导航专用能力与通用多模态能力的保持。
- **实验结果全面且有说服力**：模拟评测 + 真实机器人部署双验证，覆盖多场景、多维度的比较，定量定性相结合。

## 8. 不足与局限

- **感知精度局限（作者自述）**：单目 RGB 模型对机器人本体与周围环境的相对位置关系感知精度不足，四足机器人近距离通过障碍物时，后腿可能发生剐蹭。作者建议未来将机器人身体尺寸和状态信息作为先验知识引入。
- **训练集评估偏差风险**：由于自修正数据来自训练集自身评估产生的错误轨迹，模型的性能提升可能部分源于对训练分布更好的拟合，而非真正的分布外泛化能力提升。虽 Val-Unseen 结果证明了泛化性，但飞轮迭代的长期有效性仍待更大规模场景验证。
- **第四轮性能下降**：实验显示第四轮迭代性能出现下降，说明飞轮迭代并非无限有效，存在过拟合或数据冗余风险，文中未给出明确的停止准则或过拟合缓解策略。
- **环境覆盖有限**：模拟训练仅基于 MP3D 室内场景（尽管真实实验覆盖了部分室外校园环境），对更广泛的真实世界多样性（如极端光照、天气、室外动态场景）覆盖仍不足。
- **真实实验规模有限**：真实机器人实验仅在 3 类环境中各测试 40 条指令，样本量相对较小；且未提供不同环境下对障碍物避让的具体定量指标（如碰撞率），"动态障碍物避让"的结论更多依赖定性案例支持。
- **计算成本较高**：每一轮飞轮迭代需 20 小时在 8×A100 上训练，多轮迭代的累积成本可观，实际应用中需要权衡收益与开销。
- **MLLM 数据生成质量控制**：依赖 Qwen-VL-Plus 生成的感知描述与 QA 对的质量未做人工评估或筛选，不免引入生成噪声，可能影响训练效果的上限。

（完）
