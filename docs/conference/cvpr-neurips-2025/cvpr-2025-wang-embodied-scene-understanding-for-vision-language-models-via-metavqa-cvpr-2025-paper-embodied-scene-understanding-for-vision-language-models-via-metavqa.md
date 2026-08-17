---
title: Embodied Scene Understanding for Vision Language Models via MetaVQA
title_zh: MetaVQA：通过视觉问答实现具身场景理解
authors: "Wang, Weizhen, Duan, Chenda, Peng, Zhenghao, Liu, Yuxin, Zhou, Bolei"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_Embodied_Scene_Understanding_for_Vision_Language_Models_via_MetaVQA_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 6.0
evidence: 面向具身场景理解的闭环仿真评测
tldr: 具身AI代理需要标准化的封闭式评测来检验空间推理与序列决策能力。本文提出MetaVQA基准，利用Set-of-Mark提示和真实交通场景俯视标注自动生成大量问答对，结合闭环仿真评估视觉语言模型在动态环境中的场景理解。该基准为具身智能体的视觉语言导航与空间推理提供了可复用的评测手段。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1785, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 854, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1021, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 861, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1804, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1802, \"height\": 658, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 401, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 397, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 449, \"label\": \"Table\"}]"
motivation: 缺少标准化的封闭式基准来评估具身视觉语言模型的空间推理与决策能力。
method: 基于nuScenes与Waymo数据自动生成VQA问答对，并借助闭环仿真进行评测。
result: 构建了大规模具身场景理解基准，可衡量并增强VLM的空间与决策能力。
conclusion: 为具身AI视觉语言模型的空间推理评测提供了标准化平台。
---

## Abstract
Vision Language Models (VLMs) demonstrate significant potential as embodied AI agents for various mobility applications. However, a standardized, closed-loop benchmark for evaluating their spatial reasoning and sequential decision-making capabilities is lacking. To address this, we present MetaVQA: a comprehensive benchmark designed to assess and enhance VLMs' understanding of spatial relationships and scene dynamics through Visual Question Answering (VQA) and closed-loop simulations. MetaVQA leverages Set-of-Mark prompting and top-down view ground-truth annotations from nuScenes and Waymo datasets to automatically generate extensive question-answer pairs based on diverse real-world traffic scenarios, ensuring object-centric and context-rich instructions. Our experiments show that fine-tuning VLMs with the MetaVQA Dataset significantly improves their embodied scene understanding, which is evident not only in improved VQA accuracy but also in emerging safety-aware driving maneuvers. In addition, the learning exhibits strong transferability from simulation to real-world observation. The project webpage is at https://metadriverse.github.io/metavqa.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：视觉语言模型（VLM）在具身AI应用（如自动驾驶、机器人控制）中展现出巨大潜力，但现有评估体系存在三个关键缺陷：
  - 缺乏**标准化的闭环benchmark**来评估VLM的空间推理与序列决策能力；
  - 已有的驾驶VQA数据集（如DriveLM、ELM等）在物体的指称方式上存在**异质性**（如用像素坐标vs自然语言特征描述物体），导致零样本评估时性能不佳可能源于“沟通不畅”而非“理解能力不足”；
  - 现有工作主要局限于**开环VQA任务**，缺乏VLM与环境的交互式评估，且安全关键场景稀缺。
- **整体含义**：本文旨在构建一个名为**MetaVQA**的基准，用于标准化评估和提升通用VLM的“具身场景理解”能力——包括**空间感知**（从2D图像理解3D空间关系）和**具身理解**（以自我为中心关联物体、预判行动后果、选择安全动作）。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用Set-of-Mark（SoM）提示和场景图自动生成大规模、自然语言表达的VQA数据集，并通过开环VQA + 闭环仿真驾驶双重任务评估VLM的具身场景理解能力。
- **技术流程（三段式VQA生成流水线）** ：
  1. **场景聚合**：
     - 从Waymo Open Motion Dataset（WOMD）和nuScenes提取真实交通场景；
     - 利用ScenarioNet将场景导入MetaDrive模拟器重建为可交互的仿真环境；
     - 为nuScenes创建数字孪生，增强外观多样性。
  2. **Set-of-Mark标注**：
     - 对真实图像将3D边界框投影到2D；对仿真图像利用实例分割提取2D框；
     - 用带编号的边界框标记物体，为VLM提供直观、无歧义的指称方式。
  3. **问答生成**：
     - 基于场景图，采用模板化+搜索式方法自动生成**多项选择**问题；
     - 空间和动态信息被离散为**自然语言范畴**（如“前方”、“靠近”），并附上细粒度数值描述；
     - 生成30种问题类型，分为三大超类：**空间问题、具身问题、指称问题**；
     - 额外加入“解释”（explanation）字段用于训练，增强模型深度理解。
- **问题设计原则**：
  - 采用SoM提示替代像素坐标等非自然指称方式；
  - 将所有问题做成多项选择，使评估更直接公平；
  - 每个问题附带解释字段，防止微调时模型崩塌。

## 3. 实验设计：数据集、benchmark与方法对比

- **数据集**：
  - **MetaVQA数据集**：4,305,450个多项选择问答，从400个nuScenes场景和6,900个Waymo场景中提取的442,102个标注帧生成，覆盖59,682秒（16.5小时）驾驶日志；
  - **训练集**：15万题（5万来自Waymo仿真、5万来自nuScenes仿真、5万来自nuScenes真实图像）；
  - **测试集**：9,725题，来自212个交通场景的2,524帧，约一半仿真、一半真实图像。
- **Benchmark任务**：
  - **开环VQA任务**：评估模型在SoM标注图像上的多项选择问答准确率；
  - **闭环驾驶任务**：在MetaDrive模拟器中，VLM作为自车规划器，每0.5秒接收第一视角图像和文本提示（目的地、当前速度、允许动作），输出驾驶动作，场景涵盖60个nuScenes场景和60个CAT生成的安全关键场景。
- **对比方法**：LLaVA-NeXT、LLaVA-OneVision、GPT-4o、Qwen2、Llama3.2、InternVL2-4B、InternVL2-8B，以及随机/刹车/直行基线。

## 4. 资源与算力

- **论文未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。文中仅提及InternVL2-8B、Llama3.2、Qwen2等模型被微调，但未披露计算资源细节。

## 5. 实验数量与充分性

- **实验组数**：
  - 零样本VQA benchmark（6个VLM × 3个维度）；
  - 微调后VQA评估（4个模型）；
  - 接地性问题零样本评估（6个模型）；
  - Sim-to-Real迁移学习实验（4个训练条件对比）；
  - 数据规模消融实验（3种训练数据规模）；
  - 闭环驾驶评估（4个VLM × 微调前/后对比）；
  - 人工评估（6名参与者、35个问题）。
- **充分性评价**：实验覆盖较全面，既有开环也有闭环，既有真实也有仿真数据，既有零样本也有微调评估；但**部分实验规模有限**（如人工评估仅35题、闭环场景120个），且缺少与DriveLM等先前基准的直接对比实验。

## 6. 论文的主要结论与发现

- **SoM提示的适用性**：多数VLM（平均69.6%零样本准确率）能准确将文本标签与标记区域关联，LLaVA-NeXT除外（因输出格式失败率高）；
- **微调显著提升**：在MetaVQA上微调后，所有VLM在VQA准确率和各问题类型上均一致提升（InternVL2-8B从0.592提升至0.869）；
- **仿真到真实的可迁移性**：仅用仿真数据训练就能显著提升真实世界VQA表现，两种域混合训练效果最佳；
- **数据可扩展性**：训练数据从9,375增至150,000，测试准确率从0.794升至0.869，呈正相关；
- **闭环驾驶能力涌现**：仅经过开环VQA微调，VLM在未见的闭环驾驶任务中展现出改进的路线完成率、更低的偏离率和更优的最终位移误差，表明学习到的具身场景理解具有泛化性。

## 7. 优点：方法或实验设计上的亮点

- **标准化评估**：用SoM提示+自然语言离散范畴+多项选择格式，解决了现有benchmark之间不可比的问题；
- **闭环评估**：将VLM部署到MetaDrive仿真中做真实交互决策，弥补了纯开环评估的不足；
- **大规模+多源数据**：结合Waymo和nuScenes两个真实数据集，涵盖15+小时驾驶日志，规模远超同类工作；
- **安全关键场景**：使用CAT生成对抗性交通场景，对VLM的安全性进行压力测试；
- **Sim-to-Real迁移验证**：系统验证了仿真训练向真实世界迁移的有效性，具有实际应用价值；
- **零样本+微调多层评估**：既评估了通用VLM的即用能力，也评估了微调后的提升空间。

## 8. 不足与局限

- **观测类型单一**：数据集仅包含单帧单视角图像，缺少多步历史信息和多相机观测，限制了对复杂时序决策的评估能力（作者自述）；
- **算力信息缺失**：未报告训练所需GPU资源，不利于复现和成本评估；
- **指称问题的grounding本身有噪声**：随机标注标签的方式可能使某些接地问题答案存在歧义；
- **多项选择格式的局限**：离散化可能损失连续空间信息的精细度，模型可能在选项间猜对而非真正理解；
- **闭环评估中的碰撞率改进不具绝对一致性**：部分模型（如InternVL2-4B-微调）碰撞率反而上升，作者归因于预训练差异，但这种不一致性值得进一步探究；
- **与已有benchmark的横向对比不足**：未在DriveLM等既有基准上测试，削弱了与现有方法的直接可比性；
- **闭环评估的泛化性**：120个场景相对有限，且动作空间被离散化，与实际驾驶的连续性存在差距。

（完）
