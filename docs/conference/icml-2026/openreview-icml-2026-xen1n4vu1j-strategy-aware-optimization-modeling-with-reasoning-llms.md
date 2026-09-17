---
title: Strategy-Aware Optimization Modeling with Reasoning LLMs
title_zh: 策略感知的推理大模型优化建模
authors: "Ruiqing Zhao, Fengzhi Li, Yuan Zuo, Rui Liu, YanSong Liu, Yunfei Ma, Fanyu Meng, Junlan Feng"
date: 2026-04-30
pdf: "https://openreview.net/pdf/de4a449b053566027dc77d2da1e5755eebaa8e5c.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 策略感知的LLM优化建模与问题形式化框架
tldr: "针对LLM虽能生成语法正确的优化程序却难以可靠选择有效建模策略、导致错误形式化与求解低效的问题，本文提出策略感知框架SAGE。该方法在数据构建与后训练中显式引入建模策略，构建求解器验证的多策略数据集，并采用监督微调加分段加权GRPO训练学生模型。在八个基准上平均pass@1由72.7提升至80.3。该工作提升了LLM在运筹优化建模中的可靠性与求解效率。"
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: LLM虽能生成语法正确的优化程序，却常难以选择有效建模策略，导致形式化错误与求解低效。
method: 提出SAGE框架，显式引入建模策略，构建求解器验证的多策略数据集，并用监督微调与分段加权GRPO训练学生模型。
result: "在八个基准上平均pass@1从72.7提升至80.3，并发现多种建模策略。"
conclusion: 显式建模策略可显著提升LLM优化建模的正确性与求解效率。
---

## Abstract
Large language models (LLMs) can generate syntactically valid optimization programs, yet often struggle to reliably choose an effective modeling strategy, leading to incorrect formulations and inefficient solver behavior. We propose **SAGE**, a strategy-aware framework that makes *Modeling Strategy* explicit in both data construction and post-training. SAGE builds a solver-verified multi-strategy dataset and trains a student model with supervised fine-tuning followed by Segment-Weighted GRPO using a composite reward over format compliance, correctness, and solver efficiency. Across eight benchmarks spanning synthetic and real-world settings, SAGE improves average pass@1 from 72.7 to 80.3 over the strongest open-source baseline. With multiple generations, SAGE discovers more distinct correct formulations and improves component-level diversity at pass@16 by 19-29%. At the largest scale, SAGE produces more compact constraint systems with 14.2% fewer constraints than the baseline, consistent with solver-efficient modeling. Overall, these results show that making *Modeling Strategy* explicit improves automated optimization modeling.  The code and data are available at https://github.com/rachhhhing/SAGE.

---

## 论文详细总结（自动生成）

# 论文总结：Strategy-Aware Optimization Modeling with Reasoning LLMs

> 说明：提供的 PDF 提取文本实际为 OpenReview 验证页面，未包含论文正文。以下总结主要基于论文摘要与元数据；涉及具体公式、实验细节、算力配置等正文信息时，将明确标注“未说明”或“无法确认”。

## 1. 核心问题与整体含义

- **研究动机**：大语言模型（LLM）已经能够生成语法正确的优化程序，但在优化建模中常常难以可靠地选择有效的**建模策略**，从而导致形式化错误和求解器行为低效。
- **核心问题**：如何让 LLM 不仅“写出合法代码”，而且能“选对建模策略”，从而提升自动优化建模的正确性与求解效率。
- **整体含义**：论文提出 **SAGE**，一个**策略感知（strategy-aware）**框架，将“建模策略”显式引入数据构建与后训练过程。其核心主张是：让建模策略显式化，可以显著改善自动化优化建模。
- **论文定位**：元数据表明该工作为 ICML 2026 Accepted，主题涉及 LLM 优化建模与问题形式化，代码和数据已开源。

## 2. 方法论：SAGE 框架

- **核心思想**：在数据构建和后训练两个阶段显式引入 **Modeling Strategy**，使模型学习“面对不同问题应选择何种建模策略”，而不仅是生成语法正确的优化程序。
- **关键流程（文字化概括）**：
  1. **多策略数据构建**：构建一个由求解器验证的**多策略数据集**，即针对优化建模任务收集或生成多种建模策略，并用求解器验证其正确性与效率。
  2. **监督微调（SFT）**：先用监督微调训练学生模型，使其具备基础建模与策略跟随能力。
  3. **Segment-Weighted GRPO**：在 SFT 后采用**分段加权 GRPO** 进行后训练，优化学生模型的策略选择与生成质量。
  4. **复合奖励设计**：奖励由三部分组成：
     - 格式合规（format compliance）；
     - 正确性（correctness）；
     - 求解器效率（solver efficiency）。
  5. **策略选择与生成**：最终模型能够生成更可靠的优化形式，并在多代生成中探索更多不同的正确建模形式。
- **技术细节限制**：摘要未给出 Segment-Weighted GRPO 的具体公式、分段加权方式、奖励函数权重、策略表示形式或算法伪代码，因此无法进一步展开公式化说明。

## 3. 实验设计

- **数据集 / 场景**：
  - 使用 **八个基准（eight benchmarks）**。
  - 覆盖 **合成设置（synthetic）** 与 **真实世界设置（real-world）**。
- **Benchmark / 评价指标**：
  - 主要指标包括 **pass@1**。
  - 多代生成场景下使用 **pass@16**，并考察 **组件级多样性（component-level diversity）**。
  - 还考察生成约束系统的紧凑程度，例如约束数量。
- **对比方法**：
  - 与 **最强开源基线（strongest open-source baseline）** 对比。
  - 摘要未列出具体基线名称、模型规模或对比系统清单。
- **主要实验设置**：
  - 八个基准上的平均 pass@1 对比。
  - 多代生成下不同正确形式数量与组件级多样性。
  - 最大规模模型下的约束系统紧凑性比较。
  - 发现多种建模策略。

## 4. 资源与算力

- 提供的摘要与元数据中**未明确说明**使用的 GPU 型号、GPU 数量、训练时长、参数量规模、数据规模或总计算开销。
- 因此无法总结具体算力资源，也无法评估训练成本与可复现性所需的硬件条件。
- 仅知道代码与数据已开源，地址为：`https://github.com/rachhhhing/SAGE`。

## 5. 实验数量与充分性

- **实验数量**：
  - 至少覆盖 **8 个基准**，包含合成与真实世界设置。
  - 包含 pass@1、pass@16、组件级多样性、约束数量等多类指标。
  - 摘要提到“发现多种建模策略”，说明可能有策略层面的分析或案例研究。
  - 但**未明确说明**是否进行了消融实验、奖励项消融、策略表示消融、模型规模消融或统计显著性检验。
- **充分性与公平性判断**：
  - 从摘要看，多基准、多指标、合成与真实场景结合，实验覆盖面较广。
  - 但对比对象仅写作“最强开源基线”，未列出具体方法，难以判断公平性。
  - 未提供随机种子、方差、置信区间、显著性检验等信息。
  - 由于正文缺失，无法确认是否存在数据泄漏、基准选择偏差或调参不公平问题。
  - 开源代码和数据有助于复现，是积极信号。

## 6. 主要结论与发现

- **核心结论**：将 **Modeling Strategy** 显式化，可以提升 LLM 自动优化建模的可靠性。
- **定量结果**：
  - 在八个基准上，平均 **pass@1 从 72.7 提升到 80.3**，超过最强开源基线。
  - 在多代生成设置下，SAGE 发现更多不同的正确形式，**pass@16 的组件级多样性提升 19–29%**。
  - 在最大规模下，SAGE 生成的约束系统更紧凑，**约束数量比基线少 14.2%**，这与求解器高效建模的目标一致。
- **定性发现**：SAGE 能够发现多种建模策略，说明策略显式化有助于模型探索和选择更优形式化方式。

## 7. 优点

- **问题切入准确**：关注 LLM 优化建模中“策略选择”而非仅仅“语法正确”，更贴近实际运筹优化建模难点。
- **方法设计有针对性**：将建模策略显式引入数据构建与后训练，避免模型仅模仿代码表面形式。
- **求解器验证机制**：多策略数据经求解器验证，提升数据可靠性与监督信号质量。
- **奖励设计较全面**：复合奖励同时考虑格式、正确性和求解效率，不只追求答案正确。
- **实验指标多维**：同时报告 pass@1、pass@16、组件级多样性和约束数量，兼顾正确性与效率。
- **开源可复现**：代码和数据公开，有利于后续研究验证与扩展。
- **结果提升明显**：平均 pass@1 提升约 7.6 个百分点，多样性提升和约束减少也具实际意义。

## 8. 不足与局限

- **信息完整性限制**：提供的文本仅为摘要和元数据，缺少正文、公式、算法细节、实验表格和附录，无法全面评估方法。
- **算力未披露**：未说明 GPU 型号、数量、训练时长和成本，复现门槛不明确。
- **基线不具体**：只提到“最强开源基线”，未列出名称、规模和配置，公平性难以独立判断。
- **消融与统计不足**：未说明是否进行充分消融，也未报告方差、显著性检验或多次运行结果。
- **奖励设计风险**：复合奖励中格式、正确性、效率的权重可能影响行为，存在奖励工程敏感性与偏差风险。
- **求解器依赖**：数据构建依赖求解器验证，可能带来计算成本，并可能使模型偏向特定求解器或问题类型。
- **泛化边界未知**：研究聚焦优化建模，是否适用于其他推理或形式化任务尚不清楚。
- **真实场景覆盖有限**：虽包含真实世界设置，但仅 8 个基准，且未说明领域分布，应用限制仍需正文验证。
- **潜在偏差风险**：多策略数据集的策略分布、基准选择、评测指标设计都可能影响结论的普遍性。

（完）
