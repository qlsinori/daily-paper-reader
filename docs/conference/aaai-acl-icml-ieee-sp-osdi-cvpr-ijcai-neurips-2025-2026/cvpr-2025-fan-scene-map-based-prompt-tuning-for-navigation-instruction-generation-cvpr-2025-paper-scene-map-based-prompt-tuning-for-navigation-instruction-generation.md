---
title: Scene Map-based Prompt Tuning for Navigation Instruction Generation
title_zh: 基于场景地图提示调优的导航指令生成
authors: "Fan, Sheng, Liu, Rui, Wang, Wenguan, Yang, Yi"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Fan_Scene_Map-based_Prompt_Tuning_for_Navigation_Instruction_Generation_CVPR_2025_paper.pdf"
tags: ["query:semantic-map"]
score: 7.0
evidence: 采用场景地图提示调优，利用全局空间地图上下文生成导航指令
tldr: 针对现有导航指令生成方法只利用局部观测序列、缺乏全局空间理解，且直接输入地图文本描述难以充分发挥大语言模型能力的问题，本文提出基于场景地图的提示调优框架。该方法将场景地图中的离散空间信息转化为提示并引导大语言模型生成导航指令，从而在复杂三维环境中保持空间上下文一致性。实验结果显示该框架在基准数据集上显著提升了指令生成质量，说明显式利用场景地图有助于提升具身智能体的语言导航交互能力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 820, \"height\": 676, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 448, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1684, \"height\": 535, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1779, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1777, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1779, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 839, \"height\": 293, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 837, \"height\": 178, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 839, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 840, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 842, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 839, \"height\": 457, \"label\": \"Table\"}]"
motivation: 现有导航指令生成方法缺乏全局空间理解，在复杂3D环境中难以生成准确指示，且直接输入地图文本未充分利用LLM能力。
method: 提出场景地图提示调优框架，将地图离散空间信息转化为提示，引导大语言模型生成导航指令。
result: 在基准数据集上验证了该方法能提升导航指令生成质量，优于直接输入地图描述的基线。
conclusion: 显式建模场景地图上下文可有效增强指令生成的空间一致性，为具身智能体人机协同提供支持。
---

## Abstract
Navigation instruction generation (NIG), which provides interactive feedback and guidance to humans along a trajectory, is vital for developing embodied agents capable of human-machine communication and collaboration through natural language. Early data-driven methods directly map sequences of past observations to trajectory descriptions on limited datasets, lacking the necessary spatial understanding in complex 3D environments. While recent approaches leverage Large Language Models (LLMs) to improve NIG, they often overlook the global spatial context in navigation, such as the inherent space discretization in maps. Instead of straightforwardly feeding textual descriptions of the map into LLMs, we propose a scene map-based prompt tuning framework for NIG, MAPInstructor, which incorporates map context for parameter-efficient updating of LLMs. MAPInstructor comprises three key components: (i) scene representation encoding, where egocentric observations are projected into 3D voxels for fine-grained scene understanding; (ii) map prompt tuning, which integrates a topological map representation of the entire trajectory into an LLM-based decoder; and (iii) landmark uncertainty assessment, which mitigates hallucinations in landmark predictions, thereby enhancing the reliability and coherence of instruction generation. Extensive experiments on three navigation datasets (i.e., R2R, REVERIE, RxR) confirm the generalization and effectiveness of our algorithm.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与整体含义（研究动机与背景）

导航指令生成（NIG）是具身智能中的关键任务，要求智能体用自然语言描述导航轨迹，为人类提供交互式反馈与指引，对人类-机器人协作具有重要意义。该任务的核心挑战在于：**如何在复杂3D环境中生成空间准确、语义连贯且包含关键地标的指令**。

现有方法存在以下不足：

- **早期数据驱动方法**：直接将历史观测序列映射为轨迹描述，局限于有限数据集，缺乏复杂3D环境中的空间理解能力。
- **现有LLM方法**：虽然借助大语言模型（LLM）提升了指令质量，但往往忽略导航中的全局空间上下文——特别是地图中固有的空间离散化信息。
- **简单文本地图描述**：直接将地图转成文本送入LLM，一方面需要大量标注和训练，另一方面难以在零样本/少样本设置下捕获细粒度场景细节，易遗漏关键地标。
- **BEV表示局限**：先前的场景表示方法将高度感知特征压缩到BEV平面，损害了3D环境的整体结构，导致关键空间信息丢失。

针对上述问题，本文提出**MAPInstructor**——一种基于场景地图提示调优（Scene Map-based Prompt Tuning）的NIG框架，将拓扑地图信息与细粒度3D场景理解相结合，以参数高效方式微调LLM，从而提升导航指令生成质量。

## 二、方法论

### 核心思想

MAPInstructor的核心创新在于：**摒弃将地图转化为文本描述输入LLM的做法，而是将场景地图作为潜在特征（latent features）隐式融入LLM解码器**，同时采用3D体素（voxel）表示替代BEV平面表示以保留高度信息，并通过地标不确定性评估减少幻觉。

### 三大核心组件

**① 场景表示编码（Scene Representation Encoding）**

- **视角-动作嵌入**：将全景图像特征与离散方向信息（方位角、俯仰角）、步骤位置和观察类型结合，并通过线性层编码为语义特征。
- **透视-3D变换**：采用可变形注意力机制（Deformable Attention）与跨视角注意力（Cross-View Attention, CVA），将2D视角特征投影到3D体素空间中：`F3d = (1/K) Σ Fcva(Q, Pk, F2dk(h', w'))`，通过3D查询点采样周围视角特征，构建统一3D表示。
- **多尺度场景预测**：采用级联结构，在多个尺度上提取3D特征并逐级上采样，兼顾低层细节与高层语义。
- **场景表示**：将3D特征、视角嵌入与动作嵌入拼接映射为统一的场景节点表示 `vt`。

**② 地图提示调优（Map Prompt Tuning）**

- **拓扑地图构建**：将整条轨迹建模为有向图 `G={V,E}`，每个节点融合位置编码（2D/3D欧氏距离）与导航步骤编码，节点间通过图神经网络（采用GCN）进行迭代消息传递，聚合相邻节点的空间信息。
- **地图提示调优**：使用轻量Transformer解码器将图节点特征压缩为固定长度张量 `v̂`，作为提示（prompt）输入LLM（Llama-7B），以参数高效方式（仅微调少量参数）生成指令：
  - `xl = F_LLM(Θ*)(v̂; xl-1)`，其中 `|Θ*| ≪ |Θ|`

**③ 地标不确定性评估（Landmark Uncertainty Assessment）**

- 将生成过程分解为两阶段：**地标预测**与**指令补全**。
- 在地标预测阶段，生成M个地标序列，利用Deberta-large模型对地标列表进行语义等价性聚类。
- 计算地标语义熵（Semantic Entropy）：
  - `LE(v) = -Σc p(c|v̂) log p(c|v̂)`
- 若 `LE(v) ≤ τ`（τ=0.4），则地标预测信心充足；否则从M个地标预测中重新随机采样生成新的地标提示。
- 该机制有效缓解地标预测中的幻觉问题，提升生成指令的可靠性。

### 训练策略

- 采用两阶段训练：先训练地标预测（使用GPT-4从训练集提取真值地标作为标签），再训练指令补全（以真值地标为提示）。
- 使用PREVALENT合成的导航路线-指令对扩充训练数据。

## 三、实验设计

### 数据集

在三个主流导航指令生成基准数据集上评估：

| 数据集 | 特点 |
|---|---|
| **R2R** | 经典视觉-语言导航数据集，指令相对简洁 |
| **REVERIE** | 以目标物体检测为中心的远程参照表达数据集 |
| **RxR** | 更具挑战性的多语言密集时空定位数据集，指令更灵活复杂 |

### 评价指标

采用BLEU-1/4、CIDEr、METEOR、ROUGE、SPICE等标准文本生成评价指标。

### 对比方法

与以下主流基线方法对比：

- **非LLM方法**：BT-speaker、EDrop-speaker、CCC-speaker、Lana、Lana+
- **LLM方法**：C-INSTRUCTOR、BEVInstructor

### 额外分析实验

- **指令质量分析**：用生成的指令测试VLN导航模型（HAMT、DUET）的路径引导能力（SR/SPL指标）；作为数据增强扩充训练集，检验下游导航任务效果；进行用户研究（30名大学生对100条指令打分0-5）。

## 四、资源与算力

论文在实现细节中明确说明：

- **硬件**：单台机器配备 **2张NVIDIA A40 GPU**
- **框架**：PyTorch
- **基座LLM**：Llama-7B

⚠️ **注意**：论文未明确报告具体训练时长、总参数量、可训练参数量比例、单卡显存占用等详细信息。

## 五、实验数量与充分性

### 问卷数量统计

论文包含较为充分的实验：

- **主实验（3组）**：在R2R、REVERIE、RxR三个数据集上对比7-8个基线方法，覆盖val seen和val unseen两个划分。
- **消融实验（4组）**：
  - 各核心模块分析（SRE/MPT/LUA，5行设置）
  - 场景构建方式对比（BEV vs. 3D voxel）
  - 图映射架构对比（GraphSAGE vs. GCN vs. GAT）
  - LUA轮数影响（M=1/3/5）
- **指令质量分析（3组）**：路径引导能力（2个导航器）、数据增强（1个followers）、用户研究。

### 充分性与公平性评价

**优点**：
- 实验覆盖面较广，3个数据集+多组对比方法+消融研究+下游任务验证，构成了较完整的评估体系。
- 训练设置与基线方法BEVInstructor保持一致（batch size、优化器、学习率等），保证了对比公平性。
- 额外分析实验（导航引导、数据增强）从实用性角度验证了指令质量，是有说服力的补充。

**不足**：
- 消融实验仅报告了R2R val unseen上的结果，未展示REVERIE和RxR上的消融数据，泛化性验证有所欠缺。
- 用户研究规模有限（30人/100条指令），可能存在主观性偏差。
- 未报告实验的方差/显著性检验信息。

## 六、主要结论与发现

1. **有效性**：MAPInstructor在三个数据集上均取得最优或接近最优的综合表现。在R2R上CIDEr较最强基线提升2.7%（val seen）和4.0%（val unseen）；在REVERIE上CIDEr超越BEVInstructor 1.8%/3.8%；在RxR上val unseen的全部指标均超过所有基线（BLEU-1提升4.5%以上）。
2. **3D表示优于BEV**：相比BEV平面表示，3D体素表示能保留高度信息，提供更细粒度的场景感知，对对物体级检测和指令生成均有增益。
3. **拓扑地图的有效性**：将全局拓扑地图作为隐式提示融入LLM，比文本描述地图更有效地提供空间线索，增强了动作描述的准确性。
4. **地标不确定性评估的作用**：通过语义熵筛选地标预测、减少幻觉，能显著提升指令质量；随着轮数M增加，性能增益趋于饱和。
5. **实用价值**：生成的指令对VLN导航模型（HAMT/DUET）有更好的路径引导能力，作为数据增强时能提升下游导航模型（EDrop-follower）的SR和SPL。

## 七、优点

1. **问题定位准确**：直击NIG任务中全局空间理解缺失的核心痛点，并针对性地提出拓扑地图解决方案。
2. **技术组合有新意**：将3D体素场景表示、拓扑图神经网络、LLM参数高效微调（prompt tuning）和语义熵不确定性估计有机结合，形成了完整且自洽的技术方案。
3. **设计有认知科学依据**：参考了动物和人类主要依赖地标机制和拓扑理解导航的认知心理学证据，为拓扑地图的使用提供了理论支撑。
4. **解决了实际痛点**：地标不确定性评估机制直接应对LLM在空间场景中产生幻觉地标的顽疾，提升了系统可靠性。
5. **实验体系完整**：除生成质量评估外，还从下游应用（导航引导、数据增强、用户评估）多维度验证指令质量。

## 八、不足与局限

1. **依赖全局位置信息**：方法假设智能体能获取全局位置（如GPS），在无定位信号的室内真实场景中可能受限。
2. **计算开销**：3D体素表示和级联多尺度处理相比BEV增加了计算复杂度，对算力有更高要求；论文未报告推理效率数据。
3. **仅限离散视角导航**：实验基于R2R等离散视角（panorama view）数据集，在连续环境（continuous environment）中的有效性尚未验证。
4. **LLM选择单一**：仅使用Llama-7B作为基座LLM，未探索不同规模/类型LLM（如更大模型或更小的轻量模型）对结果的影响。
5. **消融覆盖有限**：消融实验仅在R2R上报告，未覆盖REVERIE和RxR，结论的普适性稍显不足。
6. **地标真值依赖GPT-4**：训练地标预测阶段依赖GPT-4提取地标标签，存在API成本问题和潜在的标注偏差。
7. **拓扑地图构建相对简化**：图结构仅编码了距离和方向信息，未充分利用物体语义关系、房间类型等高层次空间语义。

（完）
