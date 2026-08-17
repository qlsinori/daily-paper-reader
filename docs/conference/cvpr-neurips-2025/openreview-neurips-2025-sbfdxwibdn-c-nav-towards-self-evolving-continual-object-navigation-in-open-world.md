---
title: "C-NAV: Towards Self-Evolving Continual Object Navigation in Open World"
title_zh: C-NAV：面向开放世界的自进化连续物体导航
authors: "MingMing Yu, Fei Zhu, wenzhuo liu, Yirong Yang, Qunbo Wang, wenjun wu, Jing Liu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=SbfdxWibDn"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向新物体类别的连续物体导航与抗遗忘机制
tldr: 现有开放世界物体导航方法依赖静态轨迹和固定物体类别，难以应对动态变化场景。作者提出连续物体导航基准，要求智能体在学习新类别的同时不遗忘旧知识。C-Nav框架采用双路径抗遗忘机制，通过特征蒸馏对齐多模态特征来缓解灾难性遗忘。实验验证了该方法持续适应新类别并保持旧知识的能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有方法依赖静态轨迹和固定物体类别，无法适应开放世界的持续变化场景。
method: 提出C-Nav框架，包含双路径抗遗忘机制，利用特征蒸馏对齐多模态特征以学习新类别并缓解灾难性遗忘。
result: 在提出的连续物体导航基准上验证了C-Nav的有效性。
conclusion: C-Nav为开放世界下的连续物体导航提供了可行的学习框架与基准。
---

## Abstract
Embodied agents are expected to perform object navigation in dynamic, open-world environments. However, existing approaches typically rely on static trajectories and a fixed set of object categories during training, overlooking the real-world requirement for continual adaptation to evolving scenarios. To facilitate related studies, we introduce the continual object navigation benchmark, which requires agents to acquire navigation skills for new object categories while avoiding catastrophic forgetting of previously learned knowledge. To tackle this challenge, we propose C-Nav, a continual visual navigation framework that integrates two key innovations: (1) A dual-path anti-forgetting mechanism, which comprises feature distillation that aligns multi-modal inputs into a consistent representation space to ensure representation consistency, and feature replay that retains temporal features within the action decoder to ensure policy consistency. (2) An adaptive sampling strategy that selects diverse and informative experiences, thereby reducing redundancy and minimizing memory overhead. Extensive experiments across multiple model architectures demonstrate that C-Nav consistently outperforms existing approaches, achieving superior performance even compared to baselines with full trajectory retention, while significantly lowering memory requirements. 
The code will be publicly available at \url{https://bigtree765.github.io/C-Nav-project}.

---

## 论文详细总结（自动生成）

## C-NAV：面向开放世界的自进化连续物体导航——论文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：具身智能体被期望在动态变化的开放世界环境中执行物体导航任务（Object Navigation）。真实世界场景持续演化，新物体类别会不断出现，智能体需具备持续适应能力。
- **现有方法的不足**：当前主流方法严重依赖**静态的轨迹数据**和**固定的物体类别集合**进行训练。它们假设训练和测试时的物体类别不变，忽视了真实世界对**持续性适应**（continual adaptation）的需求，无法应对类别动态增长的实际场景。
- **核心研究问题**：如何让导航智能体在学习新物体类别导航技能的同时，**避免灾难性遗忘**已经学过的旧类别知识？现有方法对此没有提供有效方案。
- **整体含义**：该工作定义了“连续物体导航”（Continual Object Navigation）这一新问题，并为解决该问题提供了基准与算法框架，推动视觉导航从封闭静态环境走向开放动态世界的演进。

---

### 2. 方法论：核心思想、关键技术细节与算法流程

#### 核心思想
C-Nav 框架旨在通过**双路径抗遗忘机制**与**自适应记忆采样**，实现对新物体类别的持续学习能力和对旧知识的保持能力，在开放世界场景中形成“自进化”的导航智能体。

#### 关键技术一：双路径抗遗忘机制（Dual-Path Anti-Forgetting Mechanism）
该机制从**特征一致性**和**策略一致性**两个维度出发防止遗忘：

- **特征蒸馏（Feature Distillation）**：
  - 通过将**多模态输入**（如视觉、语言指令等）对齐到**一致的表征空间**，保持新旧任务间特征表示的稳定性。
  - 蒸馏过程中约束新模型的特征分布尽量接近旧模型，从而避免因新类别训练导致旧类别特征发生剧烈偏移。
- **特征回放（Feature Replay）**：
  - 在**动作解码器内部保留时序特征**，使策略网络能够回顾和利用旧经验中的时序信息。
  - 这保证了导航策略（policy）在持续学习新类别时的行为一致性，避免策略漂移。

#### 关键技术二：自适应采样策略（Adaptive Sampling Strategy）
- 从历史经验中选择**多样化且信息量丰富**的样本进行回放/训练。
- 目的是**降低样本冗余**、**最小化内存开销**，同时保留对旧知识保持最关键的样本。

#### 算法流程（文字描述）
1. 智能体接收当前导航任务目标（新类别物体）以及多模态感知输入。
2. 特征蒸馏路径将当前输入与历史模型特征进行对齐，维持表征一致性。
3. 动作解码器同时接收当前时序特征和历史回放时序特征，生成导航动作。
4. 训练期间，自适应采样策略从经验池中选取高信息量样本，用于后续回放更新。
5. 在持续学习过程中，新类别样本参与训练，旧类别样本通过蒸馏与回放路径保持记忆，从而兼顾“学习新”与“不忘旧”。

---

### 3. 实验设计

- **Benchmark**：作者**提出了一个新的持续物体导航基准**（Continual Object Navigation Benchmark），用于评估智能体在学习新物体类别时对旧类别的保持能力。
- **数据集 / 场景**：文中没有具体列出使用的场景数据集名称（如 AI2-THOR、RoboTHOR 等）。摘要提到是在该新基准上进行的实验。
- **对比方法**：
  - 与**现有多种物体导航方法**进行了对比。
  - 特别对比了 **保留完整轨迹的基线（baselines with full trajectory retention）**——即理论上限很高的记忆方式。
- **架构多样性**：实验覆盖了**多个模型架构**，验证了方法在不同网络结构下的有效性。
- **评估维度**：导航成功率、抗遗忘能力、内存开销等。

> 注：由于提供的文本以元数据和摘要为主，具体场景名称、完整基线列表及指标细节未完全展开。

---

### 4. 资源与算力

- **文中未明确说明**具体使用的 GPU 型号、数量、训练时长等算力信息。
- 仅能从论文标题（NeurIPS 2025 接收）和实验规模推测，该实验涉及多架构训练与持续学习场景，但具体计算资源配置在提供的材料中没有给出详细信息。

---

### 5. 实验数量与充分性

- **实验组数**：从摘要信息可知至少包括：
  - 多个模型架构下的评估；
  - 与多类现有方法的对比；
  - 与“全轨迹保留”强基线的对比。
- **消融实验**：摘要未明确列出独立消融实验，但“双路径机制”（蒸馏 + 回放）和“自适应采样”作为核心组件，其相对贡献理论上应通过消融验证（原文未在摘要中体现）。
- **充分性评估**：
  - **优点**：与全轨迹保留基线对比是非常有力的实验设计，能直观展示“少量记忆 + 抗遗忘机制”是否能接近甚至超越“保留所有数据”的上限，实验逻辑清晰。
  - **局限**：由于材料不完整，无法判断是否在多种真实世界场景、不同任务难度、更长持续学习序列下进行了充分测试。建议读者查阅完整论文以查看更全面实验。

---

### 6. 主要结论与发现

- C-Nav 在提出的持续物体导航基准上**持续优于现有方法**。
- 即使与**保留全部历史轨迹的强基线**相比，C-Nav 仍取得**更优或相当的性能**，同时大幅**降低内存需求**。
- 这表明通过精心设计的抗遗忘机制与经验采样策略，智能体可以在开放世界中实现“持续学习新类别”和“保持旧知识”的有效平衡，为连续物体导航提供了可行的学习框架与基准。

---

### 7. 优点（方法 / 实验亮点）

- **问题定义具有前瞻性**：首次明确提出“连续物体导航”这一研究方向，填补了现有导航研究停滞于静态类别集合的空白。
- **双路径抗遗忘设计合理**：
  - 特征蒸馏解决“表征漂移”，保证多模态对齐；
  - 特征回放保证“策略稳定性”，两者互补性强，方法论上具备理论支撑。
- **内存效率高**：自适应采样策略避免盲目存储所有旧数据，在保持性能的同时显著降低存储开销，实际部署价值高。
- **实验验证力度较强**：与全轨迹保留基线对比，有力证明了方法的效率和有效性；多架构验证增强了结论的普适性。

---

### 8. 不足与局限

- **实验细节不透明**：提供的材料中缺少具体数据集名称、场景数量、类别序列长度等关键实验配置，无法全面验证基准的挑战性和方法在不同环境下的泛化能力。
- **消融实验未在摘要体现**：对于双路径机制和自适应采样各组件贡献的量化分析，需依赖完整论文确认；若缺少详尽的消融分析，则结论的说服力会打折扣。
- **可能的偏差风险**：基准场景若与训练环境分布偏差较大，或类别顺序设置不具代表性，可能影响结果的外部有效性。
- **应用限制**：目前验证主要集中在仿真或基准测试环境；现实世界中传感器噪声、动态障碍、光照变化等复杂因素未在摘要中提及，实际部署到真实机器人平台的可行性和鲁棒性仍待验证。
- **“自进化”程度有限**：当前方法侧重“学习新类别”，对于更广义的知识迁移（如场景布局变化、语义关系变化）尚未体现明显扩展，开放世界适应性仍有一定局限。

---

（完）
