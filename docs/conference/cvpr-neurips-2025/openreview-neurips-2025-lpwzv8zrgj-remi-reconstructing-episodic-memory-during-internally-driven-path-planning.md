---
title: "REMI: Reconstructing Episodic Memory During Internally Driven Path Planning"
title_zh: REMI：内部驱动路径规划中的情景记忆重建
authors: "Zhaoze Wang, Genela Morris, Dori Derdikman, Pratik Chaudhari, Vijay Balasubramanian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=LPWzV8zrgj"
tags: ["query:vln-memory"]
score: 8.0
evidence: 导航系统中空间长期记忆机制的理论模型
tldr: 网格细胞与位置细胞如何协同支持内部驱动的路径规划仍缺乏系统性机制解释。本文提出内嗅皮层-海马连接理论，阐明感觉线索可触发目标检索、路径规划以及沿规划路径的感觉经验重建。该机制为空间长期记忆在导航中的作用提供了神经计算层面的框架，可启发具身导航记忆模块的设计。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 需要系统理论解释网格细胞与位置细胞如何协同支持内部驱动的路径规划。
method: 提出内嗅皮层-海马连接理论，建立线索触发目标检索与路径重建的认知架构。
result: 解释了空间编码如何支持规划路径上感觉经验的重建，形成长期空间记忆机制。
conclusion: 为具身导航中的空间长期记忆建模提供了神经科学基础。
---

## Abstract
Grid cells in the medial entorhinal cortex (MEC) and place cells in the hippocampus (HC) both form spatial representations. Grid cells fire in triangular grid patterns, while place cells fire at specific locations and respond to contextual cues. How do these interacting systems support not only spatial encoding but also internally driven path planning, such as navigating to locations recalled from cues? Here, we propose a system-level theory of MEC-HC wiring that explains how grid and place cell patterns could be connected to enable cue-triggered goal retrieval, path planning, and reconstruction of sensory experience along planned routes. We suggest that place cells autoassociate sensory inputs with grid cell patterns, allowing sensory cues to trigger recall of goal-location grid patterns. We show analytically that grid-based planning permits shortcuts through unvisited locations and generalizes local transitions to long-range paths. During planning, intermediate grid states trigger place cell pattern completion, reconstructing sensory experiences along the route. Using a single-layer RNN modeling the HC-MEC loop with a planning subnetwork, we demonstrate these effects in both biologically grounded navigation simulations using RatatouGym and visually realistic navigation tasks using Habitat Sim.

---

## 论文详细总结（自动生成）

# 论文总结：REMI——内部驱动路径规划中的情景记忆重建

## 1. 核心问题与整体含义

- **研究动机**：内嗅皮层（MEC）中的网格细胞（grid cells）和海马体（HC）中的位置细胞（place cells）都参与空间表征，但二者如何协同支持“内部驱动的路径规划”（例如根据线索回忆某个目标位置并规划路径）在机制层面仍缺乏系统性解释。
- **核心问题**：本文回答的是：网格细胞与位置细胞如何连接，从而支持“线索触发目标检索 → 路径规划 → 沿规划路径重建感觉经验”这一完整认知过程。
- **整体含义**：该研究提出了一个系统层面的内嗅皮层-海马连接理论，将空间编码与情景记忆重建统一在同一个神经计算框架下，为理解大脑中的长期空间记忆机制提供了理论模型，也为具身导航中空间记忆模块的设计提供了神经科学启发。

## 2. 方法论

- **核心思想**：位置细胞将感觉输入与网格细胞模式进行自联想（autoassociate），使感觉线索能够触发目标位置对应的网格模式；随后在网格表征空间中进行路径规划，并在规划过程中通过位置细胞的模式补全（pattern completion）重建沿途的感觉经验。
- **理论主张**：
  - 基于网格细胞的规划允许在未访问过的位置之间走“捷径”；
  - 它能将局部转移经验泛化到长距离路径。
- **实现模型**：
  - 使用一个单层循环神经网络（RNN）建模海马-内嗅皮层回路（HC-MEC loop），并加入一个规划子网络。
  - 模型并不依赖显式的地图存储，而是通过网格细胞模式之间的动态转换实现规划。
- **算法流程（文字化描述）**：
  1. 感觉线索输入位置细胞；
  2. 位置细胞自联想地激活对应目标位置的网格细胞模式；
  3. 在网格细胞空间中完成从当前位置到目标位置的路径规划；
  4. 规划过程中每个中间网格状态触发位置细胞的模式补全；
  5. 模式补全沿路径重建相应的感觉经验，从而形成“情景记忆”式的重构。
- **需要说明的是**：当前提供的论文内容中未给出具体数学公式或伪代码，核心方法以理论描述和仿真验证为主。

## 3. 实验设计

- **实验场景**：论文在两个不同的仿真环境中验证所提机制：
  - **RatatouGym**：生物学上更贴近啮齿动物导航条件的仿真环境；
  - **Habitat Sim**：视觉上更逼真的具身导航任务环境。
- **Benchmark**：现有内容未提到其使用固定的公开 benchmark 对比；更像是通过两类仿真环境验证机制可行性。
- **对比方法**：现有内容中未提及与其他导航模型或神经计算模型进行定量对比。

## 4. 资源与算力

- 提供的论文内容中**未明确说明**使用的 GPU 型号、数量、训练时长或总算力消耗。
- 由于论文主要提出的是理论机制并用 RNN 进行仿真验证，可能对算力的需求不高，但这一点只能视为推测，不能作为论文事实。

## 5. 实验数量与充分性

- 从摘要看，实验包括两类导航仿真：RatatouGym 和 Habitat Sim，分别对应生物合理性场景和视觉真实性场景。
- 现有内容中**没有提及消融实验、参数敏感性分析、对照模型比较或统计显著性检验**，因此无法判断实验的充分性和公平性。
- 综合来看：实验能够初步证明模型在两类环境中的有效性，但作为“系统级理论”的验证仍显有限，特别是缺少对核心假设（如自联想、模式补全机制）的单独验证，以及与已有空间导航模型的定量横向对比。

## 6. 主要结论与发现

- 网格细胞与位置细胞的连接方式可以解释“线索触发目标检索”这一过程。
- 基于网格细胞的规划能够支持跨越未访问位置的新路径，并实现从局部经验到长距离路径的泛化。
- 规划过程中通过位置细胞的模式补全，可以沿路径“重建”感觉经验，从而将空间规划与情景记忆重建统一起来。
- 该机制在生物仿真（RatatouGym）和视觉真实仿真（Habitat Sim）中均得到验证，说明其具有一定普适性。
- 总体结论是：该理论可为具身导航中的空间长期记忆建模提供可计算、可验证的神经科学基础。

## 7. 优点

- **理论创新性**：首次从系统层面将网格细胞、位置细胞、路径规划与情景记忆重建纳入同一个机制模型，填补了现有理论空白。
- **生物合理性**：模型基于内嗅皮层-海马回路的真实解剖连接，具有较强的神经科学依据。
- **计算可行性**：使用单层 RNN 实现，结构简洁，具备可仿真性。
- **多场景验证**：同时使用生物导航环境（RatatouGym）和视觉真实环境（Habitat Sim），兼顾生物合理性与工程应用导向。
- **对具身导航的启示**：提出了一种不同于传统显式地图或拓扑记忆的空间长期记忆方案，对机器人导航中的记忆模块设计具有启发价值。

## 8. 不足与局限

- **细节不完整**：当前可见的论文内容仅为摘要和元数据，缺少方法描述、公式、网络结构细节和实验设置，分析只能基于摘要展开。
- **实验覆盖有限**：只提到两个仿真环境，缺少真实神经数据验证或行为实验证据。
- **缺乏对照与消融**：没有说明是否与其他导航模型（如基于地图的方法、强化学习方法）进行对比，也未报告消融实验，导致“机制必要性”证据不足。
- **偏差风险**：如果只依赖自建仿真环境，模型可能对任务设定或环境参数有隐性依赖；没有报告随机种子、重复次数或方差，难以评估结果稳定性。
- **应用边界**：所提机制面向“线索触发的内部路径规划”，对动态障碍、实时重规划、多任务并发等真实世界需求可能还需要额外扩展。

（完）
