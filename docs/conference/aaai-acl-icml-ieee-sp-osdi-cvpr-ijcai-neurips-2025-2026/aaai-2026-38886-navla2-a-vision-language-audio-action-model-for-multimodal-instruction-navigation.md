---
title: "NaVLA$^2$: A Vision-Language-Audio-Action Model for Multimodal Instruction Navigation"
title_zh: NaVLA2：用于多模态指令导航的视觉-语言-音频-动作模型
authors: "Jugang Fan, Peihao Chen, Changhao Li, Qing Du, Jian Chen, Mingkui Tan"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38886/42848"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 通过包含物体类别、图像、语言和音频的多模态指令进行具身导航
tldr: 针对部分可观察环境中单模态指令存在歧义、容易导致导航失败的问题，本文提出MINav多模态指令导航任务及NaVLA2模型。该模型整合物体类别、RGB图像、语言描述和听觉线索来消歧并定位目标，从而提升复杂多模态环境下的导航准确性。实验表明，利用多模态指令可显著降低歧义并提高导航成功率，为具身智能体的多模态人机交互导航提供了新范式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38886/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 453, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38886/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1831, \"height\": 987, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38886/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1833, \"height\": 690, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38886/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 318, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38886/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1747, \"height\": 583, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38886/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 777, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38886/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 722, \"height\": 230, \"label\": \"Table\"}]"
motivation: 现有导航任务仅提供单模态指令，在多个相似物体的多模态环境中易产生歧义并导致导航失败。
method: 提出NaVLA2视觉-语言-音频-动作模型，融合多模态指令线索进行目标消歧和动作预测。
result: 在MINav任务上验证多模态指令能显著提升导航成功率，减少因歧义造成的错误。
conclusion: 多模态指令建模可增强具身导航的鲁棒性，拓展了人机协同导航中指令表达方式。
---

## Abstract
Embodied navigation is a fundamental capability for intelligent agents, yet remains challenging in partially observable environments where navigation instructions can be difficult to interpret. However, existing tasks only provide unimodal instructions, which are ambiguous in complex multimodal environments with multiple similar objects, and may result in misinterpretation and navigation failure. To overcome these limitations, we introduce MINav, a novel task where the navigation path is precisely described by a multimodal instruction. The instruction provides multimodal cues, including object categories, RGB images, language descriptions, and auditory descriptions, which help the agent to disambiguate and ground objects in the environment and navigate effectively. We further construct a large-scale dataset of 43.9K navigation episodes using a two-stage pipeline that first annotates multimodal references of objects and then synthesizes diverse multimodal instructions. We find that existing methods struggle on MINav task, indicating substantial room for improvement in agents' multimodal grounding. To address this, we propose NaVLA^2, a vision-language-audio-action model that additionally integrates spatial audio and employs a CoThinkAct module to jointly generate high-level reasoning and consistent low-level actions. Experimental results demonstrate that NaVLA^2 significantly outperforms competitive baselines on MINav benchmark. We hope that our proposed MINav and NaVLA^2 will facilitate future research toward agents with stronger multimodal understanding and grounding capabilities for navigation.

---

## 论文详细总结（自动生成）

# NaVLA²：用于多模态指令导航的视觉-语言-音频-动作模型 —— 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：具身导航（Embodied Navigation）是智能体与环境交互的基础能力。现有导航任务大致分为两类：
  - **目标趋近导航**（Goal-reaching）：给定点、物体类别、图像或音频目标，但容易在多相似物体或开阔环境中造成盲目搜索。
  - **指令跟随导航**（Instruction-following）：给定自然语言逐步指令，但纯文本指令在复杂场景中仍存在歧义，例如"去桌子旁边的椅子"在有多张桌椅上时难以定位。
- **核心问题**：已有任务仅提供**单模态指令**（通常是文本），无法反映人类在真实导航中天然利用视觉、语言、声音等多模态线索来定位和消歧的能力。例如，在多水槽场景中，人类会先用视觉地标定位厨房，再结合流水声锁定具体水槽，而现有智能体缺乏这种能力。
- **整体含义**：作者因此提出 **MINav（Multimodal Instruction Navigation）** 这一新任务，并构建配套数据集和 **NaVLA²** 模型，旨在推动智能体在多模态感知、目标消歧与具身导航方面的研究。

## 2. 提出的方法论

### 2.1 MINav 任务定义
- 智能体在未见过的室内环境中随机初始化，接收一条**多模态指令**，指令中包含四种模态的参照信息：
  1. 物体类别（category）
  2. 代表性图像（RGB image）
  3. 语言描述（language description）
  4. 听觉描述（auditory description，以文本形式给出，如"发出排水声的水槽"）
- 指令中最后一个物体为目标物体，之前的为路标（landmark）。
- 每步智能体接收**自我中心的 RGB 图像**和**双耳空间音频**（binaural spatial audio）。
- 动作空间为 {FORWARD, TURN_LEFT, TURN_RIGHT, STOP}，在目标物体 3 米半径内预测 STOP 视为成功。

### 2.2 数据集构建（两阶段流水线）
- **阶段一：多模态物体参考标注**，为每个物体生成四元组 ⟨r_c, r_i, r_l, r_a⟩：
  - **物体类别 r_c**：将 HM3DSem 中 1,660 个嘈杂类别映射至 312 个基础类别；
  - **代表性图像 r_i**：在物体 2 米范围内渲染多视角，用三项评分（帧覆盖率、全图与类别的 CLIP 相似度、裁剪图与类别的 CLIP 相似度）的乘积选出最优视角；
  - **语言描述 r_l**：使用 VLA-3D 的场景图提取物体间空间关系作为外在属性，用 VLM 对代表性图像生成外观描述作为内在属性，最后经 GPT 综合成流畅描述；
  - **听觉描述 r_a**：GPT 生成物体可能发出的声音文本，用 Freesound API 检索音频片段，以 BERT 相似度（阈值 0.5）筛选，音频文本作为参照、音频片段用于仿真渲染。
- **阶段二：导航片段合成**：
  - 起点与终点同楼层、距离 5–30 米；
  - 沿最短路径选取 1–5 个物体（末位为目标，其余为路标），每个物体随机选一种模态作为指令参照；
  - 逐段规划轨迹并拼接成最终路径，若最终路径相对原始最短路径的测地距离比超过 2 则丢弃；
  - 使用 GPT-4o 根据物体参照与相对方向生成多模态指令。
- **数据规模**：145 个训练场景共 **43.9K 个训练片段**，36 个测试场景共 2,628 个测试片段；另由三位人类专家筛选出 **360 个 test-mini 片段**。

### 2.3 模拟器
- 基于 Habitat 平台和 SoundSpaces 2.0 构建；
- 动态启用音频传感器，将音频片段插入参照物体中心，模拟房间脉冲响应（RIR）并与音频卷积生成带声学特性的双耳空间音频；
- 视觉与音频观测每步更新，贴近真实场景。

### 2.4 NaVLA² 模型架构
- **整体结构**：视觉（CLIP ViT-L/14）、音频（双分支）、语言指令经各模态编码器和适配器对齐后，按交错格式拼接输入 LLM（Vicuna-7B-v1.5）。
- **空间-语义双分支音频编码器（Spatial-Semantic Audio Encoder）**：
  - **语义分支**：双耳音频下混为单声道 → CLAP 编码 → 语义音频适配器；
  - **空间分支**：原始双耳信号 → SpatialAST 编码 → 空间音频适配器；
  - 两条分支输出拼接为最终音频表征，同时捕捉"什么在响"和"声源在哪"。
- **CoThinkAct 模块**：
  - 取 LLM 最后一层隐藏状态作为共享上下文；
  - **分支一**（思考）：经 lm_head 生成自然语言链式推理（CoT），描述当前目标（哪个路标或目标物）及相对方向，并以特殊 token `[NAV]` 结尾；
  - **分支二**（行动）：取出 `[NAV]` 对应的隐藏嵌入，经 action_head 解码为 N 步低级动作序列；
  - 一次前向传播中并行产出高层推理与一致的低层动作，兼顾可解释性和效率。

### 2.5 三阶段训练
1. **阶段一（音频-文本对齐）**：收集 271K 语义音频-文本对，采样 3 组混响-方向对扩充为 813K 空间音频-文本对，训练音频适配器 2 个 epoch；
2. **阶段二（多模态指令微调）**：在 1M 图像/视频/音频 QA 样本上全量微调 LLM，训练 1 个 epoch；
3. **阶段三（MINav 导航微调）**：从导航片段生成 379K 训练样本（含指令、历史视觉、当前视觉、当前音频与 N 步未来动作），LLM 采用 LoRA（rank=16），联合训练 token 嵌入、lm_head 和 action_head。

## 3. 实验设计

- **Benchmark**：自建的 MINav 基准（基于 Habitat-Matterport 3D 场景），测试在未见过环境中进行。
- **评估指标**：成功率（SR）、预言成功率（OSR）、路径长度加权成功率（SPL）、SoftSPL、导航误差（NE）、轨迹长度（TL）和规范化动态时间规整（nDTW）。
- **对比方法**：
  - **零样本**：Random（随机策略）、Qwen2.5-Omni（视觉+音频+语言多模态 LLM）、Gemini-1.5-flash（Omni-MLLM）、CA-Nav + GPT-4（VLN 子目标解析+价值地图）；
  - **微调方法**：IL(instr-nav)（行为克隆）、RL(goal-nav)（DD-PPO，仅目标）、RL(instr-nav)（DD-PPO，完整指令）以及当前开源 SOTA 导航 VLA 模型 **Navid**。
- **主要结果（Table 1）**：NaVLA² 在全部指标上显著优于基线，SR 达 **27.2%**（比最强基线 RL 高 +11.6%），SPL 达 **19.6%**（+4.4%）。
- **其他分析**：
  - 对比 RL(instr-nav) 与 RL(goal-nav) 证明完整指令提供更丰富的监督信号；
  - 按目标模态分组和按指令模态数量分组（Figure 4）分析各模态贡献，发现**代表性图像**消歧贡献最大、仅物体类别效果最差、模态数越多成功率越高。

## 4. 资源与算力

- **论文未明确报告训练所需的 GPU 型号、数量及训练时长**。
- 仅可推断：使用 Vicuna-7B 作为 LLM 主干，三阶段数据规模约 813K（阶段一）+ 1M（阶段二）+ 379K（阶段三）样本，整体训练成本在同类 7B 级 VLA 模型中属于常规水平，但具体算力配置与耗时无法从论文文本中获取。

## 5. 实验数量与充分性

- **实验组数**：主要包括 1 组主对比实验（9 个基线）、2 组消融（音频编码器双分支、CoThinkAct 模块）、1 组模态贡献分析，共约 4 大组实验。
- **充分性评估**：
  - **优点**：基线覆盖 RL、IL、零样本 Omni-MLLM、VLN SOTA 等多个范式；消融设计清晰，分别验证了音频空间分支/语义分支及 CoT/action head 的贡献；模态分析提供了与主观直觉一致的解释。
  - **不足**：仅在自己的 MINav 基准上评估，未在 VLN-CE、GOAT-Bench 等已有基准上报告迁移/泛化结果；未与同样支持音频的导航方法（如 AudioNav 类方法）直接对比；test-mini 仅 360 个片段，规模较小，统计显著性未报告；对基线的适配方式（如用 CLIP 将图像替换为类别标签）可能削弱基线表现，存在一定公平性风险。

## 6. 主要结论与发现

- 现有导航方法在 MINav 上表现不佳（如 Navid 仅 13.1% SR），说明**多模态指令导航仍是未解决且有研究空间的任务**。
- 多模态指令（尤其图像与音频线索）能有效降低歧义，显著提升导航成功率；RL 实验中完整指令优于仅目标描述，进一步验证了中途路标和多样化模态的重要性。
- 音频中的**空间信息**比语义信息对导航增益更大（空间分支单独带来 0.206→0.258 SR 的提升）。
- **CoThinkAct** 模块中的显式推理（CoT）和从 `[NAV]` token 解码动作的设计均对性能有益，且同时提供了可解释的决策过程。
- NaVLA² 作为首个视觉-语言-音频-动作导航模型，取得了 SOTA 结果（SR 27.2%，SPL 19.6%）。

## 7. 优点

- **任务设计新颖且有实际意义**：首次提出多模态指令导航，贴近人类利用视觉+听觉+语言协同定位的自然行为，弥补了现有单模态指令任务的根本缺口。
- **自动化数据流水线成熟**：两阶段管线（多模态参照标注 + 片段合成）在规模（43.9K）上具备扩展性，并设计了质量过滤（路径偏移比、BERT 相似度、人类专家筛选）。
- **音频建模有深度**：双分支空间-语义音频编码器是首个在导航 VLA 中系统区分"声源

- **音频建模有深度**：双分支空间-语义音频编码器是首个在导航 VLA 中系统区分"声源是什么"与"声源在哪里"的尝试，且通过消融实验证明了空间分支的关键作用；结合混响模拟的音频渲染，使仿真环境中的听觉感知更接近真实物理规律。
- **CoThinkAct 设计精巧**：将 LLM 的推理与行动解耦但共享上下文，既保留了 CoT 的可解释性，又通过 `[NAV]` token 嵌入实现动作解码，避免了传统"先输出文本再解析动作"的级联误差，且只需一次前向传播，效率较高。
- **实验分析较为扎实**：不仅报告了主结果，还按目标模态、指令模态数量进行了细粒度分析，揭示了不同模态对导航消歧的贡献差异，为后续研究提供了有价值的参考。

## 8. 缺点与局限

- **基准封闭性**：仅在自建的 MINav 基准上评估，未与现有主流导航基准（如 VLN-CE、GOAT-Bench、AudioNav 等）进行对比或迁移测试，难以判断模型在通用导航能力上的泛化水平。
- **基线公平性存疑**：部分基线（如 RL(goal-nav)、Navid 等）本身并非为多模态指令设计，作者仅以简化方式适配（如将图像转为类别标签、忽略音频），可能低估了基线的潜力；零样本 MLLM 基线（Qwen2.5-Omni、Gemini）的提示工程细节未充分披露，也可能影响对比公平性。
- **音频描述的主观性**：目标物体的"听觉描述"由 GPT 生成文本再检索音频片段，过滤阈值（BERT 相似度 0.5）可能引入大量语义不匹配或难以辨识的声音；同时，模拟中音频源位置固定在物体中心，未考虑发声体移动或环境背景噪声，与真实世界仍有差距。
- **语言指令依赖 LLM 生成**：多模态指令文本由 GPT-4o 合成，可能带有模板化、过度详细的问题，与真实人类指令分布存在偏移；人类指令往往更简洁、隐含更多常识，模型在真实场景中的表现可能打折扣。
- **规模与统计性**：test-mini 仅 360 个片段，主测试集 2,628 个片段，虽有一定规模，但未报告置信区间或显著性检验；且成功阈值（3 米半径）较为宽松，对目标物体较小的场景可能高估性能。
- **计算资源不透明**：未报告训练耗时、GPU 型号/数量，复现成本未知；三阶段训练（尤其阶段二的 1M 多模态 QA 数据微调）的细节（数据来源、配比）未充分说明，影响可复现性。
- **动作空间与任务粒度**：仅 3 个低级动作（前进、左转、右转），未包含后退或连续速度控制，且 STOP 判定依赖距离阈值，较简化；每一步的音频观测虽动态更新，但模型如何利用历史音频（是否仅用当前帧）未明确说明。

## 9. 个人看法与展望

- **任务定义本身具有启发意义**：将视觉、语言、音频三条线索统一到"指令"中，使导航任务更贴近人类多感官协同的认知过程，为具身智能提供了更自然的人机交互范式。其"路标+目标"的层级指令结构，也与经典 VLN 的子目标思想一脉相承。
- **数据流水线是主要贡献之一**：自动生成多模态参照（图像视角选择、GPT 语言描述、音频检索）的思路可迁移到其他具身任务（如操作、问答），但声音生成部分仍显薄弱（检索而非合成），未来可探索文本到音频生成（TTA）来丰富声学多样性。
- **模型架构的通用性**：空间-语义音频双分支设计不仅适用于导航，也可用于语音定位、音视频事件理解等；CoThinkAct 将推理和行动并行输出的思想，对未来"既能解释又能行动"的具身大模型有参考价值。
- **潜在改进方向**：
  1. 在更多公共基准上评测并开放代码、模型权重，增强可复现性；
  2. 引入更丰富的动作空间（如速度控制、连续导航）和更真实的音频仿真（动态声源、多声源混叠）；
  3. 探索音频-视觉-语言的统一预训练，使模型在未见过环境中的多模态对齐更鲁棒；
  4. 关注指令的多样性，收集真实人类语音指令，使任务更加实用。

## 10. 关键术语与缩写表

| 术语/缩写 | 全称/含义 |
|---|---|
| NaVLA² | Navigation Vision-Language-Audio-Action model（导航视觉-语言-音频-动作模型） |
| MINav | Multimodal Instruction Navigation（多模态指令导航任务） |
| HM3DSem | Habitat-Matterport 3D Semantic Dataset（三维语义场景数据集） |
| VLA-3D | 用于三维场景图提取的视觉-语言-动作模型 |
| CLIP | Contrastive Language-Image Pre-training（对比语言-图像预训练模型） |
| CLAP | Contrastive Language-Audio Pre-training（对比语言-音频预训练模型） |
| SpatialAST | 用于空间音频的 Audio Spectrogram Transformer 变体 |
| SoundSpaces 2.0 | Meta 发布的音频仿真平台，支持双耳渲染 |
| RIR | Room Impulse Response（房间脉冲响应） |
| CoT | Chain-of-Thought（思维链推理） |
| CoThinkAct | 并行思考与行动模块（Thinking + Acting） |
| LLM | Large Language Model（大语言模型） |
| LoRA | Low-Rank Adaptation（低秩适配微调技术） |
| SR / OSR | Success Rate / Oracle Success Rate（成功率 / 预言成功率） |
| SPL | Success weighted by Path Length（路径长度加权成功率） |
| SoftSPL | 基于连续距离的 SPL 变体 |
| NE | Navigation Error（导航误差） |
| nDTW | normalized Dynamic Time Warping（规范化动态时间规整） |
| VLN | Vision-and-Language Navigation（视觉语言导航） |
| VLN-CE | Vision-and-Language Navigation in Continuous Environments（连续环境视觉语言导航） |
| GOAT-Bench | 多模态目标导航基准（GOAT Benchmark） |
| DD-PPO | Decentralized Distributed Proximal Policy Optimization（去中心化分布式 PPO 强化学习算法） |
| IL | Imitation Learning（模仿学习） |
| RL | Reinforcement Learning（强化学习） |
| MLLM | Multimodal Large Language Model（多模态大语言模型） |
| test-mini | 人类专家筛选的小型测试子集（360 条） |

（完）
