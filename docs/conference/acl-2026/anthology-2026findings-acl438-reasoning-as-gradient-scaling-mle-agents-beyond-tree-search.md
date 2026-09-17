---
title: "Reasoning as Gradient: Scaling MLE Agents Beyond Tree Search"
title_zh: 推理即梯度：超越树搜索扩展机器学习工程智能体
authors: "Yifei Zhang, Xu Yang, Xiao Yang (杨潇), Bowen Xian, Qizheng Li, Shikai Fang, Jingyuan Li, Jian Wang, Minrui Xu, Yuge Zhang, Weiqing Liu, Jiang Bian"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.438.pdf"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 基于大模型智能体自动优化机器学习工程
tldr: "现有机器学习工程智能体多依赖树搜索这一无梯度优化方式，随推理能力提升其穷举式搜索效率低下。本文提出Gome智能体，将结构化诊断推理映射为梯度计算、成功记忆映射为动量、多轨迹执行映射为分布式优化，实现基于梯度的优化。在隔离外部知识的封闭协议下取得35.1%的获奖率。"
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl438/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1086, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl438/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1431, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl438/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 726, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl438/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 658, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl438/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 730, \"height\": 437, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 814, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1321, \"height\": 247, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1603, \"height\": 888, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 798, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 680, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1578, \"height\": 1461, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 796, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 801, \"height\": 184, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1346, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1510, \"height\": 1231, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 609, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 798, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 808, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 811, \"height\": 342, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl438/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 652, \"height\": 328, \"label\": \"Table\"}]"
motivation: 机器学习工程智能体普遍依赖树搜索这类无梯度优化，随推理增强其穷举搜索愈发低效。
method: 提出Gome智能体，将诊断推理映射为梯度、成功记忆映射为动量、多轨迹执行映射为分布式优化。
result: "在封闭协议下Gome在机器学习工程基准上取得35.1%的获奖率，达到先进水平。"
conclusion: 说明用梯度式推理可显著提升智能体在优化类任务上的搜索效率。
---

## Abstract
LLM-based agents for machine learning engineering (MLE) predominantly rely on tree search, a form of gradient-free optimization that uses scalar validation scores to rank candidates. As LLM reasoning capabilities improve, exhaustive enumeration becomes increasingly inefficient compared to directed updates, analogous to how accurate gradients enable efficient descent over random search. We introduce Gome, an MLE agent that operationalizes gradient-based optimization. Gome maps structured diagnostic reasoning to gradient computation, success memory to momentum, and multi-trace execution to distributed optimization. Under a closed-world protocol that isolates architectural effects from external knowledge, Gome achieves a state-of-the-art 35.1% any-medal rate on MLE-Bench with a restricted 12-hour budget on a single V100 GPU. Scaling experiments across 10 models reveal a critical crossover: with weaker models, tree search retains advantages by compensating for unreliable reasoning through exhaustive exploration; as reasoning capability strengthens, gradient-based optimization progressively outperforms, with the gap widening at frontier-tier models. Given the rapid advancement of reasoning-oriented LLMs, this positions gradient-based optimization as an increasingly favorable paradigm. We release our codebase and GPT-5 traces at: https://github.com/microsoft/RD-Agent .

---

## 论文详细总结（自动生成）

> 注：提供的提取文本主要为论文元数据与摘要，未包含正文、公式、完整实验表格细节。以下总结严格基于可见信息，并对未明确处加以标注。

# 论文总结：Reasoning as Gradient: Scaling MLE Agents Beyond Tree Search

## 1. 核心问题与整体含义

- **研究背景**：基于 LLM 的机器学习工程（MLE）智能体普遍依赖**树搜索**来寻找解决方案。树搜索本质上是一种**无梯度优化**：用标量验证分数对候选方案排序，再通过穷举式探索扩展搜索树。
- **核心问题**：随着 LLM 推理能力增强，树搜索的穷举枚举效率越来越低；相比之下，如果能够获得可靠“梯度”，定向更新会比随机/穷举搜索更高效。
- **整体含义**：论文提出应将 MLE 智能体的推理过程从“无梯度树搜索”推进到“基于梯度的优化”。这不仅是工程效率问题，也意味着当底层模型推理能力足够强时，智能体范式应从枚举候选转向方向性迭代更新。

## 2. 方法论：Gome 智能体

- **核心思想**：提出 **Gome**，一个将梯度式优化思想操作化到 MLE 智能体中的方法。它不直接对模型参数求梯度，而是把智能体的诊断、记忆和多轨迹执行过程类比为优化算法中的梯度、动量和分布式优化。
- **三个关键映射**：
  - **结构化诊断推理 → 梯度计算**：通过结构化诊断分析当前方案的问题，形成类似“梯度”的方向性改进信号，而不是仅依赖验证分数排序。
  - **成功记忆 → 动量**：将过去成功经验/方案记忆下来，作为后续更新的“动量”，避免重复探索并加速收敛。
  - **多轨迹执行 → 分布式优化**：并行或分布式地执行多条轨迹，以类似分布式优化的方式综合多个方向的信息。
- **算法流程（文字概括）**：
  1. 对当前 MLE 任务与候选方案进行结构化诊断；
  2. 根据诊断结果生成方向性改进信号，类似梯度更新；
  3. 利用成功记忆维持优化动量；
  4. 通过多轨迹执行并行探索与整合；
  5. 在封闭世界协议下迭代优化，直至达到预算限制或得到较优方案。
- **说明**：提供文本未给出具体公式、伪代码或实现细节，因此无法展开数学形式。

## 3. 实验设计

- **Benchmark**：使用 **MLE-Bench** 评估机器学习工程智能体。
- **评价指标**：主要报告 **any-medal rate**，即获得任意奖牌的比例。Gome 达到 **35.1%**。
- **实验协议**：
  - 采用**封闭世界协议**，隔离外部知识，以区分架构本身的效果与外部知识带来的增益。
  - 在**单张 V100 GPU** 上，使用受限的 **12 小时预算**。
- **对比方法**：
  - 主要对比对象是**树搜索**这类无梯度优化方法。
  - 在 **10 个不同模型**上进行 scaling 实验，观察模型推理能力变化时，树搜索与梯度式优化的相对表现。
- **可能包含的分析**：元数据中列有 17 个表格和 5 张图，说明论文可能有较多补充实验、消融或案例分析，但提供文本未展开具体内容。

## 4. 资源与算力

- **明确信息**：
  - 使用**单张 V100 GPU**。
  - 评估预算为**受限的 12 小时**。
  - 跨 **10 个模型**进行实验。
- **未明确信息**：
  - 未说明 GPU 总数量（除“单张 V100”外）。
  - 未说明训练时长、训练算力或总计算量。
  - 未说明 12 小时预算是每个任务、每组实验还是整体评估预算。
  - 未说明调用 LLM 的 API 成本、推理成本或能耗。
- **判断**：该工作主要是智能体推理/搜索评估，而非训练新模型；因此算力描述集中在评估阶段，但细节仍不完整。

## 5. 实验数量与充分性

- **从摘要可知的实验规模**：
  - MLE-Bench 主实验。
  - 10 个模型的 scaling 实验。
  - 与树搜索的对比。
- **元数据暗示**：
  - 提供文本包含 17 个表格、5 张图，说明论文可能有较丰富的补充实验、消融或统计分析。
- **充分性评估**：
  - **优点**：封闭世界协议有助于控制外部知识干扰，使架构比较更公平；固定单卡与 12 小时预算也提供了相对统一的比较条件。
  - **不足**：仅凭摘要无法确认是否报告了多次运行、随机种子、方差、显著性检验、失败案例和成本分析。基准目前只提到 MLE-Bench，覆盖范围有限。
  - **客观性**：封闭协议提升了内部公平性，但若真实 MLE 场景允许查阅资料或使用外部工具，封闭设定可能与实际应用存在差距。

## 6. 主要结论与发现

- **Gome 达到 SOTA 水平**：在封闭世界协议下，单张 V100、12 小时预算内，MLE-Bench 上取得 **35.1% any-medal rate**。
- **存在关键交叉点（critical crossover）**：
  - 对**较弱模型**，树搜索仍具优势，因为它能通过穷举探索补偿不可靠的推理。
  - 对**推理能力更强的模型**，基于梯度的优化逐渐超过树搜索。
  - 在**前沿模型**上，梯度式优化的优势进一步扩大。
- **范式意义**：随着面向推理的 LLM 快速发展，基于梯度的优化可能成为越来越有利的 MLE 智能体范式。
- **开源贡献**：论文发布了代码库和 GPT-5 traces，地址为 `https://github.com/microsoft/RD-Agent`。

## 7. 优点

- **概念创新清晰**：将“推理即梯度”作为核心类比，把诊断推理、成功记忆、多轨迹执行分别映射到梯度、动量、分布式优化，框架简洁且有解释力。
- **针对真实痛点**：指出树搜索随推理能力提升而低效的问题，提出从无梯度优化转向方向性优化的思路。
- **实验设计有控制意识**：采用封闭世界协议隔离外部知识，有助于公平比较智能体架构本身的效果。
- **跨模型 scaling 分析**：在 10 个模型上观察交叉点，增强了结论的普适性和趋势判断。
- **结果有竞争力**：在受限算力下取得 35.1% any-medal rate，并声称达到 SOTA。
- **开源可复现**：发布代码与 GPT-5 traces，有利于后续验证和扩展。

## 8. 不足与局限

- **信息不完整**：提供的文本只有摘要和元数据，无法评估公式、算法细节、超参数、提示设计和实现质量。
- **基准覆盖有限**：主要基于 MLE-Bench，未提及是否覆盖其他 MLE 或通用智能体基准，外部有效性有待确认。
- **封闭世界协议的双面性**：虽然有利于控制变量，但可能偏离真实开放环境中的 MLE 实践；在允许检索、使用外部工具或预训练知识的场景下，结论是否成立需进一步验证。
- **依赖强推理模型**：弱模型下树搜索仍占优，说明 Gome 的收益高度依赖底层 LLM 的推理能力，应用门槛较高。
- **算力预算限制**：单张 V100、12 小时预算虽体现实用性，但也可能限制对更大规模、更长周期任务的评估。
- **统计与成本报告不足**：摘要未说明重复次数、方差、显著性、失败率和成本；这些对判断稳定性与经济性很重要。
- **潜在偏差风险**：成功记忆与动量机制可能放大早期成功路径的偏差；多轨迹执行也可能带来额外推理成本。这些风险在提供文本中未展开讨论。

（完）
