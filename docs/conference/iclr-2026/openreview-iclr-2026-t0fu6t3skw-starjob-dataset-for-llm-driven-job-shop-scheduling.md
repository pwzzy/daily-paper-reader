---
title: "Starjob: Dataset for LLM-Driven Job Shop Scheduling"
title_zh: Starjob：用于LLM驱动的作业车间调度的数据集
authors: "Henrik Abgaryan, Tristan Cazenave, Ararat Harutyunyan"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=t0fU6t3Skw"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 将大语言模型直接应用于作业车间调度这一经典运筹组合优化问题
tldr: 作业车间调度是组合优化经典问题但LLM潜力未被充分探索；论文构建首个120k实例JSSP监督数据集Starjob，并使用LoRA微调LLaMA-8B做端到端调度；在标准benchmark上LLM方法超越多种传统方法；该工作为LLM求解运筹调度和组合优化建立了数据与模型基线。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM在通用编程上表现强，但其求解组合优化问题（如车间作业调度）的潜力尚未被充分验证，且缺少高质量监督数据集。
method: 构建首个包含120k实例的JSSP监督数据集Starjob，并利用LoRA方法微调LLaMA-8B模型进行端到端的作业车间调度求解。
result: 在标准基准上，该LLM方法不仅超越传统调度方法，还验证了LLM建模复杂排产策略的有效性。
conclusion: 研究表明经过针对性微调的LLM可直接求解经典组合优化问题，为LLM在运筹优化中的应用提供了重要基准与数据资源。
---

## Abstract
Large Language Models (LLMs) have shown remarkable capabilities across various domains, but their potential for solving combinatorial optimization problems remains largely unexplored. In this paper, we investigate the applicability of LLMs to the Job Shop Scheduling Problem (JSSP), a classic challenge in combinatorial optimization that requires efficient job allocation to machines to minimize makespan. To this end, we introduce Starjob, the first supervised dataset for JSSP, comprising 120k instances specifically designed for training LLMs. Leveraging this dataset, we fine-tune the LLaMA 8B model with the LoRA method to develop an end-to-end scheduling approach. Our evaluation on standard benchmarks demonstrates that the proposed LLM-based method not only surpasses traditional Priority Dispatching Rules (PDRs) but also achieves notable improvements over state-of-the-art neural approaches like L2D, with an average improvement of 11.28% on DMU and 3.29% on Taillard benchmarks. These results highlight the untapped potential of LLMs in tackling combinatorial optimization problems, paving the way for future advancements in this area.

---

## 论文详细总结（自动生成）

# Starjob：用于LLM驱动的作业车间调度的数据集——论文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：大型语言模型（LLM）在众多通用领域表现优异，但其在组合优化问题上的潜力尚未被充分探索。作业车间调度问题（JSSP）是组合优化中的经典难题，要求在机器上高效分配作业以最小化完工时间（makespan），但此前缺乏面向LLM训练的高质量监督数据集。
- **整体含义**：论文试图验证“经过针对性微调的LLM能否直接求解经典组合优化问题”，并希望为LLM在运筹优化领域的研究建立数据与模型基线。

## 2. 方法论：核心思想与关键设计

- **核心思路**：采用“数据先行 + 端到端微调”的范式，即构建大规模监督数据集，然后用LLM直接输出调度方案，而非依赖传统启发式搜索。
- **Starjob数据集**：
  - 首次为JSSP构建的监督数据集；
  - 包含约 **120k 个实例**，专门用于训练LLM。
- **模型与训练方法**：
  - 基座模型为 **LLaMA 8B**；
  - 采用 **LoRA**（低秩适配）方法进行参数高效微调；
  - 训练目标为端到端的调度生成，即输入作业车间实例，直接输出作业分配/排序方案。
- **公式/算法流程**：
  - 论文摘要未给出具体的公式或算法伪代码，但从描述可推断其整体流程为：实例编码 → 输入LLM → 自回归生成调度序列 → 与真实最优/近似最优调度计算损失并反向传播（LoRA更新参数）；推理时直接解码为完整调度，并计算makespan。

## 3. 实验设计

- **数据集/基准**：
  - 训练数据：Starjob（120k JSSP实例）。
  - 评估基准：标准JSSP benchmarks，具体提及 **DMU** 和 **Taillard** 两个系列。
- **对比方法**：
  - 传统方法：优先调度规则（Priority Dispatching Rules, PDRs）；
  - 现有神经方法：以 **L2D**（Learning to Dispatch）为代表的状态最优神经方法。
- **实验场景**：标准小规模/中规模JSSP实例上的离线调度。
- **评价指标**：与最优/已知最好解的偏差或平均完工时间改进率。

## 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长、显存消耗等算力细节。
- 仅能推断训练成本较低（因为使用LoRA对8B模型做微调，而非全参数训练），但具体数值无法从当前文本中确认。

## 5. 实验数量与充分性

- **从摘要可见的实验组数**：
  - 两组基准测试：DMU、Taillard；
  - 对照组大致三类：LLM方法（本文）、PDRs、L2D等神经方法。
- **充分性评估**：
  - **公开信息有限**：摘要只给出了平均改进率，未报告各实例的分布、方差、显著性检验、不同数据规模下的结果或消融实验。
  - **缺少关键分析**：例如LoRA秩大小、训练数据量对性能的影响，模型泛化到更大规模JSSP的能力等均未提及。
  - **总体判断**：从摘要看，实验可以作为“可行性的初步证据”，但不足以独立证明方法的普遍优越性；需结合完整论文中的更多实验（如跨规模泛化、与传统求解器比较、计算时间对比等）才能判定其充分性。

## 6. 主要结论与发现

- 经过Starjob数据集和LoRA微调的LLaMA 8B可实现端到端JSSP调度，且在标准benchmark上**优于传统PDR**。
- 相比已有神经方法L2D，本文LLM方法实现：
  - **DMU** 基准上平均改进 **11.28%**；
  - **Taillard** 基准上平均改进 **3.29%**。
- 结论：LLM有潜力直接求解经典组合优化问题，微调后的LLM能够建模较复杂的排产策略，为该方向提供了数据与模型基线。

## 7. 优点

- **填补空白**：首次提出面向JSSP的大型监督数据集Starjob，推动LLM在该领域的实证研究。
- **方法干净直接**：不设计复杂的问题专用网络，而是利用LLM通用序列生成能力做端到端调度，简化了求解流程。
- **参数高效**：采用LoRA微调8B模型，相比全量训练资源消耗更低，具有实际可操作性。
- **结果有说服力**：在多个标准benchmark上相较传统和神经方法均取得显著改进，提供了强力的积极证据。

## 8. 不足与局限

- **实验披露不足**：摘要和元数据中没有给出实验细节（如具体实例规模、训练/测试划分、重复实验次数），难以评估结果稳定性。
- **算力信息缺失**：未报告GPU型号、数据量-性能曲线、训练时间等资源成本，不利于复现和横向比较。
- **缺少消融和泛化分析**：
  - 未分析LoRA秩、数据集大小、上下文长度等关键因素对性能的影响；
  - 未检验模型在更大规模/更多约束变体JSSP上的泛化能力。
- **与传统最优/近似求解器的比较可能不够全面**：仅对比PDR和L2D，未与OR-Tools、CP-SAT、专门的元启发式算法等强基线比较，结论“超越传统方法”仅限定于PDR范畴。
- **效率问题**：LLM推理成本和时间通常高于专用神经或优化求解器，摘要未报告相关计算开销。

（完）
