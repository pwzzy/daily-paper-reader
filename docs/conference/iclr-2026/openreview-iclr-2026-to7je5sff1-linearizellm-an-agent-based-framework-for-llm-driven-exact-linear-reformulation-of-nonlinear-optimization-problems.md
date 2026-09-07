---
title: "LinearizeLLM: An Agent-Based Framework for LLM-Driven Exact Linear Reformulation of Nonlinear Optimization Problems"
title_zh: LinearizeLLM：基于智能体框架的LLM驱动非线性优化问题精确线性重构
authors: "Paul-Niklas Ken Kandora, Simon Caspar Zeller, Aaron Jeremias Elsing, Elena Kuss, Steffen Rebennack"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=tO7Je5SFF1"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 基于智能体与LLM将非线性优化问题精确线性重构，属于优化建模主题的运筹研究
tldr: 论文针对非线性优化问题的重构高度依赖人工专家经验的问题，提出LinearizeLLM这一基于大语言模型的智能体框架。框架为绝对值项、双线性乘积等不同非线性模式安排专门的重构智能体，由各智能体推导精确线性等价形式并协作组装成求解器可直接使用的线性模型。实验表明该方法能自动化完成精确线性重构流程，并显著降低非线性优化模型预处理的人工成本。该工作为LLM与多智能体在运筹优化建模与问题求解中的落地提供了有力范例。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 非线性优化问题的线性重构高度依赖人工专家知识，限制了求解器与专用算法的快速应用，亟需自动化手段。
method: 构建多智能体LLM框架LinearizeLLM，每个智能体负责一种非线性模式的精确线性重构，再协作组装为等价线性优化模型。
result: 实验验证了该框架能自动生成精确的线性重构模型，降低手工建模成本并支持后续求解。
conclusion: 该工作展示了LLM智能体在优化模型转换中的实用价值，为自动化运筹求解链路提供了可行方案。
---

## Abstract
Reformulating nonlinear optimization problems is largely manual and expertise-intensive, yet it remains essential for solving such problems with linear optimization solvers or applying special-purpose algorithms. We introduce \textit{LinearizeLLM}, an agent-based framework that solves this task by leveraging Large Language Models (LLMs). The framework assigns each nonlinear pattern to a \textit{reformulation agent} that is explicitly instructed to derive an exact linear reformulation for its nonlinearity pattern, for instance, absolute-value terms or bilinear products of decision variables. The agents then coordinate to assemble a solver-ready linear model equivalent to the original problem. To benchmark the approach, we create a dataset of 20 real-world nonlinear optimization problems derived from the established ComplexOR dataset of linear optimization problems. We evaluate our approach with several LLMs. Our results indicate that specialized LLM agents can automate linearization tasks, opening a path toward fully conversational modeling pipelines for nonlinear optimization.

---

## 论文详细总结（自动生成）

# LinearizeLLM 论文中文总结

## 1. 核心问题与整体含义
- 非线性优化问题若要直接使用线性求解器或专用算法，通常需要先进行精确的线性重构（linear reformulation）。
- 这种重构过程目前严重依赖人工专家经验，步骤繁琐、耗时且容易出错，成为运筹优化流程中的一个瓶颈。
- 论文提出用大语言模型（LLM）驱动、多智能体协作的方式，尝试将这一过程自动化，从而降低建模与预处理成本，也推动非线性优化的“会话式建模”发展。

## 2. 提出的方法论
- 核心思想：构建一个名为 **LinearizeLLM** 的智能体框架，利用 LLM 自动完成非线性模式的精确线性化。
- 模块化分工：框架将不同类别的非线性表达式视为不同的“非线性模式”，例如绝对值项、决策变量之间的双线性乘积等。
- 每个非线性模式会被分配给一个专门的**重构智能体（reformulation agent）**；该智能体被明确指示为该模式推导出数学上等价的精确线性重构形式。
- 协作整合：各重构智能体完成局部的线性化推导后，再通过协调机制将结果组装成一个**求解器可直接使用的、与原问题等价的线性优化模型**。
- 由于摘要部分未给出具体公式或提示模板，算法流程可概括为：识别原始问题中的非线性模式 → 分派对应智能体 → 智能体分别推导线性等价式 → 多智能体协作整合并输出完整线性模型。
- 研究同时提到，该框架期望打开通往“完全会话式非线性优化建模流程”的路径，即用户用自然语言描述问题，系统自动完成建模与重构。

## 3. 实验设计
- 使用了作者自行构建的基准数据集：包含 **20 个真实世界非线性优化问题**，这些问题由已有的 **ComplexOR** 线性优化问题数据集派生而来，通过在原问题中引入非线性模式形成待测试非线性模型。
- 评估方式：在多个不同 LLM 上运行 LinearizeLLM，比较不同模型在该线性化任务上的表现。
- 摘要中未列出具体 LLM 名称、未提出独立的人类专家基线，也没有与传统自动重构工具或商业建模系统进行对比。

## 4. 资源与算力
- 论文摘要与元数据中**未明确说明**使用的 GPU 型号、数量、训练时长或推理总预算。
- 由于该方法基于 LLM 智能体，通常可能以调用现成大模型 API 的方式运行，而非从头训练，因此文内并未报告任何模型训练算力开销。
- 在现有信息范围内，无法判断其实际计算成本或运行效率。

## 5. 实验数量与充分性
- 从摘要描述可见，实验主体是在**一套包含 20 个实例的基准数据集**上、以**多个 LLM** 进行对比。
- 摘要中未指明是否进行了消融实验（比如去掉多智能体分工模块、替换提示策略等），也没有给出统计显著性、错误率或失败案例分析。
- 20 个问题具备一定代表性，但相较于实际非线性规划问题本身的多样性，实验覆盖仍有限。
- 由于文中披露的评估细节有限，目前只能判断其为初步验证，尚不足以充分证明该方法在不同领域、不同难度和不同求解器配置下始终可靠。

## 6. 主要结论与发现
- 专门化的 LLM 智能体可以在非线性优化问题上完成精确线性化任务。
- 该方法能够自动化传统上依赖人工经验的重构过程，进而减少非线性模型预处理的人工成本。
- 多智能体协作结构有潜力扩展到更多非线性模式，为非线性优化实现“全会话式建模管道”提供可行性证据。

## 7. 优点
- 问题选取有价值：直击非线性优化中“线性化依赖专家”的痛点，应用场景明确。
- 方法设计新颖：将多智能体与 LLM 结合，按非线性模式分工，具有良好的模块化和可扩展性。
- 框架抽象清晰：每个智能体只负责一种模式，便于加入更多重构规则和不同非线性类别。
- 开源基准的构建思路可取：基于 ComplexOR 生成 20 个非线性问题，有助于后续在此方向上进行可重复比较。
- 使用多种 LLM 进行评估，比单一模型验证更具一般性，能初步观察不同大模型的表现差异。

## 8. 不足与局限
- 实现细节缺失：提示词设计、智能体协作机制、非线性模式识别方式、以及“精确性”的验证方法等均未在摘要层面展示。
- 实验覆盖有限：仅 20 个实例，且源于线性数据集改造，规模与多样性存在不足。
- 缺乏人类专家基线：没有直接对比专家手工重构所需时间与错误率，难以量化实际效益。
- 缺少与既有自动重构工具或商业建模语言的对比，无法说明该框架相对传统方法的相对优势。
- 未讨论 LLM 推导错误的检测与修正机制；若生成的重构并非数学上严格等价，将直接影响求解正确性，存在模型幻觉相关的风险。
- 算力与成本信息缺失，影响实际部署判断。
- 当前结果主要基于摘要层面的“宣称”，未提供可审计的详细统计指标，因此公平性和可复现性有待更多信息验证。

（完）
