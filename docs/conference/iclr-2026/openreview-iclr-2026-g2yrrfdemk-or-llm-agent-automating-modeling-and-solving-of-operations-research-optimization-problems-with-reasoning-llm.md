---
title: "OR-LLM-Agent: Automating Modeling and Solving of Operations Research Optimization Problems with Reasoning LLM"
title_zh: OR-LLM-Agent：利用推理大语言模型自动建模与求解运筹优化问题
authors: "Bowen Zhang, Pengcheng Luo, Genke Yang, SOONG BOON HEE, Chau Yuen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=G2yRrFdEmK"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 提出基于推理大语言模型的智能体框架，自动完成运筹问题的数学建模、代码生成与调试，直接命中LLM智能体用于OR建模与求解的需求。
tldr: 现有方法大多依靠提示工程或微调非推理大模型来求解运筹优化问题，能力受限且难以稳定。OR-LLM-Agent转而以推理大模型为底座，将任务拆解为数学建模、代码生成和调试三个阶段，每个阶段由专门的子智能体负责。整体框架面向运筹问题实现端到端自动化建模与求解，旨在突破非推理模型在复杂数学推理与程序生成上的瓶颈。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 当前基于提示工程或微调非推理LLM的运筹优化求解方式能力有限，无法胜任复杂建模与求解。
method: 提出以推理LLM为核心的OR-LLM-Agent，将运筹任务分解为数学建模、代码生成与调试三个阶段，由专用子智能体分工处理。
result: 该框架旨在显著提升运筹问题自动化建模、代码生成及调试的成功率，优于依赖非推理LLM的已有方案。
conclusion: 说明推理式LLM多智能体框架可更可靠地实现运筹优化问题的端到端自动化求解。
---

## Abstract
With the rise of artificial intelligence (AI), applying large language models (LLMs) to mathematical problem-solving has attracted increasing attention. Most existing approaches attempt to improve Operations Research (OR) optimization problem-solving through prompt engineering or fine-tuning strategies for LLMs. However, these methods are fundamentally constrained by the limited capabilities of non-reasoning LLMs. To overcome these limitations, we propose OR-LLM-Agent, an AI agent framework built on reasoning LLMs for automated OR problem solving. The framework decomposes the task into three sequential stages: mathematical modeling, code generation, and debugging. Each task is handled by a dedicated sub-agent, which enables more targeted reasoning. We also construct BWOR, an OR dataset for evaluating LLM performance on OR tasks. Our analysis shows that in the benchmarks NL4OPT, MAMO, and IndustryOR, reasoning LLMs sometimes underperform their non-reasoning counterparts within the same model family. In contrast, BWOR provides a more consistent and discriminative assessment of model capabilities. Experimental results demonstrate that OR-LLM-Agent utilizing DeepSeek-R1 in its framework outperforms advanced methods, including GPT-o3, Gemini 2.5 Pro, DeepSeek-R1, and ORLM, by at least 7% in accuracy. These results demonstrate the effectiveness of task decomposition for OR problem solving.

---

## 论文详细总结（自动生成）

## 说明

以下总结基于提供的论文摘要和 OpenReview 元数据整理。论文正文未直接获取，因此部分细节（如模型配置、具体实验表格、算法伪代码等）只能依据摘要内容进行推断或标注为“未提供”。

# OR-LLM-Agent：利用推理大语言模型自动建模与求解运筹优化问题——论文深度总结

## 1. 核心问题与研究动机

- 背景：大语言模型（LLM）越来越多地被用于数学问题求解，运筹优化（OR）问题也是重要应用方向。
- 现有痛点：已有研究大多依赖**提示工程（prompt engineering）**或**微调非推理型 LLM**来提升 OR 问题求解能力。但由于非推理模型在复杂数学推理、约束理解和程序生成上能力有限，这类方法存在明显的性能天花板。
- 论文核心问题：如何构建一个基于**推理 LLM** 的自动化智能体框架，使得模型能够端到端完成“自然语言 OR 问题 → 数学建模 → 求解代码 → 调试修正 → 最终解答”这一流程？
- 整体含义：作者希望通过“推理 LLM + 任务分解 + 多子智能体”的设计，突破非推理模型在 OR 任务上的瓶颈，提供一种更可靠、可泛化的自动化优化求解方式。

## 2. 方法论：OR-LLM-Agent

- **核心思想**：将原本需要单个 LLM 全链路完成的 OR 求解任务，解耦为三个顺序阶段；每个阶段由专门设计的子智能体（sub-agent）负责，以获得更有针对性的推理和更高的单步成功概率。
- **三个关键阶段**：
  1. **数学建模（Mathematical Modeling）**：将自然语言描述的运筹问题转化为数学表达，包括决策变量、目标函数、约束条件等。
  2. **代码生成（Code Generation）**：将数学模型转化为可执行程序，通常对应调用优化求解器或数值求解工具的代码。
  3. **调试（Debugging）**：运行生成的代码，根据错误信息、输出结果或约束违反情况，返回模型或代码进行修正，直至求得有效解。
- **流程概况**：  
  输入问题 → 建模子智能体 → 代码生成子智能体 → 调试子智能体 → 输出优化结果。  
  每一步都由独立智能体处理，从而避免单一长链推理导致的误差累积。
- **技术要点**：
  - 底层使用推理型 LLM（如 DeepSeek-R1）作为骨干，而非普通非推理模型。
  - 框架不依赖针对性的任务微调，而是依赖模型的推理能力和 Agent 化的任务拆解。
  - 论文摘要中未给出更细粒度的算法公式、Prompt 模板、子智能体交互协议或调试策略，因此这部分属于“待补充实现细节”。

## 3. 实验设计、数据集与对比方法

- **评估数据集/场景**：
  - `NL4OPT`：既有自然语言到数学优化问题的基准。
  - `MAMO`：用于评估 LLM 在多类 OR 任务上的建模与求解能力。
  - `IndustryOR`：工业场景下的 OR 任务基准。
  - `BWOR`：论文自建的 OR 数据集，用于更稳定和更有区分度地评估 LLM 的 OR 能力。
- **评测基准上的额外发现**：
  - 在 `NL4OPT`、`MAMO`、`IndustryOR` 等旧基准上，推理型 LLM 有时会输给**同一模型家族中的非推理版本**，说明这些基准的区分度和稳定性有限。
  - `BWOR` 则提供了更一致和更具判别力的能力评估。
- **对比方法**：
  - GPT-o3
  - Gemini 2.5 Pro
  - DeepSeek-R1
  - ORLM
- **主结果**：
  - 使用 DeepSeek-R1 作为底座的 OR-LLM-Agent 在准确率上超过上述基线模型/方法至少 **7%**。
- **未提供的信息**：
  - 各数据集上的独立结果表、误差范围、每个任务类型的难度分层、重复实验次数均未在摘要中给出。

## 4. 资源与算力

- 论文摘要和元数据中**没有说明实验所用 GPU 型号、GPU 数量、训练/推理时长、API 调用成本或部署资源**。
- 由于该框架依赖 DeepSeek-R1 这类大型推理模型，实际运行成本可能较高，但原文未披露，无法为其实用性和经济性提供评价依据。

## 5. 实验数量与充分性分析

- 从可获得的摘要信息看，实验覆盖了至少 **4 个评估数据集**（NL4OPT、MAMO、IndustryOR、BWOR），并对比了多个强基线模型，规模上具有一定覆盖面。
- 但实验充分性存在明显不足

存在明显不足：摘要中仅汇报了与多个基线模型的整体准确率对比，但没有提供分阶段子智能体对整体效果的独立贡献分析，也没有展示不同底座模型（如 GPT、Gemini 替换 DeepSeek-R1）下框架性能的稳定性，因此无法判断该框架对底层推理模型的依赖程度，以及建模、代码生成、调试三个模块之间是否存在交互增益或瓶颈。此外，BWOR 数据集的构建方法、规模、难度分布、人工验证方式及与既有基准的差异性均未说明，增强了 BWOR 结果对“更好评估”这一主张的可信性风险。在鲁棒性和泛化层面，摘要未给出不同 OR 问题族（如生产调度、路径规划、资源分配、装箱问题等）上的分项表现，也未分析输入表述噪声、约束条件复杂度、问题规模增大对求解成功率的影响。总体而言，该工作的实验设计具备多数据集和多基线的初步广度，但缺少必要的消融、误差统计和分维度分析，实验深度尚不足以充分支撑其架构设计选择和泛化性结论。

## 6. 论文的主要贡献与启发

尽管现有可见信息有限，仍可提炼出论文宣称的主要贡献：

- **提出首个面向 OR 任务的三阶段多智能体推理框架**：将“建模 → 编码 → 调试”显式拆分，赋予每个子阶段独立反思与修正的空间，这一设计理念为解决复杂 OR 文本问题提供了可复用的系统级范式。
- **将推理 LLM 与 Agent 流程结合**：区别于直接用推理模型完成整题，也区别于用非推理模型进行微调或提示，该框架提供了一种“利用底座模型原生推理能力 + 结构化任务分解”的轻量增强路线，避免对每个 OR 数据集进行昂贵的专门微调。
- **质疑现有 OR 评测基准的有效性**：作者发现推理型 LLM 在 NL4OPT、MAMO、IndustryOR 上可能不如同家族非推理模型，指出这些基准在区分度和稳定性上的缺陷，并构建了新的 BWOR 数据集来提供更清晰的评估视角。这对于 OR 领域大模型评测体系的建设具有方法论上的提醒意义。

启发方面，该工作最大的参考价值在于：将求解 OR 问题从“一个提示解决”的低可控模式，转向“多智能体流水线 + 可验证调试回路”的高可控模式。这为后续研究工作开拓了至少三个方向：① 在不同底座推理模型上验证框架的可移植性；② 深入研究智能体间交互策略（如共享中间表示、反馈信息的结构化方式）；③ 在真实工业场景中验证其实际部署价值与算力成本。

## 7. 局限性与未解决问题

- **推理成本高昂**：框架依赖 DeepSeek-R1 这种大型推理模型，并需多轮调用多个子智能体，实际生成与调试开销远高于单次提示方法。摘要未报告推理 token 数或成本，使其实用性存疑。
- **单底座模型验证有限**：核心实验仅明确使用 DeepSeek-R1，对框架是否同样适配其他推理型 LLM 缺乏证据。
- **调试机制的自动化程度不明**：文中未说明调试阶段是依据编译器报错自动修复，还是依靠运行结果与数学模型进行一致性检查，亦或需要人工介入。若依赖预设文本模板，则泛化性可能受限。
- **BWOR 数据集的公信力待验证**：新构建的数据集本身缺乏详细统计与发布说明，且论文的结论部分建立在“BWOR 更具区分度”之上，若该数据集在构造上存在同质化或与已有任务分布偏移，则主要结论可能被削弱。
- **缺少失败案例分析**：没有解释模型在哪些类型的问题上仍然失败，也没有对失败模式进行分类（如建模错误、代码逻辑错误、求解器配置错误、数值发散等）。

## 8. 结论摘要

总之，OR-LLM-Agent 是一项将推理大语言模型与多智能体流水线结合、用于运筹优化问题自动建模与求解的探索性研究工作。它通过将复杂 OR 任务拆解为数学建模、代码生成与调试三个子任务，降低了单一模型长链路推理的误差累积风险，并在多个 OR 基准上取得了明显优于现有强基线的准确率。论文同时提出了 BWOR 数据集，用于填补已有 OR 基准在区分度和稳定性上的不足。不过，目前可公开获取的内容——尤其是详细实验数据、框架实现协议和资源消耗——仍然匮乏，因此尚不足以对框架的通用性、经济性与工程可靠性作出最终判断。摘要中所报告的性能优势虽然显著，但其可信度和可复现性还需要更多公开细节来支撑。

## 9. 对读者的建议

- 若作者后续公开代码、数据集及完整实验日志，应优先关注：
  1. 三个子智能体之间的交互接口设计（传递结构化数学表达式还是纯文本？）；
  2. 调试模块具体的错误捕捉与修复策略；
  3. BWOR 数据集的题目来源、标注流程与字段定义；
  4. DeepSeek-R1 与其他推理底座（如 GPT-o3、Gemini 2.5 Pro）互换后的表现差异。
- 对于从事 OR 问题的 NLP/Agent 研究者，该框架可以作为一个新的基线系统，在自身数据集上进行对比；也可以作为改进起点，例如引入求解器反馈循环、数学规划库校验、混合人机复核等更可靠的自愈机制。
- 对于业界应用，需结合推理成本、延迟和任务复杂度综合评估，在真正需要端到端自动化的工业 OR 场景中，也许可先在小规模问题上试运行，再逐步扩展到大规模问题。

---

**（完）**
