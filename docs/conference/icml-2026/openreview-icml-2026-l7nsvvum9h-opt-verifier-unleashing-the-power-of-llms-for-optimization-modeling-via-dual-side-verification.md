---
title: "Opt-Verifier: Unleashing the Power of LLMs for Optimization Modeling via Dual-Side Verification"
title_zh: Opt-Verifier：通过双侧验证释放LLM在优化建模中的能力
authors: "Haoyang Liu, Jie Wang, Boxuan Niu, Xiongwei Han, Yian Xu, Mingxuan Ye, Zijie Geng, Fangzhou Zhu, Tao Zhong, Mingxuan Yuan, Jianye HAO"
date: 2026-04-30
pdf: "https://openreview.net/pdf/b9f8937d4d682cfdb378b2c2ce31ddbf779d9a76.pdf"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 基于LLM的运筹优化建模自动化与双侧验证框架
tldr: 构建数学优化模型是运筹学的核心环节，但高度依赖人工专业知识；近期工作虽尝试用大语言模型自动建模，却难以验证所生成模型的正确性，既不检查约束与变量的合理性，也不验证解的有效性。本文提出OptiVer，一个基于LLM的双侧验证框架，从模型结构与求解结果两个视角对生成的优化模型进行校验并据此修正。实验表明该框架显著提升建模准确率，为LLM自动化运筹优化建模提供了可靠的验证与纠错机制，推动其实际落地。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 用LLM自动构建运筹优化模型时，现有方法难以验证生成模型的约束、变量合理性与解的有效性，严重影响建模准确率。
method: 提出OptiVer框架，从模型结构与求解结果两个视角对LLM生成的优化模型进行双侧验证，并据此开展后续修正。
result: 在优化建模任务上，双侧验证机制显著提升了生成模型的正确性与整体建模准确率。
conclusion: 为LLM自动化运筹优化建模提供了可靠的验证与纠错机制，有助于该方法在真实场景中落地。
---

## Abstract
Building mathematical optimization models is critical in operations research (OR), while it requires substantial human expertise.
Recent advancements have utilized large language models (LLMs) to automate this modeling process.
However, existing works often struggle to verify the correctness of the generated optimization models, without checking the rationality of the constraints and variables or the validity of solutions to the generated models.
This hampers the subsequent verification and correction steps, and thus it severely hurts the modeling accuracy.
To address this challenge, we propose a novel LLM-based framework with Dual-side Verification (OptiVer) from both structure and solution perspectives, thereby improving the modeling accuracy.
The structure-side verification ensures that the modeling structure of the generated optimization models aligns with the original problem description, accurately capturing the problem's constraints and requirements.
Meanwhile, the solution-side verification interprets and evaluates the validity of the solutions, confirming that the optimization models are logically and mathematically sound.
Extensive experiments on several popular benchmarks demonstrate that our approach significantly outperforms the state-of-the-art, achieving over 20\% improvement in accuracy.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，而非论文全文。因此以下总结主要依据标题、作者、摘要、TLDR 与元数据整理；凡涉及具体公式、实验表格、数据集名称、算力配置等未在可用文本中出现的内容，均无法确认，不作臆造。

## 1. 核心问题与整体含义
- **研究背景**：构建数学优化模型是运筹学（OR）的核心任务，但高度依赖人工专家知识。
- **核心问题**：近期工作尝试用大语言模型（LLM）自动完成优化建模，但现有方法难以验证生成优化模型的正确性：
  - 不检查约束与变量是否合理；
  - 不验证生成模型的解是否有效；
  - 导致后续验证与修正困难，严重损害建模准确率。
- **整体含义**：论文提出 OptiVer（标题中为 Opt-Verifier）框架，试图通过“双侧验证”提升 LLM 自动优化建模的可靠性与准确率，为该方法在真实场景落地提供验证与纠错机制。

## 2. 方法论
- **核心思想**：对 LLM 生成的优化模型进行**双侧验证**，即从“模型结构”和“求解结果”两个视角同时校验。
- **结构侧验证**：
  - 检查生成优化模型的建模结构是否与原始问题描述一致；
  - 确认其是否准确捕捉原问题的约束与需求。
- **解侧验证**：
  - 解释并评估模型求解结果的有效性；
  - 确认优化模型在逻辑与数学上是否合理、可靠。
- **流程概述**：根据摘要可概括为闭环流程：
  1. 输入自然语言问题描述；
  2. LLM 生成候选优化模型；
  3. 结构侧验证模型结构与问题描述是否对齐；
  4. 解侧验证求解结果是否有效、模型是否数学合理；
  5. 根据验证结果进行修正；
  6. 输出修正后的优化模型。
- **公式与算法细节**：可用文本中未给出具体公式、伪代码、验证器训练方式或提示词设计，无法进一步展开。

## 3. 实验设计
- **数据集 / 场景**：摘要仅称在“several popular benchmarks”上进行实验，未列出具体数据集名称、领域或场景。
- **Benchmark**：未提供具体 benchmark 名称与评价协议。
- **对比方法**：声称与 state-of-the-art 方法对比，但未列出具体基线方法。
- **评价指标**：主要提及 accuracy，并声称准确率提升超过 20%。摘要未说明该提升是相对提升还是绝对百分点提升。

## 4. 资源与算力
- 可用文本中**未提及** GPU 型号、GPU 数量、训练时长、推理成本、LLM 调用次数、求解器调用量等算力或资源信息。
- 因此无法总结其计算开销，也无法评估方法的成本效率。

## 5. 实验数量与充分性
- 摘要称进行了“extensive experiments on several popular benchmarks”，但未给出具体实验组数、数据集数量、消融实验、错误分析或人工评估细节。
- 由于缺少全文，无法判断实验是否充分、客观、公平。
- 仅可确认其声称在多个流行基准上与 SOTA 对比，并取得显著准确率提升；但无法核实基线选择、数据划分、统计显著性与复现条件。

## 6. 主要结论与发现
- 双侧验证机制能够显著提升 LLM 生成优化模型的正确性与整体建模准确率。
- 摘要声称该方法在多个流行基准上显著优于 SOTA，准确率提升超过 20%。
- 该框架为 LLM 自动化运筹优化建模提供了可靠的验证与纠错机制，有助于推动实际应用落地。

## 7. 优点
- **双视角验证**：同时从模型结构与求解结果两个层面校验，较单一验证更全面。
- **闭环纠错**：验证结果可用于后续修正，而非仅做一次性生成。
- **问题定位明确**：针对 LLM 自动优化建模中的验证瓶颈，即约束/变量合理性与解有效性。
- **效果宣称显著**：若 20% 以上准确率提升属实，则对自动化优化建模有较强推动作用。
- **应用导向**：强调可靠验证与纠错，有利于真实运筹优化场景落地。

## 8. 不足与局限
- **可用文本严重不足**：抓取到的 PDF 内容为 CAPTCHA 验证页，无法获得论文全文，因此无法核实方法细节与实验数据。
- **实验信息缺失**：未列出具体数据集、benchmark、基线方法、评价协议与实验组数，复现与公平性判断受限。
- **算力与成本未说明**：缺少 GPU、训练/推理时长、LLM 调用成本、求解器开销等信息。
- **潜在偏差风险**：基准选择、SOTA 基线选择、准确率提升定义均未说明，可能存在选择性报告风险。
- **应用限制未知**：双侧验证可能依赖 LLM 解释能力与求解器可靠性；在复杂约束、大规模问题、真实工业场景中的泛化性、鲁棒性与可扩展性尚未从可用文本中确认。
- **缺乏消融与错误分析**：无法判断结构侧验证与解侧验证各自贡献，以及错误传播和误判风险。

（完）
