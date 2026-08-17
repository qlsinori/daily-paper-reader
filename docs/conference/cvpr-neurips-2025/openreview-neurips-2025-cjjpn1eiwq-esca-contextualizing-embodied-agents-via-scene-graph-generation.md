---
title: "ESCA: Contextualizing Embodied Agents via Scene-Graph Generation"
title_zh: ESCA：通过场景图谱生成赋予具身智能体上下文感知能力
authors: "Jiani Huang, Amish Sethi, Matthew Kuo, Mayank Keoliya, Neelay Velingker, JungHo Jung, Ser-Nam Lim, Ziyang Li, Mayur Naik"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=cjjPn1EIwq"
tags: ["query:semantic-map"]
score: 6.0
evidence: 面向具身智能体的场景图谱生成，桥接视觉特征与高层语义，可用于导航语义地图
tldr: 多模态大模型在作为通用具身智能体时，难以捕捉低层视觉特征与高层文本语义之间的细粒度关联。本文提出ESCA框架，通过空间-时间场景图谱对感知进行上下文关联，并训练开放域场景图谱生成模型SGCLIP，借助神经符号流水线自动对齐视频字幕与场景图谱。该方法显著改善了对环境的语义感知与定位能力，可为语义地图和导航任务提供基础支撑。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有MLLM在具身感知中缺乏低层视觉与高层语义的细粒度关联，导致定位与感知不够准确。
method: 提出ESCA框架和SGCLIP模型，用空间-时间场景图谱增强具身智能体的感知上下文。
result: 在开放域视频上训练场景图谱生成，提升了具身智能体的语义grounding和感知能力。
conclusion: 场景图谱生成是连接视觉与语义、支撑具身导航等任务的重要技术。
---

## Abstract
Multi-modal large language models (MLLMs) are making rapid progress toward general-purpose embodied agents. However, existing MLLMs do not reliably capture fine-grained links between low-level visual features and high-level textual semantics, leading to weak grounding and inaccurate perception. To overcome this challenge, we propose ESCA, a framework that contextualizes embodied agents by grounding their perception in spatial-temporal scene graphs. At its core is SGCLIP, a novel, open-domain, promptable foundation model for generating scene graphs that is based on CLIP.  SGCLIP is trained on 87K+ open-domain videos using a neurosymbolic pipeline that aligns automatically generated captions with scene graphs produced by the model itself, eliminating the need for human-labeled annotations. We demonstrate that SGCLIP excels in both prompt-based inference and task-specific fine-tuning, achieving state-of-the-art results on scene graph generation and action localization benchmarks. ESCA with SGCLIP improves perception for embodied agents based on both open-source and commercial MLLMs, achieving state of-the-art performance across two embodied environments. Notably, ESCA significantly reduces agent perception errors and enables open-source models to surpass proprietary baselines. We release the source code for SGCLIP model training at https://github.com/video-fm/LASER and for the embodied agent at https://github.com/video-fm/ESCA.

---

## 论文详细总结（自动生成）

# 论文总结：ESCA — 通过场景图谱生成赋予具身智能体上下文感知能力

## 1. 核心问题与整体含义

- **背景**：多模态大语言模型（MLLM）正快速发展为通用具身智能体，但其感知能力仍受限于对底层视觉特征与高层文本语义之间细粒度关联的建模。
- **核心问题**：现有 MLLM 在具身环境中容易出现弱 grounding（视觉定位与语义绑定不准确）和感知误差，难以支撑精确的导航、操作等任务。
- **研究动机**：作者提出利用**空间-时间场景图谱**（spatial-temporal scene graphs）作为上下文表示，将感知过程“锚定”在结构化语义关系上，从而弥补视觉与语义之间的鸿沟。
- **整体含义**：场景图谱生成可作为连接视觉与语义的桥梁，为具身智能体提供更可靠的环境理解能力，也是构建语义地图和导航系统的重要基础技术。

## 2. 方法论

- **核心思想**：通过场景图谱对具身智能体的感知进行“上下文化”（contextualize），即把视觉观察组织为包含实体、属性及空间-时间关系的结构化表示，再供 MLLM 使用。
- **框架**：提出 **ESCA**（Embodied Scene Contextualization Agent）框架，将感知结果显式地整理为场景图谱，增强基于开源或商业 MLLM 的具身智能体。
- **核心模型**：提出 **SGCLIP**
  - 基于 CLIP 的开放域、可提示（promptable）场景图生成基础模型。
  - 支持两种使用方式：直接基于提示词推理，或针对具体任务进行微调。
- **训练数据与流程**：
  - 使用 **87K+ 开放域视频**进行训练。
  - 采用**神经符号流水线**（neurosymbolic pipeline）：自动生成视频字幕，并与模型自身产生的场景图对齐，构造训练信号，**无需人工标注**。
- **算法流程**（基于摘要推断，论文未给出具体公式）：
  1. 输入视频/图像序列，提取低层视觉特征；
  2. 由 SGCLIP 生成场景图（实体节点、关系边、属性标注），同时由字幕模型生成自然语言描述；
  3. 通过神经符号对齐机制将字幕中的语义元素与场景图中的节点/关系对应，形成自监督训练目标；
  4. 训练完成后，SGCLIP 可直接用于推理或在下游任务上微调，并将生成的场景图注入具身智能体的感知流程。

## 3. 实验设计

- **场景图谱生成基准**：对比已有 SOTA 场景图生成方法，评估 SGCLIP 在开放域图像/视频上的生成质量。
- **动作定位基准**：在动作定位任务上验证 SGCLIP 的可提示推理与微调能力。
- **具身环境**：在两个不同的具身仿真/现实环境中评估 ESCA 框架，覆盖基于**开源 MLLM**（如 LLaVA 类）和**商业 MLLM**（如 GPT-4V 类）的智能体。
- **对比方法**：
  - 场景图生成/动作定位领域的现有 SOTA 方法；
  - 未使用 ESCA 的原始开源和商业 MLLM 智能体。
- **评估指标**：包括感知错误率、任务成功率/定位精度等（摘要未给出具体数值，只给出 “state-of-the-art performance” 和 “significantly reduces agent perception errors”）。

## 4. 资源与算力

- 论文提供的材料中**未明确说明**使用的 GPU 型号、数量、训练时长、显存占用等算力信息。
- 仅能确认训练数据规模为 **87K+ 开放域视频**，且官方已开源训练代码，便于后续复现。
- 如需准确资源信息，需查阅论文正文或官方 GitHub 仓库。

## 5. 实验数量与充分性

- **实验组数**（根据摘要可确认的）：
  1. SGCLIP 在场景图生成基准上的评测；
  2. SGCLIP 在动作定位基准上的评测；
  3. ESCA 在具身环境 A 上的效果（开源/商业 MLLM 对比）；
  4. ESCA 在具身环境 B 上的效果；
  5. 与 SOTA 方法以及原始 MLLM 基线的对比；
  6. 感知错误率降低的量化分析。
- **充分性评价**：
  - 覆盖了模型能力（场景图生成、动作定位）和任务效果（具身感知）两层验证，整体设计较为全面。
  - 但摘要中**未明确提及消融实验**（如去掉场景图谱、替换为其他表示等），也未给出误差棒、统计显著性检验等细节，严格来说实验证据的丰富程度还需看论文全文。
  - 由于“两个具身环境”的具体任务类型未知，难以判断泛化性是否充分。

## 6. 主要结论与发现

- SGCLIP 在场景图生成和动作定位基准上均达到 **SOTA**，证明其作为开放域、可提示的场景图模型的有效性。
- 将 SGCLIP 与 ESCA 结合后，基于开源 MLLM 的具身智能体**性能提升显著，并超越了专有（商业）MLLM 基线**。
- 场景图谱生成能有效降低具身智能体的感知错误，是连接低层视觉信息与高层语义的实用技术。
- 作者公开了 SGCLIP 训练代码与具身智能体代码，促进领域复现与后续研究。

## 7. 优点

- **方法创新性强**：首次（或少有地）将开放域场景图谱生成作为具身智能体的上下文模块，绕开了传统语义地图的繁琐手工标注。
- **自动化训练范式**：利用神经符号流水线实现字幕-场景图自对齐，消除了人工标注，可低成本扩展到大规模视频数据。
- **技术可迁移性高**：SGCLIP 基于 CLIP，兼容主流 MLLM，既可作为独立提示模型，也能进行任务微调。
- **动机明确、闭环验证**：从“感知不准确”这一实际痛点出发，既做通用模型又做应用评测，实验链完整。
- **开源贡献**：公开训练/部署代码，方便社区复现和二次开发。

## 8. 不足与局限

- **信息完整性不足**：当前提供的材料仅为摘要，缺乏方法细节、公式、训练超参和消融实验，难以全面评估技术细节和结论稳健性。
- **算力资源未披露**：没有给出 GPU 类型/数量/训练时长，影响可复现性和成本估算。
- **实验覆盖有限**：仅提到“两个具身环境”，未说明任务类型（导航、操作、问答等）、环境复杂度、场景多样性，泛化性存疑。
- **自动标注噪声风险**：使用自动生成字幕与模型自身场景图对齐，虽然免人工标注，但自动标注的错误可能被放大，需要额外质量控制。
- **潜在偏差**：训练数据来源于开放域视频，可能偏向常见物体和常见关系，长尾实体和复杂社会学动作（如交互性很强的行为）效果可能退化。
- **应用限制**：场景图谱结构本身可能无法表达全部视觉细节（如纹理、光影、几何精确度），在需要精确空间定位或高动态场景中可能受限。
- **未讨论负面案例**：摘要未展示失败模式或边界情况，如遮挡、相机抖动、多智能体交互等场景下的表现。

（完）
