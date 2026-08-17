---
title: "SimWorld-Robotics: Synthesizing Photorealistic and Dynamic Urban Environments for Multimodal Robot Navigation and Collaboration"
title_zh: SimWorld-Robotics：为多模态机器人导航与协作合成逼真动态城市场景
authors: "Yan Zhuang, Jiawei Ren, Xiaokang Ye, Jianzhi Shen, Ruixuan Zhang, Tianai Yue, Muhammad Faayez, Xuhong He, Xiyan Zhang, Ziqiao Ma, Lianhui Qin, Zhiting Hu, Tianmin Shu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=EyOtIOmMUh"
tags: ["query:embodied-nav"]
score: 8.0
evidence: 面向多模态机器人导航的具身AI仿真平台，支持逼真动态城市场景
tldr: 针对现有具身AI仿真多集中于室内家庭场景、缺乏高逼真动态城市环境的不足，论文提出 SimWorld-Robotics 仿真平台。基于 Unreal Engine 5，该平台程序化生成无限多样、包含行人与交通系统的逼真城市场景，并支持多机器人控制与通信。它在真实感、复杂度和可扩展性上超越了以往城市仿真，为大规模多模态机器人导航与协作研究提供了可复用的实验环境。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有具身AI研究多聚焦室内家庭环境，缺少大规模逼真动态的城市仿真平台支持一般性机器人导航。
method: 基于Unreal Engine 5构建程序化城市场景生成器，加入动态行人与交通系统，支持多机器人控制与通信。
result: 该平台在真实感、复杂度与可扩展性上超越以往城市仿真，可支撑大规模多模态机器人导航与协作实验。
conclusion: 为开放式城市场景中的具身导航和协作智能体研究提供了可扩展的通用仿真基础设施。
---

## Abstract
Recent advances in foundation models have shown promising results in developing generalist robotics that can perform diverse tasks in open-ended scenarios given multimodal inputs. However, current work has been mainly focused on indoor, household scenarios. In this work, we present SimWorld-Robotics (SWR), a simulation platform for embodied AI in large-scale, photorealistic urban environments. Built on Unreal Engine 5, SWR procedurally generates unlimited photorealistic urban scenes populated with dynamic elements such as pedestrians and traffic systems, surpassing prior urban simulations in realism, complexity, and scalability. It also supports multi-robot control and communication. With these key features, we build two challenging robot benchmarks: (1) a multimodal instruction-following task, where a robot must follow vision-language navigation instructions to reach a destination in the presence of pedestrians and traffic; and (2) a multi-agent search task, where two robots must communicate to cooperatively locate and meet each other. Unlike existing benchmarks, these two new benchmarks comprehensively evaluate a wide range of critical robot capacities in realistic scenarios, including (1) multimodal instructions grounding, (2) 3D spatial reasoning in large environments, (3) safe, long-range navigation with people and traffic, (4) multi-robot collaboration, and (5) grounded communication. Our experimental results demonstrate that state-of-the-art models, including vision-language models (VLMs), struggle with our tasks, lacking robust perception, reasoning, and planning abilities necessary for urban environments.

---

## 论文详细总结（自动生成）

## 论文总结：SimWorld-Robotics

### 1. 核心问题与整体含义（研究动机与背景）

- **背景**：近年来，基础模型（Foundation Models）在通用机器人领域取得了显著进展，使机器人能够根据多模态输入在开放式场景中执行多样化任务。
- **核心问题**：现有具身 AI 研究高度集中于室内家居场景，缺乏大规模、高逼真度的动态城市仿真平台来支撑一般性机器人导航与协作研究。
- **整体含义**：为了推动通用机器人在真实复杂城市环境中落地，亟需一个兼具真实感、动态性、复杂度和可扩展性的仿真基础设施，用以系统训练与评估机器人的感知、推理、规划和协作能力。

### 2. 方法论：核心思想与关键技术细节

- **核心思想**：基于 Unreal Engine 5 构建一个程序化生成的、逼真的城市级仿真平台，SimWorld-Robotics（SWR），以弥补现有城市仿真在真实感与动态性上的不足。
- **关键技术细节**：
  - **程序化场景生成**：能够无限生成多样化的逼真城市景观，突破了以往人工设计的场景规模限制。
  - **动态元素注入**：场景中加入了行人、交通信号与车辆等动态元素，模拟真实的城市运行状态。
  - **多机器人支持**：平台支持多机器人的联合控制和相互通信，为多智能体协作研究提供基础。
  - **两个基准任务设计**：
    1. **多模态指令跟随任务**：机器人需在行人和交通干扰下，依据视觉-语言导航指令抵达目标位置，考察多模态指令理解与安全长程导航能力。
    2. **多智能体搜索任务**：两个机器人需通过通信协作，相互定位并会合，考察多智能体协作与基于具身经验的通信能力。

### 3. 实验设计

- **场景/数据集**：由 SWR 平台程序化生成的城市场景，包含行人、交通系统等动态要素，场景规模与复杂度超越以往城市仿真。
- **Benchmark 构成**：上述两项新基准任务覆盖了五个关键能力维度：
  - 多模态指令接地（grounding）
  - 大场景中的 3D 空间推理
  - 行人/交通环境下的安全长程导航
  - 多机器人协作
  - 具身通信（grounded communication）
- **对比方法**：评估了当前最先进的模型，包括多个视觉-语言模型（VLMs）。

### 4. 资源与算力

- 论文摘要及元数据中**未明确说明**具体的算力资源（如 GPU 型号、数量、训练时长等），也未提及数据集统计信息。若要评估平台训练与推理成本，需查阅论文全文或附录。

### 5. 实验数量与充分性

- 摘要仅提供结论性的实验结果：**现有 SOTA 模型（含 VLM）在上述任务中表现不佳**。
- **不足之处**：当前可见信息未包含具体实验组数、消融研究、各模型量化对比表格、成功率等指标细节。因此，从摘要层面难以全面判断实验的充分性与公平性，需依赖完整论文的评估协议和消融设置。

### 6. 主要结论与发现

- SWR 平台在**真实感、复杂度和可扩展性**上均明显超越之前的城市仿真环境，能够支撑大规模多模态机器人导航与协作实验。
- 实验表明，**当前最先进的 VLM 等模型在城市环境中仍缺乏鲁棒的感知、推理与规划能力**，无法胜任所构建的两项基准任务。
- 结论是：SWR 为开放式城市场景中的具身导航与协作智能体研究提供了可扩展、可复用的通用仿真基础设施。

### 7. 优点

- **场景逼真度高**：基于 UE5，程序化生成具有高视觉保真度的城市场景。
- **动态复杂度强**：集成行人与交通系统，更贴近真实城市环境，弥补了静态场景仿真的不足。
- **可扩展性好**：程序化生成路线绕开了手工建模瓶颈，支持无限场景变体。
- **多智能体支持**：支持多机器人控制与通信，为协作研究提供坚实基础。
- **基准设计全面**：两个任务系统覆盖了从指令理解、空间推理、安全导航到多智能体协作和具身通信的核心能力维度。

### 8. 不足与局限

- **实验细节不足**：摘要中缺少具体的量化结果（如成功率、导航误差等）以及模型对比和消融实验细节。
- **计算资源未说明**：未披露训练或评估所用的算力规模，影响复现和研究成本评估。
- **基准覆盖限制**：基准任务虽然涵盖多项核心能力，但暂未涉及人机交互、复杂社会规则或极端天气等更细粒度城市场景。
- **应用边界**：仿真到真实环境的迁移（Sim-to-Real）效果尚未在摘要中提及，城市仿真与物理世界之间仍可能存在的域差距需要进一步验证。

（完）
