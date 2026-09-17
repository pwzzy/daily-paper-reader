---
title: "Crossroads of Optimization under Uncertainty: How to Choose the Optimal Model"
title_zh: 不确定性优化的十字路口：如何选择最优模型
authors: "Chengxi She, Zhiqiang Chen, Xingyu Lu, Caihua Chen, Piaoyang Zhao, Xuedong Wang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.172.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 多智能体框架自动完成不确定性优化建模与求解
tldr: 不确定性优化中存在专家门槛与模型选择困境两大难题。本文提出LLM4OuU多智能体框架，将复杂建模过程分解为五个顺序步骤，设计结合领域知识的专用大模型智能体，并基于检索增强构建跨行业混合数据集。实验表明其在六类不确定性模型的自动建模与求解上优于基线，为运筹优化建模自动化提供了新范式。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl172/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1565, \"height\": 786, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl172/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1621, \"height\": 804, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl172/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1632, \"height\": 668, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 1008, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1665, \"height\": 641, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1661, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 816, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1659, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1659, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1650, \"height\": 143, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1659, \"height\": 504, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1661, \"height\": 688, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl172/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1661, \"height\": 467, \"label\": \"Table\"}]"
motivation: 不确定性优化存在专家门槛高、模型选择困难的问题，亟需自动化手段降低建模与求解门槛。
method: 提出LLM4OuU多智能体框架，将建模拆解为五步，用专用大模型智能体结合检索增强数据进行建模与求解。
result: 在跨行业混合数据集上，LLM4OuU对六类不确定性模型的建模求解性能优于基线方法。
conclusion: 证明大模型多智能体可有效自动化运筹优化中的不确定性建模与模型选择。
---

## Abstract
To address two correlated question in Optimization under Uncertainty (OuU): Expertise Threshold and Selection Conundrum, we propose LLM4OuU, a multi-agent framework that automates both the modeling and solving of six distinct types of uncertainty models and generates mapping pairs to explore the potential relationship between optimization problems and optimal models. Firstly, we decompose the complex modeling process into five sequential steps and design specialized LLM agents combining high-level domain expertise. Secondly, we introduce a hybrid dataset spanning various industries based on Retrieval-Augmented Generation (RAG) to benchmark performance. Extensive experiments demonstrate that LLM4OuU achieves superior performance compared to baselines, even reaching up to 99% on specific model types. Finally, we establish a mapping from problem features to optimal models, with correlation analysis revealing that not only data scale but also the specific scenario significantly influence model selection.

---

## 论文详细总结（自动生成）

# 论文总结：Crossroads of Optimization under Uncertainty: How to Choose the Optimal Model

## 1. 核心问题与整体含义
- **研究动机**：不确定性优化（Optimization under Uncertainty, OuU）在交通、供应链、金融、医疗等领域很重要，但相比机器学习，其普及度较低。
- **两大核心难题**：
  - **Expertise Threshold（专家门槛）**：每个 OuU 问题通常需要人工建模、算法设计、数据处理与编码，要求运筹优化和统计专业知识。
  - **Selection Conundrum（选择困境）**：SAA、RO、DRO 等不确定性模型各有优劣，实际场景中缺乏“问题特征 → 最优模型”的映射机制。
- **整体含义**：论文提出 LLM4OuU 多智能体框架，用大语言模型自动化 OuU 的建模与求解，并构建高质量映射对，探索问题特征与最优不确定性模型之间的关系。

## 2. 方法论：核心思想与关键技术
- **核心思想**：将复杂 OuU 建模流程拆解为多阶段、多智能体协作流程，结合领域知识、RAG 和自修复机制，自动完成从自然语言问题与历史数据到最优决策的端到端建模求解。
- **六类不确定性模型**：
  - SAA（样本平均近似）
  - RO：Box、Budget、Ellipsoidal 三类不确定集
  - DRO：Wasserstein、KL 两类模糊集
- **数据生成流程**：
  - 从 2000+ 篇 arXiv OR 论文中提取摘要、引言、结论，构建检索向量库。
  - 整合 Kaggle、UCI、Mendeley、Figshare、GitHub 及企业合作数据，进行异常值处理与缺失值填补。
  - 使用 RAG 双输入（数值数据 + 检索文献）生成自然语言问题描述。
  - 将描述分解为五个要素：问题背景、决策变量、目标函数、约束、不确定参数。
- **多智能体框架 LLM4OuU**：
  - **初始建模专家**：输出变量、约束、min-max/max-min 初始模型。
  - **转换专家**：针对 6 类不确定性模型设计专用子代理，分别进行模型转换与可处理化重构。
  - **编码专家**：生成可执行 Python/Gurobi/Mosek 代码，并集成黄金比例搜索确定部分超参数（如 Wasserstein 半径）。
  - **修复专家**：根据执行错误信息迭代修复代码，支持重试机制。
- **算法流程**：对候选模型集合循环，每轮执行初始建模、模型转换、编码、执行；若出错则修复，最多 K 步；最终返回最优解。
- **领域知识增强**：将常见错误归为代码错误、加载错误、专家错误，并嵌入各智能体提示词，提升鲁棒性。
- **理论重构
