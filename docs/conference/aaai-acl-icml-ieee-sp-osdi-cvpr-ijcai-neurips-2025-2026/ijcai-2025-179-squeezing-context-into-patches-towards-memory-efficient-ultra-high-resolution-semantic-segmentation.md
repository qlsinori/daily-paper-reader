---
title: "Squeezing Context into Patches: Towards Memory-Efficient Ultra-High Resolution Semantic Segmentation"
title_zh: 将上下文压缩进图像块：迈向内存高效的超高分辨率语义分割
authors: "(PDF |   Details)"
date: 2025-08-01
pdf: "https://www.ijcai.org/proceedings/2025/0179.pdf"
tags: ["query:semantic-map"]
score: 6.0
evidence: 内存高效的超高分辨率语义分割，是导航语义地图构建中的支撑技术。
tldr: 超高分辨率图像的语义分割面临巨大的内存开销，难以在资源受限的机器人平台上实时运行。该文提出将上下文信息压缩到图像块中的方法，在不牺牲分割精度的前提下显著降低显存占用与计算成本。实验表明该方法在超高分辨率语义分割基准上达到了接近现有最优的效果，同时具有更高的内存效率。该技术可为具身导航中的语义地图构建与场景理解提供高效支撑，但其本身并不直接解决导航任务。
source: IJCAI-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-179/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1816, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-179/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1813, \"height\": 971, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-179/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 850, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-179/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1785, \"height\": 699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/ijcai-2025-accepted/ijcai-2025-179/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 876, \"height\": 498, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 901, \"height\": 783, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 897, \"height\": 657, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 900, \"height\": 1104, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 897, \"height\": 667, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 902, \"height\": 492, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 836, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/ijcai-2025-accepted/ijcai-2025-179/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1841, \"height\": 189, \"label\": \"Table\"}]"
motivation: 超高分辨率语义分割内存开销大，限制其在机器人上的应用。
method: 把上下文信息压缩到局部图像块内，减少冗余计算与内存占用。
result: 在保持高分割精度的同时显著提升内存效率。
conclusion: 为实时高分辨率场景理解与语义地图构建提供了可行方案。
---

## Abstract
No abstract is available.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：超高分辨率（Ultra-High Resolution, UHR）图像在遥感、医学影像、自动驾驶等领域广泛存在。然而，UHR图像的语义分割面临严重的 **GPU 内存瓶颈**，难以直接输入深度学习模型进行处理。
- **核心矛盾**：现有方法在处理 UHR 图像时，普遍面临 **局部细节保留** 与 **全局上下文感知** 之间的权衡：
  - 下采样范式（Downscaling）会丢失细粒度细节，导致分割粗糙；
  - 滑动窗口推理（Stride Inference）虽保留细节，但每个 patch 的上下文信息有限，易产生预测不一致。
- **现有方法的不足**：当前主流 UHR 分割方法（如细节细化、浅深融合、全局-局部融合）多采用 **多分支编码器结构**，虽然在一定程度上兼顾了局部与全局信息，但引入了额外的计算开销和内存消耗，难以部署在资源受限的边缘设备上。
- **论文目标**：在 **单分支编码器** 内同时解决全局上下文感知和局部细节保留的问题，实现 **高精度 + 低内存占用** 的 UHR 语义分割。

---

## 2. 论文提出的方法论

### 2.1 核心思想

- 提出 **SCPSeg**（Squeezing Context into Patches），将**全局上下文信息压缩进局部 patch**，使网络在滑动窗口推理时也能感知更大范围的图像上下文。
- 采用**单分支编码器**架构，避免多分支结构带来的额外内存开销。
- 借助**超分辨率辅助任务**指导局部特征对齐，增强分割解码器对局部细节的保留能力。

### 2.2 关键模块

**（1）上下文压缩模块（Context Squeezing Module, CSM）**

- 输入为一个全局 patch \(X_G\)（尺寸 \(G \times G\)），其中心为局部 patch \(X_L\)（尺寸 \(L \times L\)）。
- 先将局部 patch 下采样为 \(X_D\)；
- 将周围的上下文区域（四个边角区域）分别堆叠（stack）并 resize，形成两路压缩上下文 \(X_C^{p1}\) 和 \(X_C^{p2}\)；
- 将压缩后的上下文与缩放后的局部 patch 拼接，得到最终输入 \(X_{CS}\)，尺寸与原始局部 patch \(X_L\) 相同。
- 公式表达：
  - \(X_D = \nabla(X_L)\)
  - \(X_C^{p1} = \nabla(\text{stack}(X_C^1, X_C^3, X_C^7, X_C^9))\)
  - \(X_C^{p2} = \nabla(\text{stack}(X_C^2, X_C^4, X_C^6, X_C^8))\)
  - \(X_{CS} = \text{cat}(X_C^{p1}, X_C^{p2}, X_L^{cs})\)

**（2）局部特征对齐（Local Feature Alignment, LFA）**

- 引入**超分辨率解码器（Super-Resolution Decoder, SRD）**作为辅助任务分支，从编码特征中恢复高分辨率局部 patch。
- 超分辨率损失 \(L_{SR}\) 使用 **L1 损失** 衡量预测高分辨率 patch 与真实局部 patch 之间的差异。
- 受限于计算资源，**不计算全图特征两两相似度**，而是在局部滑动窗口（大小为 \(k \times k\)）内计算特征自相似矩阵，然后最小化分割分支与超分分支在同一位置的相似矩阵之间的差异，得到局部特征对齐损失 \(L_{LFA}\)。
- 通过这种方式，将超分分支中的**结构信息**迁移到分割分支中，强化边缘和细节预测能力。

### 2.3 整体优化目标

- 总损失为三项损失加权求和：

\[
L = L_{CE} + w_1 \cdot L_{SR} + w_2 \cdot L_{LFA}
\]

- 其中 \(w_1 = 0.5\)、\(w_2 = 0.5\)。
- 在**推理阶段**，只使用分割分支，SRD 和 LFA 均不参与，因此**不增加推理内存开销**。

---

## 3. 实验设计

### 3.1 数据集

| 数据集 | 图像尺寸 | 训练/验证/测试 | 任务类型 |
|---|---|---|---|
| ISPRS Potsdam | 6000×6000 | 18 / 6 / 14 | 城市土地覆盖 |
| BLU | 15680×15680 | 192 / 28 / 32 (crop 2048×2048) | 城乡土地覆盖 |
| DeepGlobe | 2448×2448 | 455 / 142 / 206 | 土地覆盖 |
| Inria Aerial | 5000×5000 | 126 / 27 / 27 | 建筑物提取 |

### 3.2 对比方法

- **通用分割方法**：FCN-8s、DeepLabv3+、PSPNet、ST-UNet、UNetFormer、CF-Net、LANet、U-Net、ICNet、BiseNetv1、STDC、DANet 等；
- **UHR 专用方法**：GLNet、WiCoNet、TCNet、CascadePSP、PointRend、MagNet、ISDNet、FCtL、WSDNet、GINet、GPWFormer、PPN 等。

### 3.3 评价指标

- mIoU（mean Intersection-over-Union）
- mF1（mean F1 score）
- Acc（Overall Accuracy）
- Mem（GPU 内存占用，使用 `gpustat` 工具监控）

### 3.4 实施细节

- 基础分割器：DeepLabv3+ + ResNet-18-d8（也验证了 FCN-8s、PSPNet、SegFormer、TopFormer、LANet、DDRNet、PIDNet）
- 优化器：SGD，初始学习率 0.01，余弦退火
- 训练迭代次数：40000
- 上下文窗口大小：Potsdam/BLU/Inria 均为 G=512、L=256、D=192；DeepGlobe 为 G=1024、L=512、D=384
- Batch size：16（DeepGlobe 为 8）
- 滑动窗口大小 k=7

---

## 4. 资源与算力

- 所有实验在**单张 Nvidia RTX 4090** 上进行。
- **未明确报告训练时长**（如小时数）。
- 推理时 SCPSeg 的 GPU 内存占用约为 **1818 MB（FCN-8s 基础）** 和 **1834 MB（DeepLabv3+ 基础）**，显著低于大多数对比方法。
- 训练阶段由于包含 SRD 分支，会引入额外的计算开销，但论文未具体量化训练时延或 FLOPs。

---

## 5. 实验数量与充分性

### 5.1 实验数量

论文实验较为丰富，主要包括：

- **四个 UHR 基准数据集上的主实验**（Potsdam、BLU、DeepGlobe、Inria Aerial）；
- **多种基础分割器的通用性验证**：FCN-8s、DeepLabv3+、PSPNet、SegFormer、TopFormer、LANet、DDRNet、PIDNet 共 8 种；
- **组件消融实验**：分别验证 CSM、SRD、LFA 对性能和内存的影响；
- **超参数分析**：上下文窗口大小 G 和局部下采样尺寸 D 对性能的影响；
- **特征可视化**：展示 LFA 前后分割分支特征的差异。

### 5.2 充分性评价

- **优点**：数据集覆盖城市/乡村土地覆盖和建筑物提取，场景多样；对比方法涵盖通用分割、UHR 分割；消融实验设计清晰，验证了每个模块的贡献。
- **不足**：
  - **DeepGlobe 上未达到最优**：WSDNet 的 mIoU 为 74.1，SCPSeg 为 74.0，差距很小，但说明方法在不同数据上的优势并不完全一致；
  - **缺少训练成本对比**：未报告训练时间、参数量、FLOPs；
  - **缺少更广泛的基础结构验证**：如未在更强 backbone（ResNet-101、Swin Transformer 等）上验证；
  - **未在城市场景数据集（如 Cityscapes 的 UHR 版本）上进行验证**，泛化性有限。

---

## 6. 论文的主要结论与发现

- SCPSeg 通过**将全局上下文压缩进局部 patch + 超分引导的局部特征对齐**，以**单分支架构**实现了高精度与低内存占用的兼顾。
- 在 ISPRS Potsdam 上取得 **mIoU 87.6%**，显著优于现有 UHR 方法（GLNet 84.0%、WiCoNet 84.1%、TCNet 85.0%），同时内存占用（1834 MB）低于所有对比方法（最低为 WiCoNet 的 2014 MB）。
- 在 BLU 和 Inria Aerial 上均取得最优或接近最优的性能，且内存占用最低。
- 在 DeepGlobe 上取得了与最优方法 WSDNet 相当的结果（74.0 vs 74.1），但内存更低。
- CSM 模块可即插即用地适用于多种基础分割器，平均提升约 1.2% 的 mIoU。
- 特征可视化表明，LFA 可有效将超分分支的结构信息迁移至分割分支，改善边缘质量。

---

## 7. 优点

- **单分支架构设计新颖**：与主流多分支 UHR 方法形成鲜明对比，大幅降低内存需求。
- **CSM 设计简洁高效**：通过简单的 resize + stack 即可将全局上下文“塞进”局部 patch，避免了复杂的注意力或特征融合计算。
- **多任务学习策略合理**：SRD 作为辅助任务不参与推理，LFA 在滑动窗口内计算相似性，避免了全图计算的高昂成本。
- **推理阶段零额外开销**：辅助模块仅在训练阶段生效，保证了部署时的内存效率。
- **通用性强**：CSM 可应用于 CNN 和 Transformer 等多种骨干网络，均带来稳定增益。
- **实验覆盖面广**：四大基准数据集 + 多种对比方法 + 完整消融，整体说服力强。
- **代码开源**：提供了 GitHub 仓库，便于复现和后续研究。

---

## 8. 不足与局限

- **DeepGlobe 上并非最优**：虽然差距极小，但说明上下文压缩策略并非在所有场景中都绝对优于全图编码方法。
- **训练开销未充分讨论**：SRD 分支在训练阶段会引入额外显存和计算，论文未报告训练时的显存峰值和训练耗时，这在一定程度上弱化了“内存高效”的全面性声明。
- **上下文压缩可能引入信息损失**：CSM 将大范围上下文压缩到固定 patch 中，对于上下文极其依赖的场景（如大目标跨 patch 分布），压缩比例过大会导致上下文退化（论文图 5 的实验也验证了这一趋势）。
- **未考虑跨模态/多传感器输入**：ISPRS Potsdam 数据集包含 DSM 波段，但实验中未充分利用。
- **应用范围仍限于 2D 图像分割**：尚未扩展到视频、点云等三维场景。
- **缺乏与边缘设备实机部署的验证**：虽然声称面向边缘设备，但仅在 RTX 4090 上测试，未在真实嵌入式平台（如 Jetson）上进行速度与内存实测。

---

（完）
