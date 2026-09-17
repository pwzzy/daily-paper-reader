---
title: "Textual Stochastic Gradient Descent: Discrete Optimization of External Memory for Reasoning Language Agents"
title_zh: 文本随机梯度下降：面向推理语言智能体外存记忆的离散优化
authors: "Jian Li, Hua Huang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/20d2cc89323456d72845cfab670731be07808850.pdf"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 面向推理语言智能体外存记忆的离散优化
tldr: 现有检索增强生成把记忆当作静态或只增语料，导致噪声与冗余累积的记忆饱和，性能随时间下降。论文提出经验库优化框架，把智能体外存记忆视为容量预算下的可学习参数，并设计文本随机梯度下降这一离散优化算法来精简与重组记忆。方法在有限容量下缓解记忆饱和。该工作为智能体无需参数重训的持续学习提供了离散优化方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有RAG把记忆当作静态或只增语料，导致噪声累积的记忆饱和使性能下降。
method: 提出经验库优化框架，将外存记忆视为容量约束下的可学习参数，并设计文本随机梯度下降这一离散优化算法。
result: 在有限容量预算下精简并重组记忆，有效缓解记忆饱和问题。
conclusion: 为语言智能体无需参数重训的持续学习提供了离散优化途径。
---

## Abstract
While Large Language Models (LLMs) possess strong reasoning capabilities, enabling them to learn continuously from experience without parametric retraining remains an open challenge. Existing Retrieval-Augmented Generation (RAG) approaches typically treat memory as a static or append-only corpus, leading to "memory saturation," where accumulating noise and redundant information degrade performance over time. To address this, we propose an Experience Library Optimization framework that treats the agent's external memory, which we call the experience library, as a learnable parameter under an explicit capacity budget. We introduce Textual Stochastic Gradient Descent (TSGD), a discrete optimization algorithm that refines this library via failure-driven Add, Edit, and Delete operations. TSGD estimates "textual gradients" through self-reflection and uses a dual-verification mechanism to ensure generalization, which prevents overfitting to local errors. Empirical results on MATH and AIME benchmarks show that TSGD achieves state-of-the-art performance, improving accuracy by up to $18.7\%$ over zero-shot baselines and substantially outperforming static RAG, while keeping a compact memory footprint (compressing hundreds of experiences into $\approx 30$ high-utility rules).

---

## 论文详细总结（自动生成）

> 说明：所提供的 PDF 正文提取结果是 OpenReview 的浏览器验证页面，并非论文全文。因此以下总结主要依据所附元数据与 Abstract；未披露的细节会明确标注为“未说明/无法验证”。

## 1. 核心问题与整体含义

- **研究动机**：大语言模型具备较强推理能力，但如何让语言智能体在不进行参数重训的情况下，从经验中持续学习，仍是一个开放挑战。
- **背景问题**：现有检索增强生成（RAG）通常把记忆视为静态语料或只增不减的语料库，导致噪声与冗余信息不断累积，出现“记忆饱和”（memory saturation），使智能体性能随时间下降。
- **整体含义**：论文提出把智能体的外部记忆，即“经验库”（experience library），视为容量预算下的可学习参数，并通过离散优化来精简、重组记忆。这为语言智能体无需参数重训的持续学习提供了一条新路径。

## 2. 方法论：核心思想与关键技术

- **核心框架**：Experience Library Optimization，即经验库优化框架。
- **核心假设**：智能体的外部记忆不是静态数据库，而是可以在显式容量预算下被优化的“可学习参数”。
- **算法名称**：Textual Stochastic Gradient Descent，文本随机梯度下降（TSGD）。
- **优化方式**：TSGD 是一种离散优化算法，通过失败驱动的 **Add、Edit、Delete** 三类操作来精炼经验库。
- **文本梯度**：算法通过自我反思（self-reflection）估计“文本梯度”，用类似梯度下降的方向来指导记忆的增、改、删。
- **双验证机制**：引入 dual-verification 机制，确保更新后的经验具有泛化能力，避免过拟合到局部错误。
- **算法流程（文字概括）**：
  - 从智能体的失败案例出发；
  - 通过自我反思生成“文本梯度”；
  - 据此提出对经验库的增、改、删候选操作；
  - 使用双验证机制筛选有效更新；
  - 在容量预算约束下更新经验库，使其保持紧凑且高可用。
- **未说明内容**：论文摘要与元数据未给出具体公式、伪代码、目标函数、容量预算设定方式，以及 Add/Edit/Delete 的具体触发条件。

## 3. 实验设计

- **数据集 / 场景**：MATH 和 AIME 两个数学推理基准。
- **Benchmark**：主要衡量数学推理准确率（accuracy），同时关注记忆占用量/紧凑性（memory footprint）。
- **对比方法**：
  - Zero-shot baselines；
  - Static RAG；
  - 论文声称 TSGD 达到 state-of-the-art。
- **主要实验现象**：
  - 相比 zero-shot baseline，准确率最高提升 **18.7%**；
  - 显著优于 static RAG；
  - 能将数百条经验压缩为约 **30 条高 utility 规则**，保持紧凑记忆。
- **未说明内容**：所用基础 LLM、检索器、验证器、提示模板、容量预算具体数值、评测协议等均未在给定信息中说明。

## 4. 资源与算力

- 给定摘要与元数据中**未提及** GPU 型号、GPU 数量、训练时长、推理调用量、API 成本等算力信息。
- 因此无法评估其实际计算开销与可复现性。
- 需要注意的是，TSGD 虽然不需要参数重训，但依赖 self-reflection 与 dual-verification，可能引入额外 LLM 调用开销；这一点文中未披露。

## 5. 实验数量与充分性

- 从现有信息看，至少涉及 **MATH、AIME** 两个数据集，并对比了 zero-shot 与 static RAG。
- **未说明**具体实验组数、随机种子、方差、统计显著性检验。
- **未说明**是否进行了消融实验，例如：
  - Add / Edit / Delete 各自贡献；
  - dual-verification 的作用；
  - 容量预算敏感性；
  - self-reflection 质量对结果的影响。
- **公平性方面**：无法确认基线是否使用相同基础模型、相同检索预算、相同记忆容量。
- **总体判断**：摘要层面的结果有吸引力，但仅凭现有信息无法充分判断实验的充分性、客观性与公平性。

## 6. 主要结论与发现

- TSGD 在 MATH 和 AIME 上达到 state-of-the-art 性能。
- 相比 zero-shot baseline，准确率最高提升 **18.7%**，并显著优于 static RAG。
- 在有限容量预算下，TSGD 能有效精简并重组记忆，缓解“记忆饱和”问题。
- 可将数百条经验压缩为约 **30 条高 utility 规则**，保持紧凑记忆占用。
- 为语言智能体无需参数重训的持续学习提供了离散优化方案。

## 7. 优点

- **视角新颖**：将外部记忆从静态语料提升为容量约束下的可学习参数。
- **优化方式贴合问题**：用失败驱动的 Add / Edit / Delete 离散操作维护经验库，符合记忆管理的实际需求。
- **无需参数重训**：通过文本梯度与自我反思更新记忆，避免昂贵的模型微调。
- **防过拟合设计**：dual-verification 机制有助于避免对局部错误过拟合，提升泛化。
- **内存效率高**：强调将数百条经验压缩到约 30 条规则，有利于实际部署。
- **实验结果显著**：在数学推理基准上报告了最高 18.7% 的准确率提升。

## 8. 不足与局限

- **正文不可得**：由于 PDF 提取为验证页面，无法核实方法细节、实验完整性和公式推导。
- **任务覆盖有限**：目前仅见 MATH、AIME 等数学推理基准，跨领域、开放域或交互式任务上的泛化能力未知。
- **依赖自反思与验证**：self-reflection 和 dual-verification 可能受 LLM 自评偏差、验证器质量与额外调用成本影响。
- **实验透明度不足**：未报告算力、成本、超参数敏感性、消融实验、统计显著性和随机种子。
- **基线范围有限**：主要对比 zero-shot 与 static RAG，未说明是否与更多记忆管理、持续学习或智能体记忆方法比较。
- **长期动态评估缺失**：是否彻底解决记忆饱和、长期运行下性能是否稳定，摘要未说明。
- **潜在偏差风险**：若验证或评估依赖同一类 LLM，可能存在自我偏好或基准污染风险，文中未讨论。
- **应用限制**：虽然记忆更紧凑，但经验库维护、反思与验证流程可能增加系统复杂度和推理开销。

（完）
