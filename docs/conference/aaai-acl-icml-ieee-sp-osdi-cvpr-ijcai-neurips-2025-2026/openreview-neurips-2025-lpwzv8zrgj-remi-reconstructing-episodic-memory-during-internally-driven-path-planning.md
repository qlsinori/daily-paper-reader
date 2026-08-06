---
title: "REMI: Reconstructing Episodic Memory During Internally Driven Path Planning"
title_zh: 通过内部驱动的路径规划重建情景记忆
authors: "Zhaoze Wang, Genela Morris, Dori Derdikman, Pratik Chaudhari, Vijay Balasubramanian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=LPWzV8zrgj"
tags: ["query:semantic-map"]
score: 9.0
evidence: 空间记忆、网格细胞、位置细胞与路径规划
tldr: 针对大脑如何将空间编码与记忆提取衔接的问题，该论文提出海马-内嗅皮层连接的系统级理论，说明位置细胞可将感觉输入与网格细胞模式关联，从而实现由感官线索触发的目标位置回忆、路径规划以及规划路线上的感觉经验重建。该理论把空间编码、情景记忆和内部驱动规划统一起来，为构建类脑的空间长期记忆与导航模型提供了新的理论框架。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有理论多单独解释网格细胞与位置细胞编码，缺乏对两者如何支持内部驱动规划与记忆提取的整合解释。
method: 提出系统层面的MEC-HC连接理论，通过位置细胞与网格细胞模式自动关联实现线索触发的目标提取、路径规划与感觉经验重建。
result: 在理论上阐明网格细胞与位置细胞交互支持空间记忆和内部驱动规划的回路机制。
conclusion: 该工作架起了空间认知与具身导航之间的桥梁，是空间长期记忆机制的一项核心理论贡献。
---

## Abstract
Grid cells in the medial entorhinal cortex (MEC) and place cells in the hippocampus (HC) both form spatial representations. Grid cells fire in triangular grid patterns, while place cells fire at specific locations and respond to contextual cues. How do these interacting systems support not only spatial encoding but also internally driven path planning, such as navigating to locations recalled from cues? Here, we propose a system-level theory of MEC-HC wiring that explains how grid and place cell patterns could be connected to enable cue-triggered goal retrieval, path planning, and reconstruction of sensory experience along planned routes. We suggest that place cells autoassociate sensory inputs with grid cell patterns, allowing sensory cues to trigger recall of goal-location grid patterns. We show analytically that grid-based planning permits shortcuts through unvisited locations and generalizes local transitions to long-range paths. During planning, intermediate grid states trigger place cell pattern completion, reconstructing sensory experiences along the route. Using a single-layer RNN modeling the HC-MEC loop with a planning subnetwork, we demonstrate these effects in both biologically grounded navigation simulations using RatatouGym and visually realistic navigation tasks using Habitat Sim.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：大脑中的网格细胞（位于内嗅皮层 MEC）和位置细胞（位于海马 HC）分别编码空间信息，但二者如何协同工作以支持**内部驱动的路径规划**（例如根据线索回忆目标位置并规划路径）以及**规划路径上的情景记忆重建**，目前缺乏系统性的理论解释。
- **研究背景**：先前研究多聚焦于网格细胞与位置细胞各自的空间编码特性，却较少从系统连接层面解答“空间编码如何衔接记忆提取与规划”这一关键问题。论文希望打破这一割裂，建立从空间表征到情景记忆、再到行为规划的完整理论闭环。
- **整体含义**：提出一个海马-内嗅皮层（HC-MEC）连接的系统级理论，将空间编码、情景记忆和内部驱动规划统一起来，为类脑空间长期记忆与导航模型提供新框架。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程（用文字说明即可）

- **核心思想**：位置细胞作为“桥梁”，将**感觉输入**与**网格细胞模式**自动关联（autoassociate），从而使感官线索能够触发目标位置的网格模式回忆；随后，基于网格细胞的路径规划可以利用网格的规则性实现跨越未访问位置的捷径，并将局部转移泛化为长距离路径；在规划过程中，中间网格状态又会触发位置细胞的模式补全（pattern completion），从而重建规划路线上的感觉经验。
- **系统模型**：论文用**单层循环神经网络（RNN）** 建模 HC-MEC 回路，并附加一个**规划子网络**，用以模拟线索触发目标回忆、路径生成和感觉经验重建的完整过程。
- **算法流程（文字性描述）**：
  1. 感觉线索输入 → 位置细胞激活 → 通过自动关联机制回忆对应的目标网格模式；
  2. 网格细胞网络进行路径规划，利用网格编码的几何规律产生从当前位置到目标的连续路径；
  3. 规划过程中每一步的网格状态反馈到位置细胞，触发位置细胞模式补全，重建该位置对应的感觉情景；
  4. 最终形成一条“带感觉经验标注”的规划路径，供导航使用。
- **理论分析**：论文从解析上证明基于网格的规划允许通过未访问位置生成捷径，并能将局部转移规则泛化到长距离路径，这是网格细胞规则模式的结构性优势。

### 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **实验场景**：
  - **RatatouGym**：一个基于生物学启发的导航模拟环境，用于验证网格细胞/位置细胞回路在类鼠导航任务中的行为。
  - **Habitat Sim**：一个视觉逼真的导航仿真平台，用于测试模型在现实场景图像输入下的表现。
- **任务类型**：线索触发的目标回忆、内部驱动的路径规划、规划路线上的感觉经验重建。
- **Benchmark / 对比方法**：摘要中未明确提及对比了哪些具体基线方法，也未说明是否与现有导航模型（如基于度量地图或认知地图的方法）进行比较。从可获取的信息看，论文更侧重于验证**理论模型的行为学与神经生理学合理性**，而非在标准导航 benchmark 上追求 SOTA 指标。

### 4. 资源与算力：如果文中有提到，请总结使用了多少算力（GPU 型号、数量、训练时长等）。若未明确说明，也请指出这一点。

- 在所提供的内容（abstract 和开头段落）中，**未提及任何算力资源信息**，包括 GPU 型号、数量、训练时长、参数量等。
- 因此无法给出资源与算力总结，需要查看论文正文或附录才能获取相关信息。

### 5. 实验数量与充分性：大概做了多少组实验（如不同数据集、消融实验等），这些实验是否充分、是否客观、公平

- **实验数量**：摘要中仅提到两个仿真环境：RatatouGym 和 Habitat Sim。未提及具体的实验组数、消融实验（例如移除规划子网络、破坏网格-位置连接等）或参数敏感性分析。
- **充分性评估**：
  - 从现有信息来看，实验覆盖了两个层面：**生物合理性场景**（RatatouGym）和**视觉真实场景**（Habitat Sim），具有一定代表性。
  - 但缺少与现有方法（如强化学习导航、基于图谱的规划）的系统对比，也缺少对模型组件（如位置细胞-网格细胞关联、规划子网络）的消融验证，因此实验的**充分性和公平性尚无法从摘要中完全判断**。
  - 若论文正文包含上述分析，则实验可能是充分的；但仅凭当前文本，只能说实验设计思路合理，细节待确认。

### 6. 论文的主要结论与发现

- 位置细胞能够将感觉输入与网格细胞模式形成自动关联，从而实现**线索触发的目标回忆**。
- 基于网格模式的路径规划具有结构优势：**支持捷径生成**（穿过未访问位置）和**局部转移的远距离泛化**。
- 在规划过程中，网格状态的中间序列会反向触发位置细胞模式补全，从而**重建规划路线上的感觉经验**，实现“规划即回忆”的统一机制。
- 该系统级理论成功将空间编码、情景记忆和内部驱动规划整合在一个回路模型中，并通过两个仿真环境验证了其可行性和推广性。

### 7. 优点：方法或实验设计上有哪些亮点

- **理论统一性强**：首次从系统层面将网格细胞、位置细胞、情景记忆和路径规划纳入同一框架，填补了空间编码与记忆提取之间的理论空白。
- **解析与计算结合**：既有对网格编码支持捷径与泛化的解析证明，又有 RNN 模型的行为仿真，理论与计算相互印证。
- **生物学合理性**：模型结构基于真实的 MEC-HC 解剖连接，使用单层 RNN 保持了神经动力学的简洁性，便于生物学解释。
- **双环境验证**：在生物模拟（RatatouGym）和视觉现实模拟（Habitat Sim）中测试，兼顾了神经机制与实用场景。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **实验细节不透明**：摘要未提供定量指标（如成功率、路径长度、误差等），也未说明与基线的对比，难以评估实际性能水平。
- **缺乏消融研究**：未提及对关键组件（如自动关联机制、模式补全、规划子网络）的消融分析，无法判断各模块的独立贡献。
- **模型规模与真实性**：单层 RNN 虽简洁，但可能无法完全捕捉真实海马-内嗅回路的复杂动态（如 theta 振荡、尖峰时序依赖可塑性等）。
- **适用范围局限**：目前仅在仿真环境中验证，尚未在真实机器人或神经生理数据上进行测试；对多模态感觉输入（如嗅觉、听觉）的扩展也未讨论。
- **偏差风险**：若仿真环境内置了与网格结构相关的先验，可能高估模型在真实环境中的泛化能力；需进一步在动态、非结构化场景中验证。

（完）
