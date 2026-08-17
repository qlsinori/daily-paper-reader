---
title: "TANGO: Training-free Embodied AI Agents for Open-world Tasks"
title_zh: TANGO：面向开放世界任务的免训练具身AI智能体
authors: "Ziliotto, Filippo, Campari, Tommaso, Serafini, Luciano, Ballan, Lamberto"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ziliotto_TANGO_Training-free_Embodied_AI_Agents_for_Open-world_Tasks_CVPR_2025_paper.pdf"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 以点目标导航模型作为原语，服务于多种具身开放世界任务
tldr: 具身开放世界任务多样，传统方法需要分别训练，泛化困难。TANGO利用LLM将点目标导航模型与基于记忆的探索策略组合成可执行程序，无需额外训练即可完成多种任务。经验证，该方法在开放世界分类和导航任务上表现良好，展示了以导航为核心原语构建通用具身智能体的可行性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 840, \"height\": 887}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1723, \"height\": 1124}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 874, \"height\": 255}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 875, \"height\": 802}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 422}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 820, \"height\": 542}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 655, \"height\": 485}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 898, \"height\": 384}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ziliotto-tango-training-free-embodied-ai-agents-for-open-world-tasks-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 443}]"
motivation: 具身智能体面临多样的开放世界任务，逐任务训练成本高且难以迁移。
method: 将点目标导航模型和记忆探索策略封装为原语，由LLM通过上下文示例组合成新任务程序。
result: TANGO在多个开放世界任务上达到与专门训练方法相当的性能，扩展性好。
conclusion: 利用LLM组合简单导航原语，可实现低成本、免训练的通用具身智能体。
---

## Abstract
Large Language Models (LLMs) have demonstrated excellent capabilities in composing various modules together to create programs that can perform complex reasoning tasks on images. In this paper, we propose TANGO, an approach that extends the program composition via LLMs already observed for images, aiming to integrate those capabilities into embodied agents capable of observing and acting in the world. Specifically, by employing a simple PointGoal Navigation model combined with a memory-based exploration policy as a foundational primitive for guiding an agent through the world, we show how a single model can address diverse tasks without additional training. We task an LLM with composing the provided primitives to solve a specific task, using only a few in-context examples in the prompt. We evaluate our approach on three key Embodied AI tasks: Open-Set ObjectGoal Navigation, Multi-Modal Lifelong Navigation, and Open Embodied Question Answering, achieving state-of-the-art results without any specific fine-tuning in challenging zero-shot scenarios.

---

## 论文详细总结（自动生成）

# TANGO：面向开放世界任务的免训练具身AI智能体

> 论文来源：CVPR 2025（IEEE/CVF Conference on Computer Vision and Pattern Recognition）

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：具身AI智能体需要应对多样化的开放世界任务（如目标导航、终身导航、具身问答），传统方法通常需要针对每个任务单独训练模型，成本高昂且泛化能力有限。
- **研究动机**：
  - 大语言模型（LLM）在图像领域已展现出通过程序组合（如 VisProg、ViperGPT）解决复杂视觉推理任务的能力，无需任务特定训练。
  - 然而，将这些能力拓展到**具身智能体**（需要在3D环境中感知、导航和行动）的研究仍相对空白。
  - 现有的具身导航方法中，端到端方法训练成本极高（例如 PointGoal 策略需要 25 亿步训练），模块化方法虽常共享探索/导航组件，但适配新任务仍需手动调整架构。
- **整体含义**：该论文提出了一种**免训练的神经-符号组合框架**——利用LLM将简单的导航原语（primitive）编排成可执行程序，使单一模型无需任何任务特定微调即可应对多种具身AI任务，探索了一条低成本构建通用具身智能体的可行路径。

## 2. 方法论：核心技术细节

### 2.1 总体框架（TANGO）

- **核心思想**：受 VisProg 启发——给定自然语言指令，LLM（实现中为 GPT-4o）作为规划器，基于少量“上下文示例”（15个跨任务的示例），生成可由智能体执行的**伪代码程序**。
- **神经-符号架构**：程序由一组**原语模块**序列构成，每个模块封装了预训练的视觉模型（如物体检测、VQA）或简单的 Python 子例程（如计数、求值），以及专门的导航模块（如 navigate to、explore scene）。
- **可解释性**：LLM 被要求以注释形式说明每个生成步骤的理由，每个模块输出均以变量形式传入下一模块，整个决策过程可被完整追踪，便于失败分析。

### 2.2 关键模块

| 模块类别 | 名称 | 技术实现 |
|---------|------|---------|
| 导航基础 | navigate to / explore scene | 预训练 PointGoal 导航策略（~99% 成功率），输入仅含深度图像 + GPS/指南针 |
| 探索策略 | explore scene | 基于 [55]（VLFM）的**前沿探索策略**：构建占用地图 → 检测探索前沿 → 利用 BLIP2 生成语言接地“值图”引导探索 |
| **记忆机制** | 新扩展 | 在值图上增加**特征向量图**，每个像素存储特征向量；新目标到来时计算新目标嵌入与该图的余弦相似度，更新值图；若相似度超过阈值则直接导航至记忆位置，支持**终身多目标导航** |
| 物体检测 | detect / classify | Owlv2（开放词汇检测）+ DETR（COCO 类）+ CLIP 分类器（区分细粒度子类，子类名由LLM自动输出） |
| 图像匹配 | match | SuperGlue 特征匹配网络，用于图像指定的目标实例确认 |
| 问答 | answer | BLIP2（支持VQA、图像-文本检索、图像描述等） |

### 2.3 算法流程

1. 用户输入自然语言任务/问题。
2. LLM 结合 15 个上下文示例，生成逐步可执行的伪代码程序。
3. 程序解释器按行解析参数和输出变量，执行每个模块。
4. 导航模块指导智能体在环境中移动，检测/匹配/回答模块处理视觉语义信息。
5. 输出最终结果（如找到目标、回答问题）。

## 3. 实验设计

### 3.1 数据集与基准

| 任务 | 数据集/基准 | 规模与内容 |
|------|-----------|-----------|
| 开放词汇目标导航 | HM3D-OVON | 15000+ 标注物体、379 个类别，来自真实3D扫描；validation unseen 全量评估，500步限制 |
| 多模态终身导航 | GOAT-Bench | 依次导航到 5-10 个目标，目标以类别名、描述或图片指定，312 个类别 |
| 开放具身问答 | OpenEQA（A-EQA 子集） | 1600+ 问答对，180+ 真实环境，7 类问题，500步限制 |

### 3.2 对比方法

- **OVON**：RL、BCRL、DAgRL、VLFM（确定性）、DAgRL+OD
- **GOAT-Bench**：SenseAct-NN Skill Chain、SenseAct-NN Monolithic、Modular GOAT、Modular Clip on Wheels
- **OpenEQA**：Human Agent、Blind LLMs、Socratic LLMs w/ Frame Captions、Socratic LLMs w/ Scene-Graph Captions

### 3.3 评估指标

- OVON 和 GOAT：Success Rate (SR)、Success weighted by Path Length (SPL)、Distance to Goal (DTG)
- OpenEQA：LLM-Match 评分（LLM 将模型答案与答案对比打分 1-5 分，经公式归一化）、Answer Accuracy

## 4. 资源与算力

- **论文说明**：文中明确提到**系统中所有模块均不需训练**，唯一经过训练的组件是 PointGoal 导航模型（在 HM3D 训练集上预训练，测试场景与之不重叠，即“未见过”场景）。
- **未明确信息**：论文**未**披露具体使用的GPU型号、数量或推理时间开销等算力细节，也未给出PointGoal预训练模型的具体训练成本（该模型本身来自已有工作，训练约需天数级GPU资源）。

## 5. 实验数量与充分性

### 5.1 实验数量

- **三大任务各1组**主实验（OVON、GOAT、OpenEQA），均为 validation unseen 零样本场景。
- **1组失败分析**（EQA任务）：手动分类失败原因，从可解释性角度定位系统薄弱环节。
- **无独立消融实验**（如记忆机制有无的对比、不同检测器的对比、不同示例数量的影响等均未单独呈现）。

### 5.2 充分性与客观性评估

- **优点**：三个任务覆盖了导航、终身学习、问答等不同能力维度，较好地展示了框架的通用性；零样本设定下与 SoTA 对比具有说服力；多轮随机种子报告方差（±）提升了可靠性。
- **不足**：实验组数偏少，缺少对记忆机制、LLM 组件等关键模块的系统性消融；对比方法并非全为最新方法；失败分析虽有价值，但手动分类可能引入主观偏差。

## 6. 主要结论与发现

- **TANGO 可在零样本条件下达到与专门训练方法相当甚至更优的性能**：
  - OVON：SR 35.5%、SPL 19.5%，与 SoTA（DAgRL+OD 37.1%）仅差 1.6 个点，与 VLFM 相当。
  - GOAT-Bench：SR 32.1%，**高于**所有对比方法（第二名 SenseAct-NN Skill Chain 为 29.5%，+2.6%）；SPL 16.5%（第一名 17.2%，差距仅 0.7%）。
  - OpenEQA：Score 37.2%，与 SoTA（Socratic LLMs w/ Frame Captions 38.1%）差距 <1%。
- **LLM 组合简单导航原语即可应对多任务**：单一 PointGoal 模型 + 记忆探索策略 + 视觉模块的组合具有显著通用性。
- **记忆机制对终身导航任务至关重要**：支持智能体高效返回已探索目标位置。
- **失败来源分析**：主要失败原因是**检测模块**（停在错误物体或忽略目标物体，占最大比例），探索策略仅贡献约 10% 失败，LLM 代码生成错误约 18%（其中 11.2% 属顺序/用法错误，6.9% 属目标理解歧义）。

## 7. 优点

- **免训练/零样本**：除 PointGoal 预训练模型外，所有模块无需任务特定微调，显著降低具身AI的部署成本。
- **模块化与可扩展性**：新任务只需新提示词即可适配；模块可用更新更好的开源模型无缝替换。
- **可解释性强**：LLM 生成注释 + 变量追踪，支持细粒度失败分析（图6为示范）。
- **任务泛化范围广**：同时覆盖目标导航（类别/文本/图像指定）、终身导航和具身问答，展示架构弹性。
- **记忆机制的创新**：将 VLFM 探索策略扩展为支持多目标终身导航的特征图记忆，在 GOAT 上取得 SoTA。

## 8. 不足与局限

- **性能仍有明显差距**：在 OpenEQA 上人类 Agent 得分 85.1% 远超所有 LLM 方法（约 37%），说明开放世界语义理解仍有巨大空间。
- **依赖 LLM 的规划质量**：约 18% 的失败源于 LLM 生成错误程序，对复杂或模糊指令的处理能力有限。
- **检测模块是主要瓶颈**：检测器误检/漏检导致大量失败，在合成3D场景中尤其明显（文中提到众多误报）。
- **实验覆盖不足**：仅三个任务、无消融实验；未涉及 Vision-Language Navigation（VLN）等更复杂任务；未在真实机器人上验证。
- **使用专有 LLM（GPT-4o）**：依赖商业 API，未探索开源替代方案（文中列为未来工作）。
- **未报告算力成本**：虽然免训练，但推理阶段 GPT-4o 调用的经济与时间成本未被量化。
- **记忆机制的局限**：若记忆目标识别错误，路径效率会显著下降（文中提及此问题）。

## （完）
