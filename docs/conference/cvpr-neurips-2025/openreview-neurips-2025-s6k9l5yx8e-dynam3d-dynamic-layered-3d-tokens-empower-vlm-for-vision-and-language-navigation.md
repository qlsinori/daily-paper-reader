---
title: "Dynam3D: Dynamic Layered 3D Tokens Empower VLM for Vision-and-Language Navigation"
title_zh: Dynam3D：动态分层3D标记增强视觉语言导航中的视觉语言模型
authors: "Zihan Wang, Seungjun Lee, Gim Hee Lee"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=s6k9l5yX8e"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 动态分层3D标记用于视觉语言导航
tldr: 针对视频大语言模型在视觉语言导航中三维几何理解不足、长期环境记忆有限和动态适应性差的问题，提出动态分层3D标记Dynam3D。该方法为VLM注入动态3D标记，增强空间语义感知和长期记忆能力。在VLN任务上实验取得显著性能提升，证明了动态3D标记对空间导航的有效性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: Video-VLM在VLN中三维几何理解不足，长期环境记忆有限且不适应动态场景。
method: 提出动态分层3D标记，将其注入VLM以增强空间感知和记忆。
result: 在VLN基准上取得新的最先进性能。
conclusion: 动态3D标记是提升VLN空间能力的有效途径。
---

## Abstract
Vision-and-Language Navigation (VLN) is a core task where embodied agents leverage their spatial mobility to navigate in 3D environments toward designated destinations based on natural language instructions. Recently, video-language large models (Video-VLMs) with strong generalization capabilities and rich commonsense knowledge have shown remarkable performance when applied to VLN tasks. However, these models still encounter the following challenges when applied to real-world 3D navigation: 1) Insufficient understanding of 3D geometry and spatial semantics; 2) Limited capacity for large-scale exploration and long-term environmental memory; 3) Poor adaptability to dynamic and changing environments.To address these limitations, we propose Dynam3D, a dynamic layered 3D representation model that leverages language-aligned, generalizable, and hierarchical 3D representations as visual input to train 3D-VLM in navigation action prediction. Given posed RGB-D images, our Dynam3D projects 2D CLIP features into 3D space and constructs multi-level 3D patch-instance-zone representations for 3D geometric and semantic understanding with a dynamic and layer-wise update strategy.  Our Dynam3D is capable of online encoding and localization of 3D instances, and dynamically updates them in changing environments to provide large-scale exploration and long-term memory capabilities for navigation. By leveraging large-scale 3D-language pretraining and task-specific adaptation, our Dynam3D sets new state-of-the-art performance on VLN benchmarks including R2R-CE, REVERIE-CE and NavRAG-CE under monocular settings. Furthermore, experiments for pre-exploration, lifelong memory, and real-world robot validate the effectiveness of practical deployment.

---

## 论文详细总结（自动生成）

## 论文总结：Dynam3D：动态分层3D标记增强视觉语言导航中的视觉语言模型

### 1. 核心问题与整体含义（研究动机与背景）

- **任务背景**：视觉语言导航（Vision-and-Language Navigation, VLN）是具身智能的核心任务之一，要求智能体依据自然语言指令在真实3D环境中自主移动并导航至目标位置。
- **现有方法**：视频大语言模型（Video-VLMs）凭借强大的泛化能力和丰富的常识知识，在VLN任务上已展现出优异性能。
- **三大核心挑战**：
  - **3D几何与空间语义理解不足**：Video-VLM大多基于2D帧或视频输入，缺乏对三维空间结构的深入建模能力；
  - **长期环境记忆受限**：面对大规模场景探索时，难以有效存储和利用历史空间信息；
  - **动态环境适应性差**：真实世界环境会发生变化，现有模型难以对动态场景进行及时更新与响应。
- **核心问题**：如何让VLM在VLN任务中获得更充分的三维空间感知、长期记忆和动态适应能力？**Dynam3D**对此给出了系统性回答。

### 2. 方法论：核心思想、关键技术细节与流程

#### 核心思想
- 提出**动态分层3D表示模型Dynam3D**，利用语言对齐的、可泛化的、层次化的3D表示作为视觉输入，训练3D-VLM进行导航动作预测。其核心在于将“静态的2D视觉输入”升级为“动态、可更新的3D结构化表示”。

#### 关键技术细节
- **2D特征到3D空间的投影**：给定带位姿的RGB-D图像（posed RGB-D images），将2D CLIP视觉特征投影至3D空间，实现视觉-语言特征对齐。
- **多层次3D表示（Patch-Instance-Zone）**：
  - **Patch层**：细粒度的局部3D几何与外观特征；
  - **Instance层**：3D实例级别的语义单元，支持实例级编码和在线定位；
  - **Zone层**：更高层次的区域/场所表示，辅助全局空间语义理解。
- **动态分层更新策略**：模型支持在线编码与定位3D实例，并在环境发生变化时动态更新相应层级的3D表示，从而赋予导航任务大规模探索和长期记忆能力。
- **训练流程**：先进行大规模3D-语言预训练，再进行特定VLN任务的适配微调（task-specific adaptation）。

### 3. 实验设计：数据集、基准与对比方法

- **基准数据集**：
  - **R2R-CE**（Room-to-Room，连续环境版）
  - **REVERIE-CE**（含目标定位与描述的连续环境导航）
  - **NavRAG-CE**（面向检索增强生成的连续环境导航）
- **实验设置**：采用**单目（monocular）设置**，即在仅有单目RGB-D输入的条件下进行评估。
- **对比方法**：与现有的VLN方法、Video-VLM基线进行对比，Dynam3D在三个基准上均取得了**新的最先进（SOTA）性能**。
- **其他实验场景**：
  - **预探索（pre-exploration）实验**：验证大规模探索能力；
  - **终身记忆（lifelong memory）实验**：验证长期记忆和知识保持能力；
  - **真实机器人（real-world robot）实验**：验证实际部署的可行性。

### 4. 资源与算力

- 论文提供的文本中**未明确说明**所使用的GPU型号、数量、训练时长、显存占用等算力信息。
- 这一信息缺失使得难以从算力成本角度对该方法进行完整的可行性评估。

### 5. 实验数量与充分性

- **实验数量**：实验覆盖三大公开基准（R2R-CE、REVERIE-CE、NavRAG-CE），并额外包含预探索、终身记忆和真实机器人部署实验。整体实验体系较为完整。
- **消融实验**：虽然论文总结中未详细列出消融实验的具体数量与内容，但此类多模块模型通常应有组件级消融（如层次化表示的有效性、动态更新策略的贡献等）来支撑核心设计的合理性。
- **客观性与公平性**：在统一基准（CE系列）和统一设置（单目）下对比多种方法，保证了对比的相对公平性。但若想更充分验证方法有效性，仍需补充：
  - 不同传感器配置（如深度噪声、无深度设置）下的鲁棒性测试；
  - 更多样化的环境类型与语言指令复杂度分析。

### 6. 主要结论与发现

- Dynam3D通过引入动态分层的3D表示，显著改善了VLM在VLN任务中的三维几何理解和空间语义感知能力。
- 动态更新策略赋予了模型长期环境记忆和动态场景适应能力，支持大规模持续探索。
- 在R2R-CE、REVERIE-CE和NavRAG-CE等主流基准上取得新的最先进性能，证明了动态3D标记是提升VLM空间导航能力的有效途径。
- 真实机器人实验进一步验证了该方法从仿真到现实的可迁移性和实际部署潜力。

### 7. 优点

- **问题定位清晰**：精准识别了Video-VLM在三维导航中的三大短板，并针对性提出解决方案。
- **表示设计创新**：Patch-Instance-Zone三层结构兼顾了局部细节与全局语义，动态更新机制有效解决了环境变化和长期记忆问题。
- **充分对齐语言与三维空间**：基于CLIP特征投影实现语言对齐，契合VLM的跨模态优势。
- **实验覆盖面广**：从仿真基准到真实机器人，从静态导航到长期记忆，实验安排系统、丰富。
- **应用价值显著**：支持在线更新和单目输入，使其在真实机器人部署中具备较强的实用性和通用性。

### 8. 不足与局限

- **算力与训练成本不透明**：论文未报告GPU型号、数量、训练时间等关键资源信息，不利于社区复现和成本评估。
- **单目设置下的感知局限**：仅依赖单目RGB-D输入，在实际复杂场景中可能受深度估计误差影响；论文未讨论对深度质量的敏感度。
- **大规模场景泛化性有待验证**：尽管在多个基准上表现优异，但在更具挑战性的开放世界、长时导航场景中是否依然稳定，仍需进一步验证。
- **消融实验细节未在摘要中呈现**：缺乏对每个设计组件（如Zone层必要性、动态更新策略的增益）的量化拆解，削弱了对方法贡献的精细归因分析。
- **应用边界**：动态更新机制在高动态、多人、遮挡等极端场景中的表现尚未充分讨论。

（完）
