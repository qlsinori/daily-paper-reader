---
title: Do Visual Imaginations Improve Vision-and-Language Navigation Agents?
title_zh: 视觉想象能否改进视觉语言导航智能体？
authors: "Perincherry, Akhil, Krantz, Jacob, Lee, Stefan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Perincherry_Do_Visual_Imaginations_Improve_Vision-and-Language_Navigation_Agents_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 通过文生图扩散模型生成子目标视觉想象，为VLN智能体提供导航线索
tldr: 视觉语言导航智能体需要依据自然语言指令探索未知环境，本文研究指令隐含子目标的视觉想象能否作为导航线索。利用文本到图像扩散模型，根据分割指令中的地标参考合成视觉想象，并作为额外模态提供给VLN智能体，同时增加辅助损失促使模型将想象与对应指代表达关联。实验结果显示，该方法使成功率（SR）提升约1个点，sPL值也有约0.5点增益。这说明视觉想象作为地标线索对VLN有正向作用，但提升幅度有限。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 256}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1815, \"height\": 324}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 309}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1813, \"height\": 948}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 712}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 195}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 840, \"height\": 282}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 841, \"height\": 238}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 859, \"height\": 238}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 836, \"height\": 238}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 876, \"height\": 299}]"
motivation: 探索指令中隐含子目标的视觉想象能否为VLN智能体提供有效导航线索并提升性能。
method: 用扩散模型从指令分割出的地标生成视觉想象，作为额外模态输入VLN，并设计辅助损失进行指代关联学习。
result: 在VLN基准上成功率提升约1个点，sPL提升约0.5个点，验证了视觉想象的辅助作用。
conclusion: 视觉想象可帮助VLN智能体利用指令中的地标线索，但收益有限，值得进一步优化生成与融合方式。
---

## Abstract
Vision-and-Language Navigation (VLN) agents are tasked with navigating an unseen environment using natural language instructions. In this work, we study if visual representations of sub-goals implied by the instructions can serve as navigational cues and lead to increased navigation performance. To synthesize these visual representations or "imaginations", we leverage a text-to-image diffusion model on landmark references contained in segmented instructions. These imaginations are provided to VLN agents as an added modality to act as landmark cues and an auxiliary loss is added to explicitly encourage relating these with their corresponding referring expressions. Our findings reveal an increase in success rate (SR) of ~1 point and up to ~0.5 points in success scaled by inverse path length (SPL) across agents. These results suggest that the proposed approach reinforces visual understanding compared to relying on language instructions alone.

---

## 论文详细总结（自动生成）

# 论文总结：视觉想象能否改进视觉语言导航智能体？

## 1. 核心问题与整体含义

- **研究背景**：视觉语言导航（Vision-and-Language Navigation, VLN）要求智能体依据自然语言指令在未知环境中完成导航任务。传统方法依赖跨模态对齐机制隐式地将指令中的名词短语（如"pool table"、"bedroom"）与其视觉指代物关联，但这种隐式关联在分布外或罕见地标上常常失效。
- **核心问题**：指令中隐含子目标的**视觉想象**（即在导航前用文生图模型合成的、与指令地标语义对应的图像）能否作为额外导航线索，提升VLN智能体的导航性能？
- **整体含义**：本研究验证了一种全新的思路——将文本到图像（text-to-image）扩散模型用作"视觉想象"的生成器，将语言指令中的地标描述转化为具体图像，作为"语言→图像→环境观察"之间的中介抓手，弥补语言锚定（language grounding）的不足。

## 2. 方法论：核心思想与关键技术

- **核心思想**：利用扩散模型将指令中与视觉地标相关的子指令转化为图像（称为"imaginations"），并作为额外模态输入VLN智能体，辅助其将指令中的名词短语与环境观察进行匹配。
- **视觉想象生成流程**：
  1. 使用 FG-R2R 将指令切分为平均 3.66 个子指令段；
  2. 用 Spacy 过滤掉不含名词短语的子指令，再用人工黑名单过滤无意义名词（如方向词"left"、代词"it"等）；
  3. 将筛选后的子指令输入 SDXL 扩散模型，配以正向提示词（如"indoor"、"real estate"）和负向提示词（如"humans"、"collage"）生成 1024x1024 的图像。
- **模型集成方法（模型无关）**：
  - 对每个想象图用预训练 ViT-B/16 编码，加上类型嵌入后经三层 MLP 得到想象嵌入；
  - 将想象嵌入与指令文本嵌入**拼接**后送入现有VLN智能体的跨模态编码器，参与策略预测。
- **辅助对齐损失**：引入余弦相似度损失（公式2），将想象嵌入与对应子指令中名词短语词元的平均嵌入对齐，显式强化视觉想象与语言指代的关联。
- **三阶段微调策略**：先冻结基座模型只训练新引入的想象编码器；再以较低学习率联合训练全模块；最后以统一学习率训练所有参数，以缓解灾难性遗忘。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**：
  - **R2R（Room-to-Room）**：基于 Matterport3D，90个室内环境，7189条轨迹，每条约3条指令，分为train/val-seen/val-unseen/test四个划分；
  - **REVERIE**：同样是Matterport3D环境，但指令为粗粒度高层目标（如"Adjust the picture by the lamp in the hall"）；
  - 作者还构建了 **R2R-Imagine 数据集**，共含41,558张训练想象图、3,055张val-seen、6,857张val-unseen、12,412张test想象图。
- **基准模型**：选取了两种代表性VLN架构——**HAMT**（基于层次Transformer）和 **DUET**（基于双尺度拓扑图Transformer），均在预训练检查点基础上加入想象模块进行微调。
- **评估指标**：成功率（SR）、按路径长度加权的成功率（SPL）、导航误差（NE）、轨迹长度（TL），REVERIE还使用远程接地成功率（RGS）及其路径惩罚版（RGSPL）。
- **对比方法**：主要包括基线模型（HAMT、DUET）、现有VLN方法（PREVALENT、RecBERT、ADAPT、BEVBert等）及数据增强方法（MARVAL、ScaleVLN等）。

## 4. 资源与算力

- 论文明确提到：使用**单张H100 GPU**生成一张想象图平均耗时约 **3.2秒**；微调每个VLN智能体使用 **Tesla V100 GPU、批量大小8、训练10万次迭代，约需1.5天**。
- 但论文**未明确说明**使用的GPU总数、并行配置以及生成全部R2R-Imagine数据集（约41k+张图）所消耗的总体计算资源。

## 5. 实验数量与充分性

- **实验组数**：较为丰富，包括——
  - R2R主实验（2种基座模型 × 4个划分）；
  - REVERIE实验（1组）；
  - 想象作用测试（正确/错误/空想象对比）；
  - 序列想象 vs 仅目标想象对比；
  - ViT固定 vs 微调对比；
  - 损失函数消融（无损失、InfoNCE、余弦损失）；
  - 生成质量验证（LangSAM开放词汇目标检测）。
- **充分性评价**：实验覆盖了方法有效性验证、设计选择消融、生成质量验证及定性分析，整体较充分。部分消融仅基于HAMT（如错误想象、目标想象）或未同时覆盖两模型（如损失消融），略显不够系统，但核心结论有多组数据支撑，客观性和公平性总体合格。

## 6. 主要结论与发现

- **视觉想象有效但提升有限**：在R2R val-unseen上，HAMT-Imagine SR提升约1.0点、SPL提升约0.5点；DUET-Imagine SR提升约0.6点；在R2R test上DUET-Imagine SR提升达2点。REVERIE上DUET-Imagine SR提升1.3点、RGS提升0.82点。
- **想象需与指令对齐**：使用错误（随机）想象反而低于基线；空想象性能介于基线和正确想象之间，说明训练过程具有正则化效应。
- **序列想象优于仅目标想象**：提供全部子指令的想象比只提供最终目标想象效果更好（SR高出约0.5点）。
- **通用ViT编码器足够**：无需针对VLN任务微调ViT，使用开箱即用的预训练ViT即可取得相当性能。
- **对齐损失有益但形式影响不大**：余弦损失带来明显提升（约0.5 SR），但与对比损失（InfoNCE）效果差异不显著。
- **生成质量高**：LangSAM检测显示98.78%的子指令在想象图中至少检出一个名词短语，94.99%全部检出，说明想象图能忠实反映指令地标。

## 7. 优点

- **方法简单、模型无关**：无需改动VLN智能体内部架构，只需将想象嵌入拼接到文本嵌入上，易于集成到不同模型。
- **想象力生成覆盖开放分布**：相比ADAPT只能检索训练集中的图像，本文的扩散模型可生成训练中未见过的新奇地标（如"butterfly sculptures"），更具泛化性。
- **多模型多数据集验证**：在两种架构和两种任务设定（细粒度R2R、粗粒度REVERIE）上均验证了有效性，结论有一定泛化力。
- **定性分析有启发性**：注意力可视化展示了想象在语言与视觉观察间的"枢轴"作用，能帮助区分相近概念（如unicycle与bicycle）。
- **消融较系统**：从想象正确性、序列性、编码器选择、损失设计等多角度刻画了设计空间。

## 8. 不足与局限

- **性能提升幅度有限**：SR仅提升约1点，效果属于增量改进而非突破性提升，且随模型不同波动（DUET-SPL提升仅约0.07）。
- **计算开销增加**：生成想象图和额外编码增加了总体计算成本；虽然生成可离线进行，但需额外的存储和编码资源，对实时或端侧部署不太友好。
- **想象与实际环境存在域差距**：生成的想象图并不基于真实环境，对环境中独特命名、个性化外观的对象无法准确想象。
- **测试集提升不确定**：DUET在test上SR提升有2点，但SPL几乎持平（59→60），HAMT在test上提升微弱，说明想象带来的增益在未见环境中的稳定性有待验证。
- **消融覆盖不平衡**：部分关键消融（如错误想象、目标想象）仅在HAMT上验证，未在DUET上复现；REVERIE实验仅测试了一组设置。
- **训练成本未详尽披露**：未说明全数据集想象生成的总GPU耗时及总能耗，复现成本估算困难。
- **认知科学类比未经实证**：文中引用心理意象相关认知科学文献，但并未设计实验验证两者之间的内在关联，类比成分较多。

（完）
