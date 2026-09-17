---
title: "NEMO: Execution-Aware Optimization Modeling via Autonomous Coding Agents"
title_zh: NEMO：基于自主编码智能体的执行感知优化建模
authors: "Yang Song, Anoushka Vyas, Zirui Wei, Sina Khoshfetrat Pakazad, Henrik Ohlsson, Graham Neubig"
date: 2026-04-30
pdf: "https://openreview.net/pdf/eaafad01c645f13aea55a2acf38421321edc09dd.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 自主编码智能体将自然语言决策问题转为可执行数学优化模型
tldr: 针对现有方法依赖专门LLM或定制智能体、常生成语法无效或不可执行代码的问题，本文提出NEMO系统。该方法把自主编码智能体作为一等抽象，通过沙箱执行保证代码可执行，并引入优化器与模拟器之间的非对称验证循环实现自动校验与修复。系统将自然语言决策问题描述转化为可执行的数学优化实现。该工作提升了优化建模自动化的鲁棒性与可执行性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法依赖专门LLM或定制智能体，常生成语法无效或不可执行的优化代码，鲁棒性差。
method: 提出NEMO，将自主编码智能体作为一等抽象，借助沙箱执行保证可执行，并采用优化器与模拟器间的非对称验证循环。
result: 系统可将自然语言决策问题稳定转换为可执行数学优化实现并自动校验修复。
conclusion: 表明自主编码智能体可提升自然语言到优化模型自动化的可执行性与可靠性。
---

## Abstract
We present **NEMO**, a system that translates **N**atural-language descriptions of decision problems into formal **E**xecutable **M**athematical **O**ptimization implementations using autonomous coding agents (ACAs). Existing approaches rely on specialized large language models (LLMs) or bespoke task-specific agents that are often brittle and frequently generate syntactically invalid or non-executable code. NEMO instead treats ACAs as a first-class abstraction analogous to API-based interaction with LLMs; their sandboxed execution guarantees code is executable by construction and supports automated validation and repair. We introduce novel coordination patterns including asymmetric validation loops between independently generated optimizer and simulator implementations, external memory for experience reuse, and robustness enhancements via minimum Bayes risk (MBR) decoding and self-consistency. Across nine established optimization benchmarks, NEMO achieves state-of-the-art performance on the majority of tasks with substantial margins on several datasets, demonstrating the power of execution-aware agentic architectures for automated optimization modeling.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 OpenReview 浏览器验证页面，未包含论文正文。以下总结主要依据论文元数据与摘要；凡正文未提供的信息，均标注为“未说明/无法验证”。

## 1. 核心问题与整体含义
- **研究动机**：将自然语言描述的决策问题自动转化为形式化、可执行的数学优化实现，是自动化优化建模的重要目标。
- **现有问题**：已有方法多依赖专门微调的 LLM 或定制任务智能体，鲁棒性较差，常生成语法无效或不可执行的代码。
- **整体含义**：论文提出 **NEMO**，把自主编码智能体（ACAs）作为一等抽象，类比于通过 API 调用 LLM；通过沙箱执行、自动验证与修复，提升自然语言到优化模型自动化的可执行性与可靠性。

## 2. 方法论
- **核心思想**：用自主编码智能体完成从自然语言决策问题到可执行数学优化实现的转换，并让“执行”成为验证与修复的核心机制。
- **关键设计**：
  - **沙箱执行**：ACAs 在沙箱中运行，使生成的代码“按构造可执行”，降低语法无效或不可执行风险。
  - **非对称验证循环**：分别独立生成优化器实现与模拟器实现，并在两者之间进行交叉验证，以自动发现和修复不一致或错误。
  - **外部记忆**：存储和复用过往经验，提升后续任务效率与稳定性。
  - **鲁棒性增强**：采用最小贝叶斯风险（MBR）解码与自一致性策略，提高输出可靠性。
- **流程概述**：输入自然语言决策问题 → 智能体生成优化器/模拟器代码 → 沙箱执行 → 非对称验证循环校验 → 自动修复 → 外部记忆复用经验 → MBR/自一致性聚合 → 输出可执行数学优化实现。
- **公式/伪代码**：所给摘要与元数据未提供显式公式或算法伪代码，以上为摘要层面的文字流程。

## 3. 实验设计
- **数据集/场景**：在 **九个已有优化基准** 上评估；摘要未列出具体基准名称。
- **任务形式**：自然语言决策问题描述 → 可执行数学优化实现。
- **Benchmark**：九个 established optimization benchmarks。
- **对比方法**：现有依赖专门 LLM 或定制任务特定智能体的方法；摘要未列具体基线名称。
- **主要结果**：NEMO 在多数任务上达到 state-of-the-art，并在若干数据集上取得显著领先。

## 4. 资源与算力
- 所提供摘要与元数据 **未提及** GPU 型号、数量、训练/推理时长、API 调用量或成本。
- 由于 NEMO 围绕自主编码智能体、沙箱执行与验证循环，实际运行可能涉及推理与工具调用成本，但文中未量化。
- 因此无法从现有内容判断其算力需求与效率。

## 5. 实验数量与充分性
- **主实验**：至少覆盖九个优化基准。
- **消融/组件分析**：摘要提到 MBR 解码、自一致性、外部记忆、非对称验证循环等组件，暗示可能存在相关消融实验，但所给内容未提供数量与结果。
- **充分性**：多基准评估是优点，但缺少基线细节、统计显著性、失败案例、超参敏感性和错误分析，难以完全判断实验充分性。
- **公平性**：未说明基线与 NEMO 是否在同等模型、提示、预算和执行环境下比较，无法评估公平性。

## 6. 主要结论与发现
- NEMO 能将自然语言决策问题较稳定地转换为可执行数学优化实现，并自动校验与修复。
- 在九个优化基准中的多数任务上取得 SOTA，部分数据集提升幅度较大。
- 执行感知的智能体架构有助于提升自动化优化建模的可执行性、可靠性与鲁棒性。
- 将自主编码智能体作为一等抽象，是自然语言到优化模型自动化的一条有效路径。

## 7. 优点
- **可执行性优先**：沙箱执行使代码可执行性成为系统构造的一部分。
- **自动验证与修复**：优化器与模拟器之间的非对称验证循环具有创新性。
- **经验复用**：外部记忆有助于跨任务积累和迁移经验。
- **鲁棒性增强**：MBR 解码与自一致性可缓解单次生成的不稳定性。
- **实验结果强**：九个基准上多数任务 SOTA，元数据标注为 ICML-2026 接收，评审分 9.0。

## 8. 不足与局限
- **正文缺失**：提供的 PDF 文本为验证页面，无法核实方法细节、实验设置与结果真实性。
- **基准未列名**：九个优化基准的具体名称、任务类型和难度分布未说明，覆盖范围未知。
- **算力与成本未说明**：缺少 GPU、时长、调用成本等信息。
- **公平性无法评估**：基线方法、模型规模、预算和提示策略未交代。
- **应用限制**：方法依赖沙箱执行、求解器/模拟器和验证循环，可能受环境配置、延迟与成本影响；对复杂工业场景、随机优化、多目标优化等未在摘要中说明。
- **失败模式未讨论**：非对称验证循环何时失效、错误如何传播、MBR/自一致性带来的额外开销等未提供。

（完）
