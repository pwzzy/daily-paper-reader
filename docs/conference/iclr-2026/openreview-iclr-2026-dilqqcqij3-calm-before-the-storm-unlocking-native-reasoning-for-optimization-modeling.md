---
title: "CALM Before the STORM: Unlocking Native Reasoning for Optimization Modeling"
title_zh: CALM Before the STORM：释放优化建模的原生推理能力
authors: "Zhengyang Tang, Zihan Ye, Chenyu Huang, Xuhan Huang, Chengpeng Li, Sihang Li, Guanhua Chen, Ming Yan, Zizhuo Wang, Hongyuan Zha, Dayiheng Liu, Benyou Wang"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=DILQqCQIJ3"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 面向数学规划/优化建模任务提出CALM，在大型推理模型原生推理模式中引入专家干预修正，直接对应LLM驱动的数学建模需求。
tldr: 传统域适应方法不能发挥现代大型推理模型的优势，在非反思数据集上直接微调收益有限。CALM提出在模型原生推理模式中，由专家干预者识别推理缺陷并进行轻量修正，渐进式把大推理模型适配到优化建模任务。这种纠正式适配能有效解锁其原生推理潜力，比传统微调更符合现代推理模型的特性，为自动化优化建模提供了新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统优化建模域适应方法不能利用大型推理模型的多步推理能力，直接微调非反思数据增益有限。
method: 提出CALM，在大型推理模型原生推理模式下由专家干预者发现缺陷并进行轻量修正，渐进适配优化建模任务。
result: 该方法能有效提升现代LRM在优化建模上的表现，优于对传统非反思数据进行直接微调。
conclusion: 说明面向推理模式的纠正式适配比传统微调更适合自动化优化建模。
---

## Abstract
Large Reasoning Models (LRMs) have demonstrated strong capabilities in complex multi-step reasoning, opening new opportunities for automating optimization modeling. However, existing domain adaptation methods, originally designed for earlier instruction-tuned models, often fail to exploit the advanced reasoning patterns of modern LRMs --- In particular, we show that direct fine-tuning on traditional non-reflective datasets leads to limited gains. To fully leverage LRMs’ inherent reasoning abilities, we propose **CALM** (Corrective Adaptation with Lightweight Modification), a framework that progressively refines LRMs within their native reasoning modes for optimization modeling tasks. In CALM, an expert intervener identifies reasoning flaws and provides concise corrective hints, which the LRM incorporates to produce improved reasoning trajectories. These interventions modify fewer than 2.6% of generated tokens, but generate high-quality data for soft adaptation through supervised fine-tuning. The adapted model is then further improved through reinforcement learning. Building on CALM, we develop **STORM** (Smart Thinking Optimization Reasoning Model), a 4B-parameter LRM that achieves a new state-of-the-art average accuracy of 68.9% across five popular optimization modeling benchmarks, matching the performance of a 671B LRM. These results demonstrate that dynamic, hint-based data synthesis both preserves and amplifies the native reasoning patterns of modern LRMs, offering a more effective and scalable path towards expert-level performance on challenging optimization modeling tasks.

---

## 论文详细总结（自动生成）

# CALM Before the STORM：释放优化建模的原生推理能力——论文详细总结

## 1. 核心问题与整体含义

- **研究背景**：大型推理模型（LRM）展现出强大的多步推理能力，为自动化优化建模打开了新的可能。然而，传统领域适配方法源自早期指令微调模型，未能发挥现代 LRM 的推理优势。
- **关键观察**：作者实验发现，直接在传统非反思（non-reflective）数据集上进行微调，对现代 LRM 而言收益有限。这是因为这类数据不包含模型自身的推理过程，无法引导其原生推理模式。
- **研究问题**：如何在优化建模任务中真正解锁和利用 LRM 的原生推理能力？
- **核心贡献**：提出 **CALM**（纠正式适配 + 轻量修改）框架，让模型在其原生推理模式内被专家渐进式纠正，进而训练得到 **STORM**——一个仅 4B 参数的推理模型，在 5 个优化建模基准上取得 68.9% 的平均准确率，可与 671B 的超大推理模型匹敌。

## 2. 方法论

### 2.1 核心思想

- **不同于传统监督微调**的目标：传统方法对模型输出期望答案，CALM 并不要求直接拟合标准答案，而是通过**专家干预者的轻量纠正**，引导模型在自身推理模式下产出改进后的高质量推理轨迹。
- **纠正式适配**：保留模型的原生推理过程和风格，只针对推理中的缺陷给出方向性提示，再由模型自行修正、生成更优轨迹。

### 2.2 技术流程（分阶段）

1. **推理轨迹生成**：让 LRM 在优化建模任务上以原生推理模式进行推理，输出含多步思考的轨迹。
2. **专家干预**：专家（人或自动化评估器）审查推理轨迹，发现其中存在缺陷的位置，并给出**轻量修正提示**（concise corrective hints）。
3. **轻量修改特征**：干预所修改的 token 占总生成 token 的**比例低于 2.6%**，即干预是高度局部化的，不改动整体推理风格。
4. **生产高质量训练数据**：LRM 结合修正提示生成改善后的推理轨迹，这批优质数据构成软适配的监督微调数据集。
5. **监督微调（SFT）**：在高质量修正轨迹上进行监督微调，使模型内化被纠正后的推理方式。
6. **强化学习（RL）进一步提升**：经 SFT 适配的模型再通过强化学习进行优化，增强稳定性和泛化能力。

### 2.3 最终产物

- 基于 CALM 方法训练得到 **STORM**（Smart Thinking Optimization Reasoning Model），参数规模 4B。

## 3. 实验设计

- **Benchmark**：在“五个流行的优化建模 benchmark”上评测（论文正文未逐个列出具体名称）。
- **对比方法**：
  - 传统直接微调（在非反思数据上）——被证明收益有限。
  - 671B 超大 LRM——STORM 以 4B 参数取得与其相当的平均性能。
- **关键指标**：优化建模任务的平均准确率。

## 4. 资源与算力

- **原文未明确披露**具体 GPU 型号、卡数、训练时长等细节。只能从模型规模（4B）推断所需资源相对 671B 级别模型更低，但无法量化对比。
- **提示**：若需复现，算力配置信息有待向作者索取或查阅完整技术报告。

## 5. 实验数量与充分性

- **实验组数**：基于提供摘要，可确认的实验维度包括——
  - 5 个 benchmark 上的总体性能对比；
  - CALM 训练流程 vs. 传统非反思数据直接微调的对比；
  - SFT 之后经 RL 进一步提升（消解了各阶段贡献）。
- **充分性评估**：
  - **积极方面**：横跨 5 个公开基准、纵向消解 SFT 与 RL 两个训练阶段，并与 671B 超大模型对比，形成了较有力的性能论证。
  - **局限**：文本未提及消融实验中关于专家干预密度、提示形式、数据规模等超参数敏感性分析；也未比较 CALM 相对其他推理模式适配方法（如拒绝采样微调、蒸馏等）的优越性。因此，论文结论方向可信，但细节层面的实验充分性在摘要可见范围内有限。

## 6. 主要结论与发现

- 直接微调非反思数据集无法有效唤醒 LRM 的推理能力，收益有限。
- CALM 通过“专家发现缺陷 → 轻量修正提示 → 模型自行修正”的动态合成数据方式，能在保留模型原生推理模式的前提下生成高质量训练数据。
- 轻量修改（仅低于 2.6% token）就足以产生高质量监督信号，是一种高性价比的数据合成策略。
- 经 CALM + RL 训练出的 4B STORM 模型，以远小于 671B 的参数规模达到了同等级平均准确率（68.9%），验证了纠正式适配方法在优化建模任务上的有效性与可扩展性。
- 动态、基于提示的数据综合，比静态非反思数据更适合现代 LRM 的领域适配。

## 7. 优点

- **理念先进**：直接针对现代 LRM 的“原生推理模式”进行适配，避免了传统方法破坏模型推理风格的问题。
- **干预成本低**：<2.6% token 的修改就能得到高质量数据，数据合成效率极高。
- **效果显著**：4B 模型追平 671B 模型，展示出轻量纠错式适配的巨大潜力，推理时成本大幅降低。
- **方法架构清晰**：SFT + RL 两阶段递进，流程可复现、易于迁移到其他推理密集型任务。
- **问题重要**：优化建模是运筹学与 LLM 结合的关键应用场景，该工作直面了真实需求。

## 8. 不足与局限

- **Benchmark 细节不清**：摘要只提“五个流行的优化建模 benchmark”，未列出具体名称与任务分布，难以评估覆盖面是否均衡（线性规划/整数规划/约束满足等）。
- **基线不够充足**：未与现有最强的优化建模专用模型或适配方法充分比较，只对比了 671B 推理模型的直接表现，缺少与已有 SoTA 的横向对比细节。
- **算力信息披露不足**：未提及训练 STORM 所需 GPU 与时长，外界无法估算资源门槛。
- **泛化性存疑**：只聚焦优化建模任务，不能证明 CALM 方法能泛化到其他推理领域等。自然语言任务上的表现待验证。
- **专家干预实现未展开**：干预者是纯人工还是自动化？“human-in-the-loop”的成本、可扩展性瓶颈，文中未说明。
- **部署偏差风险**：68.9% 的准确率意味着仍有近三分之一的基准任务失败，真实复杂优化建模问题能否落地仍需谨慎评估。

---

（完）
