---
title: "AR-Nav Benchmark: Augmented Reality Navigation with Vision and Language"
title_zh: AR-Nav基准：基于视觉与语言的增强现实导航
authors: "Liqi Yan, Yihao Wu, Chenyi Xu, Chao Yang, Jianhui Zhang, Pan Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38849/42811"
tags: ["query:embodied-nav"]
score: 9.0
evidence: 增强现实导航，视觉与语言结合，长期记忆用于空间智能
tldr: 针对增强现实导航在室内定位精度低、语义理解弱和长期记忆不足等问题，该文提出AR-Nav基准数据集及配套方法。其核心是增强现实视觉-语言记忆模型AR-VLM²，生成结构化且语义丰富的记忆表征，支持动态、多楼层和大规模真实场景下的导航。该基准为视觉语言导航在AR场景中的评估与长期记忆建模提供了新资源。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38849/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 579, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38849/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1827, \"height\": 793, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-38849/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1816, \"height\": 583, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38849/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1799, \"height\": 822, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38849/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 862, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-38849/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 315, \"label\": \"Table\"}]"
motivation: 现有AR导航系统在定位精度、语义理解和长期记忆方面存在不足，难以适应动态多楼层真实场景。
method: 提出AR-Nav数据集与AR-VLM²模型，生成结构化语义记忆用于增强现实导航并提供评估套件。
result: 构建了利用视觉与语言进行AR导航的基准，并通过语义长期记忆改善定位与语义理解问题。
conclusion: 该工作将视觉语言导航与长期记忆结合，推动了AR环境中空间智能研究。
---

## Abstract
Augmented Reality (AR) navigation has emerged as a transformative tool for spatial intelligence, enabling users to interactively explore complex environments through wearable and mobile AR devices. However, current AR navigation systems struggle with low indoor localization accuracy, weak semantic understanding, and limited long-term memory, which severely limits their adaptability in dynamic, multi-floor, and large-scale real-world settings. To address these challenges, we present AR-Nav benchmark, a novel dataset with corresponding suite that leverages vision and language for AR navigation. First, to construct this benchmark, we proposed an Augmented Reality Visual-Language Memory Model (AR‑VLM²), which generates structured, semantically rich, and temporally indexed representations for long-term AR navigation. Second, we design a lightweight navigation intent recommending module with hierarchical topological reasoning and language-grounded path planning, called ARN‑Pilot, enabling low-latency and personalized route selection. Third, we introduce a closed-loop AR interaction module that supports real-time multi-modal feedback, dynamic memory updates, and human-in-the-loop query refinement. Extensive experiments in indoor multi-floor and outdoor parking scenarios show that AR-Nav suite significantly outperforms state-of-the-art AR navigation methods.

---

## 论文详细总结（自动生成）

# AR-Nav Benchmark：基于视觉与语言的增强现实导航 —— 论文详细总结

## 1. 核心问题与研究动机

### 背景与问题
- **AR导航的重要性**：增强现实（AR）导航是实现空间智能的关键技术，用户通过智能手机、智能眼镜等设备获得实时环境引导。
- **现有三类AR导航范式的局限**：
  1. **标记/信标系统**（QR码、蓝牙/Wi-Fi/UWB）：依赖基础设施部署，在动态或杂乱环境中易失效；
  2. **无标记SLAM/VPS系统**（ARCore、ARKit）：大规模场景下面临漂移、遮挡和场景动态变化；
  3. **视觉-语言导航（VLN）方法**：在模拟环境中训练，泛化到真实世界困难，且计算复杂度随候选节点数二次增长，难以实时运行。
- **三大根本性缺陷**：
  - **定位精度低**：室内定位误差常超过5米，GPS/预定义地图在室内不可用或不准确；
  - **语义理解弱**：系统仅缓存短期感知数据，无法支持回顾性查询，也难以适应真实世界动态变化；
  - **长期记忆缺失**：LLM受固定上下文窗口限制，无法跨长时间保留结构化空间/时间记忆，导致关键线索频繁遗忘。

### 研究目标
构建一个**统一的视觉-语言AR导航基准（AR-Nav）**，通过结构化长期记忆、轻量级实时路径推荐和双通道交互生成，同时解决高精度定位、语义理解和长期记忆三大挑战，支持**室内多楼层、室外停车场**等大规模真实场景下的鲁棒导航。

---

## 2. 方法论

论文提出一套完整的AR导航套件，包含三个核心模块：

### 2.1 AR-VLM²：增强现实视觉-语言记忆模型
**目标**：将原始RGB-D视频流与自然语言指令转化为**结构化、语义丰富、时间索引化**的场景记忆表征。

**技术流程**：
1. **视觉编码**：每个视频帧 $v_t$ 通过视觉编码器（Video Swin Transformer）提取稠密特征图 $F_t$；
2. **区域聚类**：通过图卷积网络（GCN，2层，512维隐藏特征）在不同帧间识别同一语义区域，生成区域特征 $v^{(i)}_t$；
3. **语言编码**：导航指令经BERT/T5编码为token嵌入序列；
4. **跨模态融合**：基于cross-attention的融合模块 $\phi$，每个视觉区域特征通过注意力加权聚合文本上下文，得到融合表征 $h^{(i)}_t$：

$$h^{(i)}_t = \sum_{j=1}^{K} \alpha_{ij} \cdot l_j, \quad \alpha_{ij} = \frac{\exp(v^{(i)}_t \cdot l_j)}{\sum_{k=1}^{K}\exp(v^{(i)}_t \cdot l_k)}$$

5. **语义记忆解码**：融合表征经VLM解码器（LLaVA/BLIP-2 head）生成语义记忆嵌入 $m^{(i)}_t$；
6. **位姿索引**：每个记忆条目与SfM得到的3D位姿 $(x_t, y_t, f_t, \theta_t)$ 绑定，构成完整记忆数据库：

$$\mathcal{M} = \{(m^{(i)}_t, x_t, y_t, f_t, \theta_t)\}_{t,i}$$

7. **数据增强**：合成视点变换（$\Delta x, \Delta y, \Delta\theta$）和指令改写，提升泛化能力。

### 2.2 ARN-Pilot：轻量级导航意图推荐与路径规划模块
**目标**：将用户命令转化为实时的、个性化的导航决策。

**技术流程**：
1. **语义对齐与记忆检索**：LLM（LLaMA-7B）将用户命令 $l_{1..t}$ 与AR-VLM²生成的场景记忆对齐，基于余弦相似度检索top-k相关记忆：

$$\{m_{t,i}\}_{i=1}^{k} = \text{TopK}_{m \in \mathcal{M}} \cos(E_s(\hat{s}_t), m)$$

2. **路径候选生成**：结合检索记忆、当前轨迹和用户偏好（历史对话元数据），LLM推荐器生成排名靠前的目标与路标候选 $\{w_j\}$：

$$w_j = \arg\max_w P(w \mid \hat{s}_t, \{m_{t,i}\}, l_{1..t}, \Theta_R)$$

3. **匹配评分**：每个候选路标综合**语义一致性**和**空间可行性**打分：

$$s_j = \beta \cdot \cos(E_s(w_j), E_s(\hat{s}_t)) + (1-\beta) \cdot \text{ReLU}(d_{\max} - \|p_j - p_t\|)$$

其中 $\beta=0.6$ 权衡语义与空间权重，最终按得分排序选择最优路径，延迟控制在500ms内。

### 2.3 双通道交互合成模块
- **视觉通道**：渲染与真实环境对齐的3D箭头、样条路径和楼层指示器；
- **语音通道**：生成上下文感知的语音指令（如"Walk toward the red sign above the glass door"）；
- **闭环反馈**：支持人类在环查询优化，用户可实时提问（如"Which door should I take?"），系统针对性地检索记忆并更新AR高亮与语音回应。

---

## 3. 实验设计

### 3.1 数据集与基准
- **规模**：200个多样化真实场景（120个室内多楼层、80个室外/半室内）；
- **采样密度**：沿可行路径每≈2米设置采样点，每场景约50–70个位置；
- **视角覆盖**：每个采样点6个视角（60°间隔），构成360°全景RGB-D，另有深度图和相机位姿记录；
- **楼层数**：最多覆盖4层楼；
- **标注类型**：RGB-D视频序列、2D/3D重建地图、真实轨迹、自然语言指令（众包+专家标注，命令式+描述式）；
- **质量验证**：通过Web标注检查界面进行人工验证（Fig. 3c）。

### 3.2 对比方法（三类基线）
1. **零样本无LLM/VLM方法**：ZSON、CoW、L3MVN/V3MVN、VLFM（以及文中提及的ESC）；
2. **LLM-based方法**：LLaMa-7B、Qwen3、DeepSeek-R1、GPT-4（一次性读取全部文本描述）；
3. **VLM-based方法**：LLaVa-1.5、Qwen-VL、DeepSeek-VL2、GPT-4o（直接输入图像序列，有效帧率仅0.07 FPS）。

### 3.3 评估指标
- **描述性问题准确率**（Descriptive Question Accuracy）：空间坐标预测L2距离，15米内视为正确；
- **位置误差**（Positional Error）：预测位置与真实位置的L1距离；
- **时间误差**（Temporal Error）：时间点/时长预测的L1误差，2分钟内视为正确；
- **总体正确率**（Overall Correctness）：消融实验中将空间（<20m）和时间（<10s）阈值化为统一二进制指标。

### 3.4 主要实验结果
- 短/中/长轨迹上，描述性准确率达**0.83/0.79/0.72**，平均比最佳GPT-4o基线高出**12%以上**；
- 位置误差降至**3.4m/13.7m/25.2m**，时间误差降至**1.5s/3.3s/6.6s**；
- VLM-based方法因输入长度限制，在Medium/Long视频上无法扩展（表中标记为×），无法公平对比。

---

## 4. 资源与算力

- **论文未明确说明**GPU型号、数量、训练时长、峰值内存等具体算力信息；
- 仅提及所有实验使用3个随机种子，基线方法因计算限制仅使用单种子；
- ARN-Pilot采用LLaMA-7B推荐器，能在**500ms延迟**内完成路径选择，表明推理负载可控。

---

## 5. 实验数量与充分性

### 实验数量统计
| 实验类型 | 数量/规模 |
|---------|----------|
| 主实验（Table 1） | 3类基线 × 14种方法 × 3种轨迹长度 × 3种指标 |
| 消融实验（Table 2） | 4组（memory增强、几何融合、LLM推荐、偏好条件） |
| Top-k记忆规模实验（Table 3） | 5档（k=1,3,5,7,10） |
| 数据集覆盖 | 200个真实场景 |

### 充分性与客观性评估
- **优点**：数据集规模大（200场景）、覆盖多类型真实环境；消融实验设计合理，逐一验证核心组件贡献；报告了标准差，考虑随机种子差异；
- **不足**：
  1. **对比公平性受限**：VLM基线在Medium/Long上完全无法运行（输入长度超限），核心对比实际集中在LLM基线上；
  2. **统计力度不均**：基线仅单种子，而方法使用3种子，统计严谨性不对等；
  3. **缺乏与真实AR设备的端到端用户实验**：未报告人类用户在真实AR设备上的导航成功率、完成时间等主观/行为指标；
  4. 缺少与SLAM/VPS系统的直接对比（如表1中的基线均为VLN或LLM/VLM方法）。

---

## 6. 主要结论与发现

1. **记忆是AR导航的核心瓶颈**：显式的长期时空记忆编码（AR-VLM²）是超越纯LLM/VLM方法的关键，将语言锚定到结构化视觉区域显著提升定位精度和语义回答质量；
2. **模块化设计有效**：AR-VLM²（记忆构建）+ ARN-Pilot（规划决策）+ 交互模块（闭环反馈）三模块解耦，各组件可独立优化和替换；
3. **消融验证了设计选择的重要性**：
   - 去掉符号-几何融合（替换为朴素concat）：短序列准确率下降**16.7%**（0.78→0.65）；
   - 去掉LLM推荐器（替换为朴素相似度比较）：准确率下降**26.9%**（0.78→0.57）；
   - 去掉用户偏好条件：准确率下降**14.1%**（0.78→0.67）；
   - 去掉记忆增强（视点/指令改写）：准确率下降**6.4%**（0.78→0.73）；
4. **Top-k检索的最优规模**：k=5是召回与噪声之间最佳平衡点。

---

## 7. 方法亮点与创新

1. **三维一体的benchmark设计**：同时提供数据、方法套件和评估协议，具备标准benchmark的完整要素；
2. **AR-VLM²的双流架构设计**：将视频流和语言流通过cross-attention融合，并经VLM解码为空间锚定的语义记忆，实现"人类式记忆"的表征方式；符号-几何对齐兼顾语义与空间两个维度；
3. **ARN-Pilot的轻量级实时性**：LLM推荐 + 拓扑图建模 + 多跳子图检索，支持个性化定制的低延迟（<500ms）路径推荐；
4. **双通道交互与人类在环**：视觉（AR覆盖）+ 语音双通道同步输出，并支持用户即时发问、系统动态更新指导，形成完整闭环；
5. **360°全景采样策略**：6视点全方位采集，同时支持记忆编码和目标推荐两个下游任务；
6. **系统性消融**：每个核心设计决策都有明确的数据支撑。

---

## 8. 不足与局限性

### 实验覆盖局限
- **缺少真实AR设备部署验证**：没有报告在Hololens、Magic Leap等真实AR硬件上的主观用户体验（舒适度、认知负荷、指令可理解性），仅关注算法层面指标；
- **对比基线不完整**：未包含商业AR导航系统（如ARCore/ARKit-based VPS）或非学习的经典SLAM导航方法；
- **VLM基线对比失效**：因输入长度限制，VLM类方法在长轨迹上完全无法参与对比，削弱了"SOTA全面超越"的说服力；
- **场景多样性限制**：虽有室内外混合，但具体语言/地点文化差异、极端天气/光照条件、无障碍通道等特殊场景未涉及。

### 偏差风险
- 基线与方法统计标准不一致（单种子vs三种子），可能高估方法优势；
- LLM评判文本回答正确性引入主观偏差，虽沿用前人做法（OpenEQA），但缺少与人类评判的一致性分析；
- 消融实验使用简化的Overall Correctness阈值化指标，可能掩盖细粒度差异。

### 应用限制
- **记忆数据库规模隐忧**：每2米采样、6视角全景，大规模场景的记忆条目数量庞大，存储和检索成本未详细分析；
- **动态场景适应性**：虽然自称支持"动态环境"，但记忆一旦构建，如何高效更新/删除过期条目未详细讨论；
- **隐私与安全性**：持续记录带位姿的视觉数据涉及个人隐私和公共空间合规问题，论文未讨论；
- **LLM推荐器的可解释性**：个性化推荐依赖LLM，但推荐理由的可解释性和错误模式未分析。

---

（完）
