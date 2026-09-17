---
title: Constructing Industrial-Scale Optimization Modeling Benchmark
title_zh: 构建工业级优化建模基准
authors: "Zhong Li, Hongliang Lu, Tao Wei, Yuxuan Chen, Wenyu Liu, Yuan Lan, Fan Zhang, Zaiwen Wen"
date: 2026-04-30
pdf: "https://openreview.net/pdf/85b9112ca2b501bd72c85c2e1f61677602ea9237.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 面向LLM优化建模的工业级基准MIPLIB-NL
tldr: 针对大语言模型优化建模评测多局限于玩具或合成问题、难以反映工业级难度的瓶颈，本文提出MIPLIB-NL基准。该基准通过结构感知的逆向构建方法，从真实混合整数模型中生成自然语言规格与参考建模及求解器代码的配对。实验表明其规模达数千至百万级变量与约束，能更真实地暴露建模难点。该工作为评估与推动LLM在运筹优化建模中的能力提供了关键测试平台。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM优化建模评测多为玩具或合成规模，掩盖了工业级问题的真实难度。
method: 通过结构感知逆向构建方法，从真实混合整数模型生成自然语言规格与求解器代码配对的基准。
result: 基准覆盖数千至百万级变量与约束，更真实地暴露工业级建模难点。
conclusion: 为评估和推进LLM在运筹优化建模中的能力提供了关键测试平台。
---

## Abstract
Optimization modeling underpins decision-making in logistics, manufacturing, energy, and finance, yet translating natural-language requirements into correct optimization formulations and solver-executable code remains labor-intensive. Although large language models (LLMs) have been explored for this task, evaluation is still dominated by toy-sized or synthetic benchmarks, masking the difficulty of industrial problems with $10^{3}$--$10^{6}$ (or more) variables and constraints. A key bottleneck is the lack of benchmarks that align natural-language specifications with reference formulations/solver code grounded in real optimization models. To fill in this gap, we introduce MIPLIB-NL, built via a structure-aware reverse construction methodology from real mixed-integer linear programs in MIPLIB~2017. Our pipeline (i) recovers compact, reusable model structure from flat solver formulations, (ii) reverse-generates natural-language specifications explicitly tied to this recovered structure under a unified model--data separation format, and (iii) performs iterative semantic validation through expert review and human--LLM interaction with independent reconstruction checks. This yields 223 one-to-one reconstructions that preserve the mathematical content of the original instances while enabling realistic natural-language-to-optimization evaluation. Experiments show substantial performance degradation on MIPLIB-NL for systems that perform strongly on existing benchmarks, exposing failure modes invisible at toy scale.

---

## 论文详细总结（自动生成）

# 论文总结：Constructing Industrial-Scale Optimization Modeling Benchmark

> 说明：提供的 PDF 提取文本为 OpenReview 验证页面，未包含论文正文；以下总结主要基于标题、元数据与摘要，因此涉及实验细节、算力、对比方法等部分只能标注“文中未明确说明”。

## 1. 核心问题与整体含义
- **研究动机**：优化建模广泛支撑物流、制造、能源、金融等领域的决策，但将自然语言需求转化为正确的优化公式与求解器可执行代码仍高度依赖人工。
- **关键瓶颈**：尽管 LLM 已被用于优化建模，现有评测多局限于玩具规模或合成基准，无法反映工业级问题中 \(10^3\)--\(10^6\) 甚至更多变量与约束的真实难度。
- **整体含义**：论文提出工业级基准 **MIPLIB-NL**，旨在填补“自然语言规格—参考建模/求解器代码”之间缺乏真实优化模型支撑的空白，为评估和推动 LLM 在运筹优化建模中的能力提供测试平台。

## 2. 方法论
- **核心思想**：采用**结构感知的逆向构建方法**，从真实混合整数线性规划模型中反向生成自然语言规格与参考建模/求解器代码配对。
- **关键技术流程**：
  1. **恢复模型结构**：从扁平的求解器公式中恢复紧凑、可复用的模型结构。
  2. **反向生成自然语言规格**：在统一的“模型—数据分离”格式下，生成与恢复结构显式绑定的自然语言规格。
  3. **迭代语义验证**：通过专家评审、人类—LLM 交互以及独立重构检查，进行多轮语义验证。
- **产出形式**：最终得到 **223 个一对一重建实例**，在保留原始实例数学内容的同时，支持真实的“自然语言到优化建模”评测。

## 3. 实验设计
- **数据集/场景**：基于 **MIPLIB 2017** 中的真实混合整数线性规划实例构建 **MIPLIB-NL**。
- **Benchmark 特点**：覆盖数千至百万级变量与约束，强调工业级规模与真实建模难点。
- **对比方法**：摘要仅提到评估了“在现有基准上表现强劲的系统”，但未列出具体系统名称、模型版本或 baseline 细节。
- **任务形式**：自然语言到优化建模/求解器代码的生成与重建评测。

## 4. 资源与算力
- 可获取文本中**未明确说明** GPU 型号、数量、训练时长、推理成本或集群规模等信息。
- 因此无法判断该方法或评测本身的算力开销，也无法评估其可复现性与资源门槛。

## 5. 实验数量与充分性
- 已知实验核心围绕 **223 个一对一重建实例**展开，但摘要未给出具体实验组数、消融实验、统计检验或不同设置下的对比。
- 摘要称系统在 MIPLIB-NL 上出现“显著性能退化”，说明基准具有区分度。
- 验证流程包含专家评审、人类—LLM 交互和独立重构检查，这有助于提升数据质量与客观性。
- 但由于全文不可得，无法全面判断实验是否充分、公平，是否存在选择性报告或评测偏差。

## 6. 主要结论与发现
- 现有 LLM 优化建模评测在玩具或合成规模上可能掩盖真实工业难度。
- 在 MIPLIB-NL 上，原本在已有基准上表现强的系统出现**显著性能下降**，暴露出玩具规模下不可见的失败模式。
- MIPLIB-NL 可作为评估和推进 LLM 运筹优化建模能力的关键测试平台。

## 7. 优点
- **填补空白**：首次强调并构建工业级规模的优化建模自然语言基准。
- **真实性强**：直接基于 MIPLIB 2017 真实混合整数模型，而非合成问题。
- **方法严谨**：结构感知逆向构建、统一模型—数据分离格式、迭代语义验证和独立重构检查，提升了规格与参考代码的一致性。
- **规模覆盖广**：变量与约束从数千到百万级，能更真实地暴露建模难点。
- **评测价值高**：能够揭示现有系统在工业级问题上的性能退化与失败模式。

## 8. 不足与局限
- **全文信息缺失**：PDF 实际为验证页面，无法核验实验设计、指标、baseline、算力与复现细节。
- **覆盖范围有限**：仅基于 MIPLIB 2017，主要覆盖混合整数线性规划，未必涵盖非线性、随机、动态或多目标优化等更广泛场景。
- **自然语言规格偏差风险**：规格由逆向生成，可能与真实用户需求或行业表述存在差异。
- **数据污染风险**：MIPLIB 2017 是公开基准，LLM 预训练可能接触过相关实例，需额外检查记忆与泄漏问题。
- **实验充分性未知**：223 个重建实例虽有价值，但相对工业应用广度仍有限；缺少消融、统计显著性与多基线比较信息。
- **资源与成本未报告**：无法评估方法或评测的算力需求、推理成本和可扩展性。

（完）
