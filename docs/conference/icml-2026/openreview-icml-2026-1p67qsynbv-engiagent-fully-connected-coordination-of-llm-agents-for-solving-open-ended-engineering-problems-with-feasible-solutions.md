---
title: "EngiAgent: Fully Connected Coordination of LLM Agents for Solving Open-ended Engineering Problems with Feasible Solutions"
title_zh: EngiAgent：用于求解开放式工程问题并给出可行解的全连接LLM智能体协调框架
authors: "Xiyuan Zhou, Ruixi Zou, Xinlei Wang, Yuheng Cheng, Yan Xu, Junhua Zhao, Jinjin Gu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/7e51b5509080737b31534630ebc12807e8aa7c5b.pdf"
tags: ["query:llm-agent-or"]
score: 7.0
evidence: 多智能体LLM系统进行数学建模与可行性求解
tldr: 工程问题求解要求数学建模既能刻画复杂问题，又能在数据与物理约束下给出可行解，而现有大语言模型虽擅长推理与代码生成却难以保证可行性。本文提出EngiAgent，一种采用全连接协调机制的多智能体系统，通过智能体分工协作完成开放式分析、可行性驱动的建模与迭代修正。实验表明该方法能在开放式工程问题上生成满足约束的可行解，提升了LLM在真实决策场景中的适用性，为自动化优化建模提供了新的思路。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 大语言模型虽擅长推理与代码生成，但在工程问题求解中难以保证所建数学模型满足数据与物理约束的可行性。
method: 提出EngiAgent多智能体系统，采用全连接协调机制，通过多智能体分工完成开放式分析、可行性驱动建模与迭代修正。
result: 在开放式工程问题求解任务上，该方法能够生成满足约束的可行解，优于难以保证可行性的常规大语言模型。
conclusion: 表明多智能体协调可增强LLM自动化建模的可行性保障能力，为运筹优化建模自动化提供参考。
---

## Abstract
Engineering problem solving is central to real-world decision-making, requiring mathematical formulations that not only represent complex problems but also produce feasible solutions under data and physical constraints. Unlike mathematical problem solving, which operates on predefined formulations, engineering tasks demand open-ended analysis, feasibility-driven modeling, and iterative refinement. Although large language models (LLMs) have shown strong capabilities in reasoning and code generation, they often fail to ensure feasibility, which limits their applicability to engineering problem solving. To address this challenge, we propose EngiAgent, a multi-agent system with a fully connected coordinator that simulates expert workflows through specialized agents for problem analysis, modeling, verification, solving, and solution evaluation. The fully connected coordinator enables flexible feedback routing, overcoming the rigidity of prior pipeline-based reflection methods and ensuring feasibility at every stage of the process. This design not only improves robustness to diverse failure cases such as data extraction errors, constraint inconsistencies, and solver failures, but also enhances the overall quality of problem solving. Empirical results across four representative domains demonstrate that EngiAgent achieves substantial improvements in feasibility compared to prior approaches, establishing a new paradigm for feasibility-oriented engineering problem solving with LLMs. Our source code and data are available at https://github.com/AI4Engi/EngiAgent.

---

## 论文详细总结（自动生成）

## 重要说明
- 提供的 PDF 提取文本实际为 OpenReview 的人机验证页面，未包含论文正文、实验设置、附录或算力说明。
- 以下总结严格基于可获取的标题、摘要与元数据；凡未提及之处，均标注为“未说明”或“无法判断”，不补充臆测信息。

## 1. 论文的核心问题与整体含义
- **研究动机**：工程问题求解不同于数学题求解，它要求数学模型既能刻画复杂现实问题，又能在数据约束和物理约束下给出**可行解**。
- **核心痛点**：大语言模型虽擅长推理与代码生成，但在开放式工程问题中往往**难以保证可行性**，即可能生成形式合理但违反约束、无法求解或不可实施的方案。
- **整体含义**：论文提出 EngiAgent，试图通过多智能体协调，将工程问题求解从“生成答案/代码”推进到“开放式分析—可行性驱动建模—迭代修正—可行解产出”的完整流程，为 LLM 自动化优化建模提供新范式。

## 2. 论文提出的方法论
- **核心思想**：构建一个多智能体系统，并用**全连接协调器**模拟专家工作流；各智能体分工完成问题分析、建模、验证、求解和解评估。
- **关键技术细节**：
  - 专门智能体分别负责：问题分析、数学建模、模型验证、求解、解评估。
  - 全连接协调器支持**灵活反馈路由**，而非固定流水线式反思；当某阶段失败时，可将反馈发送到任意相关智能体进行修正。
  - 目标是在流程的每个阶段保障可行性，并提升对数据提取错误、约束不一致、求解器失败等问题的鲁棒性。
- **可概括流程**：输入工程问题 → 分析目标、数据与约束 → 构建数学模型 → 验证模型一致性 → 调用求解器求解 → 评估解是否可行 → 若失败则由协调器路由反馈并迭代修正，直至得到可行解。
- **公式/算法**：当前可获取文本中未给出具体公式、伪代码或算法细节。

## 3. 实验设计
- **数据集/场景**：摘要称在**四个代表性领域**上进行实验，但未列出具体领域名称、数据集、场景构造方式或 benchmark 名称。
- **Benchmark**：未说明 benchmark 的具体定义、评价协议或数据来源。
- **对比方法**：摘要称与“先前方法”和常规 LLM 方法比较，但未列出具体基线模型、消融设置或对比系统。
- **评价指标**：主要强调**可行性**提升，可能还涉及求解质量，但具体指标定义未说明。
- **元数据补充**：据元数据，论文被 ICML 2026 接收，并提供源代码与数据链接：https://github.com/AI4Engi/EngiAgent。

## 4. 资源与算力
- 当前可获取文本中**未提及** GPU 型号、数量、训练/推理时长、token 消耗、API 调用成本或集群规模。
- 因此无法总结其算力需求，也无法评估全连接多智能体协调带来的计算与通信开销。

## 5. 实验数量与充分性
- 从摘要仅能确认：实验覆盖**四个代表性领域**。
- 无法确认具体做了多少组实验，例如不同数据集、不同基线、消融实验、失败案例分析、统计显著性检验或人工评估。
- 因此，实验是否充分、是否客观公平，**无法仅凭当前材料判断**。
- 若论文仅以“可行性”作为核心指标，可能不足以全面反映工程解的质量、成本、鲁棒性和可解释性；但这一点需正文验证。

## 6. 论文的主要结论与发现
- EngiAgent 在四个代表性领域上相较先前方法，在**可行性**方面取得显著提升。
- 全连接协调机制可增强系统对多种失败情形的鲁棒性，包括数据提取错误、约束不一致和求解器失败。
- 多智能体协调能够增强 LLM 自动化建模中的可行性保障能力，为运筹优化建模自动化提供参考。
- 论文主张建立一种**面向可行性**的 LLM 工程问题求解新范式。

## 7. 优点
- **问题定位准确**：聚焦工程问题中“可行解”这一关键痛点，而非仅关注推理或代码生成。
- **协调机制有创新点**：全连接反馈路由相比固定流水线式反思更灵活，理论上更适合开放式、多失败源的工程任务。
- **流程覆盖完整**：从问题分析、建模、验证、求解到解评估，形成闭环迭代。
- **鲁棒性导向明确**：显式考虑数据错误、约束冲突和求解失败等现实问题。
- **可复现性信号**：提供开源代码与数据链接，且据元数据被 ICML 2026 接收，具备一定学术认可度。

## 8. 不足与局限
- **全文不可得**：当前材料仅含摘要和元数据，无法核验方法细节、实验公平性、公式推导与实现质量。
- **实验信息不足**：未说明四个领域具体是什么、benchmark 如何构建、基线有哪些、评价指标如何定义。
- **算力与成本未报告**：全连接多智能体系统可能带来较高的 token、延迟和费用开销，但论文未提供相关数据。
- **泛化性未知**：四个领域是否足以代表真实开放式工程问题，存在覆盖不足或选择偏差风险。
- **可行性依赖外部组件**：模型验证和求解仍可能依赖求解器、约束形式化质量以及 LLM 自身可靠性，错误仍可能在智能体间传播。
- **应用限制未展开**：可扩展性、实时性、安全性、人机协作方式和失败模式分析等，在当前可获取信息中均未说明。

（完）
