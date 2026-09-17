---
title: "Escaping the Sisyphus Dilemma: Experience Replay for Robust Text-to-Optimization Modeling"
title_zh: 逃离西西弗斯困境：面向稳健文本到优化建模的经验回放
authors: "Wantong Xie, Yinghao Chen, Yi-Xiang Hu, Feng Wu, Jieyang Xu, Sijia Zhang, Xiangyang Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.690.pdf"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 大模型将自然语言转化为可执行优化模型并修正建模错误
tldr: 大语言模型在将自然语言转化为可执行优化模型时存在西西弗斯困境：面对结构相似的问题反复犯同样的错误，而现有检索增强方法只取静态问题-模型对作示例，无法捕捉动态推理。本文提出EOM框架，通过经验回放把临时的纠错步骤转化为持久知识，提炼为因果纠正映射，同时索引诊断洞见与禁忌陷阱。方法利用结构化经验显著提升建模的稳健性，为自动化优化建模提供了可复用的经验机制。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl690/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl690/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1656, \"height\": 980, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl690/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1599, \"height\": 747, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl690/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 779, \"height\": 557, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl690/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1659, \"height\": 682, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl690/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1643, \"height\": 580, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl690/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1630, \"height\": 496, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl690/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 769, \"height\": 802, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl690/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 767, \"height\": 567, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl690/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 772, \"height\": 765, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl690/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 790, \"height\": 201, \"label\": \"Table\"}]"
motivation: LLM在文本到优化建模中反复犯相同错误，现有检索增强方法难以动态纠错。
method: 提出EOM框架，用经验回放将临时纠错步骤蒸馏为持久因果纠正映射。
result: 该方法索引诊断洞见与禁忌陷阱，显著提升自动化优化建模的稳健性。
conclusion: EOM为LLM驱动的优化模型生成提供了可复用的经验知识机制。
---

## Abstract
Large Language Models have shown promise in translating natural language into executable optimization models, yet they often suffer from the Sisyphus Dilemma: a memoryless cycle where identical errors are repeated across structurally similar problems. Existing retrieval-augmented strategies primarily fetch static problem-model pairs as few-shot demonstrators, failing to capture the dynamic reasoning required to resolve execution failures. To bridge this gap, we propose EOM , a framework that implements Experience Replay to transform transient rectification steps into persistent knowledge. EOM distills interaction histories into Causal Correction Mappings, indexing both diagnostic insights and prohibitive traps. By utilizing a structure-aware retrieval mechanism that aligns semantic intent with abstract syntax trees and solver tracebacks, the system enables models to recall specific correction strategies for isomorphic errors. Extensive experiments across seven benchmarks demonstrate that EOM improves modeling accuracy by 8.45% on complex tasks while reducing token consumption by 28.65% and interaction turns by 25.82%, validating the efficiency of a “Rectify Once, Solve Many” paradigm.

---

## 论文详细总结（自动生成）

说明：以下总结主要依据所给论文摘要与元数据；由于未提供正文，具体公式、基线名称、算力配置等细节无法展开，只能就已有信息进行归纳。

## 1. 核心问题与整体含义
- **研究背景**：大语言模型（LLM）已展现出将自然语言转化为可执行优化模型的潜力，但在实际建模中常陷入“西西弗斯困境”（Sisyphus Dilemma）。
- **核心问题**：面对结构相似的问题，模型会反复犯相同错误，形成“无记忆循环”，缺乏从历史纠错中积累知识的能力。
- **现有方法不足**：检索增强策略多取静态“问题—模型”对作为 few-shot 示例，无法捕捉解决执行失败所需的动态推理过程。
- **整体含义**：论文试图通过“经验回放”把临时纠错步骤转化为持久知识，提升文本到优化建模的稳健性，推动“一次纠正、多次求解”（Rectify Once, Solve Many）范式。

## 2. 方法论：EOM 框架
- **核心思想**：提出 EOM 框架，将交互历史中的临时纠错经验沉淀为可复用知识，而不是每次从零纠错。
- **关键技术细节**：
  - 将交互历史蒸馏为 **Causal Correction Mappings**（因果纠正映射）。
  - 在经验库中索引两类信息：**诊断洞见**（diagnostic insights）与**禁忌陷阱**（prohibitive traps）。
  - 使用 **结构感知检索机制**：将语义意图与抽象语法树（AST）、求解器回溯（solver tracebacks）对齐。
  - 使模型能够针对“同构错误”召回具体纠正策略。
- **算法流程（文字说明）**：
  1. 模型根据自然语言生成优化模型；
  2. 执行模型，若失败则获得求解器 traceback 或诊断信息；
  3. 模型与求解器/环境进行纠错交互；
  4. 将纠错交互历史蒸馏为因果纠正映射；
  5. 将诊断洞见与禁忌陷阱存入经验库；
  6. 新问题到来时，按语义意图、AST 和 solver traceback 检索相关经验；
  7. 将经验注入上下文，指导模型避免同类错误并完成修正。
- **公式/伪代码**：所给文本未提供明确公式或算法伪代码。

## 3. 实验设计
- **数据集/场景**：在 **7 个 benchmarks** 上评估，任务为文本到优化建模，尤其关注复杂任务。
- **评价指标**：
  - 建模准确率；
  - token 消耗；
  - 交互轮次。
- **对比方法**：主要对比现有检索增强策略，尤其是以静态“问题—模型”对作为 few-shot 示例的方法；具体基线名称未在提供文本中列出。
- **主要结果**：在复杂任务上，EOM 将建模准确率提升 **8.45%**，同时减少 token 消耗 **28.65%**、交互轮次 **25.82%**。

## 4. 资源与算力
- 所给文本 **未提及** GPU 型号、数量、训练时长、推理成本或具体算力配置。
- 因此无法判断该工作的实际算力开销，也无法评估其训练/推理效率在硬件层面的可复现性。

## 5. 实验数量与充分性
- **实验规模**：至少覆盖 7 个 benchmark 的主实验，并报告准确率、token 消耗、交互轮次等指标。
- **消融与细节**：提供文本未说明是否做了消融实验、统计显著性检验、误差棒或人工评估。
- **充分性判断**：
  - 从摘要看，多基准验证和效率指标使其具有一定说服力；
  - 但基线配置、提示模板、求解器版本、经验库规模等未给出，难以完全判断公平性与客观性；
  - 若正文包含消融和跨领域测试，则充分性会更强，目前信息不足以确认。

## 6. 主要结论与发现
- EOM 能显著缓解 LLM 在文本到优化建模中的重复错误问题。
- 经验回放机制可将临时纠错转化为持久知识，提高复杂任务建模准确率。
- 方法同时降低 token 消耗和交互轮次，验证了“一次纠正、多次求解”的效率优势。
- EOM 为 LLM 驱动的自动化优化建模提供了可复用的经验知识机制。

## 7. 优点
- **问题定位清晰**：用“西西弗斯困境”准确概括 LLM 反复犯同类错误的痛点。
- **方法有新意**：将经验回放引入文本到优化建模，把纠错轨迹蒸馏为因果纠正映射。
- **检索设计更贴近执行反馈**：结合语义意图、AST 与 solver traceback，比静态 few-shot 更能处理动态执行失败。
- **效果与效率兼顾**：不仅提升准确率，还减少 token 和交互轮次。
- **可复用性强**：经验库思想可迁移到其他需要求解器反馈的 LLM Agent 场景。

## 8. 不足与局限
- **信息不完整**：所给文本仅为摘要与元数据，无法验证方法细节、公式、算法实现和实验设置。
- **依赖求解器反馈**：方法依赖 AST 与 solver traceback，主要适用于可执行、可形式化的优化建模任务；对非形式化或无法获得执行反馈的问题可能受限。
- **经验库风险**：错误经验、过时经验或检索偏差可能被复用，同构错误判定与因果映射可靠性仍需验证。
- **实验覆盖有限**：虽覆盖 7 个 benchmark，但具体领域、难度分布、真实场景泛化能力未说明。
- **公平性待确认**：基线名称、提示设计、检索预算、求解器配置等未给出，可能影响比较公平性。
- **资源与可复现性**：未报告算力、训练细节和成本，复现难度与应用门槛不明确。

（完）
