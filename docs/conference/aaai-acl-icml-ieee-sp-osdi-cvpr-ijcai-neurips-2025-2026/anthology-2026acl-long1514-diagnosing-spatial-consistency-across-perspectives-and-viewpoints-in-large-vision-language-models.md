---
title: Diagnosing Spatial Consistency across Perspectives and Viewpoints in Large Vision-Language Models
title_zh: 诊断大型视觉-语言模型在跨视角与视点下的空间一致性
authors: "Yoonji Kim, Jieun Kim, Yujin Jeong, Sung-Bae Cho"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1514.pdf"
tags: ["query:embodied-nav"]
score: 4.0
evidence: 面向大型视觉-语言模型的空间一致性诊断基准，与具身智能体相关
tldr: 该文指出现有空间能力基准多从静态单视角自我中心视角评估，忽略了真实世界动态空间认知。为此提出SCOPE基准，系统诊断大型视觉-语言模型在跨视角和视点下的空间一致性。该基准基于人类认知理论设计，为评估具身智能体所需的空间推理提供了更全面的测试工具。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 772, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1648, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 788, \"height\": 505, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 719, \"height\": 777, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1661, \"height\": 677, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 785, \"height\": 700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1652, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 805, \"height\": 694, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 797, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 787, \"height\": 956, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 815, \"height\": 733, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 664, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1628, \"height\": 2184, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 623, \"height\": 469, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 626, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 615, \"height\": 468, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 625, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1241, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 612, \"height\": 480, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 637, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1137, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1167, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1636, \"height\": 926, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1514/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1635, \"height\": 916, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1527, \"height\": 1448, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 806, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1642, \"height\": 355, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 625, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 808, \"height\": 498, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1281, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 812, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 796, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1514/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 811, \"height\": 218, \"label\": \"Table\"}]"
motivation: 现有空间基准不能反映动态真实环境的跨视角空间一致性，限制了对具身AI空间能力的评估。
method: 构建SCOPE基准，从跨视角与跨视点维度系统诊断LVLM的空间一致性，依据人类认知理论设计评测任务。
result: 提供全面的空间一致性诊断基准，揭示现有LVLM在动态视角下的空间推理局限。
conclusion: 该工作为具身智能体的空间认知评测补充了动态视角维度。
---

## Abstract
Consistent reasoning about 3D spatial relations across changing viewpoints is fundamental for Embodied AI agents operating in dynamic environments. While Large Vision-Language Models (LVLMs) have advanced multimodal perception, their ability to maintain spatial consistency across diverse perspectives remains underexplored. Existing benchmarks primarily assess spatial capabilities from a static, single-view, and egocentric perspective, failing to capture the dynamic nature of real-world spatial cognition.To address this gap, we introduce SCOPE ( S patial CO nsistency across PE rspectives and Viewpoints), a comprehensive benchmark designed to rigorously diagnose spatial reasoning capabilities. Grounded in human cognitive theories of dual spatial representations, SCOPE discretizes the 360∘ field into multiview scenarios to systematically evaluate both allocentric and egocentric reasoning capabilities. Our dataset comprises 20.1K spatial VQA pairs derived from high-quality 3D environments. Through an extensive evaluation of 26 state-of-the-art LVLMs, we identify two fundamental limitations that prevent consistent spatial understanding across viewpoints.We hope SCOPE facilitates the diagnosis of spatial reasoning, serving as a stepping stone toward reliable embodied action.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机和背景）

- **核心问题**：大型视觉-语言模型（LVLMs）在跨视角和视点变化下，能否维持对3D空间关系的一致性理解？
- **研究动机**：
  - 具身AI智能体需要在动态、多视角环境中可靠地进行3D空间推理，这是其导航与操作的基本前提。
  - 现有空间推理基准（如VSR、What's Up、TopViewRS、3DSRBench、Spatial-MM等）主要从**静态、单视角、以自我为中心（egocentric）** 的角度评估模型，忽略了真实世界空间认知的动态性和多视角特性。
  - 已有基准往往将“自我中心”和“对齐中心（allocentric）”视角混为一谈，或仅使用单一固定视角，导致模型可能依赖虚假相关性（spurious correlation）或捷径推理（shortcut reasoning）来作答。
- **整体含义**：论文提出SCOPE基准，从跨视角一致性出发系统诊断LVLMs的空间推理能力，为构建更可靠的具身智能体提供评估工具和诊断依据。

### 2. 方法论

- **核心思想**：借鉴人类认知科学中的双重空间表征理论，将360°视野离散化为8个视角（每45°一个），系统评估模型在不同视角下的空间推理一致性。
- **基准构成**：SCOPE包含三个任务组，分别对应人类空间认知的不同子能力：
  - **Spatial Consistency（空间一致性）**：测试模型在视角变化下是否维持稳定的空间关系判断（涵盖自我中心与对齐中心）。
  - **Spatial Updating（空间更新）**：测试模型在想象旋转/视点偏移后能否正确推断空间关系（涵盖自我中心与对齐中心）。
  - **Spatial Integration（空间整合）**：测试模型是否能够将多个视角的局部观测整合为统一的全局场景结构。
- **四个核心空间推理因子**：关系（Relational）、深度（Depth）、朝向（Orientation）和遮蔽（Occlusion），用于刻画任务的认知复杂度。
- **数据构建流程**：
  - 从DL3DV-10K和WildRGB-D真实场景数据集、Blender合成场景、专家拍摄的真实照片三个来源采集数据。
  - 使用相机位姿元数据（4×4变换矩阵）进行几何筛选：圆形轨迹拟合、8角度覆盖验证、垂直位移过滤，确保视角一致性。
  - 使用Qwen2.5-VL-72B生成场景描述，使用Grounded-SAM2获取实例分割掩码并计算对象质心，再由三位领域专家进行人工审核。
  - 基于规则模板生成空间问答对，方向分布经平衡处理以消除方向偏差。
- **一致性评估公式**：
  - C(S) = (1/N) ∑ I[ ∧v∈S T<sub>v→v₀</sub>(f(I<sub>n,v</sub>)) = f(I<sub>n,v₀</sub>) ]，即所有视角的预测经坐标变换后是否在参考视角下保持一致。
- **人类认知启发式提示（Ego→Allo Prompting）**：
  - 受人类“先自我中心定位，再对齐中心整合”的认知策略启发，设计两阶段少样本提示：先在自我中心框架下定位关系，再在对齐中心框架下重构全局场景布局。

### 3. 实验设计

- **Benchmark规模**：SCOPE包含20,144个空间VQA对，来自939个场景（10个DL3DV场景、223个WildRGB-D场景、40个专家拍摄真实场景、664个Blender合成场景），共7,512个视图。
- **评估模型（共26个）**，分为五类：
  - 基线：Random（随机）、Frequency（频率）、GPT-5.2-Blind（纯文本盲测）
  - 开源模型：Qwen2.5-VL（3B/7B/32B/72B）、Llama-3.2-11B、InternVL2.5（2B/8B/14B/38B/78B）、LLaVA-OneVision（4B/8B）、Gemma3（4B/12B/27B）
  - 专有模型：GPT-5.2/GPT-5-nano/GPT-5-mini、Gemini-2.5-Pro/Flash/Flash-Lite
  - 空间专用模型：SpatialRGPT、SpatialReasoner、RoboBrain（3B/7B/32B）
  - 人类评估：13名受试者在SCOPE-188子集上测试
- **零样本设置**，采样温度设为0，四个选项的单项选择格式。
- **额外实验**：
  - 提示鲁棒性测试（自然语言改写模板问题，验证非模板模式投机）
  - 与具身基准（ManipBench、EmbodiedBench）的分数相关性分析
  - 混淆矩阵分析、误差类型分析、CoT（Chain-of-Thought）提示分析
  - 方向分布与现有基准（Spatial-MM、VSI-Bench）的对比

### 4. 资源与算力

- **论文中未明确报告**所使用的GPU型号、数量、训练时长等算力信息。
- 仅能推断：数据生成阶段使用了Qwen2.5-VL-72B（推理性使用）和Grounded-SAM2进行自动标注；评估阶段涉及26个不同规模模型（含78B参数级别模型）的推理。
- 人类评估部分提到对13名参与者每人补偿10美元。

### 5. 实验数量与充分性

- **实验数量**：整体较为丰富——26个模型在三大任务、两个视角维度下评估，覆盖开放与专有、不同参数量级别；还包括消融式分析（提示鲁棒性、CoT提示、一致性与准确性差距、混淆矩阵、误差类型、具身基准相关性等）。
- **充分性评价**：
  - **优点**：模型覆盖面广（26个模型×多尺度），评测维度较为完整（一致性、更新、整合三大任务），多维度分析深入。
  - **不足**：
    - 仅使用单一固定提示模板+温度0解码，可能低估某些模型在替代提示或解码策略下的表现。
    - 全部问答为英文，跨语言泛化未验证。
    - 所有模型只在零样本环境下测试，未进行少样本或全样本监督评估。
    - 三个空间专用模型与基础模型的对比存在不公平性（基础模型未在其训练数据上进行额外微调）。

### 6. 主要结论与发现

1. **模型规模扩大不能解决对齐中心一致性**：Qwen2.5-VL从3B扩展到72B，对齐中心一致性仍处于随机水平（25.79→25.48）；GPT-5-mini最高也只达到34.90，远低于人类的83.12。
2. **空间更新能力脆弱**：即使是自我中心空间更新，开源模型大多接近随机水平，专有模型也远低于人类水平（88.67）；对齐中心空间更新几乎所有模型均处于随机水平。
3. **多视图整合的关键难点在于关系组合而非视图聚合**：Gemini-2.5-Pro在对齐中心整合中达97.68，但在自我中心整合中仅25.00，说明模型可匹配实体却不建构统一空间表征。
4. **空间微调带来任务特异增益但缺乏泛化**：RoboBrain-32B在自我中心一致性上表现优异（87.43），但在对齐中心一致性和空间更新上仍接近随机。
5. **准确性-一致性差距显著**：GPT-mini准确率为89.6%，但一致性仅约50%，表明正确回答中约一半依赖视角特异线索而非稳健空间理解。
6. **方向偏差和关系坍缩**：模型对对角线方向混淆更严重，对左右判断优于前后判断，弱模型倾向于仅输出有限的关系子集。
7. **人类认知启发式提示有效**：Ego→Allo两阶段提示在空间整合任务上平均提升6.4%准确率（自我中心+6.35，对齐中心+6.47）。

### 7. 优点

- **认知科学基础扎实**：基于Piaget的三山实验、Simons & Wang的空间更新实验、对象文件理论等经典研究设计任务，理论依据充分。
- **首个全面覆盖多视角一致性的基准**：现有基准多为单视角评估，SCOPE通过8视角360°离散化填补了这一空白。
- **明确提出一致性度量标准**：在准确率之外引入跨视角一致性指标，揭示“高准确率低一致性”的捷径推理问题。
- **数据构建质量可控**：多阶段过滤（几何验证、人工审核）、方向分布平衡、真实与合成场景混合，减少偏差。
- **分析与诊断深入**：混淆矩阵、误差类型分析、准确性-一致性差距、人类-AI错误相关性等多维诊断，揭示了具体失败模式而非停留在总体分数。
- **与人类认知策略结合的方法改进**：Ego→Allo两阶段提示简单有效，具有可操作性与推广潜力。
- **与具身基准的强相关性验证**（ManipBench: Pearson 0.88; EmbodiedBench: Pearson 0.81），增强了基准的实用性。

### 8. 不足与局限

- **评估配置单一**：仅使用一种固定提示模板和温度0解码，未探索提示敏感性；不同提示策略下结论可能变化。
- **语言覆盖局限**：所有问题均为英文，跨语言泛化性未知。
- **问题格式局限**：全部为四选一多项选择，与真实具身场景中的开放式空间推理存在差异。
- **场景选择偏向**：多数场景来自WildRGB-D（桌面场景为主），对大型室内外场景覆盖相对有限；真实场景数量远少于合成场景（9.67% vs 35.12%），可能存在域偏差。
- **空间专用模型对比不充分**：空间专用模型（如SpatialRGPT、RoboBrain）在原始数据上微调，与零样本通用模型对比可能不够公平。
- **人工评估子集较小**：SCOPE-188仅含188个实例，统计效力有限。
- **结论的因果性有限**：准确率-一致性差距揭示了相关关系，但未实证证明“捷径推理”是导致一致性的因果机制；人类与模型错误低相关性虽支持推断，但未提供更直接证据。
- **资源信息缺失**：对算力、训练成本等未做说明，可复现性信息不够完整。

（完）
