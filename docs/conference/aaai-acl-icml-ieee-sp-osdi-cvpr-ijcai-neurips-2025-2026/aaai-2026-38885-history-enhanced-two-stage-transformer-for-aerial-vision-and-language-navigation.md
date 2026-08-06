---
title: History-Enhanced Two-Stage Transformer for Aerial Vision-and-Language Navigation
title_zh: 历史增强型两阶段Transformer用于空中视觉语言导航
authors: "Xichen Ding, Jianzhe Gao, Cong Pan, Wenguan Wang, Jie Qin"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38885/42847"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 无人机依据语言指令进行城市环境导航的空中视觉语言导航
tldr: 空中视觉语言导航要求无人机依据语言指令在大型城市场景中定位目标，目前单粒度框架难以兼顾全局环境推理与局部场景理解。本文提出历史增强两阶段Transformer（HETT），通过粗到细的导航流程：先融合空间地标与历史上下文预测粗略目标位置，再利用细粒度视觉分析精化动作。该方法在航拍VLN任务上有效提升了无人机在复杂城市环境下的导航性能。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38885/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 560, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38885/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 810, \"height\": 922, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38885/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1830, \"height\": 699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38885/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1839, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38885/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 881, \"height\": 892, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38885/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 846, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38885/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1800, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38885/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 837, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38885/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1347, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38885/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 906, \"height\": 274, \"label\": \"Table\"}]"
motivation: 空中VLN需要同时进行全局环境推理和局部场景理解，现有多数无人机框架采用单一粒度表征，难以兼顾二者。
method: 提出历史增强两阶段Transformer，先结合空间地标与历史信息预测粗粒度目标位置，再通过细粒度视觉分析精化导航动作。
result: 该粗到细框架改善了UAV在大规模城市场景中依据语言指令定位目标的性能。
conclusion: 历史信息与两阶段粗到细推理结合，为空中语言导航提供了有效的全局-局部平衡方案。
---

## Abstract
Aerial Vision-and-Language Navigation (AVLN) requires Unmanned Aerial Vehicle (UAV) agents to localize targets in large-scale urban environments based on linguistic instructions. While successful navigation demands both global environmental reasoning and local scene comprehension, existing UAV agents typically adopt mono-granularity frameworks that struggle to balance these two aspects. To address this limitation, this work proposes a History-Enhanced Two-Stage Transformer (HETT) framework, which integrates the two aspects through a coarse-to-fine navigation pipeline. Specifically, HETT first predicts coarse-grained target positions by fusing spatial landmarks and historical context, then refines actions via fine-grained visual analysis. In addition, a historical grid map is designed to dynamically aggregate visual features into a structured spatial memory, enhancing comprehensive scene awareness. Additionally, the CityNav dataset annotations are manually refined to enhance data quality. Experiments on the refined CityNav dataset show that HETT delivers significant performance gains, while extensive ablation studies further verify the effectiveness of each component.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

空中视觉语言导航（Aerial Vision-and-Language Navigation, AVLN）要求无人机（UAV）在大型城市环境中依据自然语言指令对目标进行定位，是一种新兴的具身智能挑战。该任务相比室内VLN（如R2R）存在显著区别：城市环境规模大、非结构化，包含复杂的地标布局和高度变化的城市几何，要求智能体在长时间动态轨迹中维持视觉-语言跨模态对齐，同时具备全局空间推理与局部场景理解能力。

然而，现有方法存在两类关键不足：

- **单粒度框架难以兼顾全局与局部**：局部路径规划方法擅长细粒度视觉-指令对齐和动态适应，但缺乏长距离推理能力；全局规划方法虽能构建粗粒度2D空间地图用于目标预测，却缺少精细视觉理解。目前尚无方法有效整合两种互补能力。
- **历史信息保存不完整**：现有UAV智能体大多依赖语义分割模块（如GroundingDINO、SAM）将语义掩码投影到俯视地图，这从根本上限制了细粒度视觉信息的捕获，削弱了整体场景理解。
- **数据注释质量不高**：CityNav等数据集依赖LLM自动生成注释，缺少人工审核，导致大量噪声和错误，限制了训练有效性。

基于上述问题，论文提出历史增强两阶段Transformer框架（HETT），以"粗到细"的导航pipeline弥合全局规划与局部感知的鸿沟，同时通过数据注释人工精炼提高评估可靠性。


### 2. 提出的方法论

**核心思想**：将导航过程分解为粗粒度目标预测与细粒度动作精化的两阶段策略，并引入历史网格地图维持全局空间记忆。

**关键技术细节与流程**：

- **整体框架**：每一时间步，五种类型的token（地标、指令、位姿、历史、视觉token）输入跨模态Transformer，联合产生导航决策。文本嵌入E、地标轮廓空间特征L、视觉特征Vt、位姿特征Pt、历史空间记忆Ft五类信息共同参与融合。

- **粗粒度目标预测阶段**：将指令涉及地标的多边形轮廓投影到俯视地标图 ML ∈ R^{SL×SL}，经MLP+CNN编码为地标嵌入L。随后将指令嵌入E、地标嵌入L与历史记忆Ft送入多层Transformer（MLT）融合，得到全局表征Gt，最终通过Softmax(MLP(Gt))输出标准化的目标坐标 g_t ∈ [0,1]²。

- **细粒度动作精化阶段**：通过跨模态注意力获取指令感知的视觉嵌入Vt = Attention([E;Ot])，再将Vt与地标嵌入L、历史记忆Ft、位姿嵌入Pt拼接，经MLT输出Rt与At。Rt经Sigmoid产生任务进度估计rt ∈ [0,1]（用于判断终止）；At经Arctan2(Tanh(MLP(At)))产生转角 at ∈ (-π,π]，驱动连续运动。

- **历史网格地图**：将环境离散化为固定 SH×SH 的网格。随时间步聚合视觉特征与空间坐标，每个网格单元根据与指令的关联权重聚合特征，形成结构化空间记忆 Ft ∈ R^D。

- **损失函数**：DAgger策略训练，包含三类损失——粗粒度目标预测损失LG（MSE）、动作损失LA、进度损失LR，总损失 L = α₁LG + α₂LA + α₃LR（α分别设为2.0、1.5、0.1）。


### 3. 实验设计

**数据集**：
- **CityNav**（Lee et al. 2024）：包含32,326条自然语言描述与人类示范轨迹，图片数据来自SensatUrban（伯明翰13街区、剑桥33街区的正射投影图与深度图），地标几何轮廓来自CityRefer。
- 论文对CityNav注释进行了**人工精炼**，修复缺少数（Missing）、小错误（Minor：拼写错误）、大错误（Major：关键地标提取错误）、删除无用样本（Deletion）等四类问题。

**评估指标**：Navigation Error (NE)、Success Rate (SR)、Oracle Success Rate (OSR)、Success weighted by Path Length (SPL)。成功条件为20步内发出[stop]且最终位置距目标20米内。

**对比方法**：Random、Human上限、Seq2Seq、CMA、AerialVLN、MGP共6个基线，并额外报告了在精炼数据集上训练的HETT*。


### 4. 资源与算力

论文在实现细节部分明确说明：模型使用PyTorch实现，在**4块24GB RTX A5000 GPU**上训练**20个epoch**，批大小为2，学习率为1e-4，使用AdamW优化器。算力使用规模适中，信息透明，未提及其他额外资源消耗。


### 5. 实验数量与充分性

实验设置较为充分，包含三组主要实验：

- **主实验（Table 2）**：在CityNav的Validation Seen、Validation Unseen、Test Unseen三个数据划分上对比6个基线，HETT与HETT*共报告两组结果，覆盖全部四项指标。
- **消融实验（Table 3）**：系统验证了三个组件（精炼数据、两阶段策略、历史网格地图）的独立贡献及组合效果，共5行配置。
- **数据集精炼验证（Table 4）**：额外验证了在精炼数据集上训练AerialVLN和MGP的性能提升，排除数据精炼仅对HETT有效的偏差。
- **网格尺寸分析（Table 5）**：比较0×0、3×3、5×5、7×7四种网格尺寸对性能的影响。

实验覆盖了方法有效性验证、组件贡献归因、数据集精炼的普适性影响、超参数敏感性分析，客观性和公平性较好。但缺少对HETT在每个中间阶段的具体失败案例分析，也没有与其他SOTA方法在更多样的城市场景（非CityNav）上的泛化实验。


### 6. 主要结论与发现

- **HETT在全部数据集划分与指标上优于所有基线**：在SR上，较最强基线MGP分别提高8.23%（验证seen）、9.13%（验证unseen）、12.07%（测试unseen）；测试集NE降低13.2米，OSR提高19.06%，SPL提高7.07%。
- **数据精炼带来一致增益**：HETT*在精炼数据上训练后，SR在三个划分上分别额外提升5.93%、1.62%、5.93%。
- **消融实验显示三大组件均有效**：精炼数据将SR从19.42%提至24.98%（验证seen）；两阶段策略进一步提至26.19%；历史网格地图独立贡献最大，加入后SR从24.98%提至29.31%。三者组合达到最优（31.09%）。
- **数据精炼对已有基线同样有效**：AerialVLN在精炼数据上SR从9.77%升至12.38%，MGP从16.93%升至19.17%，证明精炼数据的重要性具有普适性。
- **5×5网格为最优配置**：3×3网格OSR最佳但SR次优，7×7网格因过多特征干扰导致性能下降。


### 7. 优点

- **思想清晰，架构具有很好的针对性**：提出的两阶段粗到细策略直接回应AVLN中全局推理与局部理解难以兼顾的根本矛盾，问题定义与方案设计高度契合。
- **历史网格地图设计精巧**：将视觉特征基于空间坐标动态聚合到网格结构中，不依赖外部语义分割模块即可维持结构化空间记忆，避免了现有方法中"分割模块→语义地图"流程的信息损失。
- **实验设计严谨**：既验证了方法有效性和各组件贡献，又通过额外实验排除了"数据精炼仅对HETT有利"的潜在偏差；通过验证AerialVLN与MGP在精炼数据集上的增益，证明数据质量改进是普适的。
- **数据集人工精炼**：系统性修复了LLM生成注释的噪声，形成了更可靠的基准，对AVLN社区具有重要贡献。
- **定性分析直观**：通过可视化两阶段导航过程（粗预测渐近收敛、精化阶段纠正偏差）和网格地图的作用，为定量结果提供了直观证据。


### 8. 不足与局限

- **依赖预定义地标信息**：论文在结论中明确承认HETT依赖CityNav提供的地理优先信息（landmark priors），这限制了其在未知环境中的泛化能力。未来需要在线环境建图来增强鲁棒性。
- **训练与推理成本较高**：批大小仅2，训练需要20个epoch和4块24GB GPU，说明模型参数量或计算开销较大，不利于部署在算力受限的无人机平台。
- **缺少细粒度结果分析**：没有按指令类型（如空间关系型、地标描述型、复杂长指令）拆分分析性能差异，无法辨别HETT具体擅长或欠缺哪类指令。
- **评价场景单一**：仅在城市鸟瞰RGB-D图像的CityNav环境评测，未验证在真实城区或不同天气、光照条件下的性能；且数据集的无人机视角图像为非真实拍摄，存在Sim-to-Real差距。
- **与更强基线的对比不充分**：对比的基线（MGP、AerialVLN）数量有限，未与近期（如2024年以来）的更多AVLN方法进行横向比较（尽管论文引用了更新工作如Gao et al. 2024）。
- **成功阈值较宽松**：20米成功判定在复杂城市环境中相对容易达成，可能掩盖目标定位精度上的细微差异，SPL与NE指标部分缓解了这一问题。

（完）
