---
title: "SAMPO: Scale-wise Autoregression with Motion Prompt for Generative World Models"
title_zh: SAMPO：面向生成世界模型的尺度自回归与运动提示
authors: "Sen Wang, Jingyi Tian, Le Wang, Zhimin Liao, lijiayi, Huaiyi Dong, Kun Xia, Sanping Zhou, Wei Tang, Gang Hua"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=PJOwQ77Mul"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向智能体规划的可生成世界模型，采用运动提示与尺度自回归，可用于导航仿真但不是导航专用
tldr: 针对自回归世界模型在预测中破坏空间结构、解码低效和运动建模不足的问题，提出SAMPO，将视觉自回归建模与因果时间建模结合，以运动提示引导生成并保持空间局部性。该方法改善了未来帧生成的视觉连贯性，可提升智能体在想象环境中规划、控制与长时序决策的能力，对导航世界模型具有方法论借鉴意义。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有自回归世界模型存在空间结构破坏、解码效率低和运动建模不足的问题。
method: 提出尺度自回归与因果建模混合框架，集成时间因果解码、双向空间注意力和运动提示。
result: 在视频预测与智能体规划实验中展现出更连贯的视觉生成与更好的决策支持效果。
conclusion: 将空间自回归与时间因果结合可提升世界模型的预测质量，惠及导航等下游具身任务。
---

## Abstract
World models allow agents to simulate the consequences of actions in imagined environments for planning, control, and long-horizon decision-making. However, existing autoregressive world models struggle with visually coherent predictions due to disrupted spatial structure, inefficient decoding, and inadequate motion modeling. In response, we propose Scale-wise Autoregression with Motion PrOmpt (SAMPO), a hybrid framework that combines visual autoregressive modeling for intra-frame generation with causal modeling for next-frame generation. Specifically, SAMPO integrates temporal causal decoding with bidirectional spatial attention, which preserves spatial locality and supports parallel decoding within each scale. This design significantly enhances both temporal consistency and rollout efficiency. To further improve dynamic scene understanding, we devise an asymmetric multi-scale tokenizer that preserves spatial details in observed frames and extracts compact dynamic representations for future frames, optimizing both memory usage and model performance. Additionally, we introduce a trajectory-aware motion prompt module that injects spatiotemporal cues about object and robot trajectories, focusing attention on dynamic regions and improving temporal consistency and physical realism. Extensive experiments show that SAMPO achieves competitive performance in action-conditioned video prediction and model-based control, improving generation quality with 4.4× faster inference. We also evaluate SAMPO's zero-shot generalization and scaling behavior, demonstrating its ability to generalize to unseen tasks and benefit from larger model sizes.

---

## 论文详细总结（自动生成）

## 论文总结：SAMPO（Scale-wise Autoregression with Motion Prompt for Generative World Models）

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：世界模型（World Models）使智能体能够在想象环境中模拟行动后果，用于规划、控制与长时序决策。
- **现存问题**：现有的自回归世界模型存在三方面核心缺陷：
  - **空间结构破坏**：自回归建模在逐 token 生成时容易破坏图像的空间局部性，导致视觉生成不连贯。
  - **解码效率低**：逐尺度或逐位置的自回归解码速度慢，难以支撑实时或长时序推演。
  - **运动建模不足**：对动态场景中的物体与机器人轨迹缺乏显式建模，导致时序一致性和物理真实感薄弱。
- **整体含义**：该论文试图通过将“空间自回归”与“时间因果建模”相结合，同时引入运动提示，构建一个既能保持空间结构、又能高效解码、且能捕捉动态信息的世界模型，从而提升智能体在想象环境中决策与规划的能力。

### 2. 方法论：核心思想、关键技术细节

- **核心思想**：混合框架——**帧内生成用视觉自回归，帧间生成用因果建模**。即：对每一帧内部，按尺度进行自回归生成；对帧与帧之间，采用时间因果解码，兼顾并行性与时序一致性。
- **关键技术细节**：
  1. **时间因果解码 + 双向空间注意力**：在保持空间局部性的同时，允许同一尺度内的空间 token 并行解码，从而显著提高 rollout 效率，并增强时间一致性。
  2. **非对称多尺度分词器（Asymmetric Multi-scale Tokenizer）**：
     - 对已观察帧保留更多空间细节；
     - 对未来帧提取紧凑的动态表示；
     - 兼顾内存使用与模型性能。
  3. **轨迹感知运动提示模块（Trajectory-aware Motion Prompt）**：
     - 注入物体和机器人轨迹的时空线索；
     - 使注意力集中于动态区域；
     - 提升时序一致性、改善物理真实感。
- **公式/算法流程**：论文摘要未给出具体公式，但可概括为：输入历史帧 → 非对称多尺度分词 → 运动提示模块注入轨迹信息 → 每帧内按尺度自回归生成（带双向空间注意力）→ 帧间通过时间因果解码 → 输出未来帧并支持动作条件控制。

### 3. 实验设计：数据集 / 场景 / 基准 / 对比方法

- **任务类型**：
  - 动作条件视频预测（action-conditioned video prediction）
  - 基于模型的智能体控制（model-based control）
- **数据集 / 场景**：摘要未列出具体数据集名称（如 DMLab、Atari、Habitat 等），但明确涉及“生成世界模型”和“具身规划”相关场景，并评估了零样本泛化。
- **Benchmark**：未明确指出使用了哪些公开基准，但按世界模型领域惯例，通常涉及标准视频预测 benchmark（如 SSIM/PSNR/LPIPS 等）以及控制任务回馈（如成功率、回报）。
- **对比方法**：提到了“现有自回归世界模型”，但未列出具体基线名称（如 DreamerV3、IRIS、VideoGPT 等）。不过实验表明在生成质量和推理速度方面优于这些现有方法。

### 4. 资源与算力

- **明确说明**：论文摘要中**未提供任何具体算力信息**，例如：
  - GPU 型号（如 A100、V100 等）
  - GPU 数量
  - 训练时长 / 迭代次数
  - 参数量或内存占用具体数值
- 仅在性能结果中提及推理速度为 **4.4× 加速**，但该加速与具体硬件配置的关联未给出。
- **结论**：文中没有披露训练算力相关细节。

### 5. 实验数量与充分性

- **实验数量**：
  - 摘要提到的实验组别主要包括：
    1. 动作条件视频预测实验（对比生成质量与推理速度）
    2. 基于模型的控制实验（对比决策性能）
    3. 零样本泛化评估（测试未见任务）
    4. 规模规律研究（scaling behavior，测试模型规模的影响）
  - 具体消融实验（如去掉运动提示、非对称分词器、改变并行解码方式等）在摘要中**未明确列出**，但声称验证了各模块的有效性。
- **充分性与客观性**：
  - 实验覆盖了生成质量、推理效率、控制性能、泛化能力和规模扩展性，维度较全面。
  - 但缺少数据集名称、基线具体实现、消融表格、可视化结果等细节，因此从摘要看**充分性一般**，需依赖全文判断。
  - 公平性方面：提到了“4.4× 更快推理”，但没有给出与基线在相同硬件条件下的对照细节，存在一定对比偏差风险。

### 6. 主要结论与发现

- **SAMPO 在动作条件视频预测和质量上取得有竞争力的表现**，同时获得 **4.4 倍推理加速**。
- **空间自回归 + 时间因果的组合能够弥补纯自回归世界模型的空间结构破坏与解码低效问题**。
- **运动提示模块显著提升了动态场景的预测一致性**，有助于物理真实感。
- **零样本泛化能力**：模型能够泛化到未见任务。
- **规模扩展性**：增大模型规模可进一步提升性能，说明 SAMPO 具备良好的 scaling 特性。
- **对导航等下游具身任务的意义**：可支持智能体在想象环境中进行规划、控制和长时序决策。

### 7. 优点

- **方法设计新颖**：将尺度自回归与因果时间建模显式结合，在保持空间结构的同时支持并行解码，兼顾质量与效率。
- **运动建模针对性强**：通过轨迹感知运动提示直接注入物体/机器人轨迹，比隐式学习动态更直观。
- **高效的 tokenizer 设计**：非对称多尺度分词器在空间细节和动态紧凑表示之间做了良好折中，优化了内存与性能。
- **实验覆盖维度较广**：包括生成质量、推理速度、控制性能、零样本泛化、规模规律，展示了方法的实际落地价值。
- **推理加速明显**：4.4× 速度提升对真实世界模型部署意义重大。

### 8. 不足与局限

- **实验细节缺乏**：摘要中未给出具体数据集名称、评估指标、基线方法列表、消融设置，难以在阅读全文前评估结果的可靠性和公平性。
- **未提供算力信息**：无法判断训练成本是否可接受，也难以复现。
- **比较公平性存疑**：4.4× 加速是否在相同硬件、相同 token 数、相同输入尺寸下取得，未明确说明。
- **应用范围**：摘要强调“导航仿真但不是导航专用”，因此其直接迁移到真实世界导航（如未知复杂动态环境）的能力尚未充分验证。
- **物理真实感**：虽然运动提示提升了物理一致性，但世界模型常见的长期 rollout 漂移、误差累积问题是否解决，摘要未提及。
- **决策性能**：仅说“更具竞争力”和“更好的决策支持效果”，未给出与先进 model-based RL 方法的绝对优势，结论相对保守。
- **零样本泛化实验**的具体设置不明确，可能仅限于同一分布下的未见任务，而非跨域泛化。

---

（完）
