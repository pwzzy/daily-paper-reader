---
title: "Learn to Relax with Large Language Models: Solving Constraint Optimization Problems via Bidirectional Coevolution"
title_zh: 与大型语言模型一起学习松弛：通过双向协同演化求解约束优化问题
authors: "Beidan Liu, Zhengqiu Zhu, Chen Gao, Tianle Pu, Yong Zhao, Wei Qi, Quanjun Yin"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.48.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 大模型结合约束松弛求解约束优化问题
tldr: 针对现有LLM优化方法多将模型视为被动约束检查者而非主动策略设计者、难以应对复杂约束优化问题的问题，本文提出端到端方法AutoCO。该方法将运筹学中的约束松弛原理与LLM推理紧密结合，通过统一的策略-原理-代码三元表示，使LLM能够合成、论证并实例化松弛策略。研究实现了双向协同演化以自动求解约束优化问题。其贡献在于推动了LLM从被动检查者向主动优化策略设计者的转变，直接服务于LLM驱动的运筹优化建模。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1656, \"height\": 805, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 832, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 645, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 807, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 810, \"height\": 991, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 797, \"height\": 747, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 796, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 798, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 797, \"height\": 576, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 797, \"height\": 736, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 796, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 796, \"height\": 785, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 796, \"height\": 750, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 794, \"height\": 751, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long48/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 797, \"height\": 751, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 483, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1670, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 657, \"height\": 279, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 830, \"height\": 585, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 187, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long48/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 806, \"height\": 185, \"label\": \"Table\"}]"
motivation: 现有LLM优化方法多将模型视为被动约束检查者，难以应对复杂约束优化问题。
method: 提出AutoCO，将运筹学约束松弛原理与LLM推理耦合，用三元表示合成并实例化松弛策略。
result: 通过双向协同演化使LLM能主动设计并执行约束松弛策略求解优化问题。
conclusion: 推动LLM由被动约束检查者转变为主动运筹优化策略设计者。
---

## Abstract
Large Language Model (LLM)-based optimization has recently shown promise for autonomous problem solving, yet most approaches still cast LLMs as passive constraint checkers rather than proactive strategy designers, limiting their effectiveness on complex Constraint Optimization Problems (COPs). To address this, we present AutoCO, an end-to-end Automated Constraint Optimization method that tightly couples operations-research principles of constraint relaxation with LLM reasoning. A core innovation is a unified triple-representation that binds relaxation strategies, algorithmic principles, and executable codes. This design enables the LLM to synthesize, justify, and instantiate relaxation strategies that are both principled and executable. To navigate fragmented solution spaces, AutoCO employs a bidirectional global–local coevolution mechanism, synergistically coupling Monte Carlo Tree Search (MCTS) for global relaxation-trajectory exploration with Evolutionary Algorithms (EAs) for local solution intensification. This continuous exchange of priors and feedback explicitly balances diversification and intensification, thus preventing premature convergence. Extensive experiments on three challenging COP benchmarks validate AutoCO’s consistent effectiveness and superior performance, especially in hard regimes where current methods degrade. Results highlight AutoCO as a principled and effective path toward proactive, verifiable LLM-driven optimization.

---

## 论文详细总结（自动生成）

# 论文总结：Learn to Relax with Large Language Models: Solving Constraint Optimization Problems via Bidirectional Coevolution

## 1. 核心问题与整体含义

- **研究背景**：约束优化问题（COPs）广泛存在于物流、金融、工业规划等领域，多数为 NP-hard 问题。其困难主要来自硬约束导致的可行域碎片化与约束间耦合（如时间窗、载重、燃料等相互牵制），使得快速找到高质量可行解极为困难。
- **现有方法不足**：
  - 传统方法（分支定界、启发式、线性/拉格朗日松弛等）虽有效，但高度依赖专家经验，跨问题适应性差。
  - 基于 LLM 的方法（如 FunSearch、EoH、ReEvo）多将 LLM 视为**被动约束检查器**，依赖可行解反馈来指导算法设计。当硬约束增多、可行解难以获得时，反馈失效，搜索缺乏方向，易陷入次优设计。
  - 现有 LLM 方法侧重端到端代码生成，缺乏系统性的问题分析与策略设计，与人类专家“先松弛约束、再逐步收紧”的运筹学经验脱节。
- **整体含义**：论文主张将 LLM 从被动验证者转变为**主动的约束松弛策略设计者**，把运筹学中的约束松弛思想与 LLM 推理能力结合，以应对复杂 COPs 中可行域碎片化和决策空间巨大的挑战。

## 2. 方法论：AutoCO

### 核心思想
- 提出 **AutoCO**（Automated Constraint Optimization via LLM-driven bidirectional coevolution），一个端到端三阶段方法：**问题分析与初始策略设计 → 最优策略搜索 → 代码执行评估**。
- 核心创新是让 LLM 显式地探索、优化约束松弛策略，并将其作为算法设计的有机组成部分。

### 关键技术细节

- **三阶段流程**：
  1. **问题分析阶段**：解析问题描述，生成初始约束松弛策略集合。
  2. **最优策略搜索阶段**：双层协同优化——局部用进化算法（EA）精细优化，全局用蒙特卡洛树搜索（MCTS）探索策略空间。
  3. **代码执行阶段**：在问题实例上评估生成算法，为后续优化提供适应度反馈。

- **LLM 驱动的三步松弛方法**：
  1. **约束重要性分析**：LLM 解析问题文本，识别所有约束 \(G=\{g_1,\dots,g_m\}\)，并为每个约束分配重要性权重 \(w_i\in[0,1]\)（\(w_i=1\) 为关键约束，\(w_i=0\) 为可忽略约束）。
  2. **松弛范围建议**：基于重要性分析，为每个约束确定自适应松弛因子范围 \([\alpha_i,\beta_i]\)（\(\alpha_i\le 1\le \beta_i\)），其中 1 表示原约束边界，\(\alpha_i<1\) 允许收紧，\(\beta_i>1\) 允许受控违反。
  3. **松弛策略生成**：综合权重 \(W\) 与范围 \(R\)，生成初始策略集 \(\Sigma=\{\sigma_1,\dots,\sigma_k\}\)，每个策略 \(\sigma_j=(\delta_{j1},\dots,\delta_{jm})\) 为 \(m\) 维松弛系数向量，采样遵循约束重要性结构，而非随机产生。

- **三元表示方案（Triple Representation）**：
  - 每个个体表示为 \(I_j=\langle \sigma_j, A_j, C_j\rangle\)，即**约束松弛策略 \(\sigma_j\)、算法概念 \(A_j\)、可执行代码 \(C_j\)** 三者的统一编码。
  - 该表示确保生成的求解器显式使用其对应的约束松弛策略，实现策略—概念—代码在抽象层次上的同步演化，弥补传统方法只优化“算法+代码”二元表示的缺口。

- **双向协同演化机制（Bidirectional Coevolution）**：
  - 形式化为 \(M_{\text{exchange}} = \text{Bidirec\_Update}(T_{\text{MCTS}}, P_{\text{EA}})\)。
  - **局部 EA 层**：通过锦标赛选择父代，LLM 引导协同演化，在保持三元一致性的前提下修改策略、概念与代码，进行种群进化 \(P^{t+1}_{\text{EA}}=\text{Evolution}(P^t_{\text{EA}})\)。
  - **全局 MCTS 层**：改造树结构，交替使用约束节点 \(D\) 与松弛因子节点 \(R\)，完整路径定义一个策略 \(\sigma\)。针对两类节点设计 UCT 公式平衡探索与利用；用 LLM 生成可执行代码，其执行适应度作为奖励 \(R\) 回传更新节点值，最终输出最优策略 \(\sigma^*\)。
  - **双向信息交换**：
    - **EA → MCTS**：EA 产生的可行解持续更新 MCTS 树统计，减少 MCTS 重复探索，降低计算负担。
    - **MCTS → EA**：当 EA 停滞（基于适应度监控）或周期性触发时，将 MCTS 发现的有前景策略注入 EA，引导种群多样化，跳出局部最优。

- **代码执行与安全机制**：
  - 采用轻量级隔离执行环境，限制执行时间 \(T_{\max}=60\)s、内存 \(M_{\max}=1024\)MB。
  - 适应度评估：\(f(I)=\frac{1}{|\Pi|}\sum_{i=1}^{|\Pi|} f_i(I)\)，即个体在多个实例上的平均适应度。
  - 检测到语法或运行时错误时触发 LLM 迭代修复机制（最多 \(R_{\max}=3\) 次）；若仍失败则赋予无穷大适应度（惩罚）。

## 3. 实验设计

### 数据集 / 场景（三个 COPs 基准）
- **VRPTW**（带时间窗的车辆路径问题）：Solomon 基准，含 S(25)/M(50)/L(100) 三种客户规模。约束特点是早期决策约束后续可行性。
- **VRPTW-Fuel**（带时间窗与燃料约束的车辆路径问题）：在 VRPTW 基础上增加每路线燃料容量约束，资源累积与载重、距离耦合。
- **SFL**（安全设施布局问题）：来自 MINLPLib / CMU-IBM MINLP 项目，含 SFL-4、SFL-8、SFL-5(Dual) 实例。约束包括非重叠几何排斥、安全区域包含、连续布局与离散区域耦合等非线性约束。

### 对比方法（Baselines）
- **精确求解器**：Gurobi。
- **强化学习**：DeepACO。
- **元启发式**：SA、GA、PSO、MA、DE（均用 mealpy 3.0.3 实现）。
- **LLM 方法**：FunSearch、EoH、ReEvo。

### 评估指标
- 最优性间隙 \(\gamma=\frac{|f_{\text{best}}-f_{\text{opt}}|}{|f_{\text{opt}}|}\)。
- 端到端运行时间 \(T_{\text{e2e}}\)、首次可行解时间 \(T_{\text{tff}}\)、停滞时间 \(T_{\text{stag}}\)。

### 实现设置
- 使用 **DeepSeek-R1** 作为 LLM；种群规模 45；时间限制 2 小时；每个实例运行 100 次。
- 硬件平台：Intel® Core™ i5-13400F / NVIDIA RTX 4060 Ti。

## 4. 资源与算力

- 文中明确提到的算力相关信息：
  - **硬件**：Intel® Core™ i5-13400F CPU 与 NVIDIA RTX 4060 Ti GPU（单卡级配置）。
  - **运行限制**：每次实验时间上限 2 小时；代码执行环境限制 60 秒/次、1024 MB 内存。
  - **运行次数**：每个实例 100 次独立运行；元启发式基线使用 20 个确定性种子、epoch=80、population=45、run=100。
- **未明确说明**：论文未报告 LLM 推理的总 token 消耗、GPU 总卡时、训练/推理总时长等详细算力开销。仅能从端到端运行时间（65.07–108.87 分钟）间接推断计算成本较高。

## 5. 实验数量与充分性

- **实验组数概览**：
  - 三个问题域（VRPTW、VRPTW-Fuel、SFL）× 多个实例规模（S/M/L 及 SFL-4/8/5-Dual），与 10 余种基线方法对比（Gurobi、DeepACO、MA、DE、SA、GA、PSO、FunSearch、EoH、ReEvo）。
  - **消融实验**：4 个变体——去掉约束松弛模块（w/o σ）、去掉三步生成策略（w/o 3-steps）、去掉 MCTS（w/o MCTS）、去掉双向信息交换（w/o Bidirectional）。
  - **松弛策略有效性验证**：在 SFL-8 与 SFL-5(Dual) 上对比 AutoCO 设计策略、专家设计策略、无松弛策略，在 500–2500 计算预算下各进行 1000 次试验。
  - **优化动态分析**：在 SFL-4/8/5(Dual) 上对比基线 LLM 方法与 AutoCO 的收敛曲线。
  - **时间效率分析**：三个时间指标 × 三个规模。
- **充分性与公平性评估**：
  - **优点**：实验覆盖面较广，涵盖精确解、RL、元启发式、LLM 方法四类基线；消融实验完整拆解各模块贡献；松弛策略验证使用统一随机种子、相同初始条件、1000 次重复，统计稳健性较好。
  - **公平性设计**：元启发式基线统一用 mealpy 实现，固定超参数、确定性种子集合（\(s_0=17,\Delta=73\)，共 20 个种子），避免调参偏差与“挑选结果”。
  - **潜在不足**：LLM 方法基线（FunSearch、EoH、ReEvo）是否与 AutoCO 使用完全相同的 LLM、prompt 预算与时间预算，文中未完全对齐说明；部分结果方差较大（如 ReEvo 在某些实例上的标准差很高），统计显著性检验缺失。

## 6. 主要结论与发现

- **性能优势**：
  - 在 VRPTW-Fuel 上，AutoCO 取得最优性间隙 0.31(S)、0.00(M)、0.00(L)，显著优于 ReEvo 的 0.36(S)、0.20(M)；FunSearch 在约束增加时急剧退化（间隙 1.30）。
  - Gurobi 在较大实例上无法在限定时间内找到可行解，而 AutoCO 仍能稳定产出解，体现鲁棒性。
  - 相比 SOTA LLM 方法，平均最优性间隙降低 **24.7%**。
- **时间效率**：
  - AutoCO 首次可行解时间 \(T_{\text{tff}}\) 最短（小实例 6.39 分钟，大实例 11.65 分钟），快于 FunSearch（19.73–40.29 分钟）、EoH、ReEvo。
  - 停滞时间 \(T_{\text{stag}}\) 最低可至 5.99 分钟。
  - 端到端运行时间较长（65.07–108.87 分钟），但时间分配均衡，非集中于单一阶段。
- **消融结论**：
  - 双向协同演化机制贡献最大（平均退化 +23.73%），其次为约束松弛模块（+21.55%）、MCTS（+17.46%）、三步生成策略（+14.10%）。
- **松弛策略有效性**：
  - 在 SFL-8 上，AutoCO 策略使成功率从 0% 提升至 80%，优于专家策略（2500 次迭代时约 1.1 倍提升）；SFL-5(Dual) 上达到 53%，上升趋势最优。
- **优化动态**：
  - 现有 LLM 方法在初始解后迅速陷入局部搜索停滞；AutoCO 虽经历较长停滞期，但通过 MCTS 全局策略注入持续探测解空间，最终突破初始约束、实现显著适应度提升。

## 7. 优点

- **方法论创新**：
  - 首次将运筹学约束松弛原理系统性地编码为 LLM 可解释、可优化、可执行的三元表示，打通“策略—概念—代码”三个抽象层次。
  - 将 LLM 定位为主动策略架构师，而非被动约束检查器，思路具有范式转变意义。
- **机制设计亮点**：
  - 双向协同演化巧妙结合 EA 的局部精化与 MCTS 的全局探索，EA→MCTS 减少冗余探索，MCTS→EA 在停滞时注入全局信息，显式平衡多样化与强化。
  - 三步松弛方法将专家知识转化为 LLM 可执行的流程，降低对领域专家的依赖。
- **实验设计亮点**：
  - 覆盖三类约束特性迥异的 COPs，泛化性验证较全面。
  - 消融实验清晰量化各模块贡献；松弛策略验证采用无启发式的随机游走基线，排除搜索算法本身干扰。
  - 元启发式基线采用统一库、固定超参数与确定性种子，公平性考虑较周到。
- **可验证性**：生成代码在隔离环境中执行并带修复机制，强调“可验证的 LLM 驱动优化”。

## 8. 不足与局限

- **问题覆盖有限**：
  - 仅验证静态、确定性约束的优化问题，未涉及随机或动态优化环境。
  - 随着问题维度增加，策略空间指数增长，协同演化机制的可扩展性可能受限。
- **计算开销与效率权衡**：
  - 多组件同步（LLM 推理 + EA + MCTS）导致端到端运行时间显著长于部分基线，可能不适合实时决策场景。
  - 未报告 LLM token 消耗与总 GPU 卡时，算力成本透明度不足。
- **对 LLM 能力的依赖**：
  - 初始策略设计与演化精化的效果受 LLM 推理与编码能力影响，早期探索阶段的分析一致性可能不稳定，影响策略生成稳定性。
- **理论保证缺失**：
  - 双向协同演化机制的理论收敛性质尚未建立。
- **实验公平性与偏差风险**：
  - LLM 基线方法是否与 AutoCO 共享完全相同的 LLM 后端、prompt 预算与时间预算未明确说明。
  - 部分结果方差较大，缺乏统计显著性检验。
  - 消融实验仅报告平均退化百分比，未展示各数据集上的详细分布与置信区间。
- **应用限制**：
  - 在安全关键场景（城市物流、设施规划）中，LLM 不稳定性可能导致次优解，需人类监督。
  - 方法可能被用于高社会影响领域（关键基础设施资源分配、敏感战略规划），需领域风险评估与伦理审查。
  - 计算资源需求大，带来环境成本考量。

（完）
