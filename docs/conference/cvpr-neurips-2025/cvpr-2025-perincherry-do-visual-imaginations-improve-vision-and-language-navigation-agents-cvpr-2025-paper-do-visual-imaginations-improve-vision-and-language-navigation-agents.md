---
title: Do Visual Imaginations Improve Vision-and-Language Navigation Agents?
title_zh: 视觉想象能否提升视觉语言导航智能体？
authors: "Perincherry, Akhil, Krantz, Jacob, Lee, Stefan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Perincherry_Do_Visual_Imaginations_Improve_Vision-and-Language_Navigation_Agents_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 直接研究视觉语言导航，利用自然语言指令生成地标视觉想象以提升导航成功率
tldr: 针对视觉语言导航中智能体难以将自然语言指令中的地标与视觉观测对应的问题，利用文本到图像扩散模型为分段指令中的地标生成视觉想象，并将其作为额外模态输入VLN智能体，同时添加辅助损失鼓励与指代表达对齐。实验显示该方法在未见环境上提升成功率约1个点、s路径指标约0.5个点，验证了视觉想象可作为有效导航线索。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 256}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1815, \"height\": 324}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 309}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1813, \"height\": 948}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 712}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 195}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 840, \"height\": 282}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 841, \"height\": 238}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 859, \"height\": 238}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 836, \"height\": 238}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 876, \"height\": 299}]"
motivation: VLN智能体在未见环境中难以利用指令隐含的子目标视觉线索进行导航。
method: 用扩散模型生成地标视觉想象作为额外模态，并设计辅助损失对齐指代表达。
result: 在VLN基准上成功率和s指标均获得提升，说明视觉想象有助于导航。
conclusion: 将指令驱动的视觉想象注入VLN智能体可增强地标识别与导航决策。
---

## Abstract
Vision-and-Language Navigation (VLN) agents are tasked with navigating an unseen environment using natural language instructions. In this work, we study if visual representations of sub-goals implied by the instructions can serve as navigational cues and lead to increased navigation performance. To synthesize these visual representations or "imaginations", we leverage a text-to-image diffusion model on landmark references contained in segmented instructions. These imaginations are provided to VLN agents as an added modality to act as landmark cues and an auxiliary loss is added to explicitly encourage relating these with their corresponding referring expressions. Our findings reveal an increase in success rate (SR) of ~1 point and up to ~0.5 points in success scaled by inverse path length (SPL) across agents. These results suggest that the proposed approach reinforces visual understanding compared to relying on language instructions alone.

---

## 论文详细总结（自动生成）

好的，我已经仔细阅读了您提供的论文内容。以下是基于该论文的详细中文总结，并按照您要求的要点展开。

---

## 论文详细中文总结

### 1. 论文的核心问题与整体含义

- **研究背景**：视觉语言导航（VLN）要求智能体依据自然语言指令在未知环境中进行导航。标准方法往往依赖隐式的跨模态对齐机制，将指令中的名词短语（如“台球桌”“厨房”）与视觉观测相对应。然而，这种隐含的语言-视觉关联在训练数据有限的情况下，尤其是面临训练集中未出现过的地标时，往往效果不佳，是现有VLN模型的薄弱环节。
- **核心研究问题**：本文探讨了一个关键问题——**指令中隐含的视觉地标表征（即“视觉想象”）能否作为额外的导航线索，显著提升VLN智能体的导航性能？**
- **整体含义与动机**：论文借鉴认知科学中的“双重编码理论”和“心理意象”研究，提出利用文本到图像扩散模型为指令中的视觉地标预先生成图像，并作为附加模态输入给智能体。其核心动机在于：将隐含的“语言-视觉”关联问题，转化为更易处理的“图像-图像”匹配问题，从而强化智能体对指令的视觉理解与地标识别能力，最终提升导航表现。

### 2. 论文提出的方法论

- **核心思想**：提出一种**模型无关（Model-agnostic）** 的流程，将指令中描述的子目标地标转换为合成图像（即“想象”），并与现有VLN智能体集成。
- **关键技术细节与流程**：
    1.  **视觉想象生成管线**：
        - **指令分割**：使用FG-R2R工具将导航指令分割为多个子指令。
        - **子指令过滤**：采用基于Spacy的句法分析，过滤掉不含名词短语或名词无视觉指向（如“左转”、“它”）的子指令，从而仅针对有效的、可生成地标图像的子指令进行下一步。
        - **图像生成**：使用现成的SDXL文本到图像扩散模型为过滤后的子指令生成视觉想象（分辨率1024x1024）。通过精心设计的正向提示词（如“室内”、“房地产”）和负向提示词（如“人类”、“拼贴画”）来引导生成更接近Matterport3D环境的室内图像。
    2.  **模型集成的通用方法**：
        - **想象编码器**：每个生成的想象图像通过一个预训练的视觉Transformer（ViT）编码，再经由3层MLP网络投影为想象嵌入向量 \( h_i = MLP(ViT(Z_i) + t_{Im}) \)。
        - **模态融合**：将想象嵌入向量直接与指令的文本嵌入向量拼接，一同送入VLN智能体的跨模态编码器（如HAMT或DUET的编码器）进行行动预测。
        - **辅助对齐损失**：为了鼓励视觉想象与其对应的指代表达（名词短语）对齐，设计了一个**余弦相似度损失** \( L_{cos} \)。
    3.  **训练策略（三阶段微调）**：
        - **阶段一**：仅训练新引入的想象编码器（MLP），冻结其余所有参数。
        - **阶段二**：联合微调所有模块，但基础模型使用较低的学习率，以避免灾难性遗忘。
        - **阶段三**：所有参数以统一学习率进行最终训练。

### 3. 实验设计

- **主要数据集与Benchmark**：
    - **Room-to-Room (R2R)**：VLN的经典基准，指令细致，包含数百个室内场景。作者在此基础上创建了**R2R-Imagine**数据集，为训练/验证/测试集中的每一条指令生成了对应的视觉想象。
    - **REVERIE**：指令更宏观，主要描述高层目标（如目标物体及其位置），侧重于远端视觉指代定位。
- **对比方法**：论文在两种代表性强、架构不同的VLN基础模型上进行了集成验证：
    - **HAMT**（层级Transformer结构）
    - **DUET**（双尺度图Transformer结构）
- **评估指标**：采用VLN领域标准指标，包括**成功率（SR）**、**按路径长度加权的成功率（SPL）**、**导航误差（NE）** 和**轨迹长度（TL）**。对于REVERIE，额外报告了**远端接地成功率（RGS）** 指标。

### 4. 资源与算力

- 论文在第4.1节“实现细节”中明确提及：
    - **训练硬件**：单个**Tesla V100 GPU**。
    - **训练时长**：每个智能体（模型）的微调过程约需 **1.5天**。
    - **批量大小**：设为8。
    - 此外，在介绍R2R-Imagine数据集时，提到生成单个1024x1024分辨率的想象图像在单个H100 GPU上平均耗时**3.2秒**。

### 5. 实验数量与充分性

- **实验组数**：论文进行了多组核心实验，包括：
    - **主实验**：在R2R（验证可见、验证未见和测试集）和REVERIE（验证未见）上的性能对比。
    - **消融研究**：针对多个关键设计选择进行了详细分析，包括想象模块的作用（正确/错误/空想象对比）、顺序想象与目标想象的差异、不同视觉编码器（微调ViT vs 离线ViT）的对比、不同辅助损失函数（余弦相似度 vs InfoNCE）的对比。
    - **定性分析**：提供了注意力可视化和想象生成质量（基于开放词汇检测器）的分析。
- **充分性与客观性分析**：
    - **充分性**：实验设计较为全面，既验证了方法的有效性，又通过消融实验探索了设计空间。在多个数据集和多个模型上的验证增强了结论的可靠性。
    - **公平性**：对比实验基于相同的预训练权重和训练设置，且将方法定位于不使用额外场景数据的类别中，与数据增强类方法（如ScaleVLN）进行了区分，保证了对比的公平性。对“错误想象”的测试也有效排除了纯粹的过拟合或正则化效应，增强了结论的可信度。

### 6. 论文的主要结论与发现

- **性能提升**：为VLN智能体提供指令地标的视觉想象，能稳定地提升导航性能。在R2R验证未见集上，HAMT和DUET的成功率（SR）分别提升了约**1.0**和**0.6**个百分点；在R2R测试集上DUET的成功率提升了**2**个百分点。在REVERIE验证未见集上，DUET的成功率（SR）提升了**1.3**个百分点。
- **想象的对齐至关重要**：只有当提供**正确对齐**的想象时，智能体性能才能提升；随机或错误的想象会导致性能下降。
- **顺序想象优于单一目标想象**：为路径上的多个子目标生成一系列想象（顺序想象），比仅生成最终目标的想象更能有效提升导航性能。
- **训练和推理都有益处**：即使在测试时移除想象输入，经过想象训练的智能体仍能保持性能提升，表明该方法在训练过程中带来了正则化效果。
- **通用编码器可用**：使用现成的通用ViT即可有效编码想象，无需使用在下游任务上微调的ViT。
- **辅助损失有效**：添加对齐辅助损失能进一步提升性能，但使用更复杂的对比损失（InfoNCE）并未带来显著优势。

### 7. 优点

- **创新性与启发性**：首次系统性地探讨并验证了文本到图像生成的“视觉想象”在VLN任务中的价值，为跨模态导航提供了新思路，并具备认知科学的理论基础。
- **模型无关性与通用性**：提出了一套通用的集成框架，可轻松应用于现有VLN智能体，在多个模型（HAMT, DUET）和多个数据集（R2R, REVERIE）上均验证了有效性，展示了良好的泛化能力。
- **深入全面的实验**：通过设计周密的消融实验，不仅证明了方法的有效性，还深入分析了各组件（如想象对齐性、生成策略、编码器选择）的贡献，提供了清晰的设计洞察。
- **想象力生成的质量保障**：通过指令分割与过滤管线，确保生成的想象与指令中的有效地标精准对应，并通过开放词汇检测实验证明了高保真度。

### 8. 不足与局限

- **计算开销**：在推理（生成）阶段需要承担文本到图像模型的额外计算成本，论文也承认这对于计算资源受限的机器人端侧部署是一个限制。
- **想象与现实环境的偏差**：合成的想象图像并非来源于真实导航环境，它们与真实世界观测之间存在先天的领域鸿沟，可能不足以应对极端或高度特化（如个性化命名的物体）的场景。
- **性能提升幅度有限**：尽管提升是稳定且一致的，但成功率（SR）的提升幅度（约1个点）相对较小，其实际的、端到端的导航体验提升效果可能有限。
- **未探讨与更先进方法结合的效果**：论文验证的基础模型（HAMT, DUET）并非VLN领域最新的SOTA模型。将其引入BEVBert、ScaleVLN等采用更先进预训练或数据增强策略的模型中，能否带来同等或更大的增益，结论尚不明确。
- **缺乏长尾场景的专门分析**：论文提出了对“蝴蝶雕塑”等新奇物体想象的优势假设，但在实验中未专门针对此类长尾或分布外（OOD）地标进行深入分析和量化评估。

---

（完）
