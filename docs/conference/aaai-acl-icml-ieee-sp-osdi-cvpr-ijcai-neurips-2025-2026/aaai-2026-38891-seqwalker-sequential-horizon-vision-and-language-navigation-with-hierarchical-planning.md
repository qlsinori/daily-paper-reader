---
title: "SeqWalker: Sequential-Horizon Vision-and-Language Navigation with Hierarchical Planning"
title_zh: SeqWalker：基于分层规划的序列时域视觉语言导航
authors: "Zebin Han, Xudong Wang, Baichen Liu, Qi Lyu, Zhenduo Shang, Jiahua Dong, Lianqing Liu, Zhi Han"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38891/42853"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 基于分层规划的长程自然语言指令视觉语言导航
tldr: 长时间跨度的自然语言指令会使视觉语言导航模型因信息过载而性能下降。SeqWalker提出分层规划框架，高层规划器根据当前视觉观察动态选择与上下文相关的子指令，生成序列化导航动作。该方法缓解了长指令下信息冗余问题，提升了连续多任务轨迹导航的表现。在SH-VLN挑战中，与现有模型相比，SeqWalker显著降低了长时程指令带来的性能退化，验证了分层规划对复杂指令导航的价值。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38891/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1828, \"height\": 776, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38891/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1831, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38891/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 734, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38891/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1829, \"height\": 430, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38891/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1832, \"height\": 464, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38891/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 891, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38891/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 887, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38891/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 873, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38891/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 878, \"height\": 248, \"label\": \"Table\"}]"
motivation: 长程复杂语言指令导致视觉语言导航模型信息过载、性能显著下降。
method: 构建高层规划器动态选择相关子指令，并在分层框架下执行序列化导航。
result: 相较于现有模型，在长时域指令场景中显著减少性能退化并提升导航表现。
conclusion: 分层指令选择与规划是应对长程视觉语言导航信息过载的有效策略。
---

## Abstract
Sequential-Horizon Vision-and-Language Navigation (SH-VLN) presents a challenging scenario where agents should sequentially execute multi-task trajectory navigation guided by complex, long-horizon natural language instructions. Current vision-and-language navigation models exhibit significant performance degradation with such instructions, as information overload impairs the agent's ability to attend to observationally relevant details. To address this problem, we propose SeqWalker, a novel navigation model built on a hierarchical planning framework. Our SeqWalker features: (1) A High-Level Planner that dynamically selects global instructions into contextually relevant sub-instructions based on the agent's current visual observations, thus reducing cognitive load; (2) A Low-Level Planner incorporating an Exploration-Verification strategy that leverages the inherent logical structure of instructions for trajectory error correction. To evaluate SH-VLN performance, we also extend the IVLN dataset and establish a new benchmark. Extensive experiments are performed to demonstrate the effectiveness and superiority of SeqWalker.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：视觉语言导航（VLN）要求智能体理解自然语言指令并在复杂环境中自主导航，在机器人、家庭服务、虚拟现实等领域具有重要应用前景。现有VLN方法在单轨迹导航上已取得显著进展，但现实应用中智能体常需在同一环境中持续工作，完成由一条长指令描述的多个顺序子任务。
- **核心问题**：本文提出并研究了**序列时域视觉语言导航（SH-VLN）**任务——智能体需要遵循一条复杂的长程语言指令，在大型场景中依次完成多条导航轨迹。该任务面临三大挑战：
  - **场景持久性**：智能体需在长时间跨度的部署中保存并复用场景地图信息，而非每次从零探索。
  - **复杂长指令**：多任务指令信息过载，干扰智能体将指令与当前视觉观察准确关联的能力。
  - **多轨迹鲁棒性**：长距离顺序导航中一旦发生错误，后续轨迹容易连锁恶化，对纠错能力提出高要求。
- **核心观察**：现有VLN模型在处理长指令时性能显著下降，直接应用大规模LLM无法解决——因为大模型难以部署到机器人端，且缺乏具体导航场景知识无法指导精确动作。
- **整体意义**：本文提出SeqWalker模型，通过分层规划框架（高层指令选择 + 低层探索-验证动作规划）来解决SH-VLN问题，并构建了对应的基准数据集，推动VLN研究向更贴近真实应用的大场景、长时程、多任务方向迈进。

---

### 2. 论文提出的方法论：核心思想、关键技术细节、公式与算法流程

#### 核心思想
SeqWalker构建了一个**分层规划框架**，将导航决策分解为：
- **高层感知规划（High-Level Perception Planner）**：负责将长指令拆分为与当前观察最相关的子指令，降低认知负担。
- **低层动作规划（Low-Level Action Planner）**：在选定的子指令引导下，通过“探索-验证（Exploration and Verification, EaV）”策略预测具体动作，并在必要时纠正轨迹错误。

#### 关键技术细节

**① 高层感知规划（High-Level Perception Planner）**
- 采用**指令分割模块（Instruction Segmentation Module, ISM）**将全局长指令分割为一系列子短语。
- 使用CLIP的文本编码器 `ΨT` 对每个短语 `Sik` 编码，视觉编码器 `ΨV` 对当前RGB观测 `Rit` 编码。
- 计算短语与当前观测的余弦相似度 `θkt = Sim(ΨT(Sik), ΨV(Rit))`，通过softmax得到每个短语匹配当前状态的概率 `P(Sik)`。
- 为避免单纯取最大概率造成的错误选择，引入熵计算 `Φit = H(P(Si0), ..., P(Sin))`：
  - 若熵 `Φit < Φλ`（阈值），取最大概率短语作为当前局部指令 `k* = argmax P(Sik)`；
  - 否则使用全局指令 `Ii`。
- 使用轻量级LLM（Qwen-0.5B）作为指令编码器生成指令嵌入：`Zst = LLM(α · Sik* + (1−α) · Ii)`，其中 `α=1` 当熵低于阈值，否则 `α=0`。

**② 导航场景建图（Navigation Scene Mapping）**
- 沿用IVLN-CE的地图方法，通过**场景建图模块（SMM）**创建并保存语义地图 `Mit[sem]` 和占据地图 `Mit[ocu]`。
- 基于智能体当前位姿裁剪局部地图，经Map-Encoder（含4个CBRA块 + 空间注意力）编码为地图嵌入 `Zmt`。

**③ 低层动作规划（Low-Level Action Planner）**
- **探索导航模式（Exploration Mode）**：将地图嵌入 `Zmt` 与指令嵌入 `Zst` 输入Action Output Head（AOH，含两个GRU及交叉注意力），结合前一步隐藏状态和动作预测下一步动作 `ait`。
- **验证导航模式（Verification Mode）**：利用指令的固有逻辑顺序进行两项验证：
  - **Term-I**：当前所选短语 `Sik*` 是否为上一个已选短语 `Sik*l` 的下一个（即 `Sik* = Sik*l+1`）；
  - **Term-II**：当前观测与对应的下一个短语 `Sik*l+1` 的文本嵌入之间的相似度 `δt` 是否低于阈值 `δ0`。
- 当Term-I和Term-II同时异常时，智能体执行“回退上一步”并强制选择次高概率动作，实现轨迹纠错。

**算法流程（EaV策略）**：
1. 获取当前RGB观测，回忆上一选中短语，计算当前选中短语或全局指令；
2. 若使用全局指令或短语顺序正确（α=0或k*=k*l+1），则正常预测动作；
3. 否则计算下一短语文本嵌入与当前RGB嵌入的相似度δt；
4. 若δt < δ0，则设置动作为“回退上一步”并选择次高概率动作；
5. 否则正常预测动作。

---

### 3. 实验设计：数据集、场景、基准与对比方法

#### 数据集与基准
- **SH IR2R-CE**：本文扩展IVLN的IR2R-CE数据集构建的新基准，用于SH-VLN任务评估。
  - **轨迹拼接**：从IR2R-CE中选择终点与起点对齐的轨迹对进行拼接，使用LLaMa-13B将对应指令逻辑衔接为一条连贯长指令。
  - **指令丰富化**：使用LLaVA-OneVision（多模态大模型）结合真实轨迹中的第一视角多张RGB图像，为指令补充更具判别性的细节，以区分多轨迹导航中语义相似的子任务。
- **传统IR2R-CE**：用于验证SeqWalker在传统单任务IVLN上的表现。

#### 对比方法
- **CMA系列**（Krantz et al. 2023）：Naive-CMA、TourCMA、PoolCMA、PoolEndCMA、MAP-CMA
- **HNR**（Wang et al. 2024c）
- **ETPNav**（An et al. 2024）
- **OVER-NAV**（Zhao et al. 2024）

#### 评估指标
- 导航误差（NE）、Oracle成功率（OS）、归一化动态时间规整（nDTW）、成功率（SR）、按路径长度加权的成功率（SPL）、Tour归一化DTW（t-nDTW）、轨迹长度（TL）。
- 提出两个新指标：**CPsubT**（失败前完成子任务比例，NS/NA）与**CPsubI**（正确选择子指令的比例，NC/NT）。

#### 训练设置
- 仿真平台：Habitat。
- 两阶段模仿训练：第一阶段教师强制训练，第二阶段在未见场景微调提升泛化能力，两阶段均使用Progress Monitor辅助损失。
- CLIP参数冻结，LLM指令编码器、Map-Encoder、AOH联合训练。

---

### 4. 资源与算力

- 论文**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。
- 实现中采用了轻量级LLM（Qwen-0.5B）和CLIP ViT-B/32作为视觉-文本编码器，且CLIP参数冻结，说明模型对端侧部署友好，但具体的计算资源投入在文中未披露。

---

### 5. 实验数量与充分性

#### 实验组数概览
- **主实验1**（SH IR2R-CE）：在Val-Seen和Val-Unseen上对比7种SOTA方法，报告7项指标。
- **主实验2**（IR2R-CE传统任务）：在Val-Seen和Val-Unseen上对比7种方法。
- **消融实验1（ISM有效性）**：4组——有/无ISM × 不同LLM大小（0.5B/7B/13B）。
- **消融实验2（熵阈值Φλ）**：6组——最大值策略 + 5个不同阈值（0.45~0.85）。
- **消融实验3（分割风格）**：4组——不分割/按逗号/按连接词/按句号。
- **消融实验4（EaV策略）**：4组——无验证/仅Term-I/仅Term-II/Term-I+Term-II。

#### 充分性与客观性分析
- **优点**：实验覆盖了模型的关键设计组件（ISM、阈值、分割风格、EaV），消融设计完整，能有效验证各模块贡献。两个主实验分别验证了模型在SH-VLN新任务和传统IVLN任务上的表现，说明方法既有针对长指令的改进也有通用性能。
- **公平性**：所有对比方法在SH IR2R-CE上重新训练，确保公平；结果报告均值±标准差，采用多次运行。
- **不足**：新基准SH IR2R-CE的具体规模（轨迹数量、场景数等）在正文中仅有统计图概述，未给出详细数值；未在更大规模真实场景数据集（如HM3D）或其他VLN基准上验证跨数据集泛化。

---

### 6. 论文的主要结论与发现

1. **SeqWalker在SH-VLN任务上显著优于现有SOTA方法**：在Val-Seen和Val-Unseen上，t-nDTW分别比最优基线提高5%和6%，SR、SPL等指标均有大幅提升。
2. **分层规划有效缓解长指令信息过载**：High-Level Planner的指令分割与动态选择使智能体能够按需聚焦与当前观察相关的子指令。
3. **EaV策略显著提升轨迹鲁棒性**：通过Term-I与Term-II双重验证，及时纠正方向误判，明显提升导航成功率，虽然纠错会略微增加轨迹长度，但整体收益为正。
4. **指令分割比单纯扩大LLM参数更有效**：ISM使0.5B小模型在指令理解上超越不使用ISM的7B/13B模型，对端侧部署具有重要价值。
5. **熵阈值Φλ存在最优值**：Φλ=0.65时性能最佳；过高或过低均会造成性能下降。
6. **基于句号的分割效果最好**：每种分割风格对导航性能影响显著，Type-IV（按句号）能保证每个短语至少包含一个可对齐的物体，利于视觉-语言对齐。

---

### 7. 优点

- **任务创新**：首次系统定义并形式化SH-VLN问题，兼具场景持久性、长指令与多轨迹鲁棒性三重挑战，填补了VLN领域从单任务到序列多任务过渡的空白。
- **模型设计**：分层规划框架思路清晰，高层指令选择与低层动作规划各司其职、高度模块化；EaV策略创造性地利用指令内部逻辑顺序进行在线纠错，而非依赖额外的奖励或外部反馈。
- **工程友好**：使用0.5B轻量LLM并冻结CLIP，在保持高性能的同时兼顾实时性与端侧部署可行性；指令分割策略可有效提升小模型的长指令推理能力。
- **基准构建**：提出的SH IR2R-CE基准通过LLM连接轨迹与LLaVA丰富指令细节，考虑了指令判别性和语义连贯性，为后续SH-VLN研究提供了可复用的评测平台。
- **实验严谨**：消融实验覆盖各核心组件，阈值分析细致；对比方法在同一数据上重新训练，公平性较好；新指标CPsubT/CPsubI为子任务完成度提供了量化手段。

---

### 8. 不足与局限

- **算力信息不透明**：未报告GPU型号、数量和训练时长，难以评估方法在资源受限场景下的实际部署成本，也影响实验可复现性评估。
- **基准规模有限**：SH IR2R-CE是在IVLN-IR2R-CE基础上扩展而来，场景与环境仍受限于原数据集；未在HM3D等更大规模、多样化3D场景上验证，泛化性证据不足。
- **未与其他长指令VLN方法对比**：与LH-VLN（Song et al., 2024）等更接近的长时程导航基准没有直接对比，缺乏跨基准的位置参考。
- **验证模式的简单性**：Term-II仅依赖单帧RGB与文本的余弦相似度，对光照、视角变化和语义歧义敏感；回退策略固定为“上一步”，未考虑更复杂的错误类型（如长期偏离）。
- **依赖CLIP的匹配能力**：High-Level Planner中的指令选择依赖冻结的CLIP模型，在CLIP对某类视觉概念或指令表述不敏感时，可能造成错误选择。
- **未讨论失败案例分析**：论文未展示典型失败场景或错误模式的可视化分析，对方法局限性的诊断不够深入。
- **未经真实机器人部署验证**：实验仅限于Habitat仿真环境，与真实世界的物理交互、动态障碍物、传感器噪声等仍有差距。

---

（完）
