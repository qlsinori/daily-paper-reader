---
title: "Dynam3D: Dynamic Layered 3D Tokens Empower VLM for Vision-and-Language Navigation"
title_zh: Dynam3D：动态分层3D标记赋能视觉语言导航的VLM
authors: "Zihan Wang, Seungjun Lee, Gim Hee Lee"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=s6k9l5yX8e"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 视觉语言导航; 动态分层3D标记; VLM; 空间记忆
tldr: 视频语言大模型在视觉语言导航任务中展现出泛化能力，但对3D几何和空间语义理解不足，且难以支持大规模探索和长期环境记忆。本文提出Dynam3D，通过动态分层3D标记增强VLM，使其能更好地理解3D空间、积累长期记忆并适应动态变化环境。该方法针对真实世界3D导航的三大挑战，在VLN基准上验证了其提升导航性能的有效性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视频大模型应用于VLN时存在3D几何理解不足、长期记忆有限和动态环境适应差三大挑战。
method: 提出动态分层的3D标记表示，将其注入VLM以增强空间语义理解、大规模探索记忆和动态环境适应能力。
result: Dynam3D在VLN基准上旨在提升3D空间理解、长期记忆和动态适应性，从而改善端到端导航性能。
conclusion: 表明动态3D标记能有效弥补视频语言模型在具身导航中的空间记忆短板，推进VLN在真实世界中的应用。
---

## Abstract
Vision-and-Language Navigation (VLN) is a core task where embodied agents leverage their spatial mobility to navigate in 3D environments toward designated destinations based on natural language instructions. Recently, video-language large models (Video-VLMs) with strong generalization capabilities and rich commonsense knowledge have shown remarkable performance when applied to VLN tasks. However, these models still encounter the following challenges when applied to real-world 3D navigation: 1) Insufficient understanding of 3D geometry and spatial semantics; 2) Limited capacity for large-scale exploration and long-term environmental memory; 3) Poor adaptability to dynamic and changing environments.To address these limitations, we propose Dynam3D, a dynamic layered 3D representation model that leverages language-aligned, generalizable, and hierarchical 3D representations as visual input to train 3D-VLM in navigation action prediction. Given posed RGB-D images, our Dynam3D projects 2D CLIP features into 3D space and constructs multi-level 3D patch-instance-zone representations for 3D geometric and semantic understanding with a dynamic and layer-wise update strategy.  Our Dynam3D is capable of online encoding and localization of 3D instances, and dynamically updates them in changing environments to provide large-scale exploration and long-term memory capabilities for navigation. By leveraging large-scale 3D-language pretraining and task-specific adaptation, our Dynam3D sets new state-of-the-art performance on VLN benchmarks including R2R-CE, REVERIE-CE and NavRAG-CE under monocular settings. Furthermore, experiments for pre-exploration, lifelong memory, and real-world robot validate the effectiveness of practical deployment.

---

## 论文详细总结（自动生成）

# Dynam3D 论文中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：视觉语言导航（VLN）要求具身智能体根据自然语言指令在 3D 环境中移动并到达目标位置。近年来，视频语言大模型（Video-VLMs）凭借强泛化能力和丰富常识在 VLN 上表现优异。
- **核心问题**：将 Video-VLM 直接应用于真实世界 3D 导航仍面临三大挑战：
  1. **3D 几何与空间语义理解不足**——2D 视频token缺乏对空间结构和物体关系的建模；
  2. **大规模探索与长期环境记忆能力有限**——视频输入难以高效存储、组织和复用长时程空间信息；
  3. **对动态环境适应性差**——真实环境中物体移动、视角变化等导致静态表示失效。
- **整体含义**：现有视频语言模型缺少结构化的 3D 空间记忆，无法支撑真实机器人长期、稳健的导航。论文旨在通过引入动态分层 3D 标记来补齐这一短板，推动 VLN 从仿真走向真实应用。

## 2. 方法论（核心思想、关键技术细节、算法流程）

- **核心思想**：提出 **Dynam3D**——一种动态分层的 3D 表示模型，将语言对齐、可泛化、层次化的 3D 表示作为视觉输入，训练 3D-VLM 进行导航动作预测。
- **输入形式**：带位姿的 RGB-D 图像序列（posed RGB-D images）。
- **关键技术细节**：
  - **2D→3D 特征投影**：将 2D CLIP 特征投影到 3D 空间，为 3D 表示注入语言对齐的语义。
  - **多级 3D 表示（patch-instance-zone）**：构建三个层次的 3D 表示：
    - **Patch** 级：局部几何与外观特征；
    - **Instance** 级：可在线定位的 3D 实例（物体级）；
    - **Zone** 级：区域/场景级语义单元。
  - **动态分层更新策略（dynamic and layer-wise update）**：随探索推进，不同层级以不同频率与方式更新，以支持环境变化和记忆累积。
  - **在线编码与定位**：能够增量式编码新的 3D 实例并在环境中定位它们，无需全局重构建。
- **算法流程（文字描述）**：
  1. 对每一帧 RGB-D 图像提取 2D CLIP 特征；
  2. 利用深度图与相机位姿将特征反投影到 3D 点云/体素空间；
  3. 通过聚类/分组构建 instance 级表示，并聚合为 zone 级表示；
  4. 随着智能体移动，新观测以分层方式更新现有 3D 表示，同时维护长期记忆；
  5. 将当前视觉观测与查询的 3D token 注入 VLM，预测下一个导航动作。
- **训练策略**：先进行大规模 3D-语言预训练，再在具体 VLN 任务上进行适配微调。

## 3. 实验设计（数据集、Benchmark、对比方法）

- **数据集 / Benchmark**：
  - **R2R-CE**（Room-to-Room, Continuous Environment）；
  - **REVERIE-CE**（含远程目标定位的连续环境版本）；
  - **NavRAG-CE**（面向检索增强导航的连续环境 benchmark）。
- **实验设置**：单目（monocular）设置下进行评估。
- **额外实验场景**：
  - **预探索实验**（pre-exploration）；
  - **终身记忆实验**（lifelong memory）；
  - **真实世界机器人实验**（real-world robot）。
- **对比方法**：对比了现有 VLN-CE 方法（包括基于 Video-VLM 的方法及其他基线），论文报告 Dynam3D 在上述 benchmark 上取得新的 state-of-the-art 性能（摘要未列出具体数值和对比方法清单，正文应包含更多详情）。

## 4. 资源与算力

- **摘要与元数据中未明确说明**：
  - 未提及 GPU 型号、数量、训练时长、显存消耗、模型参数量等具体算力信息；
  - 也未说明 3D 特征投影和实时更新的计算开销。
- 需要查看论文正文的实验设置部分才能获取相关细节。

## 5. 实验数量与充分性

- **实验数量**：摘要中涉及的实验维度较广，包括：
  - 三个主流 VLN-CE benchmark（R2R-CE、REVERIE-CE、NavRAG-CE）上的主实验；
  - 三项附加评估：预探索、终身记忆、真实机器人部署；
  - 预期还有消融实验（如是否使用分层表示、是否动态更新、patch-instance-zone 各级贡献等），但摘要未列出具体消融项。
- **充分性评估**：
  - **覆盖合理**：从仿真到真实、从短期导航到长期记忆，实验覆盖面较完整；
  - **公平性疑点**：单目设置下的对比是否统一使用相同骨干网络、相同预训练数据、相同推理步数等，摘要中未说明；需谨慎判断是否完全公平；
  - **缺失细节**：未提供误差条、统计显著性检验、不同随机种子重复次数等信息，客观性无法从摘要确认。

## 6. 主要结论与发现

- 动态分层 3D 标记能显著提升 VLM 在 VLN 任务中的导航动作预测性能；
- Dynam3D 在 R2R-CE、REVERIE-CE、NavRAG-CE 上达到新的最优结果，验证了 3D 空间记忆对导航泛化的重要性；
- 预探索实验显示 Dynam3D 能利用先验探索信息提高后续导航效率；
- 终身记忆实验证明其能够持续积累环境信息并应对动态变化；
- 真实机器人实验验证了 Dynam3D 在物理世界中的实际部署可行性；
- 总体表明动态 3D 表示可有效弥补视频语言模型在具身导航中的空间记忆短板。

## 7. 优点（方法或实验设计上的亮点）

- **方法创新性**：
  - 提出“patch-instance-zone”三层级 3D 表示，兼顾局部细节、实体对象和区域语义，结构合理；
  - 引入**动态分层更新**机制，使 3D 表示适应环境变化，同时维持长期记忆；
  - 利用 CLIP 特征做语言对齐，使 3D 表示天然具备零样本/少样本泛化潜力；
  - 支持**在线增量式编码与定位**，无需全局重建，适合真实机器人探索。
- **实验设计**：
  - 在多个连续环境 benchmark 上评估，避免仅依赖离散导航指标；
  - 加入真实机器人验证，提升结论的可信度和落地价值；
  - 同时考察预探索、长期记忆等多维度应用场景，覆盖面广。

## 8. 不足与局限

- **实验覆盖方面**：
  - 仅在单目设置下评估，深度估计误差对性能的影响未被单独分析；
  - 未提供不同环境规模（如小型室内 vs 大型开放空间）下的性能分解；
  - 未与基于显式 3D 地图或多传感器融合（LiDAR + RGB-D）的方法进行对比，适用场景边界不明。
- **方法问题**：
  - 动态分层更新策略的计算效率和实时性在摘要中未给出详细开销分析；
  - 3D CLIP 特征的泛化能力可能受限于 CLIP 的训练数据分布，在长尾场景或非语义物体上可能退化；
  - 文本说明中未给出公式、伪代码或复杂度分析，相关细节需要依赖正文。
- **风险与偏差**：
  - 摘要未明确说明各实验的随机种子、重复次数和方差，存在结果偶然性风险；
  - 对比方法的配置（是否同样使用 CLIP、类似参数量、相同训练数据）未公开，可能引入不公平比较；
  - 论文发表于 NeurIPS 2025 预印本，尚未经过最终版本验证，部分实现细节可能有变化。

（完）
