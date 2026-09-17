---
title: "FlowBot: Inducing LLM Workflows with Bilevel Optimization and Textual Gradients"
title_zh: FlowBot：利用双层优化与文本梯度诱导大语言模型工作流
authors: "Hongyeon Yu, Young-Bum Kim, Yoon Kim"
date: 2026-04-30
pdf: "https://openreview.net/pdf/387d13bd62c5635a9c646236073bf28c105d72dc.pdf"
tags: ["query:llm-agent-or"]
score: 5.0
evidence: 用双层优化自动诱导LLM智能体与工作流
tldr: 协调多个LLM或智能体的工作流有潜力应对多样任务，但现有方法多依赖人工设计的流水线与提示，构成实际部署的瓶颈。论文提出FlowBot，将工作流诱导形式化为双层优化问题：外层优化工作流的高层草图，内层借助文本梯度进行优化，从而数据驱动地自动诱导智能体与工作流。方法无需人工手工设计即可产出有效工作流。该工作为自动化构建LLM智能体与工作流提供了数据驱动的新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 构建LLM工作流通常依赖人工设计的流水线与提示，成为实际部署的瓶颈。
method: 将工作流诱导建模为双层优化问题，外层优化高层草图，内层用文本梯度优化，数据驱动地诱导智能体与工作流。
result: 无需人工手工设计即可自动诱导出有效的工作流。
conclusion: 为自动化构建LLM智能体与工作流提供了数据驱动的新范式。
---

## Abstract
LLM workflows, which coordinate structured calls to individual LLMs/agents  to achieve a particular goal, offer a promising path towards  building powerful AI systems that can tackle diverse tasks. However, existing approaches for building such workflows generally rely on human-crafted pipelines and prompts, which presents a substantial bottleneck in real world deployment. How can we  automatically induce  LLM-based agents and workflows in a data-driven way? This paper describes a simple data-driven approach for  automatically inducing agents and LLM workflows. We formulate   workflow induction  as a bilevel optimization problem: an outer loop which optimizes a high-level sketch of the workflow (in particular how the LLM calls should be structured), and an inner loop which optimizes each individual LLM call one-by one. Both loops are optimized with "textual gradients" where for the inner loop we optimize each component in a modular way through "backpropagating" textual gradients layer-by-layer. We find that LLM workflows discovered through our FlowBot (work**flow** induction through **b**ilevel **o**ptimization and **t**extual gradients) approach performs competitively against strong baselines that make use of human-crafted  or generated workflows.

---

## 论文详细总结（自动生成）

# FlowBot：利用双层优化与文本梯度诱导 LLM 工作流 —— 论文总结

> **重要说明（信息可得性）**：所提供的 PDF 提取文本实际为 OpenReview 的 CAPTCHA 验证页面，**未包含论文正文**。因此本总结主要依据论文摘要（Abstract）与元数据（title/tags/tldr 等）撰写；凡摘要未涉及的部分（实验细节、算力、消融设置等），下文均明确标注为"未提供/无法确认"，不作臆测性补充。

---

## 一、核心问题与研究背景

- **研究动机**：LLM 工作流（LLM workflows）通过协调对单个 LLM/智能体的结构化调用来完成特定目标，是构建能应对多样任务的强 AI 系统的重要路径。
- **核心瓶颈**：现有构建此类工作流的方法**普遍依赖人工设计的流水线与提示（human-crafted pipelines and prompts）**，这在实际部署中构成显著瓶颈——人工设计成本高、难以规模化、难以针对新任务快速适配。
- **核心问题**：能否**以数据驱动的方式自动诱导（automatically induce）LLM 智能体与工作流**，从而摆脱对手工设计的依赖？
- **整体含义**：论文将"工作流诱导"从工程手工活转变为可优化的学习问题，为自动化构建 LLM 智能体与工作流提供了一种数据驱动的新范式（元数据 tldr 亦如此概括）。

---

## 二、方法论

### 核心思想
- 将**工作流诱导形式化为一个双层优化（bilevel optimization）问题**，分两个层级协同优化：
  - **外层循环（outer loop）**：优化工作流的**高层草图（high-level sketch）**，具体而言是决定 **LLM 调用应如何结构化/组织**（即工作流的拓扑与调用编排）。
  - **内层循环（inner loop）**：**逐个优化每一个单独的 LLM 调用**（optimize each individual LLM call one by one）。
- 方法命名即体现其三大要素：**Flow**Bot = work**flow** induction through **b**ilevel **o**ptimization and **t**extual gradients。

### 关键技术细节
- **文本梯度（textual gradients）**：两个循环均使用"文本梯度"进行优化——即以自然语言形式的反馈/指令作为更新信号（这是 LLM 时代替代数值梯度的常见范式，摘要中明确点出该术语）。
- **模块化逐层反传**：内层循环以**模块化方式**优化每个组件，方式是**逐层"反向传播"文本梯度（backpropagating textual gradients layer-by-layer）**。这暗示工作流被视作可分解的层/模块栈，误差信号自输出端逐层向前传递并转化为对每一层提示或组件的文本修改指令。
- **自动化程度**：整个流程无需人工手工设计，即可数据驱动地产出有效工作流。

### 算法流程（依摘要可推知的高层框架）
1. 初始化一个工作流的高层草图（调用结构）。
2. **内层**：固定当前结构，对其中每一个 LLM 调用/模块逐个用文本梯度优化；采用逐层反传的方式，使上游模块的更新能利用下游传来的文本反馈。
3. **外层**：基于内层优化后的表现，用文本梯度更新工作流的高层结构草图（增删/重排 LLM 调用）。
4. 交替执行内外层，直至收敛，得到最终诱导出的工作流与智能体。

> **未提供**：具体的目标函数形式、文本梯度的生成与聚合公式、外层结构的搜索空间定义、收敛判据、超参数设置等，摘要与元数据中均未给出。

---

## 三、实验设计

- **数据集 / 场景**：**未提供**。摘要未指明使用的具体任务、数据集或领域。
- **Benchmark**：**未提供**（摘要未说明评测基准的名称与构成）。
- **对比方法**：摘要明确指出与"**使用人工设计工作流或生成式工作流的强基线（strong baselines that make use of human-crafted or generated workflows）**"进行比较。可归纳为两类基线：
  1. **人工手工设计的工作流（human-crafted workflows）**；
  2. **自动生成的工作流（generated workflows）**。
- **具体基线名称、规模与实现细节**：**未提供**。

---

## 四、资源与算力

- 摘要与所给元数据中**完全未提及** GPU 型号、GPU 数量、训练/推理时长、总 token 消耗或 API 调用预算等任何算力信息。
- **无法确认**该方法的计算开销与可复现性所需的资源门槛；这一点在原文正文中可能有说明，但当前提取内容不可得。

---

## 五、实验数量与充分性

- **实验组数**：**未提供**。无法确认涉及多少个数据集、多少种任务类型，也无法确认是否包含消融实验（如：去掉外层优化、去掉内层逐层反传、替换文本梯度为直接提示等）。
- **充分性与公平性评估**：由于缺少实验细节，**无法作出客观判断**。仅从摘要表述看，作者声称方法"**perform competitively against strong baselines**"（与强基线相比具有竞争力）——注意此处措辞是"competitive"（有竞争力）而非"显著超越"，这在一定程度上是较为保守的表述。
- **元数据补充**：该论文在 OpenReview 上的评分为 **5.0**（中等偏中性），标签为 `query:llm-agent-or`，来源标注为 **ICML-2026-Accepted**。该分数与"竞争力而非压倒性优势"的表述方向一致，提示其实验说服力可能存在争议空间。

---

## 六、主要结论与发现

- **核心结论**：FlowBot 能够**在无需人工手工设计的前提下，自动诱导出有效的 LLM 智能体与工作流**。
- **性能结论**：通过 FlowBot 发现的工作流，在性能上与使用**人工手工设计或自动生成工作流的强基线相比具有竞争力**。
- **范式意义**：该工作表明"工作流诱导"可以作为双层优化问题被有效求解，为自动化构建 LLM 智能体与工作流提供了**数据驱动的新范式**，从而有望缓解实际部署中人工设计流水线与提示的瓶颈。

---

## 七、优点

- **问题定位精准且具现实价值**：直击 LLM 工作流部署中"人工设计不可扩展"的真实痛点，动机清晰。
- **方法论框架优雅**：将工作流诱导统一为**双层优化**——外层管结构（调用编排）、内层管组件（每个 LLM 调用），层次分明，天然对应"架构搜索 + 组件优化"的经典范式，概念上易于理解与推广。
- **优化手段契合 LLM 特性**：采用**文本梯度**而非数值梯度，避免了 LLM 工作流中结构不可微的难题；内层"**逐层反传文本梯度**"的模块化设计使优化信号可以在层间传递，兼顾了模块独立性与全局一致性。
- **自动化程度高**：端到端数据驱动，无需人工设计流水线与提示，具备良好的可迁移与可扩展潜力。
- **表述克制**：结论使用"competitive"而非夸大其词，学术表述相对审慎。

---

## 八、不足与局限

- **本文可得信息严重受限**：所给 PDF 提取文本为验证页面，**正文、实验章节、附录均缺失**，因此以下判断部分基于"信息缺口"而非对方法本身的否定。
- **实验覆盖未知**：未说明任务类型（推理、检索、代码、多跳问答等）、数据规模与领域多样性，无法评估泛化性。
- **无消融证据**：无法判断外层优化、内层逐层文本梯度反传、双层交替等各组件各自的贡献；若缺少消融，将难以归因性能来源。
- **公平性存疑点**：与"人工手工设计工作流"比较时，人工基线的强度高度依赖设计者投入与调优程度，存在**基线强度不透明**的风险；与"自动生成工作流"比较时，则需确认生成预算是否对齐（如 token 数、LLM 调用次数）。这些信息当前均不可得。
- **算力与成本未披露**：双层优化意味着多次 LLM 调用与迭代，**推理成本可能显著高于单次提示**；缺少算力披露使实际部署可行性难以评估。
- **潜在偏差风险**：若文本梯度由同一 LLM 生成并用于优化同一 LLM 工作流，可能引入**自我评估偏差（self-evaluation bias）**，即优化目标与评测目标同源导致的过拟合风险。此点为一般性质疑，需原文验证。
- **收敛性与稳定性**：文本梯度优化在长程、多层反传下可能出现信号衰减、误差累积或局部最优，摘要未提及相应的稳定性保障机制。
- **应用限制**：方法面向"结构化 LLM 调用"的工作流，对需要外部工具、真实环境交互或多模态的场景是否适用，尚不明确。

---

（完）
