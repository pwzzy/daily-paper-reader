---
title: Multi-LLM Collaborative Search for Complex Problem Solving
title_zh: 面向复杂问题求解的多LLM协同搜索
authors: "Sen Yang, Yafu Li, Wai Lam, Yu Cheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2115.pdf"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 多LLM智能体结合MCTS进行复杂问题求解
tldr: 针对大语言模型在复杂推理中难以覆盖庞大推理空间与应对语言歧义的问题，本文提出多搜索智能体混合范式MOSA，让多个LLM智能体独立探索并迭代精炼推理路径。方法以蒙特卡洛树搜索为骨架，聚合多智能体提出的推理步骤。在四个推理基准上实验表明，MOSA持续优于单模型方案。该工作为多智能体协同搜索式问题求解提供了通用框架。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2115/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 592, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2115/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 537, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2115/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1450, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2115/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 709, \"height\": 837, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2115/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 803, \"height\": 707, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2115/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1665, \"height\": 863, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2115/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1415, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2115/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1231, \"height\": 282, \"label\": \"Table\"}]"
motivation: 单一大语言模型难以应对庞大推理空间和自然语言歧义，复杂推理任务表现受限。
method: 提出Mixture-of-Search-Agents范式，以蒙特卡洛树搜索为骨架，让多个LLM智能体独立探索并迭代精炼、聚合推理步骤。
result: 在四个推理基准上评估，MOSA相较单模型方法取得一致且更优的准确率。
conclusion: 多智能体协同搜索能有效缓解单模型局限，为复杂推理提供可扩展的搜索式求解思路。
---

## Abstract
Large language models (LLMs) often struggle with complex reasoning tasks due to their limitations in addressing the vast reasoning space and inherent ambiguities of natural language. We propose the Mixture-of-Search-Agents (MOSA) paradigm, a novel approach leveraging the collective expertise of multiple LLMs to enhance search-based reasoning. MOSA integrates diverse reasoning pathways by combining independent exploration with iterative refinement among LLMs, mitigating the limitations of single-model approaches. Using Monte Carlo Tree Search (MCTS) as a backbone, MOSA enables multiple agents to propose and aggregate reasoning steps, resulting in improved accuracy. Our comprehensive evaluation across four reasoning benchmarks demonstrates MOSA’s consistent performance improvements over single-agent and other multi-agent baselines, particularly in complex mathematical and commonsense reasoning tasks.

---

## 论文详细总结（自动生成）

# 论文总结：Multi-LLM Collaborative Search for Complex Problem Solving（MOSA）

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLM）在复杂推理任务上仍面临困难，根源在于自然语言的复杂性与歧义性导致推理空间极其庞大。即便使用 Chain-of-Thought 等线性化推理链，也难以有效覆盖。
- **现有方案**：逐步搜索式推理（BFS、DFS、best-first search、MCTS）将问题分解为有向图上的遍历，节点与边代表推理子步骤，是较有前景的方向。
- **核心痛点**：
  - 单模型搜索难以兼顾**多样性**与**质量**。提高采样温度可增加多样性，但需精细调参 top-k/top-p，且不同基准偏好的温度不同。
  - 即使调参接近最优，单一 LLM 仍可能因数据与架构的固有偏置陷入**局部最优**。
  - 用多数投票等启发式方法确定子答案，在模型偏向错误方向时容易失效。
- **整体含义**：论文提出 **Mixture-of-Search-Agents（MOSA）** 范式，首次（据作者所述）将多 LLM 的集体专长引入搜索式推理，通过独立探索与迭代精炼相结合，缓解单模型局限。

## 2. 方法论

- **核心思想**：以蒙特卡洛树搜索（MCTS）为骨架，让多个 LLM 充当搜索智能体，在每一步推理中共同提出并聚合推理步骤（action）。方法包含两个角色：**Proposers（提议者）** 与 **Aggregators（聚合者）**。
- **基础框架**：
  - 状态 $s_j$ 表示已生成的推理步骤及对应搜索轨迹；动作 $a_j$ 表示下一步推理步骤。
  - 动作空间沿用 rStar 的定义 $A=\{A_1,\dots,A_5\}$（一步思考、剩余思考、子问题+子答案、重答子问题、改写问题），主实验采用 $A_3$（子问题 + 子答案，拼接为 action）。
  - 奖励函数：轨迹到达正确最终答案的节点获正奖励，否则为零；测试时用多数投票置信度近似。
  - 选择阶段采用 UCT 公式平衡探索与利用：
    $$UCT(s,a)=\frac{Q(s,a)}{N(s,a)}+c\sqrt{\frac{\ln N_{parent}(s)}{N(s,a)}}$$
  - 每个 MCTS 迭代包含 Selection、Expansion、Simulation、Back-propagation 四步，本文聚焦 **Expansion** 阶段。
- **MOSA as Proposers（多样化动作）**：
  - **子问题提议**：由不同 LLM 独立生成子问题，保持子问题之间的独立性，从而让初始搜索方向多样化（同一 $s_i$ 经不同 LLM 呈现不同“色彩”）。
  - **子答案生成**：每个子问题由多个 LLM 分别作答，得到多样化候选子答案，再进行聚合。
- **MOSA as Aggregators（协同精炼）**：
  - 引入神经聚合函数，提示每个 LLM 批判、比较并整合多个候选答案，产出聚合答案，再纳入多数投票。
  - 直觉示例：设 3 个 LLM 中 $k$ 个擅长某子问题，若 $k=2$，多数投票易得错误答案；通过聚合，坏聚合器可借鉴好的子答案，可能形成 4 好 2 坏的分布，从而翻转多数投票结果。
- **算法流程（Algorithm 1）**：给定选中节点 $s_i$、子问题数 $n_q$、每子问题候选答案数 $n_a$ 与 LLM 池 $\pi_{mix}$：循环 $n_q$ 次，用 `SelectLLM` 选模型生成子问题；再循环 $n_a$ 次生成候选子答案；`FinalizeSubAnswer` 用多数投票或神经聚合确定最终子答案；拼接子问题与子答案形成新动作并加入集合。

## 3. 实验设计

- **数据集 / Benchmark（4 个推理基准）**：
  - 数学推理：**GSM8K**（1319 例）、**SVAMP**（1000 例）、**MATH-500**（500 例）。
  - 常识推理：**StrategyQA**（687 例，简称 STG）。
- **模型池**：4 个开源指令微调 LLM —— Llama-3.1-8B-Instruct、Qwen-2-7B-Instruct、Ministral-8B-Instruct-2410、GLM-4-9B-Chat。
- **对比基线**：
  - Few-shot CoT（4 个 LLM 各自）。
  - Self-Consistency@4/32/128/256（单 LLM Llama 与四 LLM 版本）。
  - **RAP**（MCTS 代表方法），分别配 Llama/Ministral/Qwen/GLM 单模型。
  - RAP w/ Proposer(s)、RAP w/ Pro. & Agg. 的各单模型变体。
  - **MOSA**（RAP 骨架）与 **rStar + MOSA**（扩展动作集）。
- **超参数**：采样默认 temperature=0.75、top_k=40、top_p=0.95；rollouts=8，每节点子问题数=4，每子问题候选子答案数=4，最大深度=5。
- **公平性控制**：单 LLM 方法与多 LLM 对应方法保持大致相同的 LLM 前向调用次数；多 LLM 采样时保持伪均匀分布（如 7 次采样在 4 个 LLM 间轮流分配）。

## 4. 资源与算力

- 文中明确提到使用 **A100 GPU**，根据计算需求使用 **1 至 8 块** GPU。
- 该方法为**纯推理**框架，不涉及模型训练，因此未报告训练时长。
- **未明确说明**：总推理耗时、总 GPU 小时数、具体运行环境细节。
- 作者在局限性中给出推理开销估计：RAP/MOSA 无聚合约 **200–300 次前向调用/查询**，带聚合约 **500 次**；Self-Consistency@256 与前者相当。

## 5. 实验数量与充分性

- **主要实验组数**：
  - 表 1：主结果，覆盖 4 个数据集、约 20 余种方法配置（CoT、Self-Consistency 多档、RAP 单模型 4 种、MOSA 等）。
  - 表 2：MOSA 与 rStar 扩展动作集结合，2 组对比。
  - 表 3：Proposer/Aggregator 数量消融（单/多 × 单/多，共 6 种组合）。
  - 图 4：多样性 vs 准确率，2 个数据集 × 5 个温度点。
  - 图 5：1–4 个不同 LLM 数量的性能曲线，4 个数据集。
  - 图 1：MATH-500 上单 LLM vs 多 LLM 搜索的性能对比。
- **充分性评价**：
  - 覆盖数学与常识两大类任务，消融维度（LLM 数量、Proposer/Aggregator 角色、动作集、温度）较完整，整体较为充分。
  - **客观性与公平性**：通过控制前向调用次数来对齐计算预算，属于较公平的对比设计；但 Self-Consistency 的单 LLM 实验仅采用 Llama，可能引入模型选择偏差。
  - **覆盖不足**：未涉及代码生成、逻辑推理等其他领域；模型规模限于 7–9B，未验证更大模型或闭源模型。

## 6. 主要结论与发现

- **性能提升**：MOSA 在所有 4 个数据集上持续优于单 LLM RAP 及其他多智能体基线，平均提升 **1.71%**；MATH-500 上最高 **+1.8%**。最佳配置（RAP w/ Proposers & Aggregators + MOSA）平均 **79.97%**；与 rStar 结合后平均达 **81.47%**，MATH-500 从 59.00% 提升至 63.20%。
- **协同效应**：多智能体协作与搜索式推理存在正向协同。单→多智能体在非搜索场景提升 +0.53%，在搜索场景提升 +1.35%，加聚合器后达 +1.71%；非搜索→搜索的差距从单模型的 +0.62% 扩大到多模型的 +1.44%。
- **聚合器有效**：单 LLM 聚合器带来 +0.63% 平均提升，MOSA 聚合器进一步提升至 +0.99%。
- **复杂任务优势明显**：GSM8K、SVAMP 较易（>90%），MATH-500、StrategyQA 较难，搜索式方法在难任务上优势更突出（如 StrategyQA：72.78% vs 75.69%）。
- **多样性-性能权衡**：单 LLM 搜索随温度升高先升后降，且不同基准偏好不同温度；MOSA 用默认参数即持续占优。
- **LLM 数量正相关**：不同 LLM 数量增加总体提升准确率（仅 MATH-500 在 3→4 时略降）。
- **动作集兼容性**：MOSA 与扩展动作集兼容，但扩展动作集并非总有益（StrategyQA 上反而下降）。
- **角色重要性**：消融显示 Proposer 数量减少的负面影响（-1.23%）大于 Aggregator（-0.47%），说明 MOSA 作为提议者贡献更大。

## 7. 优点

- **方法简洁通用**：MOSA 可插拔到多种搜索算法（MCTS）与多种动作集（rStar），不依赖特定模型或任务结构。
- **双角色设计有理论直觉**：Proposer 保证搜索方向多样性，Aggregator 缓解多数投票在“少数正确”情形下的失效，并用示例清晰阐释机制。
- **实验设计较严谨**：通过控制前向调用次数对齐计算预算，避免“多算力即更强”的虚假优势；对多样性-质量权衡给出定量分析。
- **消融全面**：从 LLM 数量、Proposer/Aggregator 角色、动作集规模、采样温度等多维度验证，结论相互印证。
- **实践可行性**：多模型可借由 TogetherAI 等云服务并发部署，扩展成本可控。

## 8. 不足与局限

- **计算开销大**：带聚合约 500 次前向调用/查询，虽作者认为性能增益可抵消成本，但对延迟敏感或资源受限场景仍不友好。
- **Prompt 工程敏感**：性能依赖精心设计的提示模板，论文未做不同 prompt 集的对比，结果可能随模板变化而波动。
- **领域覆盖有限**：仅在数学（GSM8K/SVAMP/MATH-500）与常识（StrategyQA）上验证，未覆盖代码、多跳问答、形式化推理等。
- **模型规模受限**：仅使用 7–9B 开源模型，未验证更大规模或闭源 LLM 上的可扩展性。
- **非单调现象**：MATH-500 上 LLM 数量从 3 增至 4 时性能略降，说明“越多越好”并非绝对。
- **奖励函数近似**：以多数投票置信度近似奖励，本身可能继承多数投票的偏差；动作集扩展在 StrategyQA 上反而变差，也提示动作空间设计存在任务依赖性。
- **潜在偏差风险**：Self-Consistency 单 LLM 实验仅用 Llama，可能低估或高估基线；伪均匀采样策略对 LLM 选择的公平性也有细微影响。

（完）
