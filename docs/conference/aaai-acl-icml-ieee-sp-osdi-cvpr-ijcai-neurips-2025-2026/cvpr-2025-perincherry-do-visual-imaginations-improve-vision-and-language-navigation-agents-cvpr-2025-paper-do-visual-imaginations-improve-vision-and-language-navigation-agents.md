---
title: Do Visual Imaginations Improve Vision-and-Language Navigation Agents?
title_zh: 视觉想象能提升视觉语言导航智能体吗？
authors: "Perincherry, Akhil, Krantz, Jacob, Lee, Stefan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Perincherry_Do_Visual_Imaginations_Improve_Vision-and-Language_Navigation_Agents_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 利用指令地标生成的视觉想象增强视觉语言导航
tldr: 视觉语言导航智能体需要依靠语言指令在未知环境中导航。本文探究由指令地标生成的视觉想象是否可作为导航线索提升性能。作者利用文生图扩散模型合成子目标的视觉表征，并将其作为额外输入模态，同时添加辅助损失以关联指称表达。实验显示，该方法在成功率上提升约1个百分点，SPL亦有小幅度提高，验证了视觉想象作为地标线索的辅助价值。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 256, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1815, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 852, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1813, \"height\": 948, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 712, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 195, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 840, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 841, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 859, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 836, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-perincherry-do-visual-imaginations-improve-vision-and-language-navigation-agents-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 876, \"height\": 299, \"label\": \"Table\"}]"
motivation: 语言指令隐含的子目标视觉表征可能为导航提供有效的地标线索。
method: 利用文本到图像扩散模型生成指令地标的视觉想象，并作为附加模态与辅助损失训练VLN智能体。
result: 成功率提升约1个百分点，SPL提升可达0.5个百分点以上。
conclusion: 视觉想象可作为辅助地标线索，温和但稳定地改进视觉语言导航性能。
---

## Abstract
Vision-and-Language Navigation (VLN) agents are tasked with navigating an unseen environment using natural language instructions. In this work, we study if visual representations of sub-goals implied by the instructions can serve as navigational cues and lead to increased navigation performance. To synthesize these visual representations or "imaginations", we leverage a text-to-image diffusion model on landmark references contained in segmented instructions. These imaginations are provided to VLN agents as an added modality to act as landmark cues and an auxiliary loss is added to explicitly encourage relating these with their corresponding referring expressions. Our findings reveal an increase in success rate (SR) of ~1 point and up to ~0.5 points in success scaled by inverse path length (SPL) across agents. These results suggest that the proposed approach reinforces visual understanding compared to relying on language instructions alone.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：视觉语言导航（VLN）要求智能体仅凭自然语言指令在未知环境中导航。指令中常包含视觉地标（如“台球桌”“厨房”“卧室”），如何让智能体将语言中的名词短语与真实视觉观察正确关联，是 VLN 的关键难点。
- **核心问题**：论文提出一个直观问题——能否利用文本到图像扩散模型，在导航前“想象”出指令中隐含地标的视觉表征，并将这些“视觉想象”（visual imaginations）作为额外输入模态，从而帮助智能体更好地导航？
- **整体含义**：如果成立，则意味着**图像域内的语义匹配（image-to-image）比纯语言-视觉跨模态匹配更容易**；合成图像既可作为语言与视觉之间的“枢轴”，也能补充训练数据中缺失的罕见地标视觉知识。作者还引用认知科学中的双重编码理论与心理意象研究作为灵感。

---

## 2. 方法论

### 2.1 核心思想

- 将导航指令分割为若干子指令（sub-instructions）；
- 过滤出其中包含具体视觉地标名词的子指令；
- 用 SDXL 扩散模型为这些子指令生成对应的视觉想象；
- 将视觉想象嵌入后与文本编码拼接，作为 VLN 智能体的额外输入；
- 额外添加一个“文本-想象对齐”辅助损失，显式鼓励视觉想象与其对应指称表达对齐。

### 2.2 关键技术细节

- **指令分割**：使用 FG-R2R 将指令分割为平均约 3.66 个子指令。
- **子指令过滤**：先剔除没有名词短语的子指令（用 SpaCy），再用人工黑名单排除无信息量名词（如数量词“one”、方向词“left”、代词“it”等）。
- **图像生成**：
  - 使用 SDXL 扩散模型；
  - 正向提示词加入“indoor”“real estate”，负向提示词加入“humans”“collage”等，使生成图像风格接近 Matterport3D 室内环境；
  - 对过滤后的子指令逐条生成图像。
- **想象编码器**：
  - 用预训练 ViT-B/16 独立编码每个想象；
  - 加上模态类型嵌入 `t_Im`；
  - 经三层 MLP 得到想象嵌入 `h_i = MLP(ViT(Z_i) + t_Im)`。
- **模型集成**：
  - 将全部想象嵌入与指令文本嵌入拼接，作为跨模态编码器的输入；
  - 模型结构抽象为 `f_X([f_T(W), H], f_O(O_≤t))`。
- **辅助对齐损失**：
  - 对每个想象-子指令对，计算想象嵌入 `h_i` 与其子指令名词短语平均文本嵌入 `\bar{S}_i` 的余弦相似度损失；
  - 损失形式：`L_cos = (1/N_Im) Σ (1 - cos(h_i, \bar{S}_i))`；
  - 总损失：`L_base + λL_cos`，实验取 λ = 0.5。
- **微调策略**（三阶段）：
  1. 冻结基座模型，只训练新引入的想象编码器 MLP 与类型嵌入；
  2. 全部模块联合训练，但基座模型使用较低学习率；
  3. 所有参数以统一学习率训练。

---

## 3. 实验设计

### 3.1 数据集与 benchmark

- **R2R（Room-to-Room）**：
  - 基于 Matterport3D 模拟器，90 个室内场景；
  - 训练集 4675 条轨迹，val-seen 340，val-unseen 783，test 1391；
  - 评估指标：成功率（SR）、按路径长度加权的成功率（SPL）、导航误差（NE）、轨迹长度（TL）。
- **REVERIE**：
  - 粗粒度指令，只给出高层目标与目标物体；
  - 额外使用远程接地成功率（RGS）与 RGS 按路径长度加权（RGSPL）。
- **R2R-Imagine 数据集**：
  - 作者基于 R2R 生成并释放的想象数据集；
  - 规模：train 41,558 张，val-seen 3,055，val-unseen 6,857，test 12,412；
  - 图像分辨率 1024×1024。

### 3.2 对比方法

- 基线模型：
  - **HAMT**：层次化 Transformer VLN 模型；
  - **DUET**：双尺度图 Transformer VLN 模型。
- 其他参照方法：
  - PREVALENT、RecBERT、ADAPT、BEVBert、MARVAL、ScaleVLN 等；
  - 其中 MARVAL、ScaleVLN 使用额外视觉数据（超出 Matterport3D），论文注明这些方法与本文不直接可比。

### 3.3 主要结果

- **R2R val-unseen**：
  - HAMT-Imagine 比 HAMT SR 提升约 1.0（66.24 → 67.26），SPL 提升约 0.5；
  - DUET-Imagine 比 DUET SR 提升约 0.6（71.52 → 72.12），SPL 提升约 0.07；
  - Test split 上 DUET-Imagine SR 提升 2 个点（69 → 71）。
- **REVERIE**：
  - DUET-Imagine 比 DUET SR 提升 1.3（46.98 → 48.28），RGS 提升 0.82，SPL 与 RGSPL 也有小幅提高。
- **消融与诊断实验**：
  1. **想象的作用**：测试时屏蔽想象（Null）仍有正则化收益；使用“错误想象”（随机取自其他指令）则性能回落到基线甚至更差，说明想象必须与指令对齐。
  2. **顺序想象 vs 目标想象**：按子指令顺序提供全部想象的“Full”设置优于只给最终目标的“Goal”设置（SR 67.26 vs 66.79）。
  3. **视觉编码器选择**：使用在 R2R 上微调过的 ViT 与 off-the-shelf 预训练 ViT 性能相当，最终选用 off-the-shelf ViT 以保持泛化性。
  4. **辅助损失设计**：无辅助损失时 SR 66.75；InfoNCE 对比损失 67.18；余弦损失 67.26，说明对齐损失有效，但负样本并非必要。
  5. **想象保真度**：用 LangSAM 开放词汇检测验证，98.78% 的子指令在想象中至少检测到一个名词短语，94.99% 的子指令所有名词短语均被检测到。

---

## 4. 资源与算力

- 文中明确提及的算力信息有限：
  - R2R-Imagine 数据集生成：单张 H100 GPU 生成一张想象图平均耗时约 **3.2 秒**，但未说明生成全量数据集所用的 GPU 总数与总机时。
  - 微调：使用 **Tesla V100**，batch size 为 8，每个智能体（agent）微调约 **100k 迭代，耗时约 1.5 天**；但未明确说明使用的 GPU 数量。
- 总体而言，论文提供了**单张生成耗时与单智能体微调耗时**，但缺少端到端的总算力估算、显存占用、推理阶段额外开销等细节。

---

## 5. 实验数量与充分性

- **实验数量充足**：
  - 覆盖两个数据集（R2R、REVERIE）；
  - 两种代表性模型（HAMT、DUET）；
  - 四类消融实验（想象输入的有无与正确性、顺序 vs 目标想象、ViT 选择、辅助损失类型）；
  - 一次生成质量自动评估（LangSAM 检测）。
- **充分性评价**：
  - 优点：消融设计较为全面，能明确回答“想象是否有效”“为什么有效”“如何集成最有效”等问题；
  - 客观性：对比时明确区分了使用额外数据的 MARVAL、ScaleVLN，避免直接比较带来的不公平；
  - 不足：性能提升幅度较小（SR 约 0.6–2 点），未报告多次随机种子下的方差；注意力可视化仅展示了个别案例，缺少系统性的行为学统计分析；未在更多 VLN 模型（如 BEVBert、RecBERT）上验证。

---

## 6. 主要结论与发现

- 视觉想象作为额外输入模态，可以**温和但稳定地提升 VLN 智能体的导航性能**。
- 想象必须与指令正确对应才能发挥最大作用，错误想象反而有害。
- 训练时引入想象、测试时屏蔽想象仍优于纯文本基线，说明想象带来的收益部分来自**正则化/训练增强**，而不仅是推理时的辅助线索。
- 按子指令顺序提供的“序列想象”优于只提供“目标想象”。
- 文本-想象对齐损失对性能有正向贡献；负样本对比损失（InfoNCE）与简单余弦损失差异不大。
- 预训练 ViT 作为想象编码器已足够，不需要在 VLN 数据上额外微调。
- 视觉想象有潜力作为语言与视觉之间的“枢轴”，帮助智能体在开放词汇地标上实现更好的跨模态关联。

---

## 7. 优点

- **方法模型无关**：可方便地插入 HAMT、DUET 等现有 VLN 架构，无需重新设计整个网络。
- **利用扩散模型的外部知识**：相比 ADAPT 只能从训练环境检索图像，本方法能生成训练集中不存在的开放性物体/场景（如“蓝墙厨房”），更具泛化性。
- **系统性的消融**：清晰分离了“训练增强”与“测试时利用”两种收益来源，并验证了想象对齐的关键作用。
- **生成质量验证**：用开放词汇检测器对大规模想象数据集做自动质量检查，为后续研究提供了可用数据资源（R2R-Imagine）。
- **实验设计相对公平**：区分了额外数据方法（MARVAL、ScaleVLN）并作出说明；对 REVERIE 等不同指令粒度也进行了验证。

---

## 8. 不足与局限

- **性能提升幅度有限**：R2R 上 SR 仅提升约 0.6–1.0 点，SPL 提升约 0.5 点以内，虽在 test set 上达到 2 点，但总体收益较小。
- **计算开销**：生成大量想象图需要额外算力；训练时增加想象编码器、推理时增加 ViT 编码，部署到真实机器人时会产生额外计算负担。虽然作者指出生成可离线完成，但推理阶段仍需额外编码器。
- **想象未与环境对齐**：生成的想象是“理想化”的，不包含真实场景中的物体摆放、光照、视角等环境细节；对于个性化、命名化的物体或位置无法准确想象。
- **实验不确定性未充分报告**：未给出多次运行的均值/方差，也未进行显著性检验，难以判断提升是否统计显著。
- **可视化分析局限**：注意力可视化仅选取少量示例，无法证明想象与决策之间的因果关系。
- **模型覆盖面有限**：只验证了 HAMT 与 DUET 两种模型，对更现代的大视觉语言模型导航方案（如 NavGPT）是否同样有效未作研究。
- **人为过滤依赖**：子指令过滤依赖 SpaCy 与人工黑名单，方法可能受语言多样性与长尾表达影响，需要额外人工调整。

（完）
