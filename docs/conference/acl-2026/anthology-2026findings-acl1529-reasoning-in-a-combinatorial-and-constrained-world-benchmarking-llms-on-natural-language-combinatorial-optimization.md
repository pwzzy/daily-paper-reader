---
title: "Reasoning in a Combinatorial and Constrained World: Benchmarking LLMs on Natural-Language Combinatorial Optimization"
title_zh: 在组合与约束世界中的推理：面向自然语言组合优化的LLM基准评测
authors: "Xia Jiang, Jing Chen, Cong Zhang, Jie Gao, Chengpeng Hu, Chenhao Zhang, Yaoxin Wu, Yingqian Zhang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1529.pdf"
tags: ["query:llm-agent-or"]
score: 8.0
evidence: 面向自然语言组合优化的LLM基准评测
tldr: 大语言模型在数学与逻辑推理上表现突出，但在高维约束下的组合优化搜索能力仍缺乏系统评估。作者提出NLCO，一个自然语言组合优化基准，涵盖43类组合优化问题，并按变量类型、约束族、全局模式与目标类构建四层分类体系。评测要求模型在给定语言描述场景下直接输出离散解，而无需编写代码或调用外部求解器。该工作为衡量LLM在端到端组合优化推理中的真实能力提供了细粒度诊断工具，对运筹优化与LLM结合研究具有基础性意义。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 1377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1648, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1092, \"height\": 542, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1265, \"height\": 672, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1642, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1645, \"height\": 1698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1529/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1637, \"height\": 879, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 800, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1645, \"height\": 740, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 926, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1661, \"height\": 2321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1633, \"height\": 2561, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1636, \"height\": 518, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 796, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 835, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 693, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1644, \"height\": 783, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1643, \"height\": 986, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1659, \"height\": 2027, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 543, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 424, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1529/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 426, \"height\": 774, \"label\": \"Table\"}]"
motivation: 大语言模型在数学与逻辑推理上表现优异，但处理高维约束下的组合优化搜索能力仍缺乏系统评测。
method: 提出NLCO自然语言组合优化基准，覆盖43类问题并构建变量类型、约束族、全局模式与目标类的四层分类。
result: 评测要求模型依据语言描述直接输出离散解，无需写代码或调用求解器，从而暴露LLM端到端组合优化推理的薄弱环节。
conclusion: 该基准为评估和推动LLM在组合优化建模与求解中的能力提供了细粒度工具与诊断依据。
---

## Abstract
While large language models (LLMs) have shown strong performance in math and logic reasoning, their ability to handle combinatorial optimization (CO)—searching high-dimensional solution spaces under hard constraints—remains underexplored. To bridge the gap, we introduce NLCO, a **N**atural **L**anguage **C**ombinatorial **O**ptimization benchmark that evaluates LLMs on end-to-end CO reasoning: given a language-described decision-making scenario, the model must output a discrete solution without writing code or calling external solvers. NLCO covers 43 CO problems and is organized using a four-layer taxonomy of variable types, constraint families, global patterns, and objective classes, enabling fine-grained evaluation. We provide solver-annotated solutions and comprehensively evaluate LLMs by feasibility, solution optimality, and reasoning efficiency. Experiments across a wide range of modern LLMs show that high-performing models achieve strong feasibility and solution quality on small instances, but both degrade as instance size grows, even if more tokens are used for reasoning. We also observe systematic effects across the taxonomy: set-based tasks are relatively easy, whereas graph-structured problems and bottleneck objectives lead to more frequent failures. The benchmark dataset and code for data generation and evaluation are publicly available.

---

## 论文详细总结（自动生成）

# 论文总结：NLCO——面向自然语言组合优化的 LLM 基准评测

## 1. 核心问题与整体含义

- **研究动机**：大语言模型在数学、逻辑、编程等任务上表现突出，但其在**组合优化（Combinatorial Optimization, CO）**中的能力仍缺乏系统评估。CO 要求在硬约束下搜索高维离散解空间，涉及目标/约束建模、离散决策构造、全局一致性检查和近优性推理。
- **现有评测不足**：
  - 许多优化类基准主要评估 LLM 写代码、调用启发式或外部求解器的能力，难以隔离模型自身的端到端推理能力。
  - 另一些直接输出类基准覆盖问题少，且多按复杂度分类，缺少对问题结构的细粒度诊断。
- **论文目标**：提出 **NLCO**，一个自然语言组合优化基准，要求模型仅根据语言描述的决策场景，直接输出离散解，**不写代码、不调用外部求解器**。
- **整体含义**：NLCO 试图回答三个问题：
  - RQ1：LLM 能否从文本端到端求解 CO？
  - RQ2：问题结构如何影响推理可靠性？
  - RQ3：LLM 如何在解质量与推理效率之间权衡？

## 2. 方法论

- **核心思想**：
  - 将 CO 任务嵌入自然语言决策场景中，模型输入为文本描述 \(D\)，输出为离散解 \(\hat{x}\)。
  - 隐藏形式化模型 \(P=\langle X, F, f \rangle\) 仅用于评估，不给模型。
  - 形式化目标可写为：在可行集 \(F\) 下优化目标 \(f(x)\)，即  
    \[
    \min_{x\in X} f(x)\quad \text{s.t.}\quad x\in F
    \]
  - 模型需输出可行且尽量最优的解 \(\hat{x}\)。

- **四层分类体系**：
  - 对每个问题 \(P\)，定义分类元组：
    \[
