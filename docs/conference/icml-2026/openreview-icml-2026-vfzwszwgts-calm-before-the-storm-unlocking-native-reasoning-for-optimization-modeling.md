---
title: "CALM Before the STORM: Unlocking Native Reasoning for Optimization Modeling"
title_zh: 风暴前的CALM：释放优化建模的原生推理能力
authors: "Zhengyang Tang, Zihan Ye, Chenyu Huang, Xuhan Huang, Chengpeng Li, Sihang Li, Guanhua Chen, Ming Yan, Zizhuo Wang, Hongyuan Zha, Dayiheng Liu, Benyou Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/e1880509e56400b9c3d5f01fc6c21a3f27e87ee1.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 面向自动化优化建模的大型推理模型微调
tldr: 针对直接在大语言模型上微调已成文的运筹学解答会提升简单题却损害难题、干扰模型自身解题方式的问题，本文提出CALM方法。该方法先让基础推理模型尝试优化建模，在检测到首个错误时插入简短提示，让模型自我纠正。实验表明该方法在困难案例上优于直接微调。工作为自动化优化建模的后训练策略提供了更稳健的方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 直接微调运筹学解答会提升简单题却损害难题，干扰模型原生解题方式。
method: 提出CALM，让模型先尝试建模，在首个错误处插入轻量提示进行纠正式适应。
result: 在困难优化建模案例上优于直接微调，提升整体建模性能。
conclusion: 为大型推理模型自动化优化建模的后训练提供了稳健策略。
---

## Abstract
Large Reasoning Models (LRMs) create new opportunities for automating optimization modeling, but they also make post-training more delicate. In this task, strong performance often requires the model to formulate the problem, write solver code, run it, inspect the output, and revise when needed. We show that directly fine-tuning LRMs on already written-out Operations Research (OR) solutions can improve easier cases while hurting harder ones, suggesting that this training signal can interfere with the model's own way of solving the task. We therefore propose **CALM** (*Corrective Adaptation with Lightweight Modification*), which lets the base LRM attempt the problem first, then inserts a short hint at the first detected mistake and lets the model continue from there. These hints modify fewer than 2.6\% of generated tokens. The corrected solutions are used for supervised fine-tuning and then reinforcement learning, producing **STORM**, a 4B optimization-modeling specialist that reaches 68.9\% macro-average accuracy across five benchmarks and matches 671B DeepSeek-R1-0528. Under a matched hard-benchmark control, CALM also yields stronger final RL performance than direct distillation baselines that train on complete teacher-generated solutions from much stronger models. Overall, for this task, local repair of the base model's own solution is more effective than full teacher-solution replacement. Code and models are available at \url{https://github.com/tangzhy/STORM}.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 文本主体为 OpenReview 的浏览器验证页面，未包含论文正文；以下总结主要依据论文元数据与摘要。未在可获取内容中出现的细节，将明确标注为“未说明”。

## 1. 核心问题与整体含义

- **研究背景**：大型推理模型（LRMs）为自动化优化建模带来新机会，但后训练更微妙。优化建模通常要求模型完成“问题建模 → 编写求解器代码 → 运行 → 检查输出 → 必要时修正”的完整流程。
- **核心问题**：直接在已经写好的运筹学（OR）解答上微调 LRM，会提升简单案例，却损害困难案例。这说明完整教师解答的训练信号可能干扰模型自身原有的解题方式。
- **整体含义**：论文试图为 LRM 的自动化优化建模后训练提供更稳健策略，即不直接替换模型的完整解法，而是对其自身解法进行局部修复。

## 2. 方法论：CALM 与 STORM

- **核心思想**：提出 **CALM**（Corrective Adaptation with Lightweight Modification，轻量修改的纠正式适应）。
- **关键流程**：
  - 先让基础 LRM 自主尝试优化建模问题；
  - 检测其首个错误；
  - 在首个错误处插入一个简短提示；
  - 让模型从该处继续生成，形成纠正后的解；
  - 将纠正解用于监督微调（SFT），再用于强化学习（RL）；
  - 最终得到 **STORM**，一个 4B 的优化建模专家模型。
- **轻量性**：这些提示只修改不到 **2.6%** 的生成 token。
- **与直接蒸馏的区别**：CALM 是对基础模型自身解的局部修复，而不是用更强模型生成的完整教师解进行全量替换。论文认为，对这种任务而言，局部修复比完整教师解替换更有效。

## 3. 实验设计

- **任务场景**：自动化优化建模 / 运筹学问题求解。
- **Benchmark**：在 **五个 benchmark** 上评估，报告 **macro-average accuracy**；具体 benchmark 名称未在可获取文本中说明。
- **主要结果**：STORM 达到 **68.9% macro-average accuracy**，与 **671B DeepSeek-R1-0528** 匹配。
- **对比方法**：
  - 直接在已成文 OR 解答上微调 LRM；
  - 直接蒸馏基线：使用更强模型生成的完整教师解训练；
  - 在匹配的困难 benchmark 控制下，比较 CALM 与直接蒸馏的最终 RL 性能。
- **控制设置**：摘要提到“matched hard-benchmark control”，说明作者尝试在困难基准上进行匹配比较。

## 4. 资源与算力

- 可获取文本中**未说明** GPU 型号、数量、训练时长、总计算量等算力信息。
- 仅能知道：
  - STORM 是一个 **4B** 模型；
  - 训练流程包含 **SFT 和 RL**；
  - 对比对象包括 **671B DeepSeek-R1-0528**，但它主要是性能参照，不代表训练算力。
- 因此，无法从现有信息评估其训练成本、可复现性和环境影响。

## 5. 实验数量与充分性

- 从摘要可见：
  - 使用 **五个 benchmark** 评估；
  - 做了 macro-average 汇总；
  - 设置了 matched hard-benchmark control；
  - 对比了直接微调、直接蒸馏等基线；
  - 训练流程包含 SFT 和 RL。
- 但可获取内容**未提供**：
  - 具体数据集名称与规模；
  - 消融实验数量；
  - 统计显著性、重复次数、方差；
  - 不同基座模型、提示策略、错误检测方式的敏感性分析。
- 因此，仅凭摘要无法判断实验是否充分、是否完全客观公平。不过，matched control 与强教师蒸馏对比表明作者具有一定的公平比较意识。

## 6. 主要结论与发现

- 直接在完整 OR 解答上微调，会出现“简单题变好、难题变差”的现象。
- CALM 在困难案例上优于直接微调。
- 在匹配的困难 benchmark 控制下，CALM 的最终 RL 性能强于直接蒸馏完整教师解的基线。
- STORM 以 4B 规模达到 68.9% macro-average accuracy，匹配 671B DeepSeek-R1-0528。
- 总体结论：对优化建模任务，局部修复基础模型自身解，比完整教师解替换更有效。

## 7. 优点

- **保留原生推理方式**：不强行让模型模仿完整教师解，减少对自身解题路径的干扰。
- **轻量高效**：提示只修改不到 2.6% 的生成 token，干预成本低。
- **方法简洁**：首个错误处插入短提示，易于理解，也便于与 SFT、RL 结合。
- **困难案例表现更好**：针对直接微调损害难题的问题提出改进。
- **小模型表现突出**：4B STORM 匹配 671B 模型，显示较强效率优势。
- **开源可复现**：摘要提供代码和模型链接。

## 8. 不足与局限

- **正文缺失**：当前提供内容主要是验证页，无法验证完整方法、公式、算法细节和实验表格。
- **错误检测机制未知**：CALM 依赖检测“首个错误”，但摘要未说明检测器、验证器或规则是否可靠，以及误检时的影响。
- **提示设计敏感**：短提示的措辞、插入位置和时机可能影响最终性能，摘要未做敏感性分析。
- **任务范围有限**：主要面向优化建模 / OR，能否泛化到其他推理任务未知。
- **Benchmark 覆盖不透明**：只知五个 benchmark，未列名称，无法判断是否存在领域或难度偏差。
- **公平性仍需全文验证**：与 671B 模型比较的是 macro-average accuracy，不等同于全面能力等价，也不清楚推理成本与设置是否完全对齐。
- **算力与复现信息不足**：未说明 GPU、训练时长、超参数等，限制成本评估和复现。
- **统计严谨性未知**：缺少重复实验、显著性检验和消融细节，结论稳健性需进一步确认。

（完）
