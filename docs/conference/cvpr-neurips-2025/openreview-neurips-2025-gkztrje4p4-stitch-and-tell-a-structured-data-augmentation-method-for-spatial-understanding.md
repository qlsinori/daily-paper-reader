---
title: "Stitch and Tell: A Structured Data Augmentation Method for Spatial Understanding"
title_zh: 缝合与讲述：一种用于空间理解的结构化数据增强方法
authors: "Hang Yin, Xiaomin He, Peiwen Yuan, Yiwei Li, Jiayi Shi, Wenxiao Fan, Shaoxiong Feng, Kan Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=GkztRjE4P4"
tags: ["query:embodied-nav"]
score: 6.0
evidence: SiTe增强视觉语言模型的空间理解，是VLN理解自然语言指令的基础能力
tldr: 针对视觉语言模型中常见的空间幻觉问题，本文提出缝合与讲述（SiTe）方法：将图像沿空间轴拼接并自动生成空间感知的图文对，无需人工标注即可注入结构化空间监督。该方法能有效增强模型对物体相对位置的理解，缓解空间描述错误。作为即插即用的数据增强方案，SiTe可广泛应用于各类视觉语言任务，为需要空间推理的具身智能与导航系统提供支撑。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 视觉语言模型常产生空间幻觉，原因是图文数据在空间信息上不对称，缺乏结构化空间监督。
method: 提出SiTe，将图像沿空间轴拼接并生成空间感知描述或问答对，构建注入结构化空间监督的多模态训练数据。
result: 实验表明SiTe可显著提升视觉语言模型的空间理解能力，减少空间幻觉，且无需额外标注或复杂模型。
conclusion: 提供了一种简单有效的即插即用数据增强方法，能够增强模型的空间感知，为空间推理类下游任务奠定基础。
---

## Abstract
Existing vision-language models often suffer from spatial hallucinations, i.e., generating incorrect descriptions about the relative positions of objects in an image. We argue that this problem mainly stems from the asymmetric properties between images and text. To enrich the spatial understanding ability of vision-language models, we propose a simple, annotation-free, plug-and-play method named Stitch and Tell (abbreviated as SiTe), which injects structured spatial supervision into multimodal data. It constructs stitched image–text pairs by stitching images along a spatial axis and generating spatially-aware captions or question answer pairs based on the layout of stitched image, without relying on costly advanced models or human involvement. We evaluate SiTe across three architectures including LLaVA-v1.5-7B, LLaVA-Qwen2-1.5B and HALVA-7B, two training datasets, and thirteen benchmarks. Experiments show that SiTe improves spatial understanding tasks such as $\text{MME}_{\text{Position}}$ (+5.50\%) and Spatial-MM (+4.19\%), while maintaining or improving performance on general vision-language benchmarks. Our findings suggest that explicitly injecting spatially-aware structure into training data offers an effective way to mitigate spatial hallucinations and improve spatial understanding, while preserving general vision-language capabilities.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：视觉语言模型（Vision-Language Models, VLMs）在描述图像中物体的相对位置关系时经常产生**空间幻觉（spatial hallucinations）**，即生成与真实空间布局不符的错误描述。
- **问题根源**：作者认为，这一问题主要源于**图像与文本之间的不对称性**。图像本身包含丰富、精确的空间结构信息，但训练所用的文本描述往往只关注物体类别、属性或整体语义，缺乏对物体间相对位置关系的显式、结构化表达。这种不对称导致模型难以从常规图文数据中充分学习空间关系。
- **研究意义**：空间理解是视觉语言模型完成具身智能、导航等下游任务的基础能力。缓解空间幻觉、增强空间理解，对于提升模型在真实世界中的可靠性和实用性至关重要。

### 2. 论文提出的方法论

- **方法名称**：**Stitch and Tell（SiTe，缝合与讲述）**。
- **核心思想**：通过**图像拼接**将原始图像沿一条空间轴组合，形成新的、具有明确空间布局的图像；随后基于拼接后图像的布局，自动生成**空间感知的图文对**（如空间感知的标题或问答对）。这样无需人工标注、无需依赖昂贵的高级模型，即可向多模态训练数据中注入**结构化空间监督**。
- **关键技术细节**：
  - 将两幅或多幅图像沿水平或垂直方向拼接，从而在生成的图像中显式构造出左右、上下等相对位置关系；
  - 基于拼接图像的已知布局，自动生成描述或问答对，使文本中标注的空间关系与图像中的真实空间位置严格一致；
  - 该方法为**即插即用**式数据增强方案，可直接融入既有视觉语言模型的训练流程，不改变模型结构。
- **算法流程（文字说明）**：
  1. 选取原始图像并按照空间轴（如水平或垂直）进行拼接，得到缝合图像；
  2. 根据拼接顺序与图像内容，自动构造空间感知标题或问答对（例如："A 在 B 的左边"）；
  3. 将生成的图文对加入训练数据，与原始数据混合训练视觉语言模型；
  4. 模型在训练中接收到显式的空间监督信号，从而增强空间关系推理能力。

### 3. 实验设计

- **模型架构**：覆盖三种不同的视觉语言模型架构，包括：
  - LLaVA-v1.5-7B
  - LLaVA-Qwen2-1.5B
  - HALVA-7B
- **训练数据集**：使用了**两个训练数据集**（具体名称在摘要中未明确给出，但表明方法是在多个数据集上验证的）。
- **评测基准**：共在**十三个基准**上评估，其中空间理解相关任务包括：
  - **MME_Position**（位置理解任务）
  - **Spatial-MM**（空间理解评测）
  - 同时还包括**通用视觉语言基准**，以检验方法是否在提升空间能力的同时损害通用能力。
- **对比方法**：摘要中未详细列出具体基线方法名称，但从实验设计来看，主要对比的是**是否使用 SiTe 增强数据训练同一模型**的差异，即 SiTe 作为数据增强手段相对于原始训练设置的提升。

### 4. 资源与算力

- **论文摘要及现有信息中均未明确说明所使用的算力资源**，包括：
  - GPU 型号（如 A100、V100 等）；
  - GPU 数量；
  - 训练时长；
  - 显存占用等细节。
- 因此，无法从当前提供的文本中获知具体的计算资源需求。仅能推测：由于涉及 7B 和 1.5B 规模的模型微调，且使用了多个训练数据集和十三个基准评测，整个实验流程需要相当规模的计算资源。

### 5. 实验数量与充分性

- **实验规模**：
  - 覆盖 **3 种架构**（LLaVA-v1.5-7B、LLaVA-Qwen2-1.5B、HALVA-7B）；
  - 使用 **2 个训练数据集**；
  - 在 **13 个基准**上进行评估。
- **充分性分析**：
  - **优点**：多架构验证增强了结论的通用性；同时评测空间任务和通用任务，能够检验数据增强是否引入能力退化，设计较为全面。
  - **可能不足**：摘要中未明确提及针对 Stitch 方向（水平/垂直）、拼接图像数量、数据混合比例等因素的**详细消融实验**。因此，方法中各组件的具体贡献尚不完全清楚。在未有公开实验细节的前提下，实验的全面性仍有一定提升空间。
  - **公平性**：由于都是在相同模型上比较"是否使用 SiTe"的差异，属于合理的对照实验。但若未披露训练数据量是否一致、训练步数是否对齐等细节，则公平性的完整评估需要结合论文全文进一步确认。

### 6. 主要结论与发现

- SiTe 能够**显著提升视觉语言模型的空间理解能力**，减少空间幻觉。
- 具体提升幅度：
  - **MME_Position 提升 +5.50%**
  - **Spatial-MM 提升 +4.19%**
- 在提升空间理解的同时，**通用视觉语言基准上的性能得以维持或提升**，说明 SiTe 不会牺牲模型的通用能力。
- 作者由此得出结论：**在训练数据中显式注入空间感知结构**是一种缓解空间幻觉、增强空间理解的有效途径，并且该方法是简单、无标注依赖、即插即用的。

### 7. 优点

- **简单易用**：方法设计直观，不需要人工标注，也不需要依赖昂贵的先进模型（如 GPT-4V 等）生成数据。
- **即插即用**：可作为通用数据增强策略，轻松集成到各类视觉语言模型训练流程中。
- **成本低廉**：相比重新设计模型结构或引入复杂空间推理模块，仅通过数据层面的改造即可获得收益，性价比高。
- **实验覆盖面较广**：多模型、多数据集、多基准的验证方式，增强了结论的可靠性和泛化性。
- **具备通用性潜力**：由于不涉及模型结构改动，可推广到更多视觉语言任务，为具身智能、导航等对空间推理有强需求的下游应用提供支持。

### 8. 不足与局限

- **算力资源未披露**：论文未说明训练所用的 GPU 型号、数量和时间，不利于其他研究者复现成本评估。
- **消融实验细节不足**：从摘要中无法得知对拼接方向、拼接数量、数据比例等关键设计维度的消融分析，方法最优配置的论证有待全文补充。
- **无标注依赖的优势与局限并存**：虽然无需人工标注，但自动生成的空间描述可能仍存在语义覆盖不全面、文本多样性有限等问题，可能影响模型对复杂空间关系的泛化。
- **拼接式空间增强的天然局限**：拼接图像中物体的空间关系来自图像间的相对布局，而非原始场景内真实、自然的三维空间关系。这种人造的空间结构可能与真实图像中的空间分布存在偏差，对模型在真实场景中的空间理解提升效果需要进一步验证。
- **实验场景有限**：目前评测集中于已有基准（如 MME、Spatial-MM），未明确涉及真实机器人导航、操作等具身场景的端到端验证，实际应用效果仍需探索。

（完）
