---
title: "OptiVer: Unleashing the Power of LLMs for Optimization Modeling via Dual-Side Verification"
title_zh: OptiVer：通过双侧重验证释放LLM在优化建模中的潜力
authors: "Haoyang Liu, Jie Wang, Boxuan Niu, Xiongwei Han, Mingxuan Ye, Zijie Geng, Fangzhou Zhu, Jianye HAO"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=w696Vhv5B2"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 提出LLM优化建模框架并引入结构与解的双侧验证，直接对应优化模型公式化需求
tldr: 现有LLM自动生成优化模型时常常缺少可靠验证，不检查变量和约束是否合理，也不验证生成模型解的有效性，导致建模准确率受限。OptiVer提出双侧重验证框架，分别从结构视角核验模型规范性、从解视角检验模型可行性。验证信息被反馈给LLM以迭代修正和再生成，从而提升建模正确性与可信度。该工作为自动化运筹优化建模提供了更强的质量保障机制。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 数学优化模型构建需要丰富运筹学经验，LLM自动建模过程缺少对结构与解的验证，严重影响建模精度。
method: 提出OptiVer框架，从结构侧和求解侧双重验证LLM生成的优化模型，并将验证结果反馈用于模型修正。
result: 双侧重验证能提升LLM生成优化模型的规范性和合理性，改善自动建模准确度。
conclusion: 验证驱动的自动纠错有助于让LLM更可靠地完成运筹优化建模并减少人工专家依赖。
---

## Abstract
Building mathematical optimization models is critical in operations research (OR), while it requires substantial human expertise. Recent advancements have utilized large language models (LLMs) to automate this modeling process. However, existing works often struggle to verify the correctness of the generated optimization models, without checking the rationality of the constraints and variables or the validity of solutions to the generated models. This hampers the subsequent verification and correction steps, and thus it severely hurts the modeling accuracy. To address this challenge, we propose a novel LLM-based framework with Dual-side Verification (OptiVer) from both structure and solution perspectives, thereby improving the modeling accuracy. The structure-side verification ensures that the modeling structure of the generated optimization models aligns with the original problem description, accurately capturing the problem's constraints and requirements. Meanwhile, the solution-side verification interprets and evaluates the validity of the solutions, confirming that the optimization models are logically and mathematically sound. Extensive experiments on several popular benchmarks demonstrate that our approach significantly outperforms the state-of-the-art, achieving over 20% improvement in accuracy.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：构建数学优化模型是运筹学（OR）中的关键任务，但通常依赖大量人类专家经验。近年研究开始利用大型语言模型（LLM）自动化建模，以提高效率并降低门槛。
- **核心问题**：现有 LLM 自动建模方法普遍**缺乏可靠的验证机制**，具体表现为：
  - 不检查生成模型中的变量和约束是否合理；
  - 不验证生成模型对应解的有效性；
  - 这种缺失严重制约了后续的修正步骤，导致建模准确率不高。
- **整体含义**：论文瞄准“LLM 生成优化模型”这一流程中“验证缺失”这一关键短板，提出通过结构验证与解验证的双重机制，使自动生成的优化模型更加规范、合理与可靠，从而提升 LLM 在运筹优化建模任务中的实际可用性。

## 2. 论文提出的方法论：OptiVer

- **核心思想**：提出一种基于 LLM 的**双侧重验证框架（Dual-side Verification, OptiVer）**，从“结构”和“解”两个角度对 LLM 生成的优化模型进行核验，并将验证信息反馈给 LLM，驱动其迭代修正与再生成。
- **结构侧验证（Structure-side Verification）**：
  - 检查优化模型的建模结构是否与原始问题描述一致；
  - 确保模型准确刻画了问题中的约束条件和需求；
  - 主要解决“模型是否规范、是否忠实于题意”的问题。
- **解侧验证（Solution-side Verification）**：
  - 对模型求解得到的解进行解释与评估；
  - 检验解是否合理、可行，以及模型在逻辑和数学上是否自洽；
  - 主要解决“模型是否可解、解是否有效”的问题。
- **流程说明（文字化）**：
  1. LLM 根据自然语言问题描述生成候选优化模型；
  2. 对该模型同时执行结构侧验证与解侧验证；
  3. 汇总两侧验证中发现的问题和修正建议；
  4. 将验证反馈重新输入给 LLM，迭代修改模型，直至验证通过或达到预设轮次；
  5. 输出最终优化模型及其有效解。
- 论文未在摘要中公开具体公式、验证规则实现细节或迭代轮次设置。

## 3. 实验设计

- **Benchmark**：实验基于“多个流行基准”（several popular benchmarks），但摘要未列出具体基准名称。
- **数据集 / 场景**：未明确说明覆盖哪些运筹问题类别（如生产调度、路径优化、资源配置等）。
- **对比方法**：
  - 与最先进（state-of-the-art, SOTA）方法进行对比；
  - 未在摘要中给出具体对比模型名称。
- **主要指标**：建模准确率（accuracy）。
- 实验结果显示：OptiVer 相比 SOTA 方法在准确率上提升超过 **20%**。

## 4. 资源与算力

- 论文提供的文本（摘要）中**未提及任何算力信息**，包括：
  - GPU 型号与数量；
  - 训练或推理时长；
  - 模型规模（如参数量的具体数值）；
  - 求解器类型或计算资源消耗。
- 因此，无法从当前材料中对资源与算力进行量化总结。若要评价其工程可行性，需要查看论文全文的“实验设置”或“实现细节”部分。

## 5. 实验数量与充分性

- 从摘要可见，实验至少覆盖了“多个基准数据集”以及“与 SOTA 的对比”，且给出了总体准确率提升幅度。
- **未明确的信息**：
  - 具体实验组数（如不同问题类型分别多少组）；
  - 是否进行了消融实验（如只使用结构侧验证、只使用解侧验证与双侧重验证的效果对比）；
  - 是否测试了不同 LLM 后端、不同模型规模或不同提示策略；
  - 是否报告方差、多次运行的稳定性或统计显著性检验。
- **充分性评价**：由于可获得的文本仅为摘要，无法判断实验是否充分、客观、公平。原则上，“多个流行基准”+“SOTA 对比”属于较常见的实证设置，但缺少消融与敏感性分析，降低了结论的可信度；建议在论文全文中核查实验细节。

## 6. 论文的主要结论与发现

- LLM 自动生成优化模型时，**仅靠生成能力而不加验证无法保证建模质量**。
- 从**结构侧**与**解侧**同时进行验证，能够有效捕捉模型中的两类错误：
  - 结构性错误（变量、约束与题意不符）；
  - 逻辑/数学性错误（模型不可解或解不合理）。
- 将验证结果反馈给 LLM 进行迭代修正，可以显著提升优化建模的准确性。
- OptiVer 在多个流行基准上明显优于现有 SOTA 方法，准确率提升超过 20%。
- 验证驱动的自动纠错机制，有助于减少对人工专家的依赖，使 LLM 更可靠地完成运筹优化建模任务。

## 7. 优点

- **创新点明确**：提出“双侧重验证”概念，同时兼顾建模的结构规范性与求解层面的数学合理性，弥补了现有 LLM 建模流程中验证环节的空白。
- **可解释性潜力强**：结构侧验证把模型与原始问题描述对齐，解侧验证关注解的可行性与逻辑合理性，两种验证互为补充，比单一验证更全面。
- **迭代闭环设计**：验证信息不只用于“检查”，还反馈给 LLM 修正模型，形成“生成—验证—修正—再生成”的闭环，符合实际多轮建模场景。
- **效果显著**：在多个基准上相比 SOTA 提升超过 20%，说明方法改进幅度可观。
- **实用价值高**：目标直指减少人工专家依赖，对 OR 领域应用 LLM 具有现实意义。

## 8. 不足与局限

- **信息不完整**：当前文本仅为摘要，缺少对验证机制的详细展开（如结构验证的具体规则、解验证如何判断有效性、修正反馈如何构造）。
- **实验细节缺失**：
  - 未给出具体 benchmark 名称与问题类型，难以判断覆盖范围；
  - 未交代对比方法的完整名单与配置；
  - 未报告消融实验、鲁棒性分析以及失败案例；
  - 未提供时间/轮次效率或额外计算开销。
- **资源与算力未披露**：无法评估方法在实际部署中的计算成本。
- **潜在偏差风险**：
  - 验证规则可能由人工设计或基于特定假设，迁移到新问题域时可能引入偏向；
  - 若评价数据集与验证规则同源，可能产生过拟合效应；
  - 解侧验证依赖求解器，对不可解或大规模非凸问题可能失效。
- **应用限制**：
  - 方法效果可能受限于 LLM 本身对复杂运筹语义的理解能力；
  - 仅通过摘要无法确认框架是否适用于混合整数非线性、随机优化等复杂模型类型；
  - 在缺乏正式数学符号库或外部工具集成时，结构验证较难自动化。
- **结论强度有限**：基于摘要宣称的 20% 提升，尚需阅读全文验证统计显著性与跨任务一致性和公平性。

（完）
