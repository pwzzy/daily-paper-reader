---
title: What Makes an LLM a Good Optimizer? A Trajectory Analysis of LLM-Guided Evolutionary Search
title_zh: 什么样的LLM是好的优化器？LLM引导进化搜索的轨迹分析
authors: "Xinhao Zhang, Xi Chen, François Portet, Maxime Peyrard"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1252.pdf"
tags: ["query:llm-agent-or"]
score: 7.0
evidence: 大语言模型驱动的智能体优化系统与优化轨迹分析
tldr: 本文针对大语言模型在进化与智能体优化系统中为何有效这一问题展开研究，现有工作对其优化增益机制理解不足。作者收集了15个模型在8个任务上的优化轨迹并做大规模分析。结果表明零样本能力只能部分解释结果，强优化模型更像局部精炼者，频繁产生增量式改进。该发现揭示了LLM引导优化的内在机制，为设计更有效的智能体优化系统提供依据。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1616, \"height\": 757, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 714, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 793, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1623, \"height\": 907, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 811, \"height\": 371, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 302, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 707, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 241, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 790, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 786, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 662, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1639, \"height\": 1983, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1626, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1628, \"height\": 1030, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1252/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1526, \"height\": 1753, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 805, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 833, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 736, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 270, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 799, \"height\": 214, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1177, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1252/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1277, \"height\": 723, \"label\": \"Table\"}]"
motivation: 现有工作虽展示LLM可增强优化系统，但对其优化增益背后的机制仍缺乏理解。
method: 作者在8个任务上采集15个大语言模型的优化轨迹，对LLM引导进化搜索进行大规模分析。
result: 零样本能力只能部分解释优化结果，强优化模型表现为频繁增量改进的局部精炼者。
conclusion: 研究揭示了LLM驱动优化的行为机制，为构建更有效的智能体优化系统提供指导。
---

## Abstract
Recent work has demonstrated the promise of orchestrating large language models (LLMs) within evolutionary and agentic optimization systems. However, the mechanisms driving these optimization gains remain poorly understood. In this work, we present a large-scale study of LLM-guided evolutionary search, collecting optimization trajectories for 15 LLMs across 8 tasks. Although zero-shot problem-solving ability correlates with final optimization outcomes, it explains only part of the variance: models with similar initial capability often induce dramatically different search trajectories and outcomes. By analyzing these trajectories, we find that strong LLM optimizers behave as local refiners, producing frequent incremental improvements while progressively localizing the search in semantic space. Conversely, weaker optimizers exhibit large semantic drift, with sporadic breakthroughs followed by stagnation. Notably, various measures of solution novelty do not predict final performance; novelty is beneficial only when the search remains sufficiently localized around high-performing regions of the solution space. Our results highlight the importance of trajectory analysis for understanding and improving LLM-based optimization systems and provide actionable insights for their design and training.

---

## 论文详细总结（自动生成）

# 论文总结：什么样的 LLM 是好的优化器？LLM 引导进化搜索的轨迹分析

## 1. 核心问题与整体含义
- **研究动机**：近期研究显示，将大语言模型（LLM）编排进进化优化与智能体优化系统具有潜力，但这些系统为何能带来优化增益，其内在机制仍缺乏理解。
- **核心问题**：什么样的 LLM 才是好的优化器？LLM 在优化搜索中取得成功，究竟是因为其零样本问题求解能力，还是因为其在搜索轨迹中表现出的特定行为模式？
- **整体含义**：论文试图从“结果评价”转向“轨迹分析”，通过大规模收集和分析 LLM 引导进化搜索的过程数据，揭示 LLM 优化能力的来源，并为设计、训练和选择更有效的智能体优化系统提供依据。

## 2. 方法论
- **核心思想**：对 LLM 引导的进化搜索进行大规模轨迹分析。作者收集 15 个 LLM 在 8 个任务上的优化轨迹，比较不同模型的搜索过程与最终优化结果。
- **关键分析维度**：
  - 零样本问题求解能力与最终优化结果之间的相关性；
  - 搜索轨迹中的语义空间局部化与语义漂移；
  - 增量改进的频率与模式；
  - 解的新颖性指标是否能预测最终性能。
- **主要发现对应的行为刻画**：
  - 强优化器表现为“局部精炼者”：频繁产生增量式改进，并逐步将搜索局部化在语义空间中高性能区域附近。
  - 弱优化器表现为“大范围漂移”：语义漂移较大，偶有突破但随后停滞。
- **公式或算法流程**：给定提取文本中未包含具体公式、伪代码或完整算法流程；从摘要看，其方法更偏向实验性轨迹分析与行为统计，而非提出新的优化算法。

## 3. 实验设计
- **任务与场景**：在 8 个任务上研究 LLM 引导的进化搜索。具体任务名称、数据集名称和 benchmark 在给定提取文本中未列出。
- **模型**：收集 15 个 LLM 的优化轨迹。
- **对比对象**：
  - 横向比较不同 LLM 作为优化器时的搜索轨迹和最终优化结果；
  - 分析零样本能力与优化结果之间的关系；
  - 比较强优化器与弱优化器的行为差异；
  - 检验多种解新颖性度量对最终性能的预测能力。
- **评价指标**：最终优化结果、搜索轨迹特征、语义局部化/漂移、增量改进频率、解的新颖性等。具体指标定义在给定文本中未展开。
- **Benchmark**：未明确说明具体 benchmark 名称或标准评测套件。

## 4. 资源与算力
- 给定论文提取文本中**未明确说明**使用的 GPU 型号、数量、训练时长或推理算力。
- 由于研究涉及 15 个 LLM 在 8 个任务上的优化轨迹收集，实际算力消耗可能较高，但论文摘要与元数据未提供相关细节。

## 5. 实验数量与充分性
- **规模**：按“模型 × 任务”计算，至少有 15 × 8 = 120 组模型-任务设置；若每个设置包含多条优化轨迹，实际实验数量更多。
- **消融实验**：给定文本未提及具体消融实验设计。
- **充分性**：从模型数量和任务数量看，属于较大规模的轨迹研究，覆盖面较广。
- **客观与公平性**：由于缺少任务细节、重复次数、随机种子、统计检验和基线设置，无法完全判断实验是否客观公平；但同任务下横向比较多个 LLM 的设计，有助于控制任务差异。

## 6. 主要结论与发现
- 零样本问题求解能力与最终优化结果存在相关性，但只能解释部分方差。
- 初始能力相近的模型，可能产生截然不同的搜索轨迹和优化结果。
- 强 LLM 优化器更像局部精炼者：频繁产生增量改进，并逐渐把搜索集中在高性能解附近。
- 弱优化器则表现出更大的语义漂移：偶尔出现突破，但随后容易停滞。
- 解的新颖性本身不能预测最终性能；新颖性只有在搜索仍足够局部化、围绕高性能区域时才有益。
- 轨迹分析对于理解和改进 LLM 优化系统至关重要。

## 7. 优点
- **过程视角新颖**：不只比较最终分数，而是系统分析 LLM 引导进化搜索的轨迹，有助于揭示“为什么有效”。
- **实验规模较大**：覆盖 15 个 LLM 和 8 个任务，具备较好的模型与任务多样性。
- **发现具有反直觉性**：指出解的新颖性并不必然带来更好结果，挑战了“越新颖越好”的直觉。
- **可操作性强**：提出强优化器是“局部精炼者”，为设计提示、搜索算子和训练策略提供方向。
- **连接能力与行为**：说明零样本能力只能部分解释优化表现，强调搜索行为本身的重要性。

## 8. 不足与局限
- **信息覆盖有限**：给定提取文本仅包含摘要和元数据，缺少具体任务、数据集、benchmark、基线方法和实现细节。
- **算力信息缺失**：未报告 GPU 型号、数量、训练/推理时长，难以评估复现成本。
- **任务覆盖有限**：8 个任务虽具一定多样性，但是否能代表更广泛的优化场景仍不确定。
- **因果性有限**：轨迹分析主要揭示相关性，强优化器的“局部精炼”行为与最终性能之间是否为因果关系，尚需进一步验证。
- **新颖性度量依赖定义**：论文指出新颖性不预测最终性能，但具体度量方式及其稳健性在给定文本中未说明。
- **应用限制**：LLM 优化系统的效果可能受模型版本、提示设计、搜索算子、任务类型和计算预算影响，泛化边界仍需更多研究。

（完）
