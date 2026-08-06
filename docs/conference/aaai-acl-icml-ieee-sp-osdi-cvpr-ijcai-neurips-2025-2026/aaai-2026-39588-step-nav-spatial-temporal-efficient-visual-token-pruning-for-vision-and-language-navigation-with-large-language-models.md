---
title: "STEP-Nav: Spatial-Temporal Efficient Visual Token Pruning for Vision-and-Language Navigation with Large Language Models"
title_zh: STEP-Nav：面向大语言模型视觉语言导航的空间-时间高效视觉令牌剪枝
authors: "Yantao Lu, Shiqi Sun, Ning Liu, Bo Jiang, Ying Zhang, Jinchao Chen, Chenglie Du"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/39588/43549"
tags: ["query:embodied-nav"]
score: 10.0
evidence: 面向自然语言指令的视觉语言导航任务
tldr: 视觉语言导航要求智能体在未知环境中遵循自然语言指令行动，但基于大语言模型的导航方法因密集视觉令牌带来巨大计算开销。STEP-Nav提出空间-时间高效的视觉令牌剪枝方法，去除与导航无关的视觉区域（如天空和远背景）并抑制高帧率序列中的时间冗余，同时保留关键语义信息。实验表明该方法能在保持导航精度的同时显著降低计算负担，提升VLN系统在未知环境中的高效性和泛化能力。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39588/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 842, \"height\": 946, \"label\": \"Figure\"}, {\"url\": \"assets/figures/aaai-2026-accepted/aaai-2026-39588/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1740, \"height\": 859, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39588/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1832, \"height\": 652, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39588/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 885, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39588/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1828, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/aaai-2026-accepted/aaai-2026-39588/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 884, \"height\": 301, \"label\": \"Table\"}]"
motivation: 大语言模型用于视觉语言导航时，图像序列被编码为密集视觉令牌，导致计算开销大且包含大量导航无关和时域冗余信息。
method: 提出空间-时间高效视觉令牌剪枝，剔除天空等无关区域和时间冗余帧，为大语言模型保留关键视觉令牌。
result: 在VLN任务上验证了该方法能够显著减少计算开销，同时保持导航精度和泛化性。
conclusion: STEP-Nav通过视觉令牌剪枝提升了LLM导航系统的计算效率，且不影响导航性能。
---

## Abstract
Vision-and-Language Navigation (VLN) plays a critical role in tasks of embodied AI, particularly in unseen environments following natural language instructions. Recent advancements leverage large language models (LLMs) to improve the accuracy and generalizability of VLN systems by encoding image sequences as dense token representations. However, this tokenization approach incurs substantial computational overhead due to two key inefficiencies: 1) ego-centric camera views often include navigation-irrelevant re-
gions (e.g., sky or distant backgrounds), and 2) high-frame-rate image sequences introduce temporal redundancy. To address these challenges, we propose Spatial-Temporal Efficient Visual Token Pruning (STEP-Nav), a unified frame-
work that simultaneously prunes redundant visual tokens and fine-tunes VLN models to preserve navigation performance. In particular, STEP-Nav incorporates a distance- and content-aware token evaluation mechanism to remove irrelevant tokens at the spatial level, along with temporal level similarity-based filtering to reduce redundancy across sequential frames. To ensure pruning does not harm task performance, we introduce a distortion-aware fine-tuning strategy that aligns pruned-token representations with their full-token
counterparts while maintaining navigation accuracy. Experiments on the R2R and RxR benchmarks using Navid-CE and
NavGPT-2 as base models demonstrate that STEP-Nav preserves over 95% of the performance while reducing 66.7% of tokens, outperforming existing token pruning baselines.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究背景**：视觉语言导航（VLN）是具身智能中的关键任务，要求智能体在未知环境中遵循自然语言指令进行导航。近年来，基于大语言模型（LLM）的 VLN 方法（如 Navid-CE、NavGPT-2）通过将图像序列编码为密集视觉令牌（visual tokens）来提升导航精度与泛化能力。
- **核心问题**：密集令牌表示带来巨大的计算开销，主要源于两类冗余：
  1. **空间冗余**：第一视角相机图像中包含大量与导航无关的区域（如天空、远处背景），这些区域对导航决策贡献很低，却占用处理资源。
  2. **时间冗余**：高帧率图像序列中相邻帧高度相似，重复处理产生不必要的计算负担。
- **整体含义**：本文旨在通过视觉令牌剪枝，在保持导航性能的同时显著降低 LLM-VLN 系统的计算成本，从而提升其在实时或资源受限场景下的可部署性。

## 2. 方法论：核心思想、关键技术细节、公式与算法流程

### 2.1 总体框架
提出 **STEP-Nav（Spatial-Temporal Efficient Visual Token Pruning）**，统一框架同时进行：
- **空间级令牌剪枝**：在单帧图像内移除不重要的视觉令牌；
- **时间级序列剪枝**：删除跨帧冗余的帧；
- **失真感知微调**：通过对齐剪枝前后表示，确保导航性能不因剪枝而显著下降。

### 2.2 空间级图像令牌剪枝
- **内容感知分数**：利用 ViT 多头自注意力权重衡量令牌相关性：
  \[
  \gamma^{content}(p_i^{(j)}) = \frac{1}{N}\sum_{k=1}^{N} A(p_i^{(j)}, p_i^{(k)})
  \]
- **距离感知分数**：通过 RGB-D 图像获取深度信息，赋予近距离物体更高优先级：
  \[
  \gamma^{distance}(p_i^{(j)}) = \frac{1}{\bar{d}(p_i^{(j)}) + \epsilon}
  \]
- **最终重要性得分**：
  \[
  \gamma_i^{(j)} = \alpha \cdot \gamma^{content}(p_i^{(j)}) + (1-\alpha) \cdot \gamma^{distance}(p_i^{(j)})
  \]
  （\(\alpha=0.5\)）
- **剪枝方式**：保留得分最高的 Top-K 令牌，并采用多样性感知过滤避免过度剪除某些区域。

### 2.3 时间级序列令牌剪枝
- **帧间相似度计算**：对每帧图像提取全局描述子（平均池化的 patch 嵌入），计算相邻帧余弦相似度：
  \[
  Sim(I_t, I_{t-1}) = \frac{\langle f_t, f_{t-1}\rangle}{\|f_t\|\|f_{t-1}\|} > \tau \implies \text{drop } I_t
  \]
- **关键帧保留机制**：对高运动差异帧或与指令转换对齐的帧强制保留；可选地利用里程计先验动态调整阈值 \(\tau\)。

### 2.4 失真感知微调框架
- **目标函数**：
  \[
  L_{total} = L_{pruned}^{nav} + \lambda \cdot L_{dist}
  \]
- **失真损失**（对齐剪枝后表示与全令牌表示）：
  \[
  L_{dist} = \frac{1}{M}\sum_{i=1}^{M} \|g_{\theta_f}(I_i) - g_{\theta_p}(I_i)\|_2^2
  \]
- **训练策略**：从预训练的全令牌 VLN 模型初始化剪枝模型参数，联合微调剪枝模块与策略头；剪枝阈值作为超参数周期性更新。

### 2.5 算法流程（Algorithm 1 文字描述）
1. 初始化空序列 \(F_{pruned}\)；
2. 对当前帧 \(I_t\) 分块生成令牌 \(T_t\)；
3. 计算每个令牌的内容得分与距离得分，融合为 \(\gamma_j\)；
4. 选择 Top-K 令牌构成剪枝后的令牌集，并计算嵌入 \(f_t\)；
5. 计算 \(f_t\) 与上一帧 \(f_{t-1}\) 的相似度，若低于阈值 \(\tau\) 则保留该帧嵌入，否则丢弃；
6. 拼接保留的帧嵌入得到剪枝特征；
7. 同时计算全令牌特征，计算总损失 \(L_{total} = L_{nav} + \lambda\|f_{pruned}-f_{full}\|^2\)；
8. 反向传播更新参数，预测下一动作。

## 3. 实验设计

### 3.1 数据集与基准
- **模拟环境**：
  - **R2R**（基于 Matterport3D / Habitat）
  - **RxR**（跨语言、更长指令的基准）
  - 分为**离散图结构环境**（MP3D 模拟器）与**连续环境**（Habitat 模拟器）
- **真实环境**：自建室内场景（会议室、卧室、办公室走廊），使用 Scout-Mini 平台 + Azure Kinect DK 相机获取 RGB-D 数据。

### 3.2 基础模型
- **Navid-CE**：基于视频的 LVLM，用于连续环境；
- **NavGPT-2**：基于 LLM 的导航模型，评估了两种 LLM 规模：
  - FlanT5-XL（1.5B）
  - FlanT5-XXL（5B）

### 3.3 对比方法
- **Random**：随机剪枝令牌；
- **ToMe (Token Merging)**：轻量级令牌合并方法；
- **VisionZip**：基于注意力响应与相似度合并的剪枝方法；
- 以及**未剪枝的完整模型（100% tokens）**作为上界参考。

### 3.4 主要实验设置
- 在 R2R 训练集（10,819 条轨迹）上训练，在 R2R val-unseen（1,839 条）和 RxR val-unseen（1,517 条）上评估；
- 剪枝比例：66.7%、77.8%、88.9%，另有固定 85% 的 LLM 规模对比实验；
- 真实环境实验采用 77.8% 剪枝比例；
- 评估指标：SR、OS、SPL、TL、NE。

## 4. 资源与算力

- **原文未明确说明**使用的 GPU 型号、数量、训练时长或能耗等具体算力信息。
- 仅提及训练策略沿用 Navid-CE 的设置（DAgger 式 rollout 生成非 oracle 轨迹合并训练），但未给出硬件细节。
- 需要指出：**论文在资源消耗方面缺乏量化报告**，这影响了对其实际计算效率提升的精确评估。

## 5. 实验数量与充分性

### 5.1 实验组数
- **模拟环境 R2R**：
  - Navid-CE 上 3 种剪枝比例（66.7%、77.8%、88.9%）× 4 种方法（Random、ToMe、VisionZip、STEP-Nav）；
  - NavGPT-2 FlanT5-XL 上同样 3 种比例 × 4 种方法。
- **模拟环境 RxR**：Navid-CE 上 3 种剪枝比例 × 4 种方法。
- **不同 LLM 规模**：固定 85% 剪枝比例，在 FlanT5-XL 与 FlanT5-XXL 上对比 4 种方法。
- **真实环境**：3 个场景 × 4 种方法，剪枝率 77.8%。

### 5.2 充分性与客观性
- **优点**：
  - 覆盖多种剪枝率，验证不同压缩强度下的稳定性；
  - 跨数据集（R2R 与 RxR）评估泛化性；
  - 跨模型（Navid-CE、NavGPT-2）与跨 LLM 规模验证通用性；
  - 包含真实环境实验，增强说服力。
- **不足**：
  - **没有明确的消融实验**（例如：仅空间剪枝、仅时间剪枝、是否有失真感知微调等），无法清晰量化各组件贡献；
  - 真实环境场景数量有限（3 个），且未说明指令复杂度和轨迹长度分布；
  - 对比方法中缺少与更多近期 SOTA 剪枝方法的比较；
  - 未报告误差棒或重复实验统计显著性。

## 6. 主要结论与发现

- 在 Navid-CE 上，剪枝 66.7% 令牌时，STEP-Nav 保留了原模型 **超过 95% 的性能**（以 SPL、NE、OS、SR 衡量）。
- 与 ToMe 相比，在 88.9% 剪枝率下，OS 从 36.8% 提升到 46.2%，SPL 从 25.9% 提升到 33.2%。
- 与 VisionZip 相比，在 Navid-CE 88.9% 剪枝率下，SPL 提升 0.3%，SR 提升 2.5%。
- 在 NavGPT-2 上，85% 剪枝率下：
  - FlanT5-XL：SR 保持 66.3%（原 69.9%），SPL 保持 56.0%（原 58.9%）；
  - FlanT5-XXL：SR 保持 69.6%（原 73%），SPL 保持 58.4%（原 61.1%），均优于 VisionZip。
- 在 RxR 零样本迁移中，STEP-Nav 同样保持较高性能，优于对比的剪枝方法。
- 在真实环境（会议室、卧室、办公室走廊）中，剪枝 77.8% 后仍保留超过 95% 的原始成功率，验证了 sim-to-real 迁移能力。

## 7. 优点

- **问题刻画精准**：明确指出现有 LLM-VLN 系统中空间冗余和时间冗余两个计算瓶颈，并结合 VLN 场景特性设计剪枝策略。
- **空间-时间联合剪枝**：不同于通用 VLM 剪枝方法，提出距离感知（利用深度） + 内容感知（注意力）的融合评分，能有效剔除“视觉显著但导航无关”的区域。
- **时间冗余处理**：通过帧级余弦相似度过滤重复帧，并保留关键转换帧，兼顾效率与信息完整性。
- **保真微调策略**：提出失真感知损失（对齐剪枝前后中间表示），在压缩输入的同时维持策略性能，思路具有通用性。
- **实验维度丰富**：覆盖两个数据集、两种基础模型、多种剪枝率、多种 LLM 规模及真实环境，证明方法泛化性较强。
- **代码算法描述清晰**：Algorithm 1 给出了完整流程，便于复现。

## 8. 不足与局限

- **缺乏消融实验**：未单独评估空间剪枝、时间剪枝、蒸馏损失各模块的贡献，无法确定性能保持主要来自哪个设计。
- **算力信息缺失**：未报告 GPU 型号、数量、训练时间、吞吐量等，难以评估方法在计算效率上的实际优势。
- **基准和方法覆盖有限**：对比的剪枝方法仅包含 Random、ToMe、VisionZip，缺少如 DynamicViT、EViT、SPViT 等更多基准；LLM 也仅测试 FlanT5 系列。
- **真实实验规模较小**：真实环境只有 3 个室内场景，指令与轨迹多样性不足，可能存在场景偏差。
- **深度信息依赖**：空间剪枝依赖 RGB-D 输入，限制了在无深度传感器场景下的直接适用性。
- **超参数敏感**：\(\alpha\)、\(\tau\)、\(\lambda\) 等超参数需要人工设定和周期调整，自适应能力有限。
- **未考虑指令文本冗余**：仅剪枝视觉令牌，对文本分支的冗余（如已通过区域对应的指令）未作处理，作者在结论中也承认这是未来工作。

（完）
