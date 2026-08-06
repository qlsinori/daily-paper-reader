---
title: Spatial Memory for Out-of-Vision Manipulation in Vision-Language-Action
title_zh: 用于视野外操作的视觉-语言-动作空间记忆
authors: "Pengteng Li, Weiyu Guo, He Zhang, Tiefu Cai, Xiao He, Yandong Guo, Hui Xiong"
date: 2026-04-30
pdf: "https://openreview.net/pdf/95685162fa940bca32702d659b96eebf84138a75.pdf"
tags: ["query:semantic-map"]
score: 9.0
evidence: 为视觉-语言-动作模型构建持久空间记忆，支持视野外推理
tldr: 针对大多数视觉-语言-动作模型在目标移出相机视野时表现脆弱的问题，本文提出SOMA空间记忆框架。它通过可移动头部相机采集多视角观测，构建统一的语义-空间持久记忆，并利用动态记忆精炼模块维持全局一致性，使模型能超出当前视锥进行推理。该方法为具身操作提供了超越即时视觉输入的持久空间记忆能力。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有视觉-语言-动作模型通常假设任务相关物体始终可见，当目标超出相机视野时行为会变得脆弱和被动。
method: 提出SOMA框架，利用可移动头部相机扫描多视角观测，构建统一的空间-语义记忆，并通过动态记忆精炼维持全局一致性。
result: 该框架使模型能够基于持久空间记忆对视野外目标进行推理，从而克服当前视锥的局限。
conclusion: 通过引入持久空间记忆，SOMA增强了视觉-语言-动作模型在目标不可见场景下的操作能力。
---

## Abstract
We introduce SOMA, the Spatial Memory framework for Out-of-Vision Manipulation in Vision-Language-Action (VLA) models. Most existing VLAs implicitly assume that task-relevant objects are always visible, leading to brittle and reactive behaviors when targets fall outside the camera’s field of view. SOMA addresses this limitation by equipping VLAs with a persistent spatial memory constructed from multi-view observations acquired via a movable head camera, enabling reasoning beyond the current visual frustum. The framework consists of three components: Spatial Memory Construction, which aggregates angular-wise observations into a unified spatial–semantic representation through scanning; Dynamic Memory Refinement, which maintains global consistency over time; and Contextual Memory Retrieval, which activates instruction-relevant spatial cues during manipulation. We evaluate SOMA on five challenging real-world out-of-vision manipulation tasks, including multi-step and dual-arm scenarios where target objects are initially invisible. Experimental results show that SOMA not only improves task success rates, but also induces qualitatively different manipulation behaviors, with faster target localization, reduced viewpoint search, and near one-shot grasping under partial observability. Additional experiments on RoboCasa GR1 and SimplerEnv further validate the effectiveness of SOMA’s memory design under conventional fully observable settings. Code will be released soon.

---

## 论文详细总结（自动生成）

## 论文总结：SOMA——用于视野外操作的视觉-语言-动作空间记忆

### 1. 核心问题与整体含义

- **研究背景**：现有的视觉-语言-动作（VLA）模型大多隐含假设任务相关物体始终处于相机视野内。一旦目标物体移出视野，模型的行为会变得脆弱、被动，缺乏主动记忆和推断能力。
- **核心问题**：如何在目标物体不可见（out-of-vision）的情况下，让VLA模型依然能够完成操作任务？这要求模型具备超越当前视觉锥（visual frustum）的推理能力。
- **整体含义**：论文提出SOMA框架，为VLA模型赋予**持久空间记忆**，使其能够在部分可观测条件下利用历史多视角观测进行推理，从而显著提升真实世界操作任务的鲁棒性与成功率。

### 2. 方法论

- **核心思想**：通过可移动的头部相机采集多视角观测，构建一个统一的**语义-空间持久记忆**，让模型在操作时能够“回忆”视野外的目标位置与属性，而非仅仅依赖当前帧的视觉输入。
- **三大组件**：
  1. **空间记忆构建（Spatial Memory Construction）**：通过扫描（scanning）将不同角度（angular-wise）的观测聚合成统一的空间-语义表示，形成全局一致的地图式记忆。
  2. **动态记忆精炼（Dynamic Memory Refinement）**：随时间推移维护记忆的全局一致性，处理目标移动、视角变化和遮挡带来的信息过时或冲突。
  3. **上下文记忆检索（Contextual Memory Retrieval）**：在执行操作时，根据语言指令激活与任务相关的空间线索，避免无关记忆干扰决策。
- **算法流程（文字说明）**：首先，机器人使用可移动头部相机对周围环境进行多角度扫描，获取多帧观测；然后，每帧观测被编码为带语义的空间特征，并通过聚合形成统一记忆；在操作过程中，记忆会随着新观测的到来动态更新与精炼；最后，根据自然语言指令检索相关记忆，将当前视觉输入与记忆特征融合，输出动作。
- **公式**：摘要未提供具体数学公式，但整体流程符合“感知→记忆构建→记忆更新→检索→动作生成”的范式。

### 3. 实验设计

- **真实世界任务**：
  - 5个具有挑战性的**视野外操作任务**，包括：
    - 多步操作（multi-step）
    - 双机械臂协同场景（dual-arm）
    - 目标物体初始不可见（initially invisible）的场景
- **仿真/基准环境**：
  - **RoboCasa GR1**：用于验证在常规全可观测条件下记忆设计的有效性。
  - **SimplerEnv**：额外的仿真基准，进一步评估SOMA的泛化能力。
- **对比方法**：摘要未明确列出具体基线名称，但明确指出SOMA在成功率上优于已有方法，并表现出“定性不同的操作行为”。由于未给出基线细节，读者无法判断是否与最新的VLA模型（如RT-2、Octo等）进行对比。

### 4. 资源与算力

- **未明确说明**：摘要及元数据中未提及使用的GPU型号、数量、训练时长、参数量或推理开销等资源信息。因此无法评估方法的计算成本或可复现性。

### 5. 实验数量与充分性

- **实验组数**：
  - 真实世界：5个任务（多步、双臂、目标不可见等场景）。
  - 仿真：2个基准环境（RoboCasa GR1、SimplerEnv）。
  - 摘要声称有“additional experiments”，但未给出具体实验数量或消融研究细节。
- **充分性与客观性**：
  - **优点**：覆盖了真实世界与仿真环境，包含具有挑战性的视野外场景，并报告了成功率、目标定位速度、视角搜索次数和单次抓取成功率等指标。
  - **不足**：缺乏详细的消融实验（例如移除记忆精炼、检索组件的影响）、缺乏对失败案例的分析、未报告多次运行的标准差或随机种子数量，因此统计显著性不明。此外，未给出基线方法的名称及配置，公平性较难验证。

### 6. 主要结论与发现

- SOMA显著提高了VLA模型在目标不可见场景下的任务成功率。
- 引入持久空间记忆后，模型展现出**定性不同的操作行为**：
  - 更快地定位目标物体。
  - 减少视角搜索（viewpoint search）的次数。
  - 在部分可观测条件下能实现**接近单次抓取（near one-shot grasping）**。
- 在常规全可观测环境中，SOMA的记忆设计同样有效，不会损害原有性能，验证了其通用性。

### 7. 优点

- **问题切中实际**：目标物体移出视野是真实机器人操作中的常见故障，现有VLA研究较少系统解决。
- **框架完整**：记忆构建、动态更新、上下文检索三个模块分工明确，覆盖了空间记忆的生命周期。
- **多场景验证**：包含真实世界多步、双臂任务以及两个仿真基准，结果具有较强说服力。
- **行为层面改进**：不仅报告成功率，还分析目标定位速度、视角搜索频率等行为指标，揭示了方法带来的本质变化。

### 8. 不足与局限

- **缺乏对比细节**：未列出对比方法的具体名称和配置，难以评估相对最先进方法的提升幅度。
- **消融不充分**：未展示各组件（如记忆精炼、检索）的独立贡献，无法确定哪些设计是关键。
- **资源信息缺失**：未报告计算开销，无法判断该方法是否适合实时机器人控制。
- **实验范围有限**：真实世界任务数量较少，且未说明机械臂型号、相机参数、场景多样性等，可能影响泛化结论。
- **长期记忆维护未深入**：动态记忆精炼如何应对大规模场景或动态物体尚不清楚，摘要未讨论记忆容量或冲突处理细节。
- **生成式VLA的适配性**：摘要中未说明SOMA是与特定VLA架构（如RT-2、PaLM-E）结合还是独立于架构，通用性尚需验证。

（完）
