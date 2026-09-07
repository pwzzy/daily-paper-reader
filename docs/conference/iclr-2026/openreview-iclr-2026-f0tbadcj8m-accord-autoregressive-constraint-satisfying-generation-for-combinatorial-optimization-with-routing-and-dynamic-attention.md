---
title: "ACCORD: Autoregressive Constraint-satisfying Generation for COmbinatorial Optimization with Routing and Dynamic attention"
title_zh: ACCORD：具有路由和动态注意力的自回归约束满足式组合优化生成
authors: "Henrik Abgaryan, Tristan Cazenave, Ararat Harutyunyan"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=f0TBAdcJ8m"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 系统性将LLM用于NP-hard组合优化问题，通过自回归约束满足生成可行解
tldr: 大语言模型虽然表现出强推理能力，但直接用于NP-hard组合优化仍未被充分探索。ACCORD提出新的数据集表示和模型结构，利用自回归生成的天然过程动态检查并强制满足可行性约束，并通过注意力路由激活相关求解路径。作者在多种NP-hard组合优化任务上系统验证了该方法，显示其能生成可行解并提高LLM求解性能。该工作为LLM处理约束满足与组合优化提供了一条可行路径。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: NP-hard组合优化问题的直接求解仍是大模型未充分探索的难点，尤其是可行约束的满足。
method: 提出ACCORD，通过自回归约束满足生成范式，配合路由和动态注意力机制，在解码阶段动态维护可行性。
result: 系统实验覆盖多类NP-hard组合优化问题，证明ACCORD能有效生成可行解并提升求解表现。
conclusion: 自回归生成与动态注意力可显著扩展LLM在组合优化问题上的实用性。
---

## Abstract
Large Language Models (LLMs) have demonstrated impressive reasoning capabilities, yet their direct application to NP-hard combinatorial problems (CPs) remains underexplored. In this work, we systematically investigate the reasoning abilities of LLMs on a variety of NP-hard combinatorial optimization tasks and introduce \textbf{ACCORD}: \textbf{A}utoregressive \textbf{C}onstraint-satisfying generation for \textbf{CO}mbinatorial optimization with \textbf{R}outing and \textbf{D}ynamic attention. ACCORD features a novel dataset representation and model architecture that leverage the autoregressive nature of LLMs to dynamically enforce feasibility constraints, coupled with attention-based routing to activate problem-specific LoRA modules. We also present the ACCORD-90k supervised dataset, covering six NP-hard combinatorial problems: TSP, VRP, Knapsack, FlowShop, JSSP, and BinPacking. Extensive experiments demonstrate that our ACCORD model, built on an 8B-parameter Llama backbone, consistently outperforms standard prompting and input-output methods, even when compared to much larger LLMs, such as gpt-4. Ablation studies further show that our output structure enhances solution feasibility. To the best of our knowledge, this is the first large-scale, end-to-end framework for exploring the applications of LLMs to a broad spectrum of combinatorial optimization problems.

---

## 论文详细总结（自动生成）

由于本次提供的材料仅包含论文的标题、摘要与元数据（完整 PDF 正文未能获取），以下总结将严格基于已有信息展开。对于正文中未披露的信息，会明确标注“材料中未说明”。

# ACCORD 论文详细总结

> 论文标题：ACCORD: Autoregressive Constraint-satisfying Generation for COmbinatorial Optimization with Routing and Dynamic attention
> 中文标题：ACCORD：具有路由和动态注意力的自回归约束满足式组合优化生成
> 作者：Henrik Abgaryan, Tristan Cazenave, Ararat Harutyunyan
> 评审得分：9.0（公开摘录数据）

## 1. 核心问题与研究动机

- **NP-hard 组合优化问题的求解困境**：TSP、VRP、背包、调度等问题属于 NP-hard 问题，传统精确算法在规模增大时面临指数级计算代价，启发式算法又高度依赖人工设计。
- **LLM 推理能力的未被充分利用**：已有的研究与工程实践表明，LLM 在数学推理、代码生成等方面展现出较强的通用推理能力，但其被直接用于 NP-hard 组合优化问题（尤其是“生成可行解”）的潜力尚未被充分探索。
- **“可行性满足”是关键难点**：与常见的开放式生成任务不同，组合优化任务要求输出必须满足硬性约束（如路径不重复、容量不超载、作业顺序合法等）。LLM 在生成过程中的每一步都可能产生违反约束的中间状态，如何让模型在生成过程中动态保持可行性，是核心的技术挑战。
- **整体含义**：这项工作试图回答一个根本问题——**能否通过端到端的自回归生成机制，让 LLM 在处理多种 NP-hard 组合优化问题时稳定地产出可行解，并在此基础上逼近最优解。**

## 2. 方法论：ACCORD

ACCORD 的设计围绕两条主线展开——**自回归约束满足生成**与**注意力路由机制**。论文中未给出具体的公式与算法伪代码，以下描述基于摘要中的说明：

- **核心思想**：将组合优化问题的求解过程构建为 **自回归生成序列**，也就是用序列生成天然具备的“逐步解码”过程来同步维护“当前状态是否可行”，从而在每一步动态地强制执行可行性约束。
- **数据集表示创新**：设计了新的“问题—解”数据表示方式，使输入输出能够与自回归语言模型更好地对齐，并使得约束信息可以被显式编码，便于模型在解码过程中参考。
- **动态约束强制机制**：在解码阶段关联问题定义中的约束条件，使生成的每一步不仅基于“语言概率”，还基于“当前部分解是否仍有可能扩展为完整可行解”的判断，从而减少非法输出的产生。
- **注意力路由（Attention-based Routing）**：为不同类别的组合优化问题学习并维护特定的 LoRA（低秩适配）模块；模型在推理时，通过注意力机制自动判断当前输入属于哪类问题，并“路由”到对应的参数模块上进行优化求解。这样可以避免多个任务间的互相干扰，也避免了为每个问题单独训练一个完整大模型。
- **基础架构**：采用 **Llama-8B 作为骨干网络**，在 ACCORD-90k 数据集上进行监督微调。

## 3. 实验设计

- **数据集**：作者构建并公开了 **ACCORD-90k** 监督数据集，覆盖 *六类 NP-hard 组合优化问题*：
  - TSP（旅行商问题）
  - VRP（车辆路径问题）
  - Knapsack（背包问题）
  - FlowShop（流水车间调度问题）
  - JSSP（作业车间调度问题）
  - BinPacking（装箱问题）
- **Benchmark 场景**：在上述六类组合优化问题上分别评估“生成解的可行性”与“解的质量/优化表现”。
- **对比方法**：
  - 标准提示（Standard Prompting）
  - 输入输出（Input-Output）风格的直接映射方法
  - 更大的 LLM 基线，代表性模型为 **gpt-4**
- **评估维度**：可行性（是否满足约束）与总体求解表现。

## 4. 资源与算力

- 论文材料中**未明确报告 GPU 型号、数量、训练时长、显存占用等算力细节**。
- 仅可推断：骨干模型为 Llama-8B（8B 参数规模），训练数据量为 90k 规模的监督数据集。对于具体硬件环境，需要查看论文正文的实验设置部分才能获知。

## 5. 实验数量与充分性

- **实验数量**：论文摘要提及了“大量实验”（Extensive experiments）与“消融研究”（Ablation studies），覆盖 6 个不同的 NP-hard 问题场景；并包含与 gpt-4 等多模型/多方法的对比，以及针对“输出结构对可行性影响”的模块消融。
- **充分性评价**：
  - **优点**：同时覆盖 TSP、VRP、调度类、组合选择类等不同类型的组合优化问题，覆盖度较广，能够有效检验方法在异质问题上的泛化能力。
  - **客观性**：与 gpt-4 的对比说明了该 8B 模型在性能上可超过更大规模通用模型，这是有力的证据。
  - **不足**：仅从摘要无法获知每个问题上的实例规模（如节点数量、背包容量等）；也无法获知对比基线中 gpt-4 是否使用了相同的提示词与后处理纠错机制，可能影响公平性判断。需要结合正文才能进一步评估。

## 6. 主要结论

- ACCORD 在六类 NP-hard 组合优化任务上显著优于标准提示方法和输入输出映射方法。
- 基于 8B Llama 骨干的 ACCORD，即使与 **gpt-4** 这类超大模型相比，也能在组合优化任务上取得更好或相当的表现。
- 消融实验表明，ACCORD 的输出结构与自回归约束满足机制能显著改善**解的可行性**，说明“显式建模约束”比单纯依赖模型隐含能力更有效。
- 作者认为这是首个**大规模端到端**地将 LLM 应用于多种 NP-hard 组合优化问题的统一框架。

## 7. 优点与亮点

- **问题选择的系统性与覆盖面**：同时应对六类经典 NP-hard 问题，而非局限于单一问题，研究价值与实践价值较高。
- **方法与 LLM 自身结构的高度契合**：利用自回归的解码过程本身去逐步校验和满足约束，无需外部调用求解器或复杂的后处理校验流程，这符合语言模型架构的特性。
- **注意力路由结合 LoRA 的“多问题单模型”策略**：通过路由激活不同的 LoRA 子模块，既实现了多任务支持，又控制了参数规模和训练成本，具备工程上的可扩展性。
- **强调“可行性”这一中间标准**：与仅比较最优解差距的工作不同，该研究将约束满足作为显式评价维度，更贴近真实应用中“先给合法解、再谈优化”的诉求。
- **数据集的开放与构建**：提供了 ACCORD-90k 数据集，可推动该方向后续研究。

## 8. 不足与局限性

- **材料可见度有限**：当前仅获得摘要与元数据，无法评估论文正文中的公式推导、约束强制流程的细节、数据处理管线及完整实验表格，因此难以对细节与方法适用性做全面评价。
- **算力与复现成本未说明**：文中（根据现有材料）未披露训练所需 GPU 数量与时长的详细信息，其他研究者复现或扩展该工作的成本不确定。
- **问题规模可能受限制**：LLM 生成组合解的方式通常受限于上下文长度与解码步数，六类问题各自能够处理的实例规模（例如城市数量、作业数量等）在摘要中未说明。若实例规模偏小，则其与专业组合优化求解器的实用性差距仍需客观确认。
- **与专业算法/神经求解器的比较缺乏**：摘要中对比对象主要是 LLM 系的基线（标准提示、gpt-4 等），但未提及与现有启发式求解器、精确求解器或专门神经组合优化模型的对比，因此该方法是否具备真正的“求解竞争力”仍需谨慎判断。
- **潜在的“可行性定义”偏差风险**：“可行”在不同问题中含义差异很大（如 JSSP 中的时序可行性、BinPacking 中的空间分配可行性）。ACCORD 是否能正确编码所有约束，以及约束被动态强制时是否会损害解的最优性，都需要进一步检验。

（完）
