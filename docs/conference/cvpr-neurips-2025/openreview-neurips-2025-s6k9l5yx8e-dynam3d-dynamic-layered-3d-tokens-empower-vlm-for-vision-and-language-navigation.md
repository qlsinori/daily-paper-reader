---
title: "Dynam3D: Dynamic Layered 3D Tokens Empower VLM for Vision-and-Language Navigation"
title_zh: Dynam3D：动态分层3D令牌赋能视觉-语言导航大模型
authors: "Zihan Wang, Seungjun Lee, Gim Hee Lee"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=s6k9l5yX8e"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 面向自然语言指令的视觉语言导航，并解决长期环境记忆
tldr: 现有视频-语言大模型在应用于三维视觉语言导航时，面临3D几何与空间语义理解不足、大规模探索与长期环境记忆受限、动态环境适应差等问题。为此本文提出Dynam3D，构造动态分层3D令牌来增强VLN模型，以显式建模三维几何和语义，并支持长时间环境记忆。在导航任务中验证了该方法能有效提升智能体在复杂环境中理解指令和进行长时决策的能力。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有Video-VLM应用于VLN时缺乏3D几何与空间语义理解、长期环境记忆和动态适应性，本文旨在解决这些局限。
method: 提出Dynam3D，使用动态分层3D令牌表示场景，并与VLM结合，增强空间语义和长期环境记忆建模。
result: 在视觉语言导航基准上提升了指令跟随和长程导航性能，尤其在动态环境中表现出更好的鲁棒性。
conclusion: 动态分层3D令牌能够有效增强VLM在VLN任务中的空间理解与长期记忆能力，是推进具身导航的重要方向。
---

## Abstract
Vision-and-Language Navigation (VLN) is a core task where embodied agents leverage their spatial mobility to navigate in 3D environments toward designated destinations based on natural language instructions. Recently, video-language large models (Video-VLMs) with strong generalization capabilities and rich commonsense knowledge have shown remarkable performance when applied to VLN tasks. However, these models still encounter the following challenges when applied to real-world 3D navigation: 1) Insufficient understanding of 3D geometry and spatial semantics; 2) Limited capacity for large-scale exploration and long-term environmental memory; 3) Poor adaptability to dynamic and changing environments.To address these limitations, we propose Dynam3D, a dynamic layered 3D representation model that leverages language-aligned, generalizable, and hierarchical 3D representations as visual input to train 3D-VLM in navigation action prediction. Given posed RGB-D images, our Dynam3D projects 2D CLIP features into 3D space and constructs multi-level 3D patch-instance-zone representations for 3D geometric and semantic understanding with a dynamic and layer-wise update strategy.  Our Dynam3D is capable of online encoding and localization of 3D instances, and dynamically updates them in changing environments to provide large-scale exploration and long-term memory capabilities for navigation. By leveraging large-scale 3D-language pretraining and task-specific adaptation, our Dynam3D sets new state-of-the-art performance on VLN benchmarks including R2R-CE, REVERIE-CE and NavRAG-CE under monocular settings. Furthermore, experiments for pre-exploration, lifelong memory, and real-world robot validate the effectiveness of practical deployment.

---

## 论文详细总结（自动生成）

# 论文总结：Dynam3D: Dynamic Layered 3D Tokens Empower VLM for Vision-and-Language Navigation

## 1. 核心问题与整体含义

- **研究背景**：视觉语言导航（VLN）要求具身智能体根据自然语言指令在真实3D环境中移动并到达目标位置。近年来的视频-语言大模型（Video-VLMs）凭借强大的泛化能力和常识知识，在VLN上展现出较好性能。
- **核心问题**：现有Video-VLM直接应用于真实3D导航时存在三大局限：
  - 对3D几何与空间语义理解不足；
  - 大规模探索和长期环境记忆能力有限；
  - 对动态环境变化适应性差。
- **整体含义**：为了解决上述问题，论文提出Dynam3D，通过构建动态分层的3D令牌表示，将3D几何、空间语义与长期记忆显式地融入VLM，从而提升VLN智能体在复杂真实环境中的决策能力。

## 2. 方法论

- **核心思想**：使用语言对齐、可泛化、层级化的3D表示作为视觉输入，驱动 3D-VLM 进行导航动作预测。
- **关键技术细节**：
  - 输入为带位姿的RGB-D图像；
  - 将2D CLIP特征投影到3D空间；
  - 构建多级3D表示：**patch（块）— instance（实例）— zone（区域）**，分别对应底层几何细节、中层物体实例、高层场景区域语义；
  - 采用**动态分层更新策略**：支持在线编码与3D实例定位，并在环境变化时动态更新3D表示。
- **算法流程（文字描述）**：
  1. 获取RGB-D帧及其位姿；
  2. 提取2D CLIP特征并反投影至3D空间；
  3. 在3D空间中聚合生成patch级特征，进一步聚类或分割为instance级，再归纳为zone级；
  4. 按层级动态更新内存中的3D令牌，保持对新增或变化环境的及时响应；
  5. 将更新后的3D令牌输入VLM，输出导航动作。
- 公式：论文未在摘要中给出具体公式，但整体可理解为一种层级化3D特征构建与动态更新的表示学习方法。

## 3. 实验设计

- **数据集与Benchmark**：
  - **R2R-CE**：经典Room-to-Room连续环境导航；
  - **REVERIE-CE**：远程视觉定位连续导航；
  - **NavRAG-CE**：结合检索与生成的导航任务。
  - 所有实验均采用**单目（monocular）设置**，即仅使用单目RGB-D输入。
- **对比方法**：摘要未列出具体对比方法，但强调“设置新的最先进性能”（new state-of-the-art），因此对比对象应为已有的VLN/VLM基线。
- **额外评估**：
  - **预探索（pre-exploration）实验**：测试智能体在预先探索环境后的导航能力；
  - **终身记忆（lifelong memory）实验**：评估长期环境记忆中动态更新的效果；
  - **真实机器人实验**：验证实际部署可行性。

## 4. 资源与算力

- 论文摘要中**未明确提及**所使用的GPU型号、数量、训练时长、显存消耗等具体算力信息。
- 仅可推断该方法涉及大规模3D-语言预训练与任务适配，需要较重的计算资源，但缺乏量化数据。

## 5. 实验数量与充分性

- **实验组数**：从摘要可见至少包含：
  - 3个基准数据集（R2R-CE, REVERIE-CE, NavRAG-CE）的对比实验；
  - 预探索实验；
  - 终身记忆实验；
  - 真实机器人实验。
- **充分性评价**：
  - 优点：覆盖了多个VLN benchmark，验证了主要性能提升，同时考察了预探索、长期记忆和真实部署，较为全面。
  - 不足：摘要中未展示消融研究（如各层级表示贡献、动态更新策略有效性等）；未给出与具体基线的数值对比表格；单目设置虽有一定挑战性，但缺少双目/深度传感器对比，可能影响优势的公平性判断。

## 6. 主要结论与发现

- Dynam3D通过动态分层3D令牌表示，显著提升了VLM在VLN任务中的**空间理解、长期记忆和动态环境适应能力**。
- 在R2R-CE、REVERIE-CE、NavRAG-CE三个单目VLN基准上取得新的最优性能。
- 预探索和终身记忆实验表明该方法适合大规模探索和长期部署。
- 真实机器人实验验证了其在实际物理环境中的可行性。
- 作者认为动态分层3D令牌是推动具身导航的重要方向。

## 7. 优点

- **创新性**：提出“patch-instance-zone”三层级3D令牌结构，兼顾底层几何和高层语义，显著增强VLM的3D感知。
- **动态性**：支持在线更新和长期记忆，解决了传统静态3D地图无法应对环境变化的问题。
- **实用性强**：采用单目RGB-D输入，降低传感器门槛；预探索和真实机器人实验直接面向部署需求。
- **通用性**：基于语言对齐的CLIP特征，便于迁移和泛化。

## 8. 不足与局限

- **细节缺失**：摘要缺少方法论的具体公式、网络结构细节、令牌数量与更新策略参数，难以完全复现。
- **消融不足**：未在摘要中展示层级化设计的消融实验（如去掉zone级或instance级的影响），以及与动态更新策略的对比。
- **对比公平性**：未列举具体基线和数值，无法判断性能提升的幅度和统计显著性。
- **实验范围**：仅报告单目设置，未与双目或LiDAR等方法对比；真实机器人实验规模未描述。
- **算力信息缺失**：没有给出训练和推理的计算资源，不利于评估方法的实际成本。
- **潜在偏差**：3D特征投影和层级聚类可能受到深度噪声、位姿误差影响，摘要未讨论鲁棒性问题。

（完）
