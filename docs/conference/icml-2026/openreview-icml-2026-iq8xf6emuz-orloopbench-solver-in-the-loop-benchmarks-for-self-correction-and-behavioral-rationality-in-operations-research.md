---
title: "ORLoopBench: Solver-in-the-Loop Benchmarks for Self-Correction and Behavioral Rationality in Operations Research"
title_zh: ORLoopBench：面向运筹学自纠错与行为理性的求解器在环基准
authors: "Ruicheng Ao, David Simchi-Levi, Xinshang Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/16a0193aa4e71ffe6c921ac0081a66b525eea017.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 面向运筹学的求解器在环LLM不可行模型修复基准
tldr: 现有LLM基准多把运筹学视为从问题描述到求解器代码的一次性翻译，忽略了实践者通过检查不可约不可行子系统迭代修复模型的诊断循环。本文将该修复过程形式化为求解器在环的马尔可夫决策过程，每次动作触发求解器重执行与IIS重算，提供确定性可验证反馈。作者发布包含LP/MILP修复实例的ORLoopBench基准套件。该工作为评估LLM在运筹优化建模中的自纠错与行为理性提供了新基准。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM基准把运筹学当作一次性翻译，忽略了检查不可行子系统并迭代修复模型的诊断循环。
method: 将不可行模型修复形式化为求解器在环的马尔可夫决策过程，动作触发求解器重执行与IIS重算，并构建ORLoopBench基准。
result: 发布包含5362个LP/MILP修复实例的ORDebug等基准组件。
conclusion: 为评估LLM在运筹优化建模中的自纠错能力与行为理性提供了可验证基准。
---

## Abstract
Operations Research practitioners debug infeasible models through an iterative process: inspecting Irreducible Infeasible Subsystems (\textbf{IIS}), identifying constraint conflicts, and repairing formulations until feasibility is restored. Existing LLM benchmarks mostly treat OR as one-shot translation from problem descriptions to solver code, omitting this diagnostic loop. We formalize infeasible-model repair as a solver-in-the-loop Markov Decision Process in which each action triggers solver re-execution and \textbf{IIS} recomputation, yielding deterministic, verifiable feedback. We introduce \textbf{ORLoopBench}, a benchmark suite with two components: \textbf{ORDebug} releases 5,362 LP/MILP repair instances, while \textbf{ORBias} evaluates closed-form operational decision rationality across inventory settings. Solver-verified RLVR training enables an 8B model to surpass frontier APIs on LP repair (95.3\% vs 92.4\% RR@5), improves diagnostic behavior, and transfers to MILP repair. The same evaluation exposes semantic drift in whole-model code regeneration: feasible regenerated MILPs can solve the wrong problem. Process-level evaluation with solver oracles enables targeted training for reliable OR self-correction.

---

## 论文详细总结（自动生成）

# ORLoopBench 论文中文总结

> 说明：提供的 PDF 提取文本实际为 OpenReview 验证页，未包含论文正文；以下总结主要依据给出的元数据与 Abstract，未提及的信息不作臆测。

## 1. 核心问题与整体含义

- **研究动机**：运筹学（OR）实践者在模型不可行时，通常不是一次性改完，而是迭代调试：检查不可约不可行子系统（IIS），定位约束冲突，反复修复模型直至恢复可行性。
- **现有基准不足**：已有 LLM 基准多把 OR 建模视为“从问题描述到求解器代码”的一次性翻译任务，忽略了实践中的诊断—修复循环。
- **整体含义**：论文主张应评估 LLM 在 OR 建模中的**自纠错能力**与**行为理性**，并将不可行模型修复形式化为一个可验证的求解器在环过程。
- **论文定位**：提出 **ORLoopBench**，面向运筹学自纠错与行为理性的求解器在环基准；据元数据为 ICML-2026 Accepted，评分 9.0。

## 2. 方法论：核心思想与关键技术细节

- **核心思想**：将不可行模型修复形式化为**求解器在环的马尔可夫决策过程（solver-in-the-loop MDP）**。
- **交互流程（文字化算法）**：
  - 模型观察当前模型 / 约束 / IIS 等信息；
  - 模型采取修复动作；
  - 动作触发求解器重新执行；
  - 若仍不可行，重新计算 IIS；
  - 模型基于新的 IIS 反馈继续修复；
  - 重复直至可行或达到预算。
- **反馈特性**：每次动作都产生**确定性、可验证的求解器反馈**，而非仅依赖文本相似度或人工评分。
- **关键组件**：
  - **ORDebug**：发布 5,362 个 LP/MILP 修复实例。
  - **ORBias**：评估库存设置中的闭式运营决策理性。
- **训练方法**：采用 **Solver-verified RLVR 训练**，即利用求解器验证信号进行可验证奖励强化学习。
- **评估视角**：强调**过程级评估**与求解器 oracle，用于诊断行为分析和针对性训练；同时检查“整模型代码再生成”中的语义漂移问题。

## 3. 实验设计

- **基准套件**：ORLoopBench，包含两个组成部分：
  - **ORDebug**：5,362 个 LP/MILP 修复实例。
  - **ORBias**：库存场景中的闭式运营决策理性评估。
- **任务场景**：
  - LP 修复；
  - MILP 修复；
  - 库存设置下的运营决策理性。
- **对比与评估对象**：
  - 经过 solver-verified RLVR 训练的 **8B 模型**；
  - **前沿 API 模型**；
  - 整模型代码再生成方法；
  - 诊断行为与迁移能力。
- **主要指标**：LP 修复上的 **RR@5**，原文未在摘要中展开其定义。
- **未明确信息**：具体使用了哪些 frontier API、求解器类型、提示设计、预算设置、数据划分等，摘要未给出。

## 4. 资源与算力

- 论文摘要与元数据中**未明确说明**使用的 GPU 型号、数量、训练时长、总算力或能耗。
- 仅可知训练/评估涉及一个 **8B 模型**，但具体训练基础设施、并行策略、训练步数等均未提供。
- 因此，无法从现有材料总结算力开销，也无法判断复现所需资源规模。

## 5. 实验数量与充分性

- 从摘要可识别出至少覆盖以下实验维度：
  - LP 修复；
  - MILP 修复；
  - ORBias 库存决策理性；
  - 诊断行为分析；
  - RLVR 训练效果；
  - 整模型代码再生成的语义漂移分析。
- **数据规模**：ORDebug 包含 5,362 个 LP/MILP 修复实例，规模较大。
- **充分性判断**：
  - 优点：使用求解器验证反馈，实验信号较客观；覆盖修复与行为理性两个维度。
  - 局限：仅凭摘要无法知道消融实验数量、随机种子、统计显著性、超参数搜索、不同求解器/预算下的稳健性。
  - 公平性：8B 模型与前沿 API 的对比是否在相同提示、预算、工具权限下进行，摘要未说明，需看全文。
- 总体而言，实验设计方向合理，但现有信息不足以完全评估其充分性与公平性。

## 6. 主要结论与发现

- **8B 模型可超过前沿 API**：在 LP 修复任务上，经 solver-verified RLVR 训练的 8B 模型达到 **95.3% RR@5**，高于前沿 API 的 **92.4% RR@5**。
- **诊断行为改善**：训练后模型的诊断行为有所提升。
- **迁移能力**：LP 修复训练可迁移到 **MILP 修复**。
- **语义漂移风险**：整模型代码再生成可能产生“可行但解错问题”的 MILP，即模型生成了可行模型，却对应错误的问题语义。
- **过程级评估价值**：使用求解器 oracle 的过程级评估，可支持针对性的训练，从而提升 OR 自纠错的可靠性。

## 7. 优点

- **贴近真实 OR 工作流**：将不可行模型修复形式化为求解器在环 MDP，而非一次性翻译。
- **反馈可验证**：每次动作触发求解器重执行与 IIS 重算，反馈确定且可验证。
- **基准设计有层次**：ORDebug 关注 LP/MILP 修复，ORBias 关注运营决策理性。
- **训练信号可靠**：Solver-verified RLVR 利用求解器验证结果作为奖励，减少主观评估偏差。
- **发现有意义**：揭示小模型可超过前沿 API，并暴露整模型再生成的语义漂移问题。
- **强调过程评估**：推动 OR LLM 评估从最终答案正确性转向诊断与修复过程。

## 8. 不足与局限

- **正文信息缺失**：提供的 PDF 文本为验证页，无法核实方法细节、实验设置与理论推导。
- **算力未说明**：未报告 GPU 型号、数量、训练时长等，复现成本不透明。
- **实验覆盖有限**：主要围绕 LP/MILP 修复与库存决策，是否覆盖其他 OR 领域未知。
- **对比基线不明确**：前沿 API 的具体模型、版本、调用方式、预算控制均未在摘要中说明。
- **指标定义缺失**：RR@5 等关键指标未展开，影响结果解读。
- **场景简化风险**：ORBias 的闭式运营决策理性可能无法完全代表真实业务中的复杂约束与不确定性。
- **依赖求解器 oracle**：过程级评估和训练依赖反复调用求解器，可能带来计算成本与工程限制。
- **语义漂移未解决**：论文暴露了整模型代码再生成可能解错问题，但摘要未给出完整解决方案。

（完）
