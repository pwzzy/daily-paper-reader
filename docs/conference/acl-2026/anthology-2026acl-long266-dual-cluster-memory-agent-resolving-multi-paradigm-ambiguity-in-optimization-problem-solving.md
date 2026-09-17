---
title: "Dual-Cluster Memory Agent: Resolving Multi-Paradigm Ambiguity in Optimization Problem Solving"
title_zh: 双簇记忆智能体：解决优化问题求解中的多范式歧义
authors: "Xinyu Zhang, Yuchen Wan, Boxuan Zhang, Zesheng Yang, Lingling Zhang, Bifan Wei, Jun Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.266.pdf"
tags: ["query:llm-agent-or"]
score: 9.0
evidence: 大模型智能体解决优化问题建模歧义
tldr: 针对大语言模型在优化问题中常因同一问题存在多个相关却冲突的建模范式而难以有效求解的问题，本文提出双簇记忆智能体DCM-Agent。该方法无需训练，将历史解划分为建模簇与编码簇，并提炼为方法、检查表与陷阱三类结构化知识，再通过记忆增强推理动态导航。实验表明其能缓解多范式歧义、提升优化问题求解表现。其贡献在于为LLM驱动的优化建模提供了一种免训练的可复用知识增强机制。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long266/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 788, \"height\": 715, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long266/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 935, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long266/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 789, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long266/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 784, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long266/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1643, \"height\": 789, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 809, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 786, \"height\": 330, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1650, \"height\": 1545, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 800, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 805, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 708, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long266/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 726, \"height\": 658, \"label\": \"Table\"}]"
motivation: 大语言模型面对同一优化问题的多种冲突建模范式时易产生结构歧义，影响求解。
method: 提出免训练的双簇记忆智能体，将历史解分为建模与编码簇并提炼结构化指导知识。
result: 通过记忆增强推理动态导航建模范式，缓解歧义并提升优化求解效果。
conclusion: 为LLM驱动的优化问题建模与求解提供了免训练的知识增强机制。
---

## Abstract
Large Language Models (LLMs) often struggle with structural ambiguity in optimization problems, where a single problem admits multiple related but conflicting modeling paradigms, hindering effective solution generation. To address this, we propose Dual-Cluster Memory Agent (DCM-Agent) to enhance performance by leveraging historical solutions in a training-free manner. Central to this is Dual-Cluster Memory Construction. This agent assigns historical solutions to modeling and coding clusters, then distills each cluster’s content into three structured types: Approach, Checklist, and Pitfall. This process derives generalizable guidance knowledge. Furthermore, this agent introduces Memory-augmented Inference to dynamically navigate solution paths, detect and repair errors, and adaptively switch reasoning paths with structured knowledge. The experiments across seven optimization benchmarks demonstrate that DCM-Agent achieves an average performance improvement of 11%- 21%. Notably, our analysis reveals a “knowledge inheritance” phenomenon: memory constructed by larger models can guide smaller models toward superior performance, highlighting the framework’s scalability and efficiency.

---

## 论文详细总结（自动生成）

# 论文总结：Dual-Cluster Memory Agent（DCM-Agent）

## 1. 核心问题与整体含义

- **研究动机**：LLM 在优化问题求解中面临**结构性歧义（structural ambiguity）**——同一个问题往往同时含有指向多种建模范式的线索。例如一个生产计划问题中，"资源最大化"暗示整数线性规划（ILP），"精确倍数"等逻辑约束暗示约束规划（CP），"阶段依赖"暗示动态规划（DP）。这些信号同时存在时会形成**认知干扰（cognitive interference）**。
- **现有方法的不足**：
  - 微调方法（如 ORLM、SIRL）易被干扰误导，机械套用记忆中的模板，难以应对细微变体。
  - 智能体框架在验证阶段缺乏细粒度知识，只能用"检查是否正确"这类静态提示，无法区分 ILP 的线性间隙与 DP 的递推有效性等**范式特异的陷阱**。
- **核心矛盾**：干扰问题要求**灵活性**以导航范式歧义，同时又要求**针对性知识**来验证特定范式的正确性。
- **整体含义**：作者提出免训练的 DCM-Agent，把推理模式**外化到历史档案**中，通过解耦"抽象建模"与"精确编码"，在不更新参数的前提下兼顾灵活性与结构化指导，为 LLM 驱动的优化建模提供可复用、可迁移的知识增强机制。

## 2. 方法论

### 2.1 问题形式化

将求解建模为复合过程：$\hat{y} = E(h_\psi(c \mid m) \circ g_\phi(m \mid x))$，其中 $g_\phi$ 生成建模逻辑 $\hat{m}$，$h_\psi$ 合成可执行代码 $\hat{c}$，$E(\cdot)$ 为代码执行器。核心挑战是 $x \to \hat{m} \to \hat{c}$ 的**一对多**映射。

### 2.2 阶段一：双簇记忆构建（Dual-Cluster Memory Construction）

**节点级构建**：
- 收集 500 道与评测集不相交的问题，按求解轨迹分为三类：
  - **Type A（始终正确）**：多次尝试均成功，代表典范模式；
  - **Type B（可恢复）**：初次失败但重试成功，刻画失败与成功的边界；
  - **Type C（持续失败）**：多次尝试仍失败，编码根本性不匹配。
- 将每个问题—解对分解为**建模逻辑 $m_i$** 与**编码实现 $c_i$**，分别生成嵌入 $e_m, e_c$，并抽取实例级知识 $\Phi_i = \langle \phi^{approach}_i, \phi^{checklist}_i, \phi^{pitfall}_i \rangle$。
- 三类知识来源映射（论文表 1）：
  - $\phi^{approach}$（如何求解，模板与逻辑步骤）← Type A + B；
  - $\phi^{checklist}$（验证什么，有效性准则与边界检查）← Type A + B；
  - $\phi^{pitfall}$（避免什么，常见错误与约束违背）← Type B + C。

**簇级演化**：
- **簇分配**：先用嵌入检索找出 top-k 候选簇（与簇心 $\mu$ 比较），再由 LLM 验证器做语义一致性检查，决定合并到已有簇或新建簇；建模与编码独立聚类。
- **知识更新**：每个簇维护泛化知识 $\mathcal{K} = \langle \mathcal{K}^{approach}, \mathcal{K}^{checklist}, \mathcal{K}^{pitfall} \rangle$。当簇内新增节点数达到阈值 $N=5$ 时触发合成：$\mathcal{K}^{(t+1)} = \text{LLM}_{synth}(\mathcal{K}^{(t)} \cup \bigcup_{j=1}^{N} \Phi_{n_j})$，以抽象出稳健、非冗余的泛化模式。
- **二分图构建**：$G = (V_M, V_C, E)$，边权 $w_{ij}$ 表示建模簇 $C^M_i$ 与编码簇 $C^C_j$ 的共现频率；强边代表已被验证的可行路径，作为后续使用的关键先验。

### 2.3 阶段二：记忆增强推理（Memory-Augmented Inference）

**双重检索**：
- **实例级检索**：按嵌入相似度取 top-K 历史节点 $H$，捕捉细粒度语义相似性；
- **簇级检索**：将新问题嵌入 $e_{new}$ 直接与簇心 $\mu^M_k$ 比较，捕捉超越表面文本匹配的抽象算法模式；
- 合并两类结果得候选建模簇 $R = \{C^M(x_i) \mid x_i \in H\} \cup S_{cluster}$；
- 对每个 $C^M_i \in R$，查询二分图取边权最高的 top-K 编码邻居，构成轨迹池 $P$；
- LLM 选择器按逻辑契合度排序，返回优先队列 $Q = \text{Top-}M(\text{LLM}_{select}(P, x_{new}))$。

**生成—验证—修复—回溯流水线**（所有步骤均以簇级 $\mathcal{K}$ 而非节点级 $\Phi$ 为条件）：
1. **生成与验证**：$\hat{m}_{raw} = \text{LLM}_{gen}(x_{new} \mid \mathcal{K}^{approach}_i)$，随后 $\hat{m} = \text{LLM}_{verify}(\hat{m}_{raw} \mid \mathcal{K}^{checklist}_i)$；编码阶段同理使用 $\mathcal{K}^{approach}_j$ 与 $\mathcal{K}^{checklist}_j$。
2. **修复与回溯**：执行失败时，不做盲目调试，而是结合该算法类型的陷阱警告进行定向修复：$\hat{c}_{fixed} = \text{LLM}_{fix}(\hat{c}, e \mid \mathcal{K}^{pitfall}_j, \mathcal{K}^{checklist}_j)$。若修复超过次数上限，则丢弃该路径，激活队列 $Q$ 中的下一条路径 $p_{t+1}$，避免陷入局部最优。

## 3. 实验设计

- **数据集（7 个优化基准，共 1572 题）**：
  - 线性/混合整数规划基础：NL4Opt（230）、NLP4LP（242）；
  - 高难度任务：OptiBench（605）、OptiMATH（166）、MAMO 的 ComplexLP 子集（211）；
  - 真实场景：IndustryOR（100）、ComplexOR（18）。
  - 记忆构建使用 500 道**与所有评测基准不重叠**的问题。
- **对比基线**：
  - 通用 LLM 直接求解：Qwen3 系列（8B / 30B / 235B）、DeepSeek-V3.2、GPT-5.1；
  - 专用优化框架：OptiMUS（多智能体工作流）、AF-MCTS（蒙特卡洛树搜索）、OptiTree（层次化思维 + 树搜索分解）。
- **评价指标**：严格的端到端求解准确率。要求需求项数值与目标函数值均与真值匹配；允许的求解库为 Gurobi、PuLP、OR-Tools、SciPy、NetworkX。
- **额外分析**：时间成本统计、记忆预算消融（0%/10%/40%/70%/100%）、跨模型记忆迁移、簇数量统计、双簇消融、超参数敏感性（$K, N, M$）、案例分析。

## 4. 资源与算力

- **论文未明确报告 GPU 型号、数量或训练时长**。这一点需特别指出：全文（含附录）均无硬件配置、显存占用或能耗数据。
- 可以间接推断的信息：
  - 框架是**免训练**的，因此没有训练算力开销；唯一的"一次性成本"是记忆构建阶段的历史轨迹采集、分类与二分图搭建（论文在 Limitation 中承认该初始化延迟"不可忽略"）。
  - 表 3 给出的是**推理时间成本**（Qwen3-235B）：NLP4LP 22.1s、OptiBench 41.3s、OptiMATH 73.4s，明显低于 AF-MCTS（85.3s / 110.8s / 205.7s），高于 OptiTree。
- 论文仅在伦理声明中泛泛提及"减少大规模基础模型的能耗"，未提供实测数据。

## 5. 实验数量与充分性

**实验规模（粗略统计）**：
- 主实验：7 个数据集 × 5 个骨干模型 × 5 种方法（基线 + 4 种对比/本方法），即表 2 的完整矩阵；
- 时间成本：3 个数据集 × 5 种方法；
- 记忆预算消融：5 档比例 × 3 个数据集；
- 跨模型知识迁移：5（记忆构建模型）× 5（推理模型）组合 × 3 个数据集；
- 簇数量统计：5 个模型；
- 双簇消融：3 个数据集 × 3 种配置（完整 / 去建模簇 / 去编码簇）；
- 超参数敏感性：3 个参数（$K, N, M$）各 3 档取值 × 3 个数据集；
- 案例分析 1 组（狗粮混合问题的基线 vs. DCM-Agent 对比）。

**充分性与公平性评估**：
- **充分**：覆盖面较广，从 8B 小模型到 GPT-5.1 大模型、从基础 LP 到真实工业场景均有涉及，且同时做了组件消融、超参敏感性、跨模型迁移、记忆预算四类分析，维度较完整。
- **较为公平**：同一骨干模型下对比各方法，使用统一评价协议（同一求解库集合、同一匹配标准），记忆集与评测集严格不重叠，避免了数据泄漏。
- **潜在问题**：
  - ComplexOR 仅 18 题，单题正确与否即造成 5.56% 的准确率波动
