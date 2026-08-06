---
title: "Agent Journey Beyond RGB: Hierarchical Semantic-Spatial Representation Enrichment for Vision-and-Language Navigation"
title_zh: 智能体超越RGB之旅：面向视觉-语言导航的分层语义-空间表征增强
authors: "Xuesong Zhang, Yunbo Xu, Jia Li, Ruonan Liu, Zhenzhen Hu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38948/42910"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 面向未知环境的视觉-语言导航，提出分层语义-空间表征增强。
tldr: 视觉-语言导航中，智能体往往只是简单拼接RGB与其他模态特征，未能充分利用语义知识和空间布局的互补性。该文提出SUSA架构，以分层方式同时建模语义理解与空间感知，使智能体在不同尺度上感知和锚定环境。在多个VLN基准上的实验表明，该方法相比现有多模态融合方案显著提升了未知环境下的导航成功率，为视觉-语言导航的环境表征学习提供了新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38948/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 831, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38948/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1739, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38948/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38948/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 822, \"height\": 583, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38948/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38948/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 839, \"height\": 607, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38948/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1758, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38948/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 862, \"height\": 398, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38948/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38948/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 815, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38948/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 841, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38948/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 883, \"height\": 270, \"label\": \"Table\"}]"
motivation: 现有VLN方法对各模态特征利用不充分，影响未知环境下的指令定位与导航。
method: 设计分层语义理解与空间感知（SUSA）架构，在不同尺度上融合语义与空间信息。
result: 在VLN基准上显著提升未知环境的导航成功率。
conclusion: 验证了分层语义-空间表征对指令导航的有效性。
---

## Abstract
Navigating unseen environments based on natural language instructions remains difficult for egocentric agents in Vision-and-Language Navigation (VLN). 
Intuitively, humans inherently ground concrete semantic knowledge within spatial layouts during indoor navigation. 
Although previous studies have introduced diverse environmental representations to enhance reasoning, other co-occurrence modalities are often naively concatenated with RGB features, resulting in suboptimal utilization of each modality's distinct contribution. 
Inspired by this, we propose a hierarchical Semantic Understanding and Spatial Awareness (SUSA) architecture to enable agents to perceive and ground environments at diverse scales. 
Specifically, the Textual Semantic Understanding (TSU) module supports local action prediction by generating view-level descriptions, thereby capturing fine-grained environmental semantics and narrowing the modality gap between instructions and environments. 
Complementarily, the Depth-enhanced Spatial Perception (DSP) module incrementally constructs a trajectory-level depth exploration map, providing the agent with a coarse-grained comprehension of the global spatial layout.
Extensive experiments demonstrate that SUSA's hierarchical representation enrichment not only boosts the navigation performance of the baseline on discrete VLN benchmarks (REVERIE, R2R, and SOON), but also exhibits superior generalization to the continuous R2R-CE.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

视觉-语言导航（Vision-and-Language Navigation, VLN）要求智能体在未知的室内环境中，根据自然语言指令逐步导航到目标位置或识别指定物体。尽管近年来VLN领域取得了显著进展，该任务仍面临两个核心挑战：

- **模态异质性（Modality Heterogeneity）**：语言指令中的地标概念（如"couch"、"living room"）与RGB视觉特征之间存在本质的模态差异，导致智能体难以将文本中的语义描述与视觉场景精确对齐。
- **各模态表征利用不充分**：虽然已有研究引入了深度、语义、频谱等多种配准模态（co-occurrence modalities）来丰富环境表示，但这些方法大多**简单地将不同模态特征与RGB特征拼接（naive concatenation）**，未能充分挖掘每种模态的独特贡献，也缺乏对各模态作用的可解释性。

**核心观察**：人类在室内导航时，天然会将具体的语义知识（如识别地标）与空间布局感知（如理解走廊走向）结合起来。受此启发，论文提出了一种**分层语义理解与空间感知（SUSA, Semantic Understanding and Spatial Awareness）架构**，让智能体在不同尺度上感知和锚定环境：局部层面利用细粒度的文本语义描述辅助动作决策，全局层面利用深度空间地图增强对环境的整体感知。

---

### 2. 论文提出的方法论

SUSA以DUET（Chen et al., 2022b）为基线，在RGB全景图之外引入**视图级文本全景描述**和**轨迹级深度探索地图**，由三个核心模块组成：

#### （1）文本语义理解模块（TSU, Textual Semantic Understanding）

- **显著地标提取器**：利用预训练的BLIP-2-FlanT5-xxL视觉语言模型，对每个RGB视角生成文本描述（如"a living room with two chairs"），构成文本全景图 S_t = {s_{t,i}}_{i=1}^{36}；再用CLIP文本编码器提取文本语义特征 X_t^S。
- **文本语义选择器**：结合**静态匹配**与**动态匹配**两种策略，选择与指令最相关的视角：
  - **静态匹配**：计算文本语义与指令词之间的余弦相似度矩阵 M ∈ R^{n×l}，通过行方向最大池化筛选最相关地标；
  - **动态匹配**：使用标准Transformer解码器层的交叉注意力机制 TCA(X_t^S, I, I) 建模文本语义与指令之间的长程交互关系；
  - 两种策略通过平衡因子 δ 加权融合：\tilde{X}_t^S = δ · Γ_t^{stat} + (1 − δ) · Γ_t^{dyn}。

#### （2）深度增强空间感知模块（DSP, Depth-Enhanced Spatial Perception）

- **深度增强探索地图构建**：使用ResNet-50（在Gibson数据集上预训练）提取深度全景特征，CLIP提取RGB全景特征，通过共享权重的两层Transformer全景编码模块，逐步构建深度探索地图 T_t^D 和RGB探索地图 T_t^R，记忆导航轨迹信息。
- **跨模态交互与推理**：设计四层跨模态Transformer编码器，结合图感知自注意力（GASA）、跨模态注意力和前馈网络，使指令与深度地图、RGB地图、RGB全景图分别进行交互，得到细化表征 \tilde{T}^D、\tilde{T}^R 和 \tilde{X}^R，支持全局和局部预测。

#### （3）分层聚合与预测模块（HAP, Hierarchical Aggregation and Prediction）

- **混合表征聚合**：通过注意力池化将文本语义、深度地图、RGB全景和RGB地图投影到低维潜在空间，并使用可学习的平衡向量 B = [β₁, β₂, β₃, β₄]ᵀ 进行加权聚合，得到混合环境表征 E_hyb。
- **分层动作预测**：分别对局部（\tilde{X}^S 与 \tilde{X}^R）和全局（\tilde{T}^D 与 \tilde{T}^R）预测分数进行加权融合，再通过动态融合策略预测最终动作 a_t。

#### 训练策略

- **部分预训练**：仅对黑色箭头所示的计算流进行预训练（MLM、MRC、SAP、OG辅助任务），避免深度/文本语义稀疏导致过拟合；
- **对比学习**：引入对比学习损失 L_cl 对齐混合环境表征与指令语义；
- **模仿学习**：采用混合单步动作预测损失 L_hsap，最终总损失为 L_SUSA = λ₁L_hsap^gt + L_hsap* + λ₂L_cl，其中 λ₁=0.2，λ₂=0.8。

---

### 3. 实验设计

论文在**四个VLN基准**上评估了SUSA的性能：

| 基准 | 任务特点 |
|------|----------|
| R2R（Anderson et al., 2018） | 仅需根据详细指令逐步导航 |
| REVERIE（Qi et al., 2020） | 导航到目标物体并从候选框中识别正确物体 |
| SOON（Zhu et al., 2021） | 需要利用物体检测器生成候选边界框 |
| R2R-CE（Krantz et al., 2020） | 连续环境（Habitat模拟器），用于评估泛化能力 |

**评估指标**：SR（成功率）、OSR（Oracle成功率）、NE（导航误差）、SPL（路径加权成功率）以及REVERIE/SOON的RGS/RGSPL。

**对比方法**：包括DUET（基线）、GridMM、KERM、AZHP、FDA、CONSOLE、ACME、SEAT、ETPNav等近年来的主流VLN方法。为保证公平，排除了涉及预探索或大规模数据增强的方法。

---

### 4. 资源与算力

- 论文明确提到：**所有实验均在单个 NVIDIA RTX 4090 GPU 上完成**。
- 预训练进行了 **100k 次迭代**，批大小为32；微调进行了 **25k 次迭代**，各任务的批大小分别为 R2R=4、REVERIE=8、SOON=2、R2R-CE=16。
- **未明确说明**训练总时长、GPU使用天数等具体算力消耗细节。

---

### 5. 实验数量与充分性

论文开展了**较为丰富的实验**，具体包括：

- **主实验**：在REVERIE、R2R、SOON三个离散基准上的全面对比，以及在R2R-CE连续环境上的泛化验证；
- **消融实验**共4组：
  1. **图像特征 vs. 结构特征**：对比ViT/CLIP作为RGB编码器，ImageNet/Gibson预训练的ResNet-50作为深度编码器的效果；
  2. **静态匹配 vs. 动态匹配**：分析平衡因子 δ 在不同取值（0、0.5、1.0、自适应）下的影响；
  3. **改进泛化的预训练策略**：对比部分预训练、完全预训练和随机初始化在seen/unseen分割上的性能差距；
  4. **总体组件消融**：逐个移除/添加DSP、TSU、HAP模块验证各自贡献；
- **定性分析**：展示SUSA与DUET在R2R上的轨迹对比案例。

**充分性评价**：实验覆盖了从离散到连续环境、从细粒度消融到全局对比的多个维度，整体较为充分。但以下方面可进一步优化：如SOON基准上对比方法数量较少；未报告多次运行的标准差；部分消融（如表6）在validation和test上的趋势不完全一致，论文对此给出了合理解释。

---

### 6. 论文的主要结论与发现

1. **SUSA显著优于基线DUET**：在REVERIE test unseen上，SPL/RGSPL达到41.5%/27.3%，较基线提升 **5.5%/5.3%**；在R2R test unseen上SPL达63.8%，较基线提升4.8%；在SOON上SPL达25.4%，较基线提升4.0%。
2. **分层语义-空间表征增强能够有效提升导航泛化能力**：TSU模块通过文本语义桥接指令与环境的模态鸿沟，DSP模块通过深度探索地图增强空间感知，二者在局部和全局尺度上形成互补。
3. **部分预训练策略优于完全预训练**：在REVERIE上，部分预训练将seen/unseen之间的SR差距缩小至21.11%，相比完全预训练减少了5.92%的差距，有效缓解过拟合。
4. **深度编码器预训练数据的选择至关重要**：使用Gibson（具有空间结构信息）预训练的ResNet-50比ImageNet预训练在SPL指标上取得显著更优效果。
5. **SUSA在连续环境R2R-CE上展现出良好的泛化能力**（SR=50.9、SPL=43.9），验证了离散环境中学习的表征可以迁移到连续导航场景。

---

### 7. 优点

- **方法设计有明确动机**：从"人类在导航中天然融合语义知识与空间布局"这一直觉出发，分层建模局部语义和全局空间信息，逻辑清晰、结构合理。
- **突破了简单的特征拼接范式**：通过TSU和DSP分别对文本语义和深度模态进行独立建模和指令对齐，增强了各模态的可解释性和利用效率。
- **利用现成大规模预训练模型（BLIP-2、CLIP）**：无需额外标注，以低成本获取丰富的文本语义描述。
- **部分预训练策略新颖且有效**：考虑到深度和文本语义的稀疏性，仅预训练关键路径，兼顾了训练效率与泛化性能。
- **实验覆盖面广**：涵盖4个基准（3个离散+1个连续），组内消融细致，且有定性案例支撑主要结论。
- **代码已开源**，便于复现和后续研究。

---

### 8. 不足与局限

- **对预训练视觉语言模型的依赖**：BLIP-2生成的文本描述质量直接影响TSU效果，若场景中物体描述不准确或遗漏，可能引入噪声。论文虽在补充材料中对描述质量有所讨论，但未给出定量评估指标。
- **深度图的来源限制**：DSP模块使用的是Matterport3D仿真器提供的**ground truth深度图**，在真实机器人场景中难以直接获取，限制了其在物理世界中的直接部署。
- **静态/动态匹配的平衡因子问题**：δ=0.5时效果最优，而自适应设置（δ可学习）反而性能下降，说明简单的可学习参数设计可能不够鲁棒，需要更精细的调节机制。
- **消融结果存在波动**：表6显示同时加入DSP+TSU（#4）在validation unseen上表现最优，但引入HAP后（#5）SR反而下降（51.7% vs 55.0%），论文归因于注意力池化的可学习token引入噪声，但这一现象也表明模块之间的交互效应尚未完全理解。
- **算力信息不够详细**：未报告单卡训练的具体时长、显存占用等，难以评估方法在资源受限场景下的可复现性。
- **没有报告多次实验的方差**，统计显著性未验证，结论的稳健性有待进一步确认。

---

（完）
