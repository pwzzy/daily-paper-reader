---
title: "Opt-Miner: Empowering Information-Seeking Agent with Tree-Guided Data Synthesis for Optimization Modeling"
title_zh: Opt-Miner：以树引导数据合成赋能信息寻求智能体的优化建模
authors: "Haoyang Liu, Yuyang Cai, Jie Wang, Xiongwei Han, Minyang Hu, Shuqi LIU, Mingxuan Yuan, Jianye HAO, Feng Wu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/d0f8a7133a96d3fbe107104139c6da4cfc40de10.pdf"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 面向自动化优化建模的信息寻求LLM智能体
tldr: 针对现实优化建模问题知识密集、现有方法受静态参数知识限制而缺乏领域专长、易出错的问题，本文提出Opt-Miner框架。该智能体学会识别缺失知识、从网络检索技术文档并据此对数学模型进行接地，其核心是树引导的数据合成流程。实验表明该方法在复杂优化建模任务上取得更好性能。工作直接推进了LLM智能体自动化优化建模的能力。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现实优化建模知识密集，现有方法受静态知识限制缺乏领域专长而易出错。
method: 提出Opt-Miner，让智能体识别缺失知识、检索网络文档并以树引导数据合成接地模型。
result: 在复杂优化建模任务上提升了建模准确性与性能。
conclusion: 直接推进了LLM智能体在自动化优化建模中的知识寻求能力。
---

## Abstract
Large Language Model (LLM) agents have shown significant potential in automated optimization modeling for mathematical problems. However, real-world problems are still challenging due to their knowledge-intensive nature. Existing methods, constrained by static parametric knowledge, often lack the domain expertise required to comprehend complex scenarios and apply appropriate mathematical techniques, leading to errors.
  To address this challenge, we propose the Opt-Miner framework, where the agent learns to identify missing knowledge, retrieve technical documents on the web, and ground its mathematical models for improved modeling performance.
  The core of Opt-Miner is a novel tree-guided data synthesis pipeline coupled with a retrieval-based group relative policy optimization (R-GRPO) algorithm, designed to foster the agent’s information-seeking capabilities.
  Specifically, we first formulate each problem into a tree structure, with its scenario contexts and mathematical techniques embedded in subtrees.
  We then employ subtree union, transfer, and knowledge fogging to synthesize complex, multi-domain problems that incorporate knowledge gaps, thereby necessitating active information seeking to solve these problems. 
  Based on synthesized data, we propose R-GRPO for agent reinforcement learning. Experiments demonstrate that Opt-Miner-Qwen3-8B achieves performance comparable to 32B state-of-the-art specialized agents and commercial reasoning models.

---

## 论文详细总结（自动生成）

# Opt-Miner 论文中文总结

> 说明：抓取到的 PDF 文本实际为 OpenReview 的浏览器验证/CAPTCHA 页面，而非论文正文。因此以下总结主要依据论文摘要与元数据；凡正文未提供的信息，均明确标注为“未说明/无法核验”。

## 1. 核心问题与整体含义
- **研究背景**：大语言模型智能体在数学问题的自动化优化建模中已展现潜力。
- **核心问题**：现实优化建模问题具有知识密集特征，常涉及复杂场景与专门数学技术；现有方法受限于静态参数知识，缺乏领域专长，容易误解场景或选用不恰当的数学方法，导致建模错误。
- **整体含义**：论文提出让智能体主动识别缺失知识、从网络检索技术文档，并据此“接地”数学模型，从而提升自动化优化建模能力，推进 LLM 智能体的信息寻求能力。

## 2. 方法论
- **核心思想**：提出 **Opt-Miner** 框架，将“信息寻求”能力注入优化建模智能体，核心由 **树引导数据合成流程** 与 **基于检索的组相对策略优化（R-GRPO）** 组成。
- **关键技术细节**：
  - 将每个问题建模为**树结构**，场景上下文和数学技术嵌入不同子树。
  - 使用 **子树联合（subtree union）**、**子树迁移（transfer）** 和 **知识雾化（knowledge fogging）** 合成复杂、多域、带知识缺口的问题，迫使智能体主动检索信息。
  - 基于合成数据提出 **R-GRPO**，用于智能体强化学习，培养其识别缺失知识、检索文档并接地数学模型的能力。
- **算法流程（文字说明）**：
  1. 将原始问题转化为树结构；
  2. 通过子树操作合成含知识缺口的复杂多域问题；
  3. 智能体尝试建模并识别缺失知识；
  4. 从网络检索技术文档；
  5. 将检索知识用于接地数学模型；
  6. 使用 R-GRPO 优化智能体策略。
- **未说明**：奖励函数、树构建细节、检索接口、训练目标公式、R-GRPO 的具体超参数等。

## 3. 实验设计
- **数据集/场景**：摘要仅称在“复杂优化建模任务”上验证，未给出具体数据集名称或场景列表。
- **Benchmark**：未提供明确 benchmark 信息。
- **对比方法**：提到与 **32B 的 SOTA 专用智能体** 和 **商业推理模型** 进行比较，但未列出具体模型名称。
- **评估指标**：未说明，可能涉及建模准确性与性能，但无法核验。

## 4. 资源与算力
- 文中可见信息**未明确说明** GPU 型号、数量、训练时长、总算力或检索调用成本。
- 仅可知使用 **Qwen3-8B** 作为基座模型之一，形成 Opt-Miner-Qwen3-8B。
- 因此无法对训练/推理资源消耗进行可靠总结。

## 5. 实验数量与充分性
- 从摘要与元数据无法确定具体实验组数、数据集数量、消融实验数量或统计显著性检验。
- 摘要仅报告一个代表性结果：**Opt-Miner-Qwen3-8B 达到与 32B SOTA 专用智能体和商业推理模型相当的性能**。
- 由于缺少正文、实验表格和附录，**无法判断实验是否充分、客观、公平**；基线配置、检索预算、提示设置、评测协议等均未说明。

## 6. 主要结论与发现
- Opt-Miner 能通过主动信息寻求提升复杂优化建模表现。
- 树引导数据合成与 R-GRPO 能有效培养智能体识别知识缺口、检索技术文档并接地数学模型。
- **Opt-Miner-Qwen3-8B** 以 8B 规模取得与 32B 专用智能体及商业推理模型可比的性能。
- 工作直接推进了 LLM 智能体在自动化优化建模中的知识寻求能力。

## 7. 优点
- **问题定位准确**：聚焦现实优化建模的知识密集与静态知识不足问题，强调主动检索。
- **数据合成有创意**：以树结构组织问题，并通过子树联合、迁移和知识雾化制造知识缺口。
- **算法结合合理**：R-GRPO 面向检索与信息寻求行为进行强化学习。
- **小模型高效**：8B 模型可比 32B/商业模型，具备较强部署潜力。
- **应用价值高**：自动化优化建模在运筹、调度、规划等领域有广泛需求。

## 8. 不足与局限
- **信息不完整**：抓取文本为验证页，无法核验方法细节、实验数据与附录。
- **实验覆盖未知**：数据集、benchmark、消融、统计检验均未提供。
- **公平性风险**：商业模型与 32B 基线的配置、检索预算、推理成本未说明，比较公平性无法判断。
- **检索依赖风险**：网络文档质量、时效性、版权、隐私、离线可用性等可能限制应用。
- **合成数据偏差**：子树合成与知识雾化可能引入不自然分布，偏离真实问题。
- **奖励设计未知**：R-GRPO 的稳定性、奖励黑客、检索行为退化等问题无法评估。
- **算力与成本未报告**：训练、推理和检索调用成本不明。
- **高风险场景需人工验证**：生成的数学模型可能看似合理但实际错误，直接应用存在风险。

（完）
