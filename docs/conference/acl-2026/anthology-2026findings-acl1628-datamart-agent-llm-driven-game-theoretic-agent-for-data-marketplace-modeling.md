---
title: "Datamart-Agent: LLM-Driven Game-Theoretic Agent for Data Marketplace Modeling"
title_zh: Datamart-Agent：面向数据市场建模的大模型驱动博弈智能体
authors: "Pangjing Wu, Peter Q. Chen, Xiaodong Li, Wenqi Fan, Qing Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1628.pdf"
tags: ["query:llm-agent-or"]
score: 5.0
evidence: 用大模型智能体进行均衡建模
tldr: 现有数据市场研究多假设静态均衡与完全信息，缺乏现实性。本文提出EvoDM智能体建模框架，将静态市场扩展为动态、不完全信息场景并提供可解的均衡基准，进而构建Datamart-Agent这一由大语言模型驱动的博弈智能体来改进均衡一致性决策。实验验证其在可解析市场中能做出更符合均衡的决策。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1628/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1562, \"height\": 837, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1628/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 800, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1628/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 796, \"height\": 212, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1628/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 283, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1628/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 794, \"height\": 253, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1628/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 470, \"height\": 338, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1628/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 676, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1628/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 807, \"height\": 375, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1628/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 152, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1628/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 121, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1628/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 804, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1628/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 805, \"height\": 296, \"label\": \"Table\"}]"
motivation: 现有数据市场研究多停留在静态均衡与完全信息假设，难以刻画动态且信息不完全的真实交易场景。
method: 提出EvoDM智能体建模框架，并构建由大语言模型驱动的博弈智能体Datamart-Agent进行均衡一致性决策。
result: 在可解析的均衡基准下，Datamart-Agent能够做出更符合均衡的决策，优于基线。
conclusion: 表明大模型智能体可有效用于复杂市场博弈与均衡建模任务。
---

## Abstract
Data marketplaces analyze strategic data exchanges among users, platforms, and buyers. However, most existing studies model static equilibria and complete information, which limits their realism. In this work, we study whether large language model (LLM)-driven agents can make equilibrium-consistent decisions in analytically tractable data marketplaces with evolving and incomplete-information. Specifically, we introduce EvoDM, an agent-based modeling framework that extends the static data marketplace to dynamic and incomplete-information settings while providing tractable equilibrium benchmarks for evaluating agent decisions. Building upon EvoDM, we propose Datamart-Agent, an LLM-driven game-theoretic agent that improves equilibrium-consistent decision execution through dynamic game tree memory and mechanism-guided reflection, without requiring parameter updates. Experiments demonstrate that Datamart-Agent closely matches equilibrium-consistent decision-making, achieving the lowest utility gap and over 20% higher Pass@ 𝜖 than strong baselines. After validating its effectiveness, we employ EvoDM with Datamart-Agent to analyze competition and regulation in assumption-relaxed settings where closed-form ground truth is unavailable, providing exploratory simulation-based insights into market dynamics and regulatory effects.

---

## 论文详细总结（自动生成）

# Datamart-Agent 论文总结

## 1. 核心问题与整体含义

- **研究背景**：数据市场（如 AWS Data Exchange）在现代 AI 基础设施中扮演核心角色，连接用户、平台与买家三层主体，涉及数据共享、定价、隐私与竞争等战略互动。
- **核心问题**：现有数据市场研究大多依赖**静态均衡**与**完全信息（CI）** 假设，无法刻画真实市场中**时间演化**（平台进入/退出、买家逐轮到达）与**信息不完全（INC）** 的现实情形。将模型扩展到这些场景在解析上不可解（analytically intractable）。
- **关键追问**：LLM 驱动的智能体能否在可解析求解的数据市场中做出**与均衡一致的决策**？LLM 本身并不天然具备对收益、信念与战略依赖关系进行推理的能力。
- **整体含义**：本文既提出一个可验证的智能体建模（ABM）框架，又检验 LLM 智能体作为"理性决策者"的可靠性，并进一步将验证后的智能体用于无闭式解场景下的竞争与监管探索性分析。

## 2. 方法论

### 2.1 核心思想
- 构建 **EvoDM**（演化+不完全信息数据市场 ABM 框架），将经典静态三层数据市场扩展到动态、INC 场景，并在简化制度下推导出**可解析的均衡基准**作为 ground truth。
- 在 EvoDM 之上提出 **Datamart-Agent**：一个无需参数更新、通过记忆与机制反思实现均衡一致决策的 LLM 博弈智能体。

### 2.2 三层数据市场的形式化
- **静态 CI 市场**：定义为四阶段博弈——①平台同时选择进入 $e_i$ 与噪声 $\sigma_i$；②用户选择共享决策 $a$；③进入平台定价 $p$；④买家选择购买 $b$。
- **效用函数**（基于互信息）：
  - 平台：$U_i = [a_i(I_i + b_i p_i) - c_i] \cdot e_i$
  - 用户：$U_u = \sum_i a_i e_i I_i - \alpha I(\sigma,e,a,b)$（服务收益 vs 隐私损失）
  - 买家：$U_b = \beta I(\sigma,e,a,b) - \sum_i b_i p_i$
- 关键引理：用户侧揭示信息 $I_i = \frac{1}{2}$；买家侧信息由矩阵形式 $I(\sigma_S) = m_S^\top M_S^{-1} m_S$ 给出；均衡噪声满足等比例结构 $\frac{2+\sigma_i^2}{\gamma_i^2} = 2\alpha - K + 1$；平台定价等于其对买家的**边际信息贡献**。

### 2.3 两种扩展设定
- **Evolving（演化市场）**：$T$ 轮离散交互，新买家逐轮到达，平台集合从 $S_{t-1}$ 演化到 $S_t$。每轮效用解析给出（命题 1）：用户剩余被压至 0，在位平台获恒定流收益，新进入者按 $p_j = \beta_t/(2\alpha)$ 定价。
- **β-INC（买家估值不完全信息）**：买家估值 $\beta$ 服从连续无原子分布 $F$，平台与用户需形成与完美贝叶斯均衡一致的信念。按隐私阈值 $\alpha_{\text{crit}}$ 分为**低隐私**（$\sigma^*=0$）与**高隐私**（约束绑定）两种制度，各自给出闭式噪声与价格。

### 2.4 Datamart-Agent 的三大组件
1. **动态角色条件化感知**：将结构化数值状态/观测翻译为角色专属的自然语言描述，随轮次更新以反映平台进入、退出、用户共享等变化。
2. **动态博弈树记忆**：将历史交互在线组织为博弈树 $\mathcal{T}=(V,E)$，按角色维护记忆池，通过余弦相似度检索 Top-$N$ 相似轨迹并总结为自然语言反思，作为决策的上下文证据。
3. **机制引导反思决策**：提示智能体显式依据机制给出的效用公式与约束推理候选行动的影响，但不直接给出最优动作。最终决策为：
$$a_*^{(t)} = \text{LLM}\big(C_*^{(t)}\big), \quad C_*^{(t)} = (\phi_{\text{perc}}, \phi_{\text{mem}}, \phi_{\text{ref}})$$

## 3. 实验设计

### 3.1 场景与 Benchmark
- 基于 EvoDM 构建三类基准：**CI**、**Evolving**、**β-INC**，每类均含标准版与 **OOD**（分布外）版本。
- 每个场景独立采样用户/平台/买家特征：训练集 1000 例、测试集 200 例；OOD 场景扩大参数范围（$\alpha \sim U(0,10)$、$\beta \sim U(0,2)$）与平台数量（最多 16 个）。
- 平台成本 $c_i \sim U(0,1)$，平台-用户对齐参数 $\gamma_i \sim U(0,1)$。

### 3.2 对比方法
- **RL 基线**：RL-ABM（DQN、PPO）。
- **LLM 基线**：LLM-State（仅当前状态）、LLM-Recent（近期轨迹平坦记忆）、LLM-I（相似轨迹推理）、LLM-E（自然语言+符号推理）。
- **骨干模型**：GPT-4o、LLaMA-3.1-8B-Instruct、Qwen-2.5-32B-Instruct。

### 3.3 评价指标
- **Utility Gap $\Delta U$**（越低越好）：预测效用与均衡效用的平均绝对偏差。
- **Pass@$\epsilon$**（越高越好）：预测效用落入均衡 $\epsilon$ 容差内的比例。
- 细粒度指标：离散动作（$e,a,b$）准确率、连续动作（$\sigma,p$）的 MSE。

## 4. 资源与算力

- 文中**未明确说明**训练/推理的总算力规模（如 GPU 数量、总时长、能耗等）。
- 仅在计算开销分析中提及：使用**单张 NVIDIA H20 GPU**，对 Qwen-2.5-32B-Instruct 在 CI 场景下测量平均 token 用量与推理延迟（Ours：约 9778 tokens、18.8 秒）。
- 作者提到计算资源由香港理工大学大型 AI 模型中心（CLAIM）提供，但未给出具体配额。
- 结论：**算力披露不充分**，无法评估复现成本与环境影响。

## 5. 实验数量与充分性

- **主实验**：6 个设定（CI、Evolving、β-INC 及各自 OOD）× 多种骨干模型 × 多基线，规模较大。
- **消融实验**：分别去除感知模块的自然语言表示、博弈树记忆、相似检索、机制引导反思，共约 5 组配置 × 3 设定。
- **附加分析**：决策准确率/MSE 对比、检索相似度与 $\Delta U$ 的相关性分析（Pearson = −0.331）、计算开销对比、效用分布随机制变化、用户共享概率、买家购买概率、平台寿命（随 $T$ 与 $K_{\max}$）、异质隐私偏好下的平台选择、监管制度对比（Gini 系数）。
- **公平性**：所有基线在同一 EvoDM 环境、同一观测空间下评估；RL 基线使用向量化观测满足马尔可夫性。整体实验设计较为客观、覆盖全面。
- **潜在不足**：主实验未报告多次运行的方差/置信区间；OOD 设置虽扩大范围，但仍是受控的解析场景。

## 6. 主要结论与发现

- **有效性（RQ1）**：Datamart-Agent 在所有 6 个设定中取得**最低 Utility Gap 与最高 Pass@$\epsilon$**；GPT-4o 版本比最强基线 LLM-E 的 Pass@$\epsilon$ **高出 20% 以上**，在离散动作准确率与连续决策 MSE 上也最优。
- **消融**：感知模块的自然语言表示最关键（去除后 $\Delta U$ 增加 0.391）；相似检索对记忆模块至关重要；机制引导反思亦带来提升。
- **涌现动态（RQ2）**：严格数据删除规则提升用户效用但略降平台与买家效用；价格再优化提升买家效用、适度惠及平台但略损用户；隐私敏感度显著影响共享行为；买家购买概率随价格下降、随隐私保护上升（隐私可作为互补价值信号）；平台寿命随竞争加剧而缩短，出现选择效应。
- **应用（RQ3）**：**成本感知的分层隐私监管**（Tiered Mandate）将寿命 Gini 系数降至 0.259，显著优于统一监管（0.387）与隐私禁令（0.435），在公平性与平台存续之间取得更好平衡。

## 7. 优点

- **可验证性**：在动态+INC 场景下仍提供解析可解的均衡基准，使 LLM 智能体的评估具备 ground truth，而非仅凭行为仿真。
- **无需参数更新**：通过博弈树记忆 + 机制反思实现经验积累与泛化，避免昂贵的微调。
- **机制引导的显式推理**：将效用公式与约束注入提示，使决策从"模式模仿"转向"效用驱动"，提升均衡一致性。
- **两阶段研究设计**：先验证有效性，再用于无闭式解场景的探索性分析，逻辑闭环清晰。
- **记忆开销可控**：仅检索 Top-$N$ 路径，prompt 长度有界，额外开销相对基线温和。

## 8. 不足与局限

- **均衡一致性评估的边界**：仅在可解析均衡场景下验证，未考虑**战略非均衡**、面对非均衡对手、或存在**多重均衡**的情形（作者自述）。
- **算力披露不足**：未报告训练/推理总算力，影响复现与效率评估。
- **人设同质性**：未引入多样化人格、风险偏好与行为偏差，智能体异质性有限。
- **监管器为固定规则**：未扩展为多目标优化或闭环自适应监管。
- **潜在偏差风险**：依赖 LLM 作为决策核心，可能继承基座模型的系统性偏差；记忆检索相似度与 $\Delta U$ 的相关性（−0.331）仅为中等，检索质量对性能的稳定性仍需进一步验证。
- **应用限制**：模型建立在非排他性数据交易与信息定价假设之上（作者在附录 C.4 论证其等价性），若数据具有排他性、容量约束或买家侧拥塞，结论可能不成立。

（完）
