---
title: "CoT-VLNBench: A Benchmark for Visual Chain-of-Thought Reasoning in Vision-Language-Navigation Robots"
title_zh: CoT-VLNBench：视觉语言导航机器人视觉思维链推理基准
authors: "Xiao Zhao, Chang Liu, Ruiteng Ji, Zheyuan Zhang, Mingxu Zhu, Linna Song, Zhe Ren, Luo Qingliang, YuHang Gao, Zhaolong Du, Chufan Guo, Kuifeng Su"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40980/44941"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 面向四足机器人视觉语言导航的大规模思维链推理基准与数据集
tldr: 针对现有机器人中心数据集缺乏视觉语言任务支持、难以评估可解释导航的问题，本文提出CoT-VLNBench，首个面向四足机器人视觉语言导航的大规模思维链推理基准。数据集涵盖室内外多场景、多步导航轨迹和丰富自然语言指令，并支持思维链标注。该基准为评估和推动具身智能体的可解释VLN能力提供了重要测试平台，有望促进视觉语言模型在真实机器人导航中的应用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40980/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1129, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40980/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 115, \"height\": 117, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40980/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 879, \"height\": 824, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40980/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1844, \"height\": 882, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40980/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1848, \"height\": 1259, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-40980/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 864, \"height\": 324, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40980/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1831, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40980/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 755, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40980/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-40980/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1829, \"height\": 488, \"label\": \"Table\"}]"
motivation: 现有机器人数据集侧重传统3D感知与预测，缺少视觉语言导航和思维链推理支持，无法充分评估可解释导航能力。
method: 构建CoT-VLNBench基准，收集多场景多步轨迹与自然语言指令并引入思维链推理标注。
result: 该基准首次大规模支持四足机器人VLN的思维链评测，可用于衡量VLM导航推理能力。
conclusion: 通过提供专门基准，填补了具身视觉语言导航中思维链推理评测的空白。
---

## Abstract
Recent advances in vision language models (VLMs) have demonstrated remarkable potential in embodied navigation tasks. However, existing robot-centric datasets primarily focus on traditional 3D tasks such as perception and prediction, lacking adequate support for vision-language tasks. Vision-language-navigation (VLN) is a key capability for achieving human-like and interpretable navigation in complex environments. In this study, we present CoT-VLNBench, the first large-scale benchmark and dataset designed for chain-of-thought (CoT) reasoning in quadruped robot navigation. Our dataset encompasses a diverse range of indoor and outdoor scenes, multi-step navigation trajectories, and rich natural language instructions, all annotated with fine-grained CoT reasoning traces. Specifically, it contains 175K frames, 5.25M 3D bounding boxes, and 875K vision–question–answer (VQA) pairs. This comprehensive resource enables thorough evaluation of embodied agents’ perceptual and step-by-step reasoning abilities. Furthermore, we propose a novel CoT-VLN model, a state-of-the-art 7B VLN model that integrates visual, linguistic, and reasoning modules, to facilitate interpretable and effective navigation. Extensive experiments demonstrate that our approach significantly outperforms existing non-VLMs baselines on the new benchmark, underscoring the importance of CoT-VLN in embodied navigation. We hope that CoT-VLNBench will serve as a valuable resource to advance research at the intersection of robotics, vision, language, and reasoning.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：视觉语言模型（VLM）在具身导航任务中展现了巨大潜力，但现有机器人中心数据集（如 CODa、SIT、JRDB）主要聚焦于传统 3D 感知、目标检测与跟踪，缺乏对视觉语言导航（VLN）与高级推理任务的支持。
- **关键缺口**：现有数据集不提供逐步、可解释的推理轨迹（即思维链标注），难以理解智能体在面对复杂或多步指令时的导航决策过程。
- **研究目标**：填补"机器人 + VLM + 思维链推理"交叉领域的空白，构建首个面向四足机器人 VLN 的大规模思维链推理基准与数据集，推动可解释、类人化的具身导航研究。

## 2. 方法论

- **核心思想**：采用 Chain-of-Thought（CoT）范式，将高层的自然语言指令与低层导航动作之间的鸿沟，通过显式的中间推理步骤进行桥接，使模型能够"可视化地思考"如何完成任务。
- **数据采集平台**：基于宇树 Go2 四轮足机器人，配备 Hesai XT32 激光雷达（10Hz）、5 个 1920×1080 相机（150°视场角，覆盖 360°，10Hz）、IMU/GNSS（500Hz），通过 ROS2 与 PTP 时间同步采集数据。
- **数据集规模**：60 个场景（含十字路口、人行道、地铁入口等室内外场景），每段 300 秒、10Hz 采样，总计 175K 帧（5 小时）、875K 图像、约 5.25M 个 3D 边界框、875K VQA 对。
- **CoT 四步推理流程**（核心创新）：
  1. **环境感知**：描述整体场景上下文（天气、时间、场景类型等）。
  2. **关键主体分析**：分析静态道路特征与可移动物体，引入深度信息实现 3D 空间理解。
  3. **运动决策推理**：引入**多选格式**，将未来轨迹和动作决策抽象为两个元状态——Servo status（KEEP/ACCELERATE/DECELERATE/STOP）和 Path status（RIGHT TURN/LEFT TURN/STRAIGHT/IDLE），以提高推理的准确性与一致性。
  4. **轨迹预测输出**：输出结构化的未来 3 秒航点（6 个轨迹点，0.5s 间隔）。
- **标注生成**：使用 GPT-4.1 分步生成 VQA 推理，经规则校验与人工专家复核修正，最终统一为面向规划任务的 VQA 对格式。
- **模型架构**：提出 CoT-VLN 模型，基于 Qwen2.5-VL 7B，冻结图像编码器，仅训练投影层与语言模型，采用监督微调（SFT）优化。

## 3. 实验设计

- **Benchmark 划分**：140K 训练实例（80%）与 35K 验证实例（20%），均来自 GO2 平台采集数据。
- **对比方法**：
  - **VLM 模型**：InternVL3-8B、Qwen2.5-VL、Janus-Pro、LLaVA-1.6，每种模型训练三种变体——纯语言模型（LN 模式）、多模态非推理（VLN 非推理）、多模态推理（VLN 推理，通过"think"关键词触发 CoT）。
  - **非 VLM 方法**：SparseDrive（图像端到端）和 DiffusionPlanner（结构化数据），做了适当修改（如移除 DiffusioPlanner 的车道编码）以适应数据集。
- **评估指标**：
  - **轨迹预测**：L2 距离（米），分别计算 1s、2s、3s 及平均 L2 误差。
  - **推理质量**：使用 GPT-4.1 作为自动裁判，从事实准确性、逻辑一致性和语义完整性三个维度对 CoT 推理步骤打分（1–100）。

## 4. 资源与算力

- 文中明确说明：所有模型在 **8 张 NVIDIA L40 GPU** 上训练。
- **未说明**：具体训练时长、总 GPU 时数、数据标注的人力成本与耗时。

## 5. 实验数量与充分性

- **实验组数**：4 个 VLM × 3 种训练模式 = 12 组实验 + 2 个非 VLM 基线 + 1 组 GPT-4.1 主观评测，总体实验规模较为充实。
- **充分性评估**：
  - 消融设计合理：通过 LN vs VLN 对比验证视觉信息的作用，通过非推理 vs 推理对比验证 CoT 的作用，能够有效回答"视觉是否必要、推理是否必要"的问题。
  - 对比公平性较好：同一数据集、同一训练协议、统一评估指标；非 VLM 方法做了适配性修改。
  - **不足**：仅做开环评估（open-loop），缺少闭环的实机导航验证；非 VLM 基线的适配改动较多，可能影响其性能上限；未对不同 CoT 提示策略进行敏感性分析。

## 6. 主要结论与发现

- **CoT 推理显著提升性能**：所有模型在 CoT 推理设置下均达到最佳精度，Qwen2.5-VL 表现最优，平均 L2 误差达 **0.29m**。
- **视觉与语言信息缺一不可**：无推理能力平均 L2 误差增加 **8.8%**；无视觉输入精度下降 **13.5%**，说明多模态信息对复杂空间理解任务至关重要。
- **VLM 优于传统非 VLM 方法**：CoT-VLN（Qwen2.5-VL）平均误差 0.29m，优于 SparseDrive（0.42m）和 DiffusionPlanner（0.37m），表明在开放世界场景中 VLM 凭借有效推理可生成更精确的轨迹。
- **GPT-4.1 主观评估与客观指标基本一致**：Qwen2.5-VL 主观评分最高（75.67），但也出现个别不一致（如 LLaVA-1.6 主观分低于 Janus-Pro，但在 L2 误差上反超）。

## 7. 优点

- **首创性**：首个面向四足机器人 VLN 的大规模 CoT 推理基准，填补领域空白。
- **数据规模与质量**：5.25M 3D 边界框和 875K VQA 对远超同类数据集（如表 1 所示），且提供 10Hz 高标注密度而非插值，保证细粒度；轨迹多样性与状态分布均衡性优于 SIT 和 CODa。
- **推理结构设计巧妙**：将高自由度动作空间抽象为 Servo/Path 元状态多选格式，既降低标注复杂性，又提升推理的准确性与可评估性。
- **CoT 标注质量保障**：GPT-4.1 生成 + 规则校验 + 人工复核的三级管道增强标注可靠性。
- **消融设计清晰**：LN/VLN × 推理/非推理的对比框架能清晰剥离各因素贡献。

## 8. 不足与局限

- **评估范围受限**：仅进行开环轨迹预测评估，未验证闭环导航中的实际表现；L2 误差只衡量 3 秒内短时预测，未覆盖长时规划能力。
- **平台泛化性**：数据仅来自单一机器人平台（宇树 Go2），四轮足式配置的迁移性到其他形态机器人（双足、轮式）未验证。
- **标注质量依赖 LLM 与人工**：GPT-4.1 自动标注可能存在系统性偏差，人工复核成本高，可扩展性存疑。
- **主观评估偏差风险**：以 GPT-4.1 作为裁判评估 VLM 的推理质量，可能存在偏好偏差（self-preference bias）。
- **模型训练策略简化**：仅冻结图像编码器 + 训练投影层/语言模型，未探索 LoRA、全参数微调等替代方案；未报告训练时长等算力细节，复现成本不透明。
- **应用限制**：VQA 对模式对长程导航任务（如跨楼层、多房间探索）的支持尚未验证，CoT 推理在开放动态场景中的鲁棒性需进一步测试。

（完）
