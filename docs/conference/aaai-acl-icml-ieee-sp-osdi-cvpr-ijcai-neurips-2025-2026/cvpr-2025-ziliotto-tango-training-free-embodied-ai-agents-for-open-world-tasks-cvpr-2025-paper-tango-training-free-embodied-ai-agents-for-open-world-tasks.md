---
title: "TANGO: Training-free Embodied AI Agents for Open-world Tasks"
title_zh: TANGO：无需训练的开世界具身智能体
authors: "Ziliotto, Filippo, Campari, Tommaso, Serafini, Luciano, Ballan, Lamberto"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ziliotto_TANGO_Training-free_Embodied_AI_Agents_for_Open-world_Tasks_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 点目标导航原语、记忆化探索、LLM程序组合
tldr: 该文提出TANGO方法，将大语言模型的程序组合能力扩展到具身智能体。通过采用简单的点目标导航模型和基于记忆的探索策略作为基础原语，由LLM根据少量上下文示例组合这些原语以解决具体任务，无需额外训练即可应对开放世界中的多种任务。该方法展示了基础导航模型与LLM结合的高效性和通用性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 840, \"height\": 887, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1723, \"height\": 1124, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 874, \"height\": 255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 802, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 422, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 820, \"height\": 542, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 655, \"height\": 485, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 898, \"height\": 384, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 443, \"label\": \"Table\"}]"
motivation: 具身智能体需要在不重新训练的情况下适应开放世界中的多样任务。
method: 以点目标导航模型和记忆化探索策略为原语，利用LLM进行程序组合与上下文学习。
result: 单个模型无需额外训练即可解决多样开放世界任务，验证了组合原语的有效性。
conclusion: 训练无关的LLM组合方式为开放世界具身任务提供了一种简洁通用的解决方案。
---

## Abstract
Large Language Models (LLMs) have demonstrated excellent capabilities in composing various modules together to create programs that can perform complex reasoning tasks on images. In this paper, we propose TANGO, an approach that extends the program composition via LLMs already observed for images, aiming to integrate those capabilities into embodied agents capable of observing and acting in the world. Specifically, by employing a simple PointGoal Navigation model combined with a memory-based exploration policy as a foundational primitive for guiding an agent through the world, we show how a single model can address diverse tasks without additional training. We task an LLM with composing the provided primitives to solve a specific task, using only a few in-context examples in the prompt. We evaluate our approach on three key Embodied AI tasks: Open-Set ObjectGoal Navigation, Multi-Modal Lifelong Navigation, and Open Embodied Question Answering, achieving state-of-the-art results without any specific fine-tuning in challenging zero-shot scenarios.

---

## 论文详细总结（自动生成）

# TANGO：无需训练的开世界具身智能体（CVPR 2025）论文详细总结

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：如何让具身智能体（Embodied AI Agent）在不进行任何任务特定训练或微调的情况下，适应开放世界中的多种复杂任务（如目标导航、多模态终身导航、具身问答）？
- **背景**：
  - 大语言模型（LLM）已在图像领域的程序组合任务中展现出强大能力（如 VisProg、ViperGPT），通过少量上下文示例即可生成可执行程序，无需训练。
  - 然而，这种范式在具身智能领域（特别是导航任务）尚未得到充分探索。传统方法要么依赖端到端训练（成本极高，如 PointGoal 策略需训练 25 亿步），要么依赖任务特定的模块化设计，缺乏通用性和可扩展性。
- **整体含义**：TANGO 将 LLM 的程序组合能力从图像任务扩展到三维环境中的具身决策，利用一个通用的点目标导航原语和记忆化探索策略，配合多种感知模块，由 LLM 在推理时动态组合这些原语，从而以零样本（zero-shot）方式解决多个开放世界任务，无需任何任务专属训练或微调。

## 2. 论文提出的方法论

### 2.1 核心思想

- 采用**神经符号组合方法（neuro-symbolic compositional approach）**：由 LLM 作为高层规划器，将用户输入的自然语言指令转换为由一系列**原语（primitives）** 组成的可执行伪代码程序。
- 每个原语对应一个预训练模块或 Python 子程序，涵盖视觉感知、导航控制、语义匹配、问答等功能。
- 通过提供**少量上下文示例（in-context examples）**，LLM 能根据任务需求灵活组合模块，泛化到未见过的任务，无需任何训练或微调。

### 2.2 系统组成

- **TANGO Interpreter（程序解释器）**：
  - 负责解析 LLM 生成的伪代码，逐行执行模块，并维护程序状态（变量绑定）。
  - 包含视觉识别模块，用于提取场景语义。
  - 支持可解释性：LLM 生成的步骤附带注释，可追溯决策过程。
- **导航模块（Navigation Module）**：
  - 使用预训练的 **PointGoal 导航策略**作为基础导航原语，输入仅为深度图像和相对目标的方向/距离，可实现接近 99% 的 PointGoal 导航成功率。
- **探索策略（Exploration Policy）**：
  - 基于 VLFM [55] 的前沿探索策略：利用深度观测构建占用图，结合 BLIP2 生成的“语言接地价值图”引导探索。
  - **扩展：记忆机制**——维护一个“特征图”（feature map），每个像素编码为向量，随探索逐步更新。当新目标出现时，计算该目标嵌入与像素特征向量的余弦相似度，更新价值图。若相似度超过阈值，说明智能体“记得”该目标位置，可直接导航过去，从而支持**终身导航**（多目标序列）。

### 2.3 关键模块列表（Figure 3）

- **Python 子程序模块（橙色）**：`count`、`is_found`、`eval` 等。
- **视觉模型模块（蓝色）**：`detect`（Owlv2 开放词汇检测器 + DETR 用于 COCO 类别）、`classify`（CLIP 分类器，用于区分细粒度子类）、`answer`（BLIP2 用于 VQA/图像描述）、`match`（SuperGlue 用于图像实例匹配）。
- **导航模块（绿色）**：`navigate to`（PointGoal 导航到指定坐标）和 `explore scene`（记忆化探索，支持多目标）。
- 每个模块都有规范的输入/输出变量，便于 LLM 理解和程序状态更新。

### 2.4 算法流程（文字描述）

1. 用户输入自然语言指令/问题。
2. 将指令与 15 个固定上下文示例一起输入 LLM（GPT-4o）。
3. LLM 输出分步伪代码程序，每行调用一个 TANGO 原语，并附带注释。
4. TANGO Interpreter 逐行解析并执行模块，更新变量状态。
5. 智能体在 Habitat 模拟器中执行动作（前进、左右转、抬头、低头、停止），完成导航或问答任务。

## 3. 实验设计

### 3.1 数据集与基准（Benchmark）

| 任务 | 数据集 | 内容 |
|---|---|---|
| 开放词汇目标导航 | **HM3D-OVON** | 超过 15,000 个标注对象，379 个类别，来自真实 3D 场景扫描；智能体需在 500 步内导航到指定目标类别（val unseen 集）。 |
| 多模态终身导航 | **GOAT-Bench** | 智能体需连续导航 5-10 个目标，目标可指定为类别名、文本描述或图像；312 个类别，开放词汇（val unseen 集）。 |
| 开放具身问答 | **OpenEQA（A-EQA 子集）** | 超过 1,600 个问题-答案对，来自 180+ 真实环境；智能体需自主导航并回答开放性问题，500 步限制。 |

### 3.2 评估指标

- **SR（Success Rate）**：成功到达目标的比例（OVON、GOAT）。
- **SPL（Success weighted by Path Length）**：路径最优性加权成功率（OVON、GOAT）。
- **DTG（Distance to Goal）**：结束时到目标的平均距离（OVON、GOAT）。
- **LLM-Match Score**：由 LLM 将模型输出与参考答案比较，打分 1-5，经公式 S = (1/N)∑(σi − 1)/4 × 100% 归一化为百分比（OpenEQA）。

### 3.3 对比方法

- **OVON**：RL、BCRL、DAgRL、VLFM、DAgRL+OD。
- **GOAT-Bench**：SenseAct-NN Skill Chain、SenseAct-NN Monolithic、Modular GOAT、Modular Clip on Wheels。
- **OpenEQA**：Human Agent、Blind LLMs、Socratic LLMs with Frame Captions、Socratic LLMs with Scene-Graph Captions。

## 4. 资源与算力

- **论文未明确说明**使用了多少 GPU（型号、数量）以及训练时长。
- 唯一提到的训练相关细节是：PointGoal 导航模型在 HM3D 训练集上预训练（但测试场景均为未见场景），其余所有模块（Owlv2、DETR、BLIP2、CLIP、SuperGlue）均使用公开的预训练模型，**没有任何任务特定训练或微调**。
- 由于 TANGO 仅需推理时调用 LLM 和预训练模型，计算开销主要集中在推理阶段，但论文未给出具体运行时间或硬件配置数据。

## 5. 实验数量与充分性

### 实验数量
- 三个主任务（OVON、GOAT-Bench、OpenEQA）各有一组对比实验，共 3 组主实验。
- 另外补充了 OpenEQA 的失败分析（Figure 6），但**没有正式的消融实验**（如记忆机制的有无、不同检测器的影响、上下文示例数量变化等）。
- 表 3 中 GOAT-Bench 的对比实验除了 SR 和 SPL 外，未报告 DTG。

### 充分性与客观性评估
- **优点**：三个任务覆盖了导航、终身记忆和多模态问答，验证了框架的通用性；对比方法均为相关领域的代表方法（包括 SoA）；所有任务均使用标准评估协议（如 val unseen split）。
- **不足**：
  - 缺乏对记忆机制的消融验证，难以量化该扩展对 GOAT 任务的具体贡献。
  - 失败分析仅针对 EQA 任务，未对 OVON 或 GOAT 进行系统错误分析。
  - 未报告 OpenEQA 的 Answer Accuracy（在补充材料中），主文中仅用 LLM-Match 分数。
  - 多模态目标（图像、描述）在 GOAT 中的分项表现未拆分，无法评估 LLM 对每种目标类型的处理能力。
  - 实验均在 Habitat 模拟器中进行，未包含真实机器人实验，泛化到真实世界的能力仍需验证。

## 6. 论文的主要结论与发现

- TANGO 在三个任务上均达到或接近最优性能：
  - **OVON**：SR 35.5%、SPL 19.5%，与 SoA（DAgRL+OD 和 VLFM）持平。
  - **OpenEQA**：LLM-Match Score 37.2%，仅比最佳 Socratic 方法（38.1%）低 0.9%，但优于纯盲 LLM 和场景图 Socratic 方法。
  - **GOAT-Bench**：SR 32.1%，超过所有对比方法（最高提升 +2.6%）；SPL 16.5%，位列第二（比最佳低 0.7%）。
- 实验证明：**单个模型无需任务特定训练即可解决多种开放世界具身任务**，表现出很强的零样本泛化能力。
- 记忆机制对终身导航至关重要，能显著提升多目标导航的成功率。
- 失败分析显示：主要失败原因来自视觉检测模块（约 70% 以上），而 LLM 生成错误代码或目标仅占约 18%，说明底层感知模块的性能是系统瓶颈，而非 LLM 规划能力。

## 7. 优点（亮点）

- **完全免训练**：除 PointGoal 导航器外，所有模块均为现成预训练模型或简单 Python 函数，任务侧零训练，大大降低计算成本。
- **高度通用**：通过 LLM 组合原语，能够灵活应对多种任务，无需重新设计架构。
- **可解释性强**：LLM 生成的伪代码带注释，模块执行状态可追踪，便于错误定位和理解智能体行为。
- **记忆扩展**：将 VLFM 的单目标探索策略扩展为多目标终身导航，通过特征图存储环境语义，支持跨目标重用已知位置。
- **模块可替换性**：可随时用更新更强的视觉模型替换原有模块，保持系统先进性。
- **对比实验显示 SoA 或接近 SoA**，验证了该范式的有效性。

## 8. 不足与局限

- **感知模块依赖强**：检测器误检/漏检是主要失败来源，在合成 3D 场景中尤其常见假阳性，虽然引入了 CLIP 分类器辅助，仍不够鲁棒。
- **依赖云 LLM（GPT-4o）**：需要外部 LLM 服务，存在延迟、成本和隐私问题；未尝试开源 LLM（论文提到未来工作）。
- **上下文示例固定为 15 个**：未消融示例数量对性能的影响，LLM 输出质量可能对示例选择敏感。
- **导航效率一般**：在 GOAT 中 SPL 略低于最优方法（16.5 vs 17.2），说明路径规划仍有优化空间。
- **复杂或歧义指令处理有限**：论文承认 LLM 在生成目标或顺序时可能出错，导致任务失败。
- **实验范围局限**：仅在仿真环境（Habitat）中评估，未在真实机器人上验证；未覆盖 VLN（视觉语言导航）等其他具身任务。
- **算力信息缺失**：未报告推理时延、GPU 占用等硬件资源消耗，影响实际部署可参考性。

（完）
