---
title: "Chain-of-Search: Parameter-Efficient Reasoning for Zero-Shot Object Navigation"
title_zh: 搜索链：零样本物体导航的参数高效推理
authors: "Hanrui Chen, Liqi Yan, Qifan Wang, Jianhui Zhang, Fangli Guan, Pan Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37150/41112"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 零样本物体导航；迭代语义推理；参数高效LLM框架
tldr: 针对零样本物体导航中视觉语言导航方法存在的语义对齐误差与LLM导航专用性不足问题，提出参数高效的链式搜索框架。该框架用最优效益多地图构建替代传统全局地图，并通过迭代语义推理实现类人决策。实验显示该方法能更高效地定位未知环境中的目标物体，为物体导航提供了低成本且有效的推理范式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37150/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37150/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1727, \"height\": 849, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-37150/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1685, \"height\": 792, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37150/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 676, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37150/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 761, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37150/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 881, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37150/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 876, \"height\": 219, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-37150/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 877, \"height\": 272, \"label\": \"Table\"}]"
motivation: 现有LLM导航方法存在语言地图与真实布局语义错位，且对大模型导航任务专化不足。
method: 提出链式搜索参数高效框架，构建最优效益多地图并迭代进行语义推理。
result: 在未知环境目标定位上展现更高效率和准确性，减少了对大型模型微调的依赖。
conclusion: 参数高效的迭代语义搜索可显著提升零样本物体导航性能。
---

## Abstract
Zero-shot object navigation tasks agents with locating target objects in unseen environments—a core capability of embodied intelligence. While recent vision-language navigation methods leverage Large Language Models (LLMs) for multimodal reasoning, they suffer from two key limitations: (1) semantic misalignment between language-grounded maps and real-world layouts, and (2) inefficiency due to LLMs’ lack of specialization for navigation-specific tasks. To address these challenges, we propose Chain-of-Search (CoS), a novel parameter-efficient framework that enables human-like decision-making via iterative semantic reasoning. First, CoS replaces traditional global maps with an optimal-benefit multi-map construction that continuously balances expected gain and cost throughout the navigation process. Second, we introduce a Parameter-Efficient Intent Aligner (PEIA), trained via a prompt-guided paradigm to align directional decisions with navigation intent. PEIA injects semantic cues into benefit-aware maps, enabling more rational and goal-consistent exploration. Finally, a Reflection-Guided Destination Verifier (RDV) confirms whether the target is reached via language-driven reasoning and corrects potential errors through self-reflection. CoS achieves state-of-the-art performance on HM3D (+2.8% SR) and MP3D (+1.2% SR) without relying on LLMs, demonstrating the effectiveness of lightweight, reasoning-centered navigation.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义

- **任务背景**：零样本物体导航（Zero-Shot Object Navigation）要求智能体在从未见过的环境中定位目标物体，是具身智能的核心能力之一。该任务本质上是未知环境下的探索 + 语义推理问题。
- **现有方法的两个关键缺陷**：
  - **语义错位（Semantic Misalignment）**：基于语言建模的全局地图常常与实际环境布局不一致。由于相机视野有限、语言-视觉融合不完备，构建的语义地图会累积错误，误导智能体朝向无关区域探索，降低效率与成功率。
  - **计算效率低下**：主流方法依赖大规模语言模型（LLM），如 NavGPT、GAMap、ImagineNav 等使用 GPT-4/4V、GPT-4o-mini 等，参数规模从几十亿到上万亿。然而，通用 LLM 并未针对导航任务特化，规模庞大但“力不专精”，在细粒度的空间-时间决策上推理效率低且常常次优。
- **论文的核心主张**：一个轻量级、参数高效的、不依赖 LLM 的推理驱动导航框架，能够模拟人类的搜索行为（逐步推理、平衡收益与代价、验证目标），从而在零样本条件下达到 SOTA 性能。

## 2. 方法论：Chain-of-Search (CoS)

### 2.1 核心设计思想

CoS 将零样本物体导航视为一个“多阶段链式搜索”过程，模仿人类在陌生环境中的决策方式：原地旋转建立初始环境认知 → 基于语义先验与距离代价选择最有希望的探索方向 → 接近疑似目标时反复验证 → 最终确认并停止。其核心架构由三部分构成：**最优效益多地图构建（Optimal-Benefit Multi-Map Construction）**、**参数高效意图对齐器（PEIA）** 和 **反思引导目的地验证器（RDV）**。

### 2.2 最优效益多地图构建

- **初始地图与可导航边界**：通过里程计和深度图投影建立自上而下的 2D 占据地图，动态记录机器人的轨迹与观测；可导航边界（frontiers）定义为探索区域边界的中点。
- **语义地图（Semantic Map）**：将地图探索形式化为图像-描述预测任务。PEIA 对当前 RGB 图像和包含 `<mask>` 标记的提示文本进行编码，预测掩码位置的词概率，从而为视野内每个像素赋予语义价值（公式 1）；重叠区域通过置信度加权更新（公式 2）。
- **置信度地图（Confidence Map）**：模拟人类正前方观察更可靠的感知偏差。置信度随偏离航向角度的增大而按余弦函数递减（公式 3）；重叠区域取加权值（公式 4）。
- **成本地图（Cost Map）**：考虑距离因素，鼓励机器人沿当前方向向远处探索，避免频繁回访已探索区域。成本值定义为与距离的 k 次幂成反比（公式 5）。
- **地图融合与最优边界选择**：对每个边界计算其周围半径 r 以内的平均语义得分与置信度得分的乘积（融合得分），选择得分最高的边界作为最优效益前端（公式 6）。

### 2.3 参数高效意图对齐器（PEIA）

- **整体结构**：采用编码器-解码器架构，Swin Transformer 作为视觉编码器，文本与视觉 token 经跨模态注意力对齐。大部分组件在预训练后冻结，仅训练少量连续提示（continuous prompts）和分类头。
- **两阶段训练策略**：
  - **预训练（离散提示）**：自动对输入文本中的名词和动词进行掩码（如“There may be a `<mask>` in the front area”），模型学习依据图像和上下文恢复被掩码的词，获得图像-文本对齐基础（公式 7）。
  - **微调（连续提示）**：参照 VPT（Visual Prompt Tuning），在 Transformer 解码器的每一层注入可学习的低维提示嵌入（公式 8），通过全连接层投影到注意力层，仅更新提示参数和预测头（公式 9-10）。
- **训练数据**：仅使用 MS COCO 数据集（约 0.33M 样本），模型总参数量约 0.122B（即 1.22 亿），远小于 BLIP2 的 7.8B，也不需要 LLM 级别的推理调用。

### 2.4 反思引导目的地验证器（RDV）

- **目标检测与分割**：采用 YOLOv7 检测 COCO 类别物体，对开放词汇目标（如任意文本描述的目标）使用 Grounding-DINO 进行开放集检测；随后使用 Mobile-SAM 生成分割掩码，用于目标的精确空间定位。
- **VQA 确认**：将检测到的目标与导航目标拼接为视觉问答提示（如“Question: Is this a bed? Answer: ____”），通过 VQA 模块进行二次确认。若否定回答则返回探索阶段；若肯定回答则融合 RGB/深度生成点云，取最近 25% 点的质心作为导航终点。
- **可见区域导航策略**：所有局部导航行为（前往边界或目标点）统一采用基于 VER 策略的 point-goal 导航策略，只需深度输入和目标相对位置，无需语义监督，提升了对遮挡场景的鲁棒性。

## 3. 实验设计

- **数据集与基准**：
  - **HM3D**（Habitat-Matterport 3D）：验证集包含 6 个目标类别、20 个场景、2000 个 episode。
  - **MP3D**（Matterport3D）：验证集包含 21 个目标类别、11 个场景、2195 个 episode。
  - 评估在 Habitat 模拟器中进行。
- **评价指标**：成功率（SR↑）、基于路径长度的成功率加权（SPL↑）、到目标距离（DTG↓）、导航误差（NE↓）。
- **对比方法**：
  - **非零样本方法**：SemExp、PONI、L3MVN（Feed-forward）。
  - **使用 LLM/VLM 的零样本方法**：PixNav（GPT-4）、ESC（InstructGPT）、VoroNav（GPT-3.5）、ImagineNav（GPT-4o-mini）、GAMap（GPT-4V）、UniGoal（LLaMA-2-7B）。
  - **不使用 LLM/VLM 的零样本方法**：ZSON、CoW、L3MVN（Zero-Shot）、VLFM（CLRA 24 Best Paper）。

## 4. 资源与算力

- **论文未明确说明**具体使用的 GPU 型号、数量及训练时长。
- **可参考的信息**：
  - PEIA 总参数量约 **0.122B**，而 BLIP2（OPT 版）为 **7.8B**，参数量约为后者的 1/64。
  - PEIA 训练数据仅为 **0.33M 样本**（MS COCO），相比之下 BLIP2 使用了 129M 样本。
  - 整体框架参数量为 **469M**（含检测、分割等模块），远低于以 LLM 为基础的方案（GPT-4V 方案为 1.37T，PixNav 为 1.8T）。
  - 可以推断，CoS 的显存占用、训练代价和推理延迟都远低于 LLM-based 方法，但论文未给出精确的 FLOPs 对比或推理时延数据。

## 5. 实验数量与充分性

- **实验组数**：
  - **主实验**：HM3D 和 MP3D 两个数据集上的综合对比（Table 1，覆盖全部 13 种对比方法）。
  - **详细对照**：与 VLFM 在 HM3D 上的额外对比（Table 2），包括 DTG、Travel Stairs 指标及定性路径可视化（Fig. 3）。
  - **模块消融**（Table 3）：逐一移除置信度地图、成本地图、语义地图、RDV 模块的对比实验。
  - **PEIA 对比实验**（Table 4）：PEIA vs. BLIP2（OPT）在 HM3D 上的对比。
  - **Prompt 训练策略消融**（Table 5）：移除预训练阶段和移除微调阶段的对比。
- **充分性评估**：
  - **优点**：在主实验覆盖了两个大规模真实场景数据集和多类基线（零样本/非零样本、有LLM/无LLM），消融实验覆盖了每个核心模块，且对 SPL 下降原因做了专门分析（多楼层探索），较为全面。
  - **不足**：实验完全依赖模拟器（Habitat），缺乏真实机器人部署验证；MP3D 上未报告对照消融结果，消融均在 HM3D 上完成，维度稍单一；部分对比数据来自论文原文而非统一代码库复现，可能存在环境与实现的微小差异（虽然有补充 VLFM 的复现实验，但仅限一个方法）。

## 6. 主要结论与发现

- **性能 SOTA**：CoS 在 **HM3D** 上 SR 达 **55.9%**（较 GAMap（GPT-4V）高 +2.8%，较 VLFM 高 +3.4%）；在 **MP3D** 上 SR 达 **37.6%**（较 VLFM 高 +1.2%），且全程不依赖任何 LLM/VLM。
- **参数效率突出**：与依赖 GPT-4V 的 GAMap（1.37T）相比，CoS 仅需 469M 总参数，即做到了更高的成功率，验证了“轻量化推理”路线的可行性。
- **各模块均有贡献**：语义地图对最终定位精度（DTG）贡献最大；RDV 对降低导航误差（NE）最为关键（移除后面 NE 增加 8.6%）；置信度地图和成本地图均能稳定提升整体性能。
- **两阶段 prompt 训练有效**：预训练阶段对 SR 贡献显著（移除后 SR 降 3.55%），微调阶段贡献较小但仍在 DTG 上有改善，说明先学习基础语义再对齐导航意图是合理的学习范式。
- **更类人的搜索行为**：CoS 比 VLFM 更倾向于跨楼层探索（Travel Stairs +2.0%），在需要推理的复杂场景下策略更接近人类。

## 7. 优点

- **轻量而有效**：首次以大约 1 亿参数的视觉语言模型替代 10 亿/万亿级 LLM/ VLM 完成零样本导航的语义推理，在 SR 上全面超越 LLM 路线。
- **模块解耦清晰**：地图构建、语义推理、目标验证三段式分工明确，每一模块都是独立可替换的组件（可替换为更强的检测器/分割器/VQA），具有良好的扩展性。
- **训练成本极低**：PEIA 仅需 MS COCO 即可完成训练，无需任何物体导航数据集或强化学习信号，降低了数据门槛。
- **推理过程可解释**：通过最优效益地图+链式搜索+反射验证，每一步决策都有可追溯的依据（语义得分、置信度、成本），而非 LLM 的黑盒输出。
- **刻意处理了公平性**：文中补充了 VLFM 的复现对比（Table 2），定性可视化（Fig. 3）直观展示了路径质量差异，并对 SPL 指标略低的原因（多楼层探索）给出了显性解释，而非回避。

## 8. 不足与局限

- **SPL 指标尚有差距**：在 HM3D 上 SPL（29.1%）低于 VLFM（30.4%），论文将其归因于跨楼层搜索的倾向，但这也说明路径效率并非最优。CoS 对简单场景可能过度探索。
- **真实环境部署未验证**：所有实验均在 Habitat 模拟器中进行，未在真实机器人上验证感知误差、运动控制噪声等对框架的影响；检测/分割/VQA 模块的级联错误在实际环境中可能被放大。
- **训练与推理资源未透明化**：未报告 GPU 型号/数量/训练时间/推理延迟等关键资源数据，读者难以精确评估部署门槛。
- **消融实验范围有限**：模块消融仅在 HM3D 上执行，MP3D 上的消融缺失；未对 k（成本函数超参数）、r（边界融合半径）等关键超参数做敏感性分析。
- **依赖组件较多**：框架串联了 YOLOv7、Grounding-DINO、Mobile-SAM、VQA 等多个外部模型，任一环节的精度都会影响整体，整体可靠性高度依赖各子模块的质量。
- **对长尾目标覆盖不足**：PEIA 的语义先验来源于 MS COCO，虽然 Grounding-DINO 支持开放词汇检测，但 PEIA 的语义引导仍偏向常见家居物体，对罕见类别物体的先验估计可能较弱。

（完）
