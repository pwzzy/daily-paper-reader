---
title: "$A_2$DEPT: Large Language Model–Driven Automated Algorithm Design via Evolutionary Program Trees"
title_zh: A₂DEPT：基于进化程序树的大语言模型驱动自动算法设计
authors: "Bin Chen, Shouliang Zhu, Beidan Liu, Yong Zhao, Tianle Pu, Huichun Li, Zhengqiu Zhu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a84031f7a4918d98ffcd600af11109e4cbd28ab9.pdf"
tags: ["query:llm-agent-or"]
score: 8.0
evidence: 基于进化程序树的大语言模型驱动组合优化自动算法设计
tldr: 为组合优化问题设计启发式通常依赖大量领域专家经验，近期基于大语言模型的自动启发式设计虽能自主生成组件，却因强制固定算法模板而局限于组件级调优，缺乏系统级算法表达能力。论文提出A₂DEPT，将大语言模型视为系统级算法设计者，通过进化程序树进行开放式的求解器合成。方法突破刚性模板约束，实现更灵活的系统级算法搜索。该工作拓展了LLM在组合优化自动算法设计中的能力边界。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 组合优化启发式设计依赖专家经验，现有LLM自动启发式设计受固定模板限制，只能做组件级调优。
method: 提出A₂DEPT，把LLM视为系统级算法设计者，用进化程序树实现开放式求解器合成。
result: 突破刚性模板约束，实现更灵活的系统级算法表达与搜索。
conclusion: 拓展了LLM在组合优化自动算法设计中的能力边界。
---

## Abstract
Designing heuristics for combinatorial optimization problems (COPs) is a fundamental yet challenging task that traditionally requires extensive domain expertise. Recently, Large Language Model (LLM)-based Automated Heuristic Design (AHD) has shown promise in autonomously generating heuristic components with minimal human intervention. However, most existing LLM-based AHD methods enforce fixed algorithmic templates to ensure executability, which confines the search to component-level tuning and limits system-level algorithmic expressiveness. To enable open-ended solver synthesis beyond rigid templates, we propose Automated Algorithm Design via Evolutionary Program Trees (A$_2$DEPT), which treats LLMs as system-level algorithm architects.
A$_2$DEPT explores the vast program space via a tree-structured evolutionary search with hybrid selection and hierarchical operators, enabling iterative refinement of complete algorithms.
To make open-ended generation practical, we enforce executability with a lightweight program-maintenance loop that performs feedback-driven repair.
In experiments, A$_2$DEPT consistently outperforms state-of-the-art baselines across standard and highly constrained benchmarks, reducing the optimality gap by an average of 9.8\%. Our work implies that system-level algorithm synthesis is a viable and scalable paradigm for LLM-driven optimization.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 正文提取结果为 OpenReview 浏览器验证页，未包含论文全文；以下总结主要依据论文摘要与元数据。凡材料未给出的实验、算力与复现细节，均明确标注为“未说明/无法判断”。

## 1. 核心问题与整体含义（研究动机和背景）

- 论文关注组合优化问题（COPs）中的启发式算法设计。传统上，这类设计高度依赖领域专家经验，成本高且难以规模化。
- 近期基于大语言模型（LLM）的自动启发式设计（AHD）已能自动生成启发式组件，减少人工干预。
- 但现有 LLM-based AHD 方法通常强制使用固定算法模板，以保证生成程序可执行，这导致搜索空间被限制在“组件级调优”，缺乏“系统级算法表达”。
- A₂DEPT 的整体含义在于：将 LLM 从组件生成器提升为系统级算法架构师，通过开放式求解器合成突破刚性模板限制，拓展 LLM 在组合优化自动算法设计中的能力边界。

## 2. 方法论：核心思想与关键技术

- 核心思想：提出 A₂DEPT（Automated Algorithm Design via Evolutionary Program Trees），把完整算法表示为程序树，并用 LLM 在进化搜索中生成、修改和组合算法，实现系统级算法设计。
- 关键技术细节：
  - 使用树结构进化搜索探索庞大的程序空间。
  - 采用混合选择策略与层次化算子，对完整算法进行迭代精炼。
  - 不依赖固定算法模板，允许更开放的求解器合成。
  - 引入轻量级程序维护循环，通过反馈驱动修复，保证开放生成程序的可行性/可执行性。
- 算法流程可概括为：
  1. 将候选算法编码为程序树；
  2. LLM 基于任务描述、历史反馈和当前程序生成或修改算法；
  3. 评估候选算法的可执行性与优化性能；
  4. 通过混合选择保留优质个体；
  5. 使用层次化算子产生新候选，支持节点级、子树级或系统级变异/组合；
  6. 通过程序维护循环对错误或不可执行程序进行反馈修复；
  7. 迭代搜索，最终输出性能最佳的完整算法。
- 材料未给出显式数学公式或伪代码，因此无法进一步复现具体选择概率、算子设计或修复策略。

## 3. 实验设计

- 场景：组合优化问题中的自动算法/启发式设计。
- 基准：摘要称在“标准基准”和“高度约束基准”上进行验证，但未给出具体数据集名称、问题类型、实例规模或约束形式。
- 对比方法：与 state-of-the-art baselines 对比，但未列出具体基线方法名称。
- 评价指标：主要报告最优性差距（optimality gap），并称平均降低 9.8%。
- 由于缺少全文，无法确认是否使用统一评估协议、相同时间/调用预算、相同硬件条件等。

## 4. 资源与算力

- 论文摘要与元数据未说明使用的 GPU 型号、数量、训练/推理时长。
- 未说明 LLM 调用成本、程序评估次数、进化迭代代数或总预算。
- 由于方法涉及 LLM 生成与反馈修复，实际算力开销可能主要来自 LLM 推理和候选程序评估，但当前材料无法量化。
- 因此，资源与算力部分无法从现有信息中总结。

## 5. 实验数量与充分性

- 摘要仅表明在两类基准上验证：标准基准与高度约束基准。
- 未说明具体数据集数量、问题实例数量、重复实验次数、消融实验、敏感性分析或统计显著性检验。
- 因此无法判断实验组数是否充分。
- 公平性方面：未提供基线配置、预算控制、评估协议和随机种子等信息，无法核实对比是否完全公平。
- 元数据中 ICML-2026 接收与 score 8.0 表明评审对工作有一定认可，但这不能替代对实验细节的独立判断。

## 6. 主要结论与发现

- A₂DEPT 在标准与高度约束基准上一致优于现有最先进基线。
- 平均降低最优性差距 9.8%。
- 系统级算法合成是 LLM 驱动优化中可行且可扩展的范式。
- 突破固定模板约束后，方法能够实现更灵活的系统级算法搜索。
- 该工作拓展了 LLM 在组合优化自动算法设计中的能力边界。

## 7. 优点

- 问题定位清晰：指出已有 LLM-based AHD 受固定模板限制，只能做组件级调优。
- 方法具有范式创新：将 LLM 视为系统级算法架构师，而非单纯组件生成器。
- 搜索机制设计较合理：树结构进化、混合选择、层次化算子有助于在开放程序空间中迭代精炼完整算法。
- 关注可执行性：轻量程序维护循环通过反馈修复，缓解开放式生成中程序不可运行的问题。
- 实验信号积极：在标准和高约束场景中均报告优于 SOTA，并给出平均 9.8% 的最优性差距降低。

## 8. 不足与局限

- 当前材料缺少

- 当前材料缺少具体实验细节、基线名称、数据集配置、预算控制、消融实验与统计检验等信息，因此无法独立验证其性能优势是否稳健。
- 方法层面的潜在局限：开放式程序合成虽然扩大了搜索空间，但也可能带来更严重的搜索效率问题、LLM 调用成本问题，以及生成程序脆弱、过拟合基准或依赖偶然提示模式的风险。
- 程序维护循环的具体能力边界未说明：它可能主要修复语法错误、运行错误或接口不匹配，但是否能保证算法逻辑正确、约束满足、数值稳定，尚无法判断。
- 可复现性不足：未说明使用的 LLM 版本、提示词模板、超参数、随机种子、代码是否开源、程序评估环境与沙箱设置，复现难度可能较高。
- 公平性存疑：未说明 SOTA 基线是否在相同 LLM 预算、相同程序评估次数、相同时间限制或相同硬件条件下比较；若预算不一致，9.8% 的平均最优性差距降低可能被高估或低估。
- 统计严谨性不足：仅报告平均最优性差距降低 9.8%，未给出方差、置信区间、显著性检验或多次运行结果，无法判断提升是否稳定。
- 泛化性未知：论文称在标准基准与高度约束基准上验证，但未说明具体问题类型、实例规模、约束形式与分布外测试情况，因此跨问题、跨规模、跨约束的泛化能力无法判断。
- 理论保证缺失：作为进化式程序搜索方法，未说明是否提供收敛性、复杂度、最优性边界或可行性保证；这类保证在组合优化中通常较难，但至少需要经验性稳定性证据。
- 应用与安全风险：自动生成并执行程序可能涉及代码安全、资源消耗、外部依赖与不可解释算法问题；当前材料未说明沙箱、资源上限与失败处理机制。
- 评审信号有限：ICML-2026 接收与 score 8.0 说明工作受到一定认可，但这不能替代对实验细节、复现性和公平性的独立核查。

## 9. 总体评价与可信度判断

- 从摘要与元数据看，A₂DEPT 的核心贡献具有明确的范式创新：把 LLM 从“组件生成器”推进到“系统级算法架构师”，并以程序树进化搜索支撑开放式求解器合成。
- 该方向若成立，确实可能拓展 LLM 在组合优化自动算法设计中的能力边界，并对减少领域专家依赖、提升算法设计自动化程度具有潜在意义。
- 但当前可获取材料不足以支撑对其实证强度的完整判断。关键实验协议、基线配置、算力成本、消融分析、统计显著性与复现细节均缺失。
- 因此，更稳妥的评价是：这是一项问题定位清晰、方法设想有吸引力、初步结果积极的工作；但其相对现有方法的真实优势、可扩展性与可复现性，仍需依赖论文全文或代码发布进一步确认。
- 若后续全文能补充充分实验与开源实现，该工作有望成为 LLM 驱动组合优化算法设计中的一个有影响力方向；若缺少这些证据，则当前结论应被视为有前景但尚未充分验证。

（完）
