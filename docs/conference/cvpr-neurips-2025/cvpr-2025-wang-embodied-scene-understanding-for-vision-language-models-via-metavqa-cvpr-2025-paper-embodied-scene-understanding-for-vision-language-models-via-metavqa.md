---
title: Embodied Scene Understanding for Vision Language Models via MetaVQA
title_zh: 通过MetaVQA实现视觉语言模型的具身场景理解
authors: "Wang, Weizhen, Duan, Chenda, Peng, Zhenghao, Liu, Yuxin, Zhou, Bolei"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_Embodied_Scene_Understanding_for_Vision_Language_Models_via_MetaVQA_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 8.0
evidence: MetaVQA提供面向具身场景理解与空间推理的闭环仿真基准，直接涉及具身导航
tldr: 视觉语言模型在具身AI移动应用中潜力巨大，但缺乏标准化的闭环评测基准。本文提出MetaVQA，利用Set-of-Mark提示和来自nuScenes、Waymo的俯视真值标注，自动生成多样真实交通场景中物体中心、上下文丰富的问答对，用于评测和增强VLM的空间关系理解和顺序决策能力。在闭环仿真中验证了该基准的有效性，为具身智能体的场景理解与导航评估提供了标准化工具。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1785, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 854, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1021, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 861, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1804, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1802, \"height\": 658, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 312, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 401, \"height\": 142, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 397, \"height\": 163, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 801, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-embodied-scene-understanding-for-vision-language-models-via-metavqa-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 449, \"label\": \"Table\"}]"
motivation: 现有VLM缺乏标准化闭环基准来评估空间推理和顺序决策能力，阻碍具身应用。
method: 提出MetaVQA基准，基于真实交通场景自动生成问答对，结合闭环仿真和Set-of-Mark提示评测VLM。
result: 通过大量问答对和闭环仿真验证，MetaVQA能有效评估并增强VLM的具身场景理解能力。
conclusion: 为具身AI智能体在模拟环境中的空间理解和决策研究提供了标准化评价平台。
---

## Abstract
Vision Language Models (VLMs) demonstrate significant potential as embodied AI agents for various mobility applications. However, a standardized, closed-loop benchmark for evaluating their spatial reasoning and sequential decision-making capabilities is lacking. To address this, we present MetaVQA: a comprehensive benchmark designed to assess and enhance VLMs' understanding of spatial relationships and scene dynamics through Visual Question Answering (VQA) and closed-loop simulations. MetaVQA leverages Set-of-Mark prompting and top-down view ground-truth annotations from nuScenes and Waymo datasets to automatically generate extensive question-answer pairs based on diverse real-world traffic scenarios, ensuring object-centric and context-rich instructions. Our experiments show that fine-tuning VLMs with the MetaVQA Dataset significantly improves their embodied scene understanding, which is evident not only in improved VQA accuracy but also in emerging safety-aware driving maneuvers. In addition, the learning exhibits strong transferability from simulation to real-world observation. The project webpage is at https://metadriverse.github.io/metavqa.

---

## 论文详细总结（自动生成）

好的，我将按照您的要求，基于提供的论文内容，生成一份结构化的中文总结。

## 论文总结：通过MetaVQA实现视觉语言模型的具身场景理解

### 1. 论文的核心问题与整体含义

- **研究动机与背景**：
  - 视觉语言模型（VLM）在具身AI智能体（如自动驾驶、机器人控制）中展现出巨大潜力，其核心能力是**具身场景理解（Embodied Scene Understanding）**，包含两个关键方面：
    - **空间感知（Spatial Awareness）**：通过单目摄像头图像理解3D世界中物体间的空间关系。
    - **具身理解（Embodied Understanding）**：以自我为中心关联观察对象，预判动作后果，并选择最优行动。
  - 然而，现有VLM主要在海量离线图文数据上预训练，其空间感知和具身理解能力受限。
  - 尽管已有许多工作（如DriveLM、ELM、DriveVLM）通过创建定制的VQA（视觉问答）数据集来微调VLM以提升驾驶能力，但存在核心缺陷：
    - **不兼容性**：不同数据集使用不同的文本/视觉表达方式和引用协议（如像素坐标、字符串三元组），与人类自然语言习惯不符，导致评估结果无法归因于模型真实能力缺陷。
    - **评估方式单一**：主要在**开环（Open-loop）VQA**任务上评估，缺乏在交互环境中的**闭环（Closed-loop）**评估。
    - **缺乏安全关键场景**：现有工作多使用真实数据，难以收集危险情况，无法对VLM进行压力测试。

- **核心问题**：缺乏一个标准化、可扩展、具有闭环评估能力的基准，用于公平评估和提升通用VLM的具身场景理解能力。

### 2. 论文提出的方法论（MetaVQA）

- **核心思想**：构建一个从真实世界数据中提取场景，自动生成海量、统一格式的VQA数据集，并结合模拟器进行闭环评估的基准。
- **设计原则**：
  - **有效沟通**：采用 **Set-of-Mark (SoM) 提示**，使用数字标签直观地标记图像中的对象（通过2D边界框），避免使用VLM不熟悉的坐标或复杂引用协议。
  - **格式标准化**：所有问题设置为**多项选择**格式，确保评估直接、公平。空间和动态信息被离散化为常见短语（如“左”、“右”、“近”）进行分类，并提供更细粒度的数值作为解释。
  - **全面评估**：设计了30种问题类型，涵盖**空间问题**（如相对距离、方位）、**具身问题**（如碰撞预测、动作后果）和**接地问题**（诊断模型关联标记与文本的能力）。
- **技术流程**：
  1. **场景聚合（Scenario Aggregation）**：
     - 从**nuScenes**和**Waymo Open Motion Dataset (WOMD)** 中提取真实世界交通场景。
     - 使用**MetaDrive**模拟器和**ScenarioNet**平台，将Waymo场景重建为仿真场景，并为nuScenes场景创建数字孪生，以增强外观多样性。
  2. **Set-of-Mark标注**：
     - 在真实图像中，将3D边界框投射到2D空间。
     - 在仿真图像中，使用基于着色器的实例分割相机提取2D边界框。
     - 使用数字标签（如<3>, <2>）标记所有相关对象。
  3. **问答对生成（QA Generation）**：
     - 使用基于搜索的方法，从场景图中为模板化问题编程提取答案。
     - 为每个问题生成正确选项和干扰选项，并提供“解释”字段用于模型训练（增强场景理解），但不用于评估。

### 3. 实验设计

- **数据集与场景**：
  - **MetaVQA Dataset**：包含 **4,305,450** 个多项选择问题，来源于**400个nuScenes场景**和**6,900个Waymo场景**（共59,682秒驾驶日志）的**442,102个标注帧**。
  - **训练集**：150,000个问题（各5万来自Waymo仿真、nuScenes仿真、nuScenes真实图像）。
  - **测试集**：9,725个问题，来自212个交通场景，其中约一半为仿真图像，一半为真实图像。
- **Benchmark任务**：
  1. **开环VQA基准（Open-loop VQA Benchmark）**：在保留的测试集上评估模型的零样本能力和微调后的表现，主要指标为准确率。
  2. **闭环驾驶评估（Closed-loop Evaluation）**：在MetaDrive模拟器中，将VLM作为自车规划器，接收第一人称视角的SoM标注图像和文本提示，输出驾驶动作。场景包括60个nuScenes场景和60个由CAT生成的对抗性安全关键场景。评估指标包括：碰撞率、偏离率、平均位移误差（ADE）、最终位移误差（FDE）和路线完成率。
- **对比的VLM模型**：
  - **零样本评估**：LLaVA-NeXT、LLaVA-OneVision、GPT-4o、Qwen2-VL、Llama3.2、InternVL2-8B。
  - **微调评估**：Qwen2-VL、Llama3.2、InternVL2-4B、InternVL2-8B。

### 4. 资源与算力

- **论文未明确说明**训练微调模型所使用的GPU型号、数量或训练时长等具体算力信息。仅提及使用了InternVL2-8B、Llama3.2和Qwen2等模型进行微调。

### 5. 实验数量与充分性

- **实验组别**：
  1. **零样本VQA性能基准**（Tab. 4, Fig. 7a）：对比了6个代表模型。
  2. **微调后VQA性能提升**（Tab. 4, Fig. 7b）：展示了4个模型（Qwen2、Llama3.2、InternVL2-4B/8B）微调后的一致提升。
  3. **Sim-to-Real迁移学习验证**（Tab. 2）：InternVL2-8B在仿真/真实数据上训练的相互提升效果。
  4. **数据可扩展性验证**（Tab. 3）：在9,375/37,500/150,000数据规模下的微调效果。
  5. **闭环驾驶性能对比**（Tab. 5）：在120个场景中对比了微调前后的4个模型。
  6. **人类评估**：6名参与者对35个问题进行作答，准确率88%。
  7. **接地性能评估**（Tab. 1）：在467个接地问题上评估零样本接地能力。
- **充分性与客观性评价**：
  - **充分**：实验设计较为全面，覆盖了从数据构建质量（人类评估、接地测试）、核心基准（VQA）、能力验证（闭环驾驶）、学习特性（Sim-to-Real，可扩展性）等方面，能够有力支撑论文的主要结论。
  - **客观**：测试集采用未参与训练的保留数据；闭环评估场景（如CAT生成的对抗性场景）对模型是unseen的，增加了评估的客观性和挑战性。
  - **局限**：虽然对比了多个VLM，但主要微调实验集中于InternVL2系列，对其他系列（如Qwen、Llama）的深入分析较少。闭环评估的真人对比实验规模（6人）较小，但作为初步的人机一致性验证是足够的。

### 6. 论文的主要结论与发现

- 微调后的VLM在**开环VQA任务**上准确率显著提升，且这种提升不仅限于VQA，还泛化到了**未训练过的闭环驾驶任务**上，具体表现为路线完成率提升、碰撞率和偏离率下降，证明了学习MetaVQA数据集有助于提升VLM的具身场景理解能力和实际决策水平。
- **Sim-to-Real迁移性强**：仅在仿真数据上训练的模型，在真实世界数据上也能取得显著的零样本QA性能提升，支持了大规模使用仿真数据增强学习可行性和价值。
- **学习具有可扩展性**：模型性能与训练数据规模呈现正向相关，表明MetaVQA数据集的巨大体量是有价值的。

### 7. 优点

- **标准化的评估协议**：通过统一的SoM提示和多项选择格式，解决了现有VQA基准不兼容、不直观的问题，使评估更公平、更具诊断性。
- **丰富的场景与问题覆盖**：利用数据量更大的Waymo数据集并结合仿真重建，比仅使用nuScenes的现有工作（如DriveLM）覆盖更广的交通情况和问题类型（30种）。
- **创新的闭环评估设计**：将VLM作为模拟器中的驾驶智能体进行评估，弥合了静态VQA与真实具身交互之间的鸿沟，能够更真实地反映模型的具身决策能力。
- **自动化的数据构建管线**：从真实数据集到场景图再到自动QA生成的完整管线，支持大规模数据集构建，且通过人类评估验证了问题的可回答性。

### 8. 不足与局限

- **观察形式单一**：数据集目前仅使用单帧、固定视角的**单目图像**，缺乏多视角信息（如多摄像头）和多步历史信息，这可能限制了模型在需要时序推理场景下的表现。
- **感知问题被简化**：通过SoM提示直接提供边界框，假设感知任务基本解决，这使得基准专注于推理能力，但回避了端到端自动驾驶中感知模块错误传播的复杂性。
- **评估场景与真实差距**：尽管使用了仿真环境，但仿真渲染与真实世界仍存在外观和物理上的视觉差距。闭环评估主要基于规则化的模拟器，可能与真实世界的开放性和动态性存在偏差。
- **算力细节缺失**：论文未提供微调所需的具体计算资源（GPU型号、数量、时长），这不利于其他研究者复现实验或估算成本。
- **有限的人类评估规模**：人类评估的样本量（6人，35问）较小，虽然初步验证了问题的可答性，但其统计效力有限。

（完）
