---
title: "OPT-Engine: Benchmarking the Limits of LLMs in Optimization Modeling via Complexity Scaling"
title_zh: OPT-Engine：通过复杂度扩展评估大语言模型在优化建模中的能力边界
authors: "Yitian Chen, Cheng Cheng, Yinan Sun, Zi Ling, Dongdong Ge"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b828c0351adb1dcab728e4b2291e5f40842e13f3.pdf"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 评估LLM从线性规划到混合整数规划的优化建模能力
tldr: 大语言模型在优化建模这一需要结构化推理与精确数学表述的领域中的能力与可扩展性尚不明确。论文提出OPT-Engine，一个复杂度可量化、可控制的可扩展基准框架，覆盖十类经典运筹学问题，并从线性规划逐步扩展到混合整数规划，系统探测自动化建模与求解的极限。研究据此考察纯文本推理等方法的有效性，揭示LLM在优化建模中的能力边界。该基准为评估LLM自动化运筹优化建模提供了结构化环境。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: LLM在需要结构化推理与精确建模的优化建模任务中的能力与可扩展性尚不明确。
method: 提出OPT-Engine可扩展基准框架，涵盖十类经典运筹问题，从线性规划到混合整数规划系统扩展复杂度。
result: 用该基准考察纯文本推理等方法，揭示LLM在自动化建模与求解上的极限。
conclusion: 为评估LLM自动化运筹优化建模提供了可控复杂度的基准环境。
---

## Abstract
We investigate the capabilities and scalability of Large Language Models (LLMs) in optimization modeling, a domain requiring structured reasoning and precise formulation.  
To this end, we introduce OPT-ENGINE, an extensible benchmark framework with quantifiable and controllable complexity. OPT-ENGINE spans ten canonical Operations Research problems, systematically scaling from Linear Programming to Mixed-Integer Programming, providing a structured environment to probe the limits of automated problem formulation and solving.  
Utilizing OPT-Engine, we address three pivotal research questions.  
First, we examine whether Pure-Text Reasoning (PTR) via classical Chain-of-Thought can efficiently tackle optimization tasks, finding that PTR suffers from a critical robustness gap as task complexity increases.  
Second, we examine whether integrating external computational tools can mitigate PTR's arithmetic weaknesses and improve performance. Our results show that while such tools aid local calculations, they still fail to adhere to global optimization constraints.  
Finally, we pinpoint that for the current SOTA paradigm, Solver-integrated Reasoning (SIR), the automated formulation of constraints represents the primary bottleneck.  
These findings clarify current paradigms' limitations and provide a structured roadmap for developing next-generation LLMs for optimization modeling.  
We release our code and data to facilitate future research (https://github.com/Cardinal-Operations/OPTEngine).

---

## 论文详细总结（自动生成）

# OPT-Engine 论文总结

> 说明：当前提供的 PDF 提取文本并非论文正文，而是 OpenReview 的浏览器验证/CAPTCHA 页面。因此以下总结只能依据标题、元数据与摘要完成；涉及具体公式、实验细节、算力配置、模型列表与统计结果等内容，均无法从现有材料核实。

## 1. 核心问题与整体含义

- **研究动机**：大语言模型在优化建模这一需要结构化推理与精确数学表述的领域中的能力与可扩展性尚不明确。
- **背景**：优化建模不同于一般文本推理，它要求将自然语言问题准确转化为数学规划模型，并满足变量、目标函数与约束条件等严格形式化要求。
- **整体含义**：论文提出 OPT-Engine，试图通过复杂度可量化、可控制的基准框架，系统探测 LLM 在自动化问题建模与求解上的能力边界，为评估和开发下一代优化建模 LLM 提供结构化环境。

## 2. 方法论

- **核心思想**：构建一个可扩展基准框架 OPT-Engine，覆盖十类经典运筹学问题，并从线性规划逐步扩展到混合整数规划，以复杂度缩放方式评估 LLM 的优化建模能力。
- **关键设计**：
  - 复杂度可量化、可控制；
  - 覆盖十类经典 Operations Research 问题；
  - 从 Linear Programming 到 Mixed-Integer Programming 系统扩展；
  - 用于探测自动化问题表述与求解的极限。
- **三个核心研究问题**：
  - 纯文本推理是否足以高效处理优化任务；
  - 集成外部计算工具能否缓解算术弱点并提升表现；
  - 当前 SOTA 范式 Solver-integrated Reasoning 的主要瓶颈在哪里。
- **公式或算法流程**：摘要未给出具体公式或算法伪代码。从摘要可推断的流程是：构建十类 OR 问题模板，按复杂度从 LP 到 MIP 生成实例，让 LLM 以不同推理范式完成建模，再通过求解器或工具评估结果，并比较不同范式的表现。
- **开源**：论文声明发布代码与数据，链接为 https://github.com/Cardinal-Operations/OPTEngine。

## 3. 实验设计

- **数据集 / 场景**：使用 OPT-Engine 作为基准环境，覆盖十类经典运筹学问题。
- **Benchmark**：OPT-Engine 本身即为论文提出的可扩展基准框架。
- **复杂度设置**：从线性规划逐步扩展到混合整数规划，形成系统性的复杂度梯度。
- **对比方法 / 范式**：
  - Pure-Text Reasoning，即经典 Chain-of-Thought 驱动的纯文本推理；
  - 集成外部计算工具的方法；
  - Solver-integrated Reasoning，即求解器集成推理范式。
- **具体模型、指标、数据规模**：摘要与元数据未列出具体 LLM 模型、评价指标、问题实例数量或数据规模，无法进一步确认。

## 4. 资源与算力

- 当前摘要和元数据中**未提及** GPU 型号、GPU 数量、训练时长、推理成本或算力资源。
- 由于 PDF 提取文本为验证页面，无法判断正文是否包含相关说明。
- 因此，关于算力与资源消耗，现有材料不足以总结。

## 5. 实验数量与充分性

- 从摘要看，实验至少围绕三个研究问题展开：
  - 纯文本推理在复杂度增加下的鲁棒性；
  - 外部计算工具对算术弱点的缓解；
  - Solver-integrated Reasoning 的瓶颈定位。
- 实验覆盖十类经典 OR 问题，并包含从 LP 到 MIP 的复杂度扩展，设计上具有一定系统性。
- 但具体做了多少组实验、是否有消融实验、是否统计显著性检验、是否跨模型比较，摘要均未说明。
- 因此，实验的充分性、客观性与公平性无法仅凭现有材料判断，需要全文支持。

## 6. 主要结论与发现

- **纯文本推理存在关键鲁棒性差距**：随着任务复杂度增加，经典 Chain-of-Thought 驱动的 Pure-Text Reasoning 难以稳定处理优化任务。
- **外部计算工具有限帮助**：集成外部工具可以改善局部计算，但仍无法保证遵守全局优化约束。
- **SIR 的主要瓶颈是约束自动表述**：对于当前 SOTA 范式 Solver-integrated Reasoning，自动形式化约束是核心瓶颈。
- **总体判断**：当前范式在优化建模上仍有明显局限，论文据此提供了结构化路线图，以推动下一代面向优化建模的 LLM 发展。

## 7. 优点

- **复杂度可控、可量化**：OPT-Engine 将优化建模难度系统化，从 LP 到 MIP 形成可扩展梯度。
- **覆盖面较广**：涵盖十类经典运筹学问题，有助于评估 LLM 在不同问题结构上的泛化能力。
- **研究问题明确**：围绕纯文本推理、工具集成、求解器集成推理三类范式展开，问题意识清晰。
- **结论具有诊断性**：不仅报告性能，还指出 SIR 中约束自动表述是主要瓶颈，对后续研究有指导意义。
- **开源可复现**：发布代码和数据，有利于社区复现与扩展。

## 8. 不足与局限

- **全文不可得**：当前 PDF 提取文本为 OpenReview 验证页面，无法核实方法细节、公式、实验配置与统计结果。
- **算力信息缺失**：未说明 GPU 型号、数量、训练/推理时长，难以评估资源成本与可复现性。
- **实验细节不足**：摘要未列出具体模型、评价指标、实例数量、消融实验与显著性检验，实验充分性和公平性无法确认。
- **潜在偏差风险**：基准问题选择、复杂度定义、求解器配置、提示工程和模型版本都可能影响结果，存在基准偏差风险。
- **应用限制**：优化建模要求精确约束与全局可行性，当前 LLM 在全局优化约束上仍不可靠，实际部署可能需要人工监督与形式化验证。
- **未来方向**：需要更多真实场景、跨领域问题、系统消融和标准化评测，以更全面评估 LLM 优化建模能力。

（完）
