---
title: "UrbanNav: Learning Language-Guided Embodied Urban Navigation from Web-Scale Human Trajectories"
title_zh: UrbanNav：从网络规模人类轨迹学习语言引导的具身城市导航
authors: "Yanghong Mei, Yirong Yang, Longteng Guo, Qunbo Wang, Ming-Ming Yu, Xingjian He, Wenjun Wu, Jing Liu"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38916/42878"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 基于自由语言指令的城市场景具身导航
tldr: 城市环境中的语言导航面临噪声指令、模糊空间指代和动态街景等挑战，现有方法依赖精确坐标或图像目标，难以用于真实送货机器人。UrbanNav提出大规模可扩展框架，利用网络级城市步行轨迹训练具身智能体遵循自由形式语言指令。该方法能在多样城市环境中实现无需精确目标的鲁棒导航，为最后一英里配送等自主代理提供了可扩展的解决方案。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38916/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1827, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38916/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1835, \"height\": 599, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38916/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1432, \"height\": 600, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38916/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1820, \"height\": 814, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38916/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 392, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38916/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1355, \"height\": 268, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38916/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 841, \"height\": 371, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38916/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 788, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38916/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 871, \"height\": 230, \"label\": \"Table\"}]"
motivation: 现有视觉导航方法受限于仿真或封闭街道环境，且依赖精确坐标或图像作为目标，难以用于陌生城市中的自由语言指令导航。
method: 提出UrbanNav，利用网络级城市步行轨迹，以自监督方式训练智能体遵循自由形式自然语言指令进行城市导航。
result: UrbanNav在多样化城市环境中实现了鲁棒的语言引导导航，支持无需精确目标的轨迹学习。
conclusion: 利用海量人类步行轨迹可有效训练智能体在复杂城市环境中执行自由形式语言导航。
---

## Abstract
Navigating complex urban environments using natural language instructions poses significant challenges for embodied agents, including noisy language instructions, ambiguous spatial references, diverse landmarks, and dynamic street scenes. Current visual navigation methods are typically limited to simulated or off-street environments, and often rely on precise goal formats, such as specific coordinates or images. This limits their effectiveness for autonomous agents like last-mile delivery robots navigating unfamiliar cities. To address these limitations, we introduce UrbanNav, a scalable framework that trains embodied agents to follow free-form language instructions in diverse urban settings. Leveraging web-scale city walking videos, we develop an scalable annotation pipeline that aligns human navigation trajectories with language instructions grounded in real-world landmarks. UrbanNav encompasses over 1,500 hours of navigation data and 3 million instruction-trajectory-landmark triplets, capturing a wide range of urban scenarios. Our model learns robust navigation policies to tackle complex urban scenarios, demonstrating superior spatial reasoning, robustness to noisy instructions, and generalization to unseen urban settings. Experimental results show that UrbanNav significantly outperforms existing methods, highlighting the potential of large-scale web video data to enable language-guided, real-world urban navigation for embodied agents.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：在真实城市场景中，具身智能体（如最后一英里配送机器人、自动驾驶汽车、辅助机器人）需要遵循自然语言指令进行导航。城市环境具有高度动态性、地形多样、行人密集等特点，且人类指令通常是自由形式的、模糊的（例如“去古桥旁那家咖啡馆”、“到公园对面的书店”），包含空间指代和地标参照，对智能体提出极高的推理要求。
- **现有方法的局限**：
  - 当前视觉导航方法主要局限于仿真环境或室内场景，依赖精确目标格式（GPS坐标、目标图像等），难以部署到真实城市环境中。
  - 通过远程操控收集专家轨迹的方法数据多样性有限、标注成本高昂，泛化能力不足。
  - 从不可控网络视频学习存在两个关键问题：①并非所有视频片段都适合训练机器人（视角与运动方向不一致、不安全行为等）；②如何从野外视频中获取指令-动作监督信号。
- **论文核心贡献**：提出 **UrbanNav** 框架，利用网络规模的城市场景人类步行视频，通过自动化数据管线构建大规模语言引导导航数据集，训练具身智能体遵循自由形式自然语言指令在多样城市环境中导航，无需精确目标格式。

## 2. 论文提出的方法论

### 2.1 核心思想

利用人类在城市中步行时的第一视角视频作为训练数据源，通过自动化标注管线将视频轨迹与地标语言指令对齐，构建大规模模仿学习数据集，训练语言引导的导航策略模型。

### 2.2 数据构造管线（三步流程）

- **Step 1: 轨迹标注**
  - 从YouTube收集超过2,000小时的野外第一人称城市步行视频，涵盖繁华街道、居民区、公园等多样化场景。
  - 将原始视频均匀分割为2分钟片段，使用视觉里程计模型 **DPVO** 估计相机姿态，以首帧为原点标注每一帧的相对相机位姿，共获得106,603条带姿态标签的轨迹，合计3,553小时。
  - 策略仅在短时间窗口（过去8步）内做预测，减轻了视觉里程计的累积漂移问题。

- **Step 2: 机器人兼容性过滤**
  - **俯仰角过滤**：估计每帧相机俯仰角，剔除垂直振荡过大（变化超过15°）的轨迹，排除仰视建筑、俯视地面等情况。
  - **偏航角过滤**：用滑动窗口分析运动方向与观察方向的一致性，剔除差异超过60°的片段（如突然转头、侧视）。
  - **人群密度过滤**：使用YOLOv10检测行人，剔除单帧超过5人且出现超过3帧的轨迹，确保安全性。
  - 最终保留 **47,008条高质量轨迹，共1,566小时**。

- **Step 3: 语言指令标注**
  - 使用Qwen2.5-VL-72B VLM自动检测并定位地标（排除行人和车辆等动态实体，要求地标在轨迹附近且具有清晰的视觉特征）。
  - VLM输出地标边界框和初步名称，人工审核过滤低置信度标注。
  - 再次提示VLM生成基于地标的自然语言导航指令，最终获得 **300万个指令-轨迹-地标三元组**，每条轨迹平均含65个地标，指令平均长度17个单词。

### 2.3 策略模型架构

- **输入**：语言指令、当前视觉观测、过去k=8帧历史观测。
- **编码**：CLIP编码文本，DINOv2编码视觉帧，两个编码器冻结不训练。
- **特征融合**：使用 **FiLM（Feature-wise Linear Modulation）** 模块，用语言特征调制当前视觉嵌入，实现语言与视觉的语义对齐。
- **Transformer编码器**：将所有语言嵌入、FiLM调制的当前视觉特征、历史视觉特征拼接，捕捉时序动态和跨模态交互。
- **输出**：预测未来8步的ego-centric坐标系waypoints，同时预测运动方向和到达状态。

### 2.4 训练目标

总损失为四个损失的加权和：

\[
L_{total} = \lambda_{reg} L_{reg} + \lambda_{ori} L_{ori} + \lambda_{arr} L_{arr} + \lambda_{hall} L_{hall}
\]

- **Lreg（waypoint回归损失）**：预测与真实未来位置的L2距离，保证空间预测精度。
- **Lori（方向损失）**：预测与真实运动方向的负余弦相似度，惩罚角度偏差。
- **Larr（到达预测损失）**：二元交叉熵损失，监督模型判断是否已到达目标。
- **Lhall（特征hallucination损失）**：L1距离，引导模型预测未来观测的高级视觉特征：

\[
L_{hall} = \frac{1}{k} \sum_{f=1}^{k} \|\hat{h}_{t+f} - h_{t+f}\|_1
\]

### 2.5 训练数据采样策略

- 每次训练随机选择一条轨迹和其中一个已标注地标及其语言指令。
- 起始时间步在目标时间前10~60帧内随机采样，使智能体从不同初始距离和方向学习导航。
- 同时模拟“已到达目标”的场景（采样时间步非常接近目标时间），帮助模型学会判断何时停止。

## 3. 实验设计

### 3.1 数据集与Benchmark

- **离线数据集**：UrbanNav数据集，包含1,566小时高质量轨迹和300万指令-轨迹-地标三元组。验证集分为“seen”（训练集中出现的场景）和“unseen”（全新环境）两部分。
- **真实世界部署**：在物理机器人平台上部署，评估导航成功率（成功到达目标地标且无碰撞的百分比）。

### 3.2 评估指标

- **离线指标**：
  - **AOE（平均方向误差）** 和 **MAOE（最大平均方向误差）**：预测与真实运动方向的角偏差，单位度。
  - **ADE（平均距离误差）** 和 **MADE（最大平均距离误差）**：预测与真实轨迹位置的L2距离偏差，后者即离散形式的Fréchet距离，单位米。
- **真实世界指标**：导航成功率，即成功到达目标地标且无碰撞的试验百分比。

### 3.3 对比方法

- **NoMaD + CLIP**：原为图像目标导航，加入CLIP文本编码和融合层以支持语言指令。
- **ViNT + CLIP**：原为基础视觉导航模型，同样适配语言输入。
- **LeLaN**：原为室内目标导航语言条件策略，修改输出头以回归未来waypoints。
- **UrbanNav\***：仅用真实世界数据训练、无网络级预训练的变体，用于消融验证。

### 3.4 实验场景设计

- **真实世界部署**：分为白天和夜间两种条件。
- **鲁棒性测试**：
  - **Normal（正常）**：目标在初始视野内，指令清晰。
  - **Noisy（噪声指令）**：使用模糊或误导性语言指令。
  - **Obstructed（遮挡）**：目标在视野外或被遮挡。

## 4. 资源与算力

- **论文未明确说明**训练所使用的GPU型号、数量、训练时长等算力信息。
- 仅能推断使用了大规模VLM（Qwen2.5-VL-72B，72B参数）进行离线数据标注，以及DPVO、YOLOv10等模型进行数据处理；策略模型本身使用冻结的CLIP和DINOv2编码器，训练开销主要集中在Transformer编码器部分。
- 数据规模为1,500~3,000小时级别的视频处理和300万条标注，数据管线本身的计算开销较大，但论文未提供具体量化数据。

## 5. 实验数量与充分性

### 5.1 实验数量概览

1. **离线基准测试**：在seen和unseen两个子集上，对比4种方法、4项指标。
2. **真实世界部署**：总体、白天、夜间三个条件的成功率对比（4种方法+1个消融变体）。
3. **鲁棒性分析**：正常、噪声、遮挡三个难度场景的成功率对比（5种方法）。
4. **模型组件消融**：特征hallucination损失和FiLM模块的消融实验。
5. **网络数据规模消融**：从300到1,500小时训练数据量的扩展实验，观测各指标变化。

### 5.2 充分性与客观性评价

- **优点**：实验设计覆盖离线评估与在线真实部署两个层面，消融研究既包括架构组件也包括数据规模，鲁棒性分析涵盖指令噪声和目标遮挡等实际挑战，实验较全面。
- **不足**：
  - 真实世界部署的试验次数未明确报告（从成功率83.3% = 10/12推测每组约12次试验），样本量偏小，统计显著性未说明。
  - 未提供误差条或多次随机种子的方差信息。
  - 未与基于LLM的零样本导航方法（如NavGPT、Open-Nav等）对比。
  - 未与CityWalker（同为利用网络视频做城市导航的近期工作）进行直接对比，尽管技术路线是最相近的。
  - 离线评估采用轨迹预测误差而非端到端任务完成率，与实际导航性能之间的关联性未充分验证。

## 6. 论文的主要结论与发现

- **UrbanNav在离线基准上全面领先**：在seen和unseen场景下所有指标均优于NoMaD+CLIP、ViNT+CLIP和LeLaN。unseen场景下AOE降低至9.22°（LeLaN为10.36°），ADE降低至0.88m（LeLaN为0.98m），表明具有良好的泛化能力。
- **真实世界部署中显著优于所有基线**：总体成功率达83.3%（白天91.7%，夜晚75.0%），远超LeLaN的62.5%（白天75.0%，夜晚58.3%）。
- **网络级预训练是关键**：仅用真实数据训练的UrbanNav\*总体成功率仅33.4%，远低于完整模型的83.3%，证明大规模网络视频预训练提供了强泛化基础。
- **噪声指令鲁棒性**：UrbanNav在噪声指令条件下成功率仍达87.5%，体现了大规模多样数据训练的收益。
- **遮挡目标仍是挑战**：遮挡场景下成功率降至62.5%，说明方法是面向局部导航而非长期探索设计，但在该场景下仍优于所有基线。
- **FiLM融合模块至关重要**：去除FiLM导致显著性能下降，说明语言指令对视觉特征的调制对导航决策至关重要。
- **特征hallucination损失有效**：与某些先前工作的负面结论不同，在高质量、机器人兼容数据上该辅助损失带来明确收益。
- **数据规模与性能正相关**：错误指标随训练数据从300小时增至1,500小时持续下降，在约1,200小时后趋于平台期，验证了框架的可扩展性。

## 7. 优点

- **大规模可扩展的数据管线**：利用网络视频而非人工遥操作，自动化完成轨迹标注、过滤和指令生成，成本低、规模大，突破了真实世界导航数据获取的瓶颈。
- **重视机器人兼容性过滤**：系统性地解决网络视频中常见的视角偏移、不安全行为等问题（俯仰角、偏航角、人群密度三重过滤），确保训练数据质量，这是此前工作较少关注的。
- **真实地标语言指令**：将指令锚定于真实世界地标（含边界框和视觉描述），相比于合成的仿真指令更贴近实际应用场景，有助于语义理解与空间推理。
- **多步预测架构**：同时预测未来8步waypoints、方向和到达状态，使导航更平滑、更具前瞻性。
- **完备的训练目标设计**：四个互补的损失项联合监督空间精度、方向正确性、目标感知和未来场景理解，提升策略的综合性能。
- **充分的实验验证**：从离线基准到真实机器人部署，从正常条件到噪声/遮挡等挑战性场景，从组件消融到数据规模扩展，实验设计较为全面，结论可信度高。

## 8. 不足与局限

- **算力信息不透明**：文中未报告GPU型号、数量、训练时长、数据标注计算成本等关键资源信息，难以评估方法的实际部署门槛。
- **真实世界试验规模有限**：未明确报告试验总次数和每次试验的具体配置，每组约12次的试验量在统计上不够充分，未提供方差或置信区间。
- **遮挡目标的长期探索能力不足**：方法设计面向局部导航，对于初始不可见或遮挡的目标成功率有限（62.5%），限制了在复杂城市环境中的通用性。
- **真实部署场景多样性有限**：真实世界测试主要在单一平台的白天/夜间条件下进行，未验证不同机器人平台、不同城市、不同天气条件的泛化。
- **对比方法适配方式可能存在偏差**：基线方法被修改以适应语言指令任务，但修改方式可能未充分调优，存在对比公平性的潜在质疑。
- **数据偏向性风险**：YouTube步行视频来源分布可能偏向特定城市、文化和路况，可能导致模型在某些地理区域或文化背景下表现不佳。
- **VLM生成的指令与真实用户指令存在差距**：虽然指令语言自然，但与真实人类指令的分布（如含路径描述、历史参照、非地标信息等）可能仍有偏差。
- **未与其他同路线工作对比**：CityWalker在技术路线上最为接近（同为网络视频+视觉里程计标注），但论文未将其纳入对比，削弱了结论的区分度和说服力。
- **离线评估与真实导航的mismatch**：离线指标衡量轨迹预测偏差而非任务完成率，两者之间的相关性未得到充分论证。

（完）
