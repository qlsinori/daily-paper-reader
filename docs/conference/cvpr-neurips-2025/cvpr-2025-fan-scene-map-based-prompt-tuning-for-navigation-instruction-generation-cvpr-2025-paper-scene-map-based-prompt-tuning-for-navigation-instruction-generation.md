---
title: Scene Map-based Prompt Tuning for Navigation Instruction Generation
title_zh: 基于场景地图的提示调优用于导航指令生成
authors: "Fan, Sheng, Liu, Rui, Wang, Wenguan, Yang, Yi"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Fan_Scene_Map-based_Prompt_Tuning_for_Navigation_Instruction_Generation_CVPR_2025_paper.pdf"
tags: ["query:semantic-map"]
score: 7.0
evidence: 基于场景地图的提示调优用于导航指令生成
tldr: 针对现有导航指令生成方法缺乏复杂三维环境空间理解的问题，提出基于场景地图的提示调优框架。该方法不直接向大语言模型输入文本化地图描述，而是将地图空间离散化信息融入提示，使模型更好利用全局空间上下文。实验表明该方法在导航指令生成上取得更优的空间一致性，为具身智能体的人机交互提供了更可靠的指令反馈。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 820, \"height\": 676}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 448}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1684, \"height\": 535}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1779, \"height\": 370}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1777, \"height\": 370}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1779, \"height\": 392}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 839, \"height\": 293}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 837, \"height\": 178}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 839, \"height\": 210}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 840, \"height\": 213}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 842, \"height\": 453}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-fan-scene-map-based-prompt-tuning-for-navigation-instruction-generation-cvpr-2025-paper/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 839, \"height\": 457}]"
motivation: 导航指令生成需理解复杂3D环境的空间结构，现有方法忽略全局地图上下文。
method: 提出场景地图提示调优框架，将地图空间离散化信息融入LLM提示。
result: 在导航指令生成任务上空间相关指令质量显著提升。
conclusion: 地图提示增强了大语言模型对空间任务的理解。
---

## Abstract
Navigation instruction generation (NIG), which provides interactive feedback and guidance to humans along a trajectory, is vital for developing embodied agents capable of human-machine communication and collaboration through natural language. Early data-driven methods directly map sequences of past observations to trajectory descriptions on limited datasets, lacking the necessary spatial understanding in complex 3D environments. While recent approaches leverage Large Language Models (LLMs) to improve NIG, they often overlook the global spatial context in navigation, such as the inherent space discretization in maps. Instead of straightforwardly feeding textual descriptions of the map into LLMs, we propose a scene map-based prompt tuning framework for NIG, MAPInstructor, which incorporates map context for parameter-efficient updating of LLMs. MAPInstructor comprises three key components: (i) scene representation encoding, where egocentric observations are projected into 3D voxels for fine-grained scene understanding; (ii) map prompt tuning, which integrates a topological map representation of the entire trajectory into an LLM-based decoder; and (iii) landmark uncertainty assessment, which mitigates hallucinations in landmark predictions, thereby enhancing the reliability and coherence of instruction generation. Extensive experiments on three navigation datasets (i.e., R2R, REVERIE, RxR) confirm the generalization and effectiveness of our algorithm.

---

## 论文详细总结（自动生成）

# 基于场景地图的提示调优用于导航指令生成——论文总结

## 1. 论文的核心问题与整体含义

- **研究任务**：论文研究导航指令生成（NIG, Navigation Instruction Generation），即让具身智能体基于一条导航轨迹（全景视觉观测+动作序列）用自然语言生成指令，以帮助人类或下游智能体沿轨迹导航。
- **核心问题**：
  - 早期数据驱动方法直接在有限数据集上将观测序列映射为轨迹描述，缺乏复杂3D环境中的空间理解。
  - 近期方法虽然引入大语言模型（LLM），但往往忽略导航中的全局空间上下文（如地图本身具有的空间离散化结构）。
  - 简单地以文本形式描述地图并喂给LLM，会丢失细粒度场景细节，且需要大量标注和训练。
- **关键动机**：
  - 现有方法将高度感知特征压缩到鸟瞰图（BEV）平面，损失了3D环境的整体结构信息，不利于复杂场景中的空间关系建模。
  - 拓扑地图能够为智能体提供环境的全局视角，但如何以更优的方式（而非文本描述）将地图信息注入LLM仍未充分探索。
- **论文主张**：提出**MAPInstructor**框架，将拓扑地图信息作为潜在特征（latent feature）通过提示调优的方式注入LLM，并采用3D体素表示构建局部场景理解，从而提升指令生成的空间一致性和细粒度准确性。

## 2. 论文提出的方法论

### 2.1 核心思想

- 不直接向LLM输入地图的文本描述，而是将场景地图构建为可学习的**提示特征（prompt features）**，实现参数高效的LLM更新。
- 将局部3D体素感知与全局拓扑地图联合建模，弥补先前方法在“局部细粒度空间理解”和“全局拓扑关系建模”两方面的不足。
- 通过“地标预测→指令补全”的两阶段生成流程，并引入基于语义熵的不确定性评估，缓解地标幻觉问题。

### 2.2 关键技术细节

**（1）场景表示编码（Scene Representation Encoding）**
- **视角-动作嵌入（Perspective-Action Embedding）**：对每个全景视角图像提取CLIP特征，与方向特征（heading/elevation）、时间步、token类型等相加得到视角嵌入；动作嵌入采用类似方式，基于当前heading和被选视角计算。
- **视角-3D变换（Perspective-3D Transformation）**：利用一组可学习的3D query，通过跨视角注意力（CVA，基于deformable attention）将多个2D视角特征投影到3D体素空间（分辨率7×7×7），保留高度维度信息，避免BEV压缩带来的信息损失。
- **多尺度场景预测**：将视角-3D变换分为J个级联尺度，逐步上采样，兼顾低层细节与高层语义。
- **场景表示**：将最终尺度的3D特征与视角嵌入、动作嵌入融合，得到每个时间步的场景节点表示 $v_t$。

**（2）地图提示调优（Map Prompt Tuning）**
- **拓扑地图构建**：将整个轨迹建模为有向图 $G=\{V,E\}$。每个节点由场景表示加上位置编码（由2D/3D空间距离推导）和导航步编码构成；边编码节点间的相对朝向和距离。
- **图神经网络聚合**：采用GCN（默认）等图神经网路进行迭代消息传递，使节点表示聚合邻域拓扑上下文信息。
- **提示调优**：使用轻量级Transformer解码器将节点特征压缩为固定长度的提示张量 $\hat{v}$，送入冻结的LLM（Llama-7B）进行自回归指令生成，仅更新少量参数（$|\Theta^*| \ll |\Theta|$）。

**（3）地标不确定性评估（Landmark Uncertainty Assessment）**
- **两阶段生成**：第一阶段让LLM生成M条候选地标序列；第二阶段以地标为提示，补全完整导航指令。
- **语义熵（Semantic Entropy）**：使用Deberta-large判断地标序列间的语义等价性，将M条序列聚类后按簇聚合概率，计算语义熵 $LE(v)$。熵低于阈值 $\tau$ 则视为语义确定，否则从所有地标预测中随机采样作为新提示。
- **目的**：减少地标预测中的幻觉和冗余，提高指令生成的可靠性与连贯性。

### 2.3 算法流程摘要

1. 对每个时间步的全景观测提取2D特征，经CVA投影为3D体素特征。
2. 融合3D特征与视角/动作嵌入，得到局部场景节点。
3. 将节点构建为拓扑图，通过GCN聚合邻域信息，得到全局地图感知的场景表示。
4. 用Transformer解码器将图节点压缩为LLM的提示特征。
5. LLM先生成M条地标序列，经语义熵评估筛选后，再以地标为提示生成最终指令。

## 3. 实验设计

### 3.1 数据集与基准

| 数据集 | 特点 |
|---|---|
| R2R（Room-to-Room） | 基于Matterport3D的真实室内场景，标准NIG基准，含val seen/val unseen切分 |
| REVERIE | 目标导向、物体中心型的指令生成数据集，强调物体检测能力 |
| RxR（Room-Across-Room） | 多语言、指令更灵活复杂，难度更高 |

### 3.2 评价指标
均采用自然语言生成标准指标：BLEU-1/BLEU-4、CIDEr、METEOR、ROUGE、SPICE（RxR不报告SPICE）。

### 3.3 对比方法
- 非LLM方法：BT-speaker、EDrop-speaker、CCC-speaker、Lana、Lana+
- LLM方法：C-INSTRUCTOR、BEVInstructor
- 此外还进行了**指令质量分析**实验：
  - 路径引导能力：用生成的指令分别驱动HAMT和DUET两个VLN模型，比较成功率（SR）与SPL。
  - 数据增强：将生成的指令用于增强EDrop-follower的训练数据，比较下游导航性能。
  - 用户研究：30名学生为100条生成指令打分（0~5）。

## 4. 资源与算力

- **文中明确信息**：模型基于PyTorch实现，使用**单台机器、2张NVIDIA A40 GPU**进行训练。
- **未明确信息**：具体训练时长、总GPU小时数、批处理大小等在论文中未提及。

## 5. 实验数量与充分性

- **主要实验**：在R2R、REVERIE、RxR三个数据集上对val seen和val unseen两个切分进行评测，共6组对比实验，覆盖全部指标。
- **消融实验**：
  - 关键组件消融：SRE、MPT、LUA三类模块逐步叠加（5组实验）。
  - 场景构建方式对比：BEV vs. 3D体素。
  - 图神经网络架构对比：GraphSAGE、GCN、GAT。
  - 地标评估轮数对比：M=1、3、5。
- **指令质量分析**：路径引导（2个VLN模型）、数据增强、用户研究共3组实验。
- **总体评价**：
  - 实验设计全面，涵盖了定量对比、模块消融、架构选择、下游导航验证和人工评估，维度丰富，客观性较强。
  - 消融实验设计合理，能够清晰验证每个模块的贡献。
  - 在公平性方面，训练设置与BEVInstructor保持一致，对比方法来自近年高水平论文，基本公平。
  - 不足之处：REVERIE上SPICE、METEOR、ROUGE指标低于部分方法；RxR缺少SPICE报告；未提供指令长度的统计分析或失败案例。

## 6. 论文的主要结论与发现

- MAPInstructor在三个数据集的大多数指标上优于所有对比方法。在R2R val seen/unseen上CIDEr分别提升2.7%和4.0%。
- 在REVERIE上，MAPInstructor在CIDEr上超越BEVInstructor 1.8%（seen）和3.8%（unseen），表明3D体素表示比BEV更适合物体级场景理解。
- 在RxR上，MAPInstructor全面超越所有基线，Bleu-1达到0.507/0.411（seen/unseen），验证了其在复杂、灵活指令生成中的有效性。
- 3D体素场景表示优于BEV，能保留更细粒度的空间几何信息；拓扑地图的图结构特征作为提示比文本地图描述更有效地提升空间对齐能力；语义熵地标筛选可显著减少幻觉。
- 用户研究显示MAPInstructor获得最高平均分（4.11），具备更高的实用性和自然度。

## 7. 优点

- **方法论创新**：将拓扑地图以“潜在特征”而非文本形式注入LLM，免除了繁琐的地图文本标注，同时保持了全局空间信息。
- **3D体素表示**：相比BEV，保留了高度维度和细粒度几何信息，实现更准确的物体级空间描述。
- **参数高效**：只微调少量LLM参数，保留预训练世界知识，计算开销可控。
- **语义熵引入**：将大模型幻觉检测领域的语义不确定性思想引入NIG，缓解地标幻觉。
- **实验验证充分**：除标准指标外，还用高阶VLN模型（HAMT、DUET）做路径引导验证，并通过数据增强检验指令质量对下游任务的实际增益，说服力较强。
- **代码开源**：提供GitHub仓库，有利于复现和后续研究。

## 8. 不足与局限

- **实验覆盖的局限性**：
  - 在REVERIE上，SPICE、METEOR和Rouge指标低于部分基线（如SPICE在seen较C-INSTRUCTOR的0.191低至0.186），说明物体级语义描述仍有改进空间。
  - RxR数据集没有报告SPICE指标，缺少对语义细粒度的验证。
- **资源信息不完整**：未报告训练时长、总计算量等细节，难以评估其计算门槛和可复现成本。
- **方法依赖较强假设**：
  - 假设智能体可获取全局位置（如GPS），在某些真实部署场景中不一定成立。
  - 地标标注依赖GPT-4从训练集提取，可能引入外部模型偏差。
- **图结构建模相对简单**：消融表明GCN、GAT、GraphSAGE差异很小，说明当前图结构对消息传递方式并不敏感，可能未充分发挥拓扑图潜力。
- **仅限室内环境**：实验全部基于Matterport3D相关室内数据集，未验证在室外或大规模开放场景中的泛化能力。
- **缺乏错误分析**：无失败案例或输出样本的系统性偏差分析。

---

（完）
