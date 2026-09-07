---
title: "OptiMind: Teaching LLMs to Think Like Optimization Experts"
title_zh: OptiMind：教LLM像优化专家一样思考
authors: "Zeyi Chen, Xinzhi Zhang, Humishka Zope, Hugo De Oliveira Barbalho, Konstantina Mellou, Marco Molinaro, Janardhan Kulkarni, Ishai Menache, Sirui Li"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=CvwLtwlraW"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 聚焦利用LLM将自然语言转化为MILP优化模型，直接匹配混合整数规划建模需求
tldr: 从自然语言生成数学规划模型是依赖专家技能的困难任务，现有LLM方法因训练数据稀少且含噪、缺少领域知识而准确率有限。OptiMind系统性地融入优化专家知识，利用半自动化数据生成与靶向训练来提升混合整数线性规划建模能力。实验结果显示该框架能更准确地把自然语言问题转换为可执行的MILP模型。该工作为知识增强的LLM自动化运筹建模提供了实用范式。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 数学规划表达需要运筹学专业知识，现有LLM建模方法受限于数据稀缺、噪声高且未利用领域知识，准确率不足。
method: 提出OptiMind框架，将优化专家知识系统性融入LLM，利用半自动数据组织方式改善MILP模型生成能力。
result: 相比现有自动建模方法，OptiMind显著提升混合整数线性规划公式化的准确率。
conclusion: 领域知识增强的训练策略能有效提高LLM生成可执行优化模型的能力，降低建模门槛。
---

## Abstract
Mathematical programming -- the task of expressing operations and decision-making problems in precise mathematical language -- is fundamental across domains, yet remains a skill-intensive process requiring operations research expertise. Recent advances in large language models for complex reasoning have spurred interest in automating this task, translating natural language into executable optimization models. Current approaches, however, achieve limited accuracy, hindered by scarce and noisy training data without leveraging domain knowledge. In this work, we systematically integrate optimization expertise to improve formulation accuracy for mixed-integer linear programming, a key family of mathematical programs. Our OptiMind framework leverages semi-automated, class-based error analysis to guide both training and inference, explicitly preventing common mistakes within each optimization class. Our resulting fine-tuned LLM significantly improves formulation accuracy by 21.4\% across multiple optimization benchmarks, with consistent gains under test-time scaling methods such as self-consistency and multi-turn feedback, enabling further progress toward robust LLM-assisted optimization formulation.

---

## 论文详细总结（自动生成）

# OptiMind 论文中文总结

## 1. 论文的核心问题与整体含义

- **背景与动机**：数学规划——用精确数学语言刻画运营与决策问题——在众多领域中是基础性的，但它高度依赖运筹学专业知识，属于技能密集型任务。近年来，大语言模型在复杂推理上的进展促使研究者探索将自然语言问题自动转化为可执行的优化模型。
- **现有瓶颈**：当前 LLM 自动建模方法准确率有限，主要受限于训练数据稀缺且噪声较大，同时未充分挖掘和利用领域知识。
- **核心问题**：如何系统性地将优化专家知识融入 LLM，提升混合整数线性规划（MILP）建模的准确率。
- **整体含义**：论文提出 OptiMind 框架，试图为知识增强的 LLM 自动化运筹建模提供一种可复用的实用范式，最终目标是降低数学建模的专业门槛。

## 2. 论文提出的方法论

- **核心思想**：将优化专业知识系统地整合到 LLM 中，采用“半自动、基于类别的错误分析”（semi-automated, class-based error analysis）来同时指导训练和推理过程，显式地预防每一类优化问题中的常见错误。
- **MILP 专门化**：方法聚焦于 MILP——数学规划的重要子类；通过针对其结构特点进行错误模式归纳与规避。
- **训练阶段**：利用类别化的错误分析构造数据与训练信号，对 LLM 进行微调（fine-tuned），使模型内化专家知识。
- **推理阶段**：同样的类别化错误分析被用于引导推理，在生成 MILP 公式时主动避免该类别中典型错误。
- **算法流程（文字描述）**：给定自然语言问题 → 判断问题所属优化类别/类模板 → 结合该类别已知易错点进行受约束的推理 → 输出可执行的 MILP 模型。摘要未给出具体数学公式、损失函数或模型结构细节。

## 3. 实验设计

- **数据集 / 基准**：摘要提到在“多个优化基准”（multiple optimization benchmarks）上进行了评估，但未列出具体基准名称（如 NL4OPT、AMPL 等）和样本规模。
- **对比方法**：与“现有自动建模方法”进行了对比，但未给出具体基线方法名称。
- **评测指标**：公式化准确率（formulation accuracy）。
- **扩展性测试**：额外评估了 test-time scaling 方法——self-consistency（自洽性）和 multi-turn feedback（多轮反馈）——下模型的增益是否保持。
- **主要结果**：OptiMind 相比现有方法显著提升公式准确率 21.4%，且在 self-consistency / 多轮反馈等推理时扩展方法下获得一致的增益。

## 4. 资源与算力

- 所提供的摘要和元数据中**没有明确说明**使用的 GPU 型号、数量、训练时长、模型参数规模或计算预算。
- 仅能推断该方法涉及“微调 LLM”，但无法据此估计所需算力。

## 5. 实验数量与充分性

- 摘要层面可确认的实验观测包括：多个 MILP 优化基准上的主实验 + 与 self-consistency / multi-turn feedback 结合的扩展实验。
- **未提供**：具体实验数量、每个基准的条目数、消融实验、不同优化类别的分项表现、基线的详细配置。
- 因此，仅凭现有信息**无法充分评估实验的客观性与公平性**，例如无法判断是否覆盖了足够多样化的 MILP 问题形态、类别定义是否完整，也难以检查是否存在数据泄漏或基准选择偏差。

## 6. 论文的主要结论与发现

- OptiMind 通过在训练和推理中注入类别化优化专家知识，显著改善了 LLM 从自然语言生成 MILP 模型的能力。
- 在多个基准上相对现有自动建模方法取得 21.4% 的准确率提升。
- 该方法与 self-consistency、多轮反馈等 test-time scaling 策略兼容，表明其收益可叠加，支持进一步通过推理时计算获得更强性能。
- 总体结论：领域知识增强的训练策略可以有效提高 LLM 生成可执行优化模型的能力，为自动化运筹建模提供了一条可行路径。

## 7. 优点

- **知识注入方式有针对性**：不是单纯增加语料数据，而是利用优化类别进行结构化错误分析，能够显式规避常见失误，更具可解释性。
- **训练与推理统一**：同一套类别化错误分析同时用于训练和推理，前后一致，易于工程化。
- **性能提升显著**：21.4% 的准确率提升幅度可观，且增益在多种推理时扩展方式下保持，说明结论具有稳健性。
- **降低建模门槛**：具有较强的应用价值，可帮助非运筹学专家生成正确的 MILP 模型。

## 8. 不足与局限

- **信息完整度不足**：提供的文本仅含摘要与元数据，缺少完整论文细节，无法评估具体方法实现、数据来源和实验设置的严密性。
- **问题范围有限**：仅关注 MILP，未讨论对非线性、随机、动态规划等其他数学规划族的适用性。
- **依赖类别体系**：方法依赖预定义的优化类别及每类常见错误模板；若类别体系覆盖不全或遇到新的问题类型，效果可能明显下降。
- **数据质量风险**：半自动数据生成依然可能引入噪声，摘要未说明噪声控制和质量筛选机制。
- **基准与泛化问题**：未给出基准的细粒度描述，也未验证在真实世界、非规范化自然语言输入上的鲁棒性；公开摘要无法排除对特定基准风格过拟合的可能性。

（完）
