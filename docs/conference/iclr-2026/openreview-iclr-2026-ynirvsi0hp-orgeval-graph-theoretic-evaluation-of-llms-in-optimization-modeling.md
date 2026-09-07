---
title: "ORGEval: Graph-Theoretic Evaluation of LLMs in Optimization Modeling"
title_zh: ORGEval：基于图论的大语言模型优化建模评测
authors: "Zhuohan Wang, Ziwei Zhu, Ziniu Li, Yizhou Han, Yufeng Lin, Zhihang Lin, Angyang Gu, Xinglin Hu, Ruoyu Sun, Tian Ding"
date: 2025-09-20
pdf: "https://openreview.net/pdf?id=YNIrVSI0hp"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 针对LLM生成的线性与混合整数线性规划模型，提出图论评测框架
tldr: 大语言模型有望自动化优化建模，但现有求解器评测存在不一致、不可行与高成本问题。本文提出ORGEval，用图结构表示线性与混合整数线性规划模型，将等价检测归约为图同构测试，并证明对称分解条件下可高效判别。该框架为评估LLM建模能力提供了更一致且可扩展的评测基准。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 优化建模需大量人力且缺稳健评测指标，现有基于求解器的评测存在不一致、不可行和高成本缺陷。
method: 将优化模型表示为图，利用图同构测试判别模型等价性，并利用对称分解充分条件提高效率。
result: 提出的ORGEval能对LLM生成线性与混合整数规划的建模能力给出稳健一致的评价。
conclusion: 图论评测框架可替代基于求解器的评测，为评估LLM建模能力提供基准。
---

## Abstract
Formulating optimization problems for industrial applications demands significant manual effort and domain expertise. While Large Language Models (LLMs) show promise in automating this process, evaluating their performance remains difficult due to the absence of robust metrics. Existing solver-based approaches often face inconsistency, infeasibility issues, and high computational costs. To address these issues, we propose ORGEval, a graph-theoretic evaluation framework for assessing LLMs’ capabilities in formulating linear and mixed-integer linear programs. ORGEval represents optimization models as graphs, reducing equivalence detection to graph isomorphism testing. We identify and prove a sufficient condition, when the tested graphs are symmetric decomposable (SD), under which the Weisfeiler–Lehman (WL) test is guaranteed to correctly detect isomorphism. Building on this, ORGEval integrates a tailored variant of the WL-test with an SD detection algorithm to evaluate model equivalence. By focusing on structural equivalence rather than instance-level configurations, ORGEval is robust to numerical variations.  Experimental results show that our method can successfully detect model equivalence and produce 100\% consistent results across random parameter configurations, while significantly outperforming solver-based methods in runtime, especially on difficult problems. Leveraging ORGEval, we construct the Bench4Opt dataset and benchmark state-of-the-art LLMs on optimization modeling. Our results reveal that although optimization modeling remains challenging for all LLMs, DeepSeek-V3 and Claude-Opus-4 achieve the highest accuracies under direct prompting, outperforming even leading reasoning models.

---

## 论文详细总结（自动生成）

# ORGEval：基于图论的大语言模型优化建模评测

## 1. 核心问题与整体含义（研究动机与背景）

- **背景**：工业应用中的优化问题建模（如线性规划 LP、混合整数线性规划 MILP）需要大量人工经验与领域知识。大语言模型（LLM）被视为可自动化这一过程的潜在工具。
- **核心问题**：如何稳健、一致且高效地评估 LLM 生成的优化模型是否正确，现有评测手段存在明显缺陷。
- **现有方法的不足**：
  - **基于求解器（solver-based）的评测存在三大问题**：结果不一致（不同参数配置下波动大）、可行性问题（模型无法求解或退化）、以及高计算成本（求解困难问题耗时严重）。
- **本文总体含义**：提出一种不依赖求解器的图论评测框架 ORGEval，为 LLM 优化建模能力提供一致、可扩展的评测基准，从而推动 LLM 在运筹优化自动化方向的发展。

## 2. 方法论：核心思想、关键技术细节与流程

- **核心思想**：放弃求解模型获取数值解来判断正确性，转而在**结构层面**判断 LLM 生成的模型与参考答案是否等价。通过将优化模型编码为图结构，把模型等价性问题转化为**图同构测试**问题。
- **技术细节**：
  - **图表示**：线性与混合整数线性规划模型被表示为图，变量、约束、目标函数等结构信息映射到图的节点与边，保留模型的数学结构。
  - **等价性约化**：两个优化模型等价当且仅当对应图同构。因此，给定 LLM 生成模型与参照模型，评测即判断二者图的同构性。
  - **充分性条件**：论文识别并证明了一个充分条件——当被测试图满足**对称可分解（Symmetric Decomposable, SD）** 性质时，**Weisfeiler-Lehman（WL）测试**可以保证正确判定同构。
  - **算法流程**：ORGEval 将一种定制化的 WL 测试变体与 SD 检测算法相结合：先检测图是否属于 SD 类，若是则使用 WL 测试做确定性的等价判断。
- **理论性质**：
  - 对 SD 类图，WL 测试不存在误判，保证判定的正确性。
  - 评测关注结构等价而非实例数值配置，因此对随机参数摄动（numerical variations）具有天然鲁棒性。

## 3. 实验设计：数据集、场景与对比方法

- **Benchmark 构建**：作者基于 ORGEval 构建了 **Bench4Opt** 数据集，用于系统评测 LLM 的优化建模能力。
- **评测场景**：覆盖线性规划（LP）与混合整数线性规划（MILP）的建模任务，要求 LLM 输出模型并根据图论等价性判定正确性。
- **对比对象**：在直接提示（direct prompting）设置下，对多种 SOTA LLM 进行评测，包括推理型模型与通用型模型，其中涉及的模型有：
  - DeepSeek-V3
  - Claude-Opus-4
  - 以及其他多位 SOTA 推理型模型

## 4. 资源与算力

- 论文内容中**未明确说明**训练或评测所使用的 GPU 型号、数量、总运行时长或计算集群配置。
- 可以推测：由于 ORGEval 本身旨在替代高成本求解过程，其评测开销主要由图构建与 WL 测试构成，理论上远低于数值求解；但论文未给出具体的算力需求数字。

## 5. 实验数量与充分性评估

- **已报告实验**：
  - 等价性检测有效性实验：验证 ORGEval 能正确检测模型等价性；
  - 一致性实验：在不同随机参数配置下重复评测，取得 **100% 一致**的结果；
  - 效率对比实验：在求解困难问题上相较 solver-based 方法显著减少运行时间（具体数值摘要未列出）；
  - Benchmark 评测实验：基于 Bench4Opt 对多个 SOTA LLM 进行建模准确率对比。
- **客观性与公平性**：从摘要来看，作者同时控制了随机参数变化并测试了一致性，这对评测类工作是关键指标。100% 一致性说明方法对参数配置不敏感，具备较强的客观性。
- **充分性判断**：由于仅有摘要信息、缺少详细的实验表格与消融细节（如不同图规模下的扩展性、非 SD 图处理策略的对比等），难以对整体实验充分性做最终判断。但核心维度的验证（正确性、一致性、效率、模型 benchmark）基本都有覆盖。

## 6. 主要结论与发现

- **方法有效性**：ORGEval 可成功检测优化模型等价性，且在不同随机参数配置下保持**100% 的评测一致性**。
- **效率优势**：运行时间大幅优于基于求解器的方法，在困难问题上优势尤其明显。
- **核心基准发现**：
  - 优化建模对现有所有 LLM 而言仍然是一大挑战（准确率普遍有限）；
  - 但在直接提示下，**DeepSeek-V3 与 Claude-Opus-4 达到最高准确率**，甚至超过了领先的推理型模型。

## 7. 优点与亮点

- **问题切入精准**：准确指出基于求解器的 LLM 优化建模评测中存在的三大痛点（不一致、不可行、高成本），动机清晰且实用价值高。
- **理论保证**：不依赖启发式相似度度量，而是将评测建立在图同构的数学基础上，并给出 SD 条件下 WL 测试正确性的形式化证明，方法具有理论可靠性。
- **结构 vs 数值解耦**：基于结构等价而非数值求解，从根源上解决了求解器带来的随机不一致问题，同时大幅降低计算成本。
- **可扩展性**：图同构与 WL 测试均有成熟的算法支撑，相比重复求解优化问题，评测流程更容易扩展到大规模评测集。
- **基准贡献**：构建 Bench4Opt 数据集，为后续 LLM 优化建模能力研究提供了标准化评测资源。

## 8. 不足与局限

- **覆盖范围有限**：从摘要来看，评测对象限于线性规划（LP）与混合整数线性规划（MILP），不涉及非线性规划、随机优化、整数非线性规划（MINLP）等更复杂的优化类型，应用边界有待扩展。
- **SD 条件为充分而非必要**：WL 测试保证正确性的前提是 SD 条件成立；对不满足 SD 条件的图，WL 测试理论上可能存在同构误判（或需额外处理），摘要中未说明非 SD 情况下的处理策略与失败率。
- **实验与实现细节缺失**：原文仅有摘要，没有提供图表示的具体编码维度、WL 测试变体的超参数、求解器对比的具体基准实现等细节，第三方复现存在困难。
- **算力信息缺失**：未报告任何 GPU/CPU 资源使用信息，无法评估方法在硬件层面的可负担性。

（完）
