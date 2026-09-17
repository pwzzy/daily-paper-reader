---
title: "PathWise: Planning through World Model for Automated Heuristic Design via Self-Evolving LLMs"
title_zh: PathWise：通过世界模型规划的自演化LLM自动启发式设计
authors: "Oguzhan Gungordu, Siheng Xiong, Faramarz Fekri"
date: 2026-04-30
pdf: "https://openreview.net/pdf/faa9536e47383d2283c1ccdef674c8feed96f577.pdf"
tags: ["query:llm-agent-or"]
score: 8.0
evidence: 面向组合优化的多智能体LLM自动启发式设计
tldr: 针对现有LLM自动启发式设计依赖固定进化规则与静态提示、导致启发式生成短视和冗余评估的问题，本文提出PathWise多智能体推理框架。该方法将启发式生成建模为蕴含图上的序贯决策过程，以状态化记忆承载搜索轨迹，使系统能复用历史决策。实验表明其在组合优化问题上的启发式设计质量与效率优于既有方法。该工作推动了LLM智能体在组合优化自动建模与求解上的应用。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有LLM自动启发式设计依赖固定进化规则和静态提示，易产生短视启发式与冗余评估。
method: 提出多智能体推理框架PathWise，将启发式生成建模为蕴含图上的序贯决策过程并维护状态化搜索记忆。
result: 实验显示该方法能减少冗余评估并生成更优的组合优化启发式。
conclusion: 表明世界模型式多智能体推理可有效提升LLM驱动的组合优化自动启发式设计。
---

## Abstract
Large Language Models (LLMs) have enabled automated heuristic design (AHD) for combinatorial optimization problems (COPs), but existing frameworks' reliance on fixed evolutionary rules and static prompt templates often leads to myopic heuristic generation, redundant evaluations, and limited reasoning about how new heuristics should be derived. We propose a novel multi-agent reasoning framework, referred to as Planning through World Model for Automated Heuristic Design via Self-Evolving LLMs (PathWise), which formulates heuristic generation as a sequential decision process over an entailment graph serving as a compact, stateful memory of the search trajectory. This approach allows the system to carry forward past decisions and reuse or avoid derivation information across generations. A policy agent plans evolutionary actions, a world model agent generates heuristic rollouts conditioned on those actions, and critic agents provide routed reflections summarizing lessons from prior steps, shifting LLM-based AHD from trial-and-error evolution toward state-aware planning through reasoning. Experiments across diverse COPs show that PathWise converges faster to better heuristics, generalizes across different LLM backbones, and scales to larger problem sizes.

---

## 论文详细总结（自动生成）

# PathWise 论文总结

> 说明：提供的“PDF 提取文本”实际为 OpenReview 浏览器验证页，而非论文正文。以下总结主要依据标题、摘要与元数据；凡正文未给出的实验细节，均标注为“未说明/无法核实”。

## 1. 核心问题与整体含义
- **研究背景**：大语言模型已被用于组合优化问题（COPs）中的自动启发式设计（AHD）。
- **核心痛点**：现有 LLM-AHD 框架依赖固定进化规则与静态提示模板，导致：
  - 启发式生成短视；
  - 冗余评估较多；
  - 对“新启发式应如何推导”的推理能力有限。
- **整体含义**：PathWise 试图把 LLM 驱动的自动启发式设计从“试错式进化”转向“状态感知的规划”，通过世界模型与多智能体推理提升启发式设计质量与效率。

## 2. 方法论
- **核心思想**：将启发式生成建模为“蕴含图上的序贯决策过程”，用蕴含图作为紧凑、有状态的搜索轨迹记忆。
- **关键组件**：
  - **策略智能体**：规划进化动作。
  - **世界模型智能体**：根据策略动作生成启发式 rollout。
  - **评论家智能体**：提供路由式反思，总结先前步骤的经验教训。
- **算法流程（文字化）**：
  1. 在蕴含图上表示当前搜索状态与历史决策；
  2. 策略智能体选择下一步进化动作；
  3. 世界模型智能体以该动作为条件生成候选启发式；
  4. 评论家智能体进行反思并路由反馈；
  5. 系统更新状态化记忆，使后续生成可复用或避免已有推导信息；
  6. 循环迭代，直至收敛或达到预算。
- **公式**：摘要未给出显式公式；可理解为在蕴含图上进行策略规划与状态更新的序贯决策框架。

## 3. 实验设计
- **场景**：多样化组合优化问题（COPs）。
- **数据集/基准**：未具体说明，摘要仅称“across diverse COPs”。
- **对比方法**：未列出具体 baseline；元数据称“优于既有方法”，但缺少方法名与指标。
- **评估维度**：从摘要看包括：
  - 收敛速度与启发式质量；
  - 对不同 LLM backbone 的泛化；
  - 对更大问题规模的扩展性。
- **指标、数据规模、具体问题类型**：未提供。

## 4. 资源与算力
- 未说明 GPU 型号、数量、训练或推理时长。
- 未说明 LLM 调用成本、token 消耗或总计算预算。
- 因此无法评估可复现性与实际开销。

## 5. 实验数量与充分性
- **可见实验覆盖**：多类 COP、多个 LLM backbone、较大问题规模。
- **消融实验**：未说明。
- **具体实验组数**：未说明。
- **充分性/客观性/公平性**：仅凭摘要无法判断。需全文核实：baseline 是否调优、计算预算是否对齐、是否统计显著、是否报告方差、是否包含消融与失败案例。

## 6. 主要结论与发现
- PathWise 能更快收敛到更好的启发式。
- 在不同 LLM backbone 上具有泛化能力。
- 能扩展到更大规模问题。
- 世界模型式多智能体推理可有效提升 LLM 驱动的组合优化自动启发式设计。
- 状态化记忆有助于减少冗余评估、缓解短视生成。

## 7. 优点
- 问题定位清晰：针对固定进化规则与静态提示导致的短视和冗余问题。
- 方法结构有创新：策略、世界模型、评论家分工，将 AHD 转为规划问题。
- 蕴含图作为状态化记忆，有望复用历史决策、避免重复推导。
- 实验宣称覆盖多 COP、多 backbone 与规模扩展，应用潜力较强。
- 元数据表明其被 ICML 2026 接收、评审分 8.0，说明工作受到一定认可。

## 8. 不足与局限
- 可获取材料不是全文，无法验证方法细节、公式、实验设置与结论强度。
- 具体数据集、benchmark、baseline、评价指标、消融和统计检验均未给出。
- 算力与成本未披露，难以判断效率优势是否扣除额外 LLM 调用与蕴含图维护开销。
- 世界模型与评论家路由反思可能增加系统复杂度和推理成本；实际部署限制未知。
- 对特定 LLM backbone、提示、超参的依赖性和鲁棒性未知。
- 在更复杂、真实约束下的 COP 上是否有效，仍需全文实验支撑。
- “优于既有方法”的公平性、可复现性和偏差风险，因缺少细节无法评估。

（完）
