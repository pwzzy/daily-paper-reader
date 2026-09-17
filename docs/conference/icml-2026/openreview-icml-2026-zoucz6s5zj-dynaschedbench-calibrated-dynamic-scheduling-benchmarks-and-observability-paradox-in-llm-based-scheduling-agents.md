---
title: "DynaSchedBench: Calibrated Dynamic Scheduling Benchmarks and Observability Paradox in LLM-based Scheduling Agents"
title_zh: DynaSchedBench：校准的动态调度基准及基于LLM的调度智能体中的可观测性悖论
authors: "Shijie Cao, Yuan Yuan, Jing Liu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0d6a4a01cd5d552e0b23228d076849fa446dc717.pdf"
tags: ["query:llm-agent-or"]
score: 7.0
evidence: 面向动态车间调度组合优化的LLM调度智能体基准
tldr: 动态柔性作业车间调度的神经组合优化研究受制于两类问题：静态基准导致过拟合，未校准的实例生成器又用随机噪声掩盖算法真实能力。论文提出DynaSchedBench诊断框架，用顺序事件空间校准器计算调度压力指数，按难度分层生成可控实例。结果表明该校准器比进化方法更高效，并揭示了基于LLM的调度智能体中存在的可观测性悖论。该工作为组合优化与LLM调度智能体提供了可诊断的评测基准。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 动态柔性作业车间调度研究中，静态基准易致过拟合，未校准生成器又用随机噪声掩盖算法真实能力。
method: 提出DynaSchedBench诊断框架，用顺序事件空间校准器计算调度压力指数，按难度分层生成实例。
result: 校准器比进化方法计算更高效，并揭示基于LLM调度智能体的可观测性悖论。
conclusion: 为神经组合优化与LLM调度智能体提供了可控、可诊断的评测基准。
---

## Abstract
Progress in neural combinatorial optimization for Dynamic Flexible Job Shop Scheduling Problem (DFJSP) is currently hindered by a methodological tension: static benchmarks encourage benchmark overfitting, while uncalibrated generators obscure algorithmic capability with stochastic noise.
To resolve this, we introduce \textbf{DynaSchedBench}, a diagnostic framework for DFJSP that rigorously controls the instance-generation process.
Instead of relying on parameter sampling, our approach utilizes Sequential Event-Space Calibrator (SESC) that computes a novel Schedule Stress Index (SSI) to stratify instances by difficulty.
We demonstrate that SESC is substantially more computationally efficient than evolutionary baselines while converging reliably to the target metrics.
The framework integrates modular components for instance generation, snapshot-based simulation, agents, evaluation, and visualization, thereby enabling rigorous testing of reactive and lookahead-based policies.
Leveraging this calibrated environment, we identify key limitations of LLM-based scheduling agents.
Specifically, in step-wise online decision-making for dynamic scheduling, we identify an ``Observability Paradox'': providing agents with oracle access to full structural information can degrade policy performance, underperforming concise information.
Furthermore, despite substantial token overhead, tool-augmented and refinement strategies fail to reliably improve performance, and most LLM agents fail to consistently surpass strong dispatching baselines—behaving more like robust heuristic approximators than superior optimizers.

---

## 论文详细总结（自动生成）

> 说明：当前提供的 PDF 提取文本为 OpenReview 验证页面，未包含论文正文；以下总结主要依据论文摘要与 Markdown 元数据，凡正文未提供的信息均作明确标注。

## 1. 论文的核心问题与整体含义

- 论文关注 **动态柔性作业车间调度问题（DFJSP）** 中的神经组合优化与基于 LLM 的调度智能体。
- 核心方法学矛盾：
  - **静态基准**容易导致“基准过拟合”，即算法在固定实例上表现好，但泛化能力不足。
  - **未校准的实例生成器**会引入随机噪声，掩盖算法真实能力，使评测结果不可靠。
- 因此，论文提出 **DynaSchedBench**，一个用于 DFJSP 的诊断式基准框架，目标是严格控制实例生成过程，使调度难度可控、可分层、可诊断。
- 整体含义：为神经组合优化和 LLM 调度智能体提供更可控、更可诊断的评测环境，并揭示 LLM 智能体在动态调度中的真实局限。
- 元数据标注该工作为 **ICML-2026-Accepted**，评分 7.0。

## 2. 论文提出的方法论

- **核心思想**：不依赖传统参数采样，而是通过 **顺序事件空间校准器（Sequential Event-Space Calibrator, SESC）** 控制实例生成过程。
- **关键指标**：提出 **调度压力指数（Schedule Stress Index, SSI）**，用于衡量实例难度，并按难度对实例进行分层。
- **算法流程（文字说明）**：
  1. 在顺序事件空间中校准实例生成过程；
  2. 计算每个实例或实例分布的 SSI；
  3. 依据 SSI 将实例按难度分层；
  4. 生成可控、可诊断的 DFJSP 实例；
  5. 在统一框架中运行快照式仿真、调度智能体、评估与可视化。
- **框架模块**：实例生成、基于快照的仿真、智能体、评估、可视化。
- **策略测试对象**：支持测试 **反应式策略（reactive policies）** 和 **前瞻式策略（lookahead-based policies）**。
- 摘要未给出显式公式或伪代码，因此无法进一步说明 SSI 的具体数学定义与 SESC 的更新规则。

## 3. 实验设计

- **场景/问题**：动态柔性作业车间调度问题（DFJSP）。
- **Benchmark**：DynaSchedBench。
- **实例生成**：使用 SESC 计算 SSI，并按难度分层生成受控实例。
- **对比方法/基线**：
  - SESC 与 **进化方法（evolutionary baselines）** 对比，评估计算效率与收敛可靠性。
  - LLM 调度智能体与 **强调度启发式基线（strong dispatching baselines）** 对比。
  - 信息条件对比：**oracle 全结构信息** vs **简洁信息**。
  - 策略增强对比：**工具增强（tool-augmented）** 与 **refinement 策略**。
- 摘要未说明具体使用了哪些公开数据集、实例规模、调度目标、评价指标细节或 LLM 模型版本。

## 4. 资源与算力

- 提供的摘要与元数据中 **未提及 GPU 型号、数量、训练时长、显存消耗或 API 调用成本**。
- 因此无法评估其计算资源规模、训练/推理成本和可复现性。
- 仅能确认：论文声称 SESC 在计算效率上显著优于进化基线。

## 5. 实验数量与充分性

- 从摘要可推断至少包含以下几类实验：
  1. SESC 与进化基线的效率与收敛对比；
  2. 基于 SSI 的难度分层实例生成；
  3. 反应式与前瞻式策略测试；
  4. LLM 智能体在 oracle 信息与简洁信息下的对比；
  5. 工具增强与 refinement 策略评估；
  6. LLM 智能体与强 dispatching 基线的对比。
- 但具体实验组数、数据集数量、消融实验规模、统计显著性检验等均未在摘要中说明。
- 因此，**无法判断实验是否充分、客观、公平**。例如，LLM 智能体表现可能受提示词、模型版本、工具设计影响，摘要未提供控制细节。

## 6. 论文的主要结论与发现

- **SESC 有效性**：SESC 比进化方法计算效率更高，并能可靠收敛到目标指标。
- **可观测性悖论（Observability Paradox）**：
  - 在动态调度的逐步在线决策中，给 LLM 智能体提供 **oracle 级别的完整结构信息**，反而可能降低策略性能；
  - 简洁信息有时表现更好。
- **LLM 调度智能体局限**：
  - 尽管存在大量 token 开销，工具增强与 refinement 策略未能可靠提升性能；
  - 大多数 LLM 智能体无法持续超越强 dispatching 基线；
  - 它们更像“鲁棒启发式近似器”，而非更优的优化器。
- **基准贡献**：DynaSchedBench 为神经组合优化与 LLM 调度智能体提供了可控、可诊断的评测基准。

## 7. 优点

- **问题动机清晰**：准确指出静态基准过拟合与未校准生成器噪声掩盖能力的问题。
- **方法有针对性**：用 SESC 和 SSI 实现实例难度校准与分层，而非简单参数采样。
- **诊断性强**：框架模块化，覆盖生成、仿真、智能体、评估与可视化。
- **评测视角有价值**：不仅比较性能，还揭示 LLM 智能体的“可观测性悖论”和工具增强的无效性。
- **基线较强**：与进化方法和强 dispatching 基线对比，有助于检验 LLM 智能体是否真正优于传统启发式。
- **结论对领域有警示意义**：提示 LLM 调度智能体可能被高估，强调需要更严谨的评测。

## 8. 不足与局限

- **正文不可得**：当前 PDF 文本为验证页面，无法核对完整方法、公式、实验细节与附录。
- **资源信息缺失**：未说明 GPU、训练时长、推理成本或 API 开销，难以评估可复现性与实际部署成本。
- **数据集与实验细节不足**：未列出具体数据集、实例规模、目标函数、评价指标和统计检验。
- **公平性风险**：LLM 智能体表现高度依赖模型版本、提示词、工具接口与 token 预算，摘要未说明这些因素是否受控。
- **结论泛化有限**：主要围绕 DFJSP，是否适用于其他组合优化或实际生产调度场景仍需验证。
- **“可观测性悖论”机制未明**：摘要只给出现象，未解释为何完整信息反而有害，可能需要更多消融与理论分析。
- **SESC 与 SSI 的设计影响未知**：SSI 如何定义、是否引入偏差、是否与真实调度难度一致，摘要未说明。

（完）
