---
title: Evolving Agentic Workflow Driven by Human-Agent Collaboration
title_zh: 人机协作驱动的智能体工作流进化
authors: "Yuxin Liu, Jinxuan Zhang, Yuezhang Peng, Hefeng Zhou, Xiangfeng Wang, Jiong Lou, Chentao Wu, Jie LI, Jingjing Qu, Chaochao Lu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1250.pdf"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 用进化算法搜索最优多LLM智能体工作流
tldr: 针对智能体工作流手工设计成本高、搜索效率低且难以动态适应新任务与用户偏好的问题，本文提出人机协作的进化框架HFlow。该框架用进化算法对工作流的结构、提示词与底层LLM进行变异与交叉，自动搜索最优工作流，并以人类偏好引导快速收敛。分层经验记忆提升泛化与适应能力。工作将优化搜索用于智能体编排，为复杂问题求解提供可自动化的工作流构建方法。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1250/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 729, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1250/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 687, \"height\": 449, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1250/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1564, \"height\": 889, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1250/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 724, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1250/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 725, \"height\": 314, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1250/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1661, \"height\": 699, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1250/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 509, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1250/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 682, \"height\": 430, \"label\": \"Table\"}]"
motivation: 多LLM智能体工作流存在手工设计成本高、智能体搜索低效与动态适应性差的问题。
method: 提出进化框架HFlow，对工作流结构、提示词与LLM主干进行变异交叉搜索，并由人类偏好引导收敛。
result: 分层经验记忆与人类偏好引导使工作流搜索更快收敛并更好适应新任务。
conclusion: 将进化优化引入智能体编排，降低人工设计成本并提升复杂问题求解的自动化程度。
---

## Abstract
Agentic workflows, composed of multiple collaborating Large Language Models (LLMs), have become a key paradigm for complex problem-solving. However, their effectiveness is often hindered by three critical challenges: high manual design costs, inefficient agentic search, and poor dynamic adaptability to new tasks and human preferences. To address these limitations, we propose HFlow, an evolutionary framework for generating agentic workflows through human-agent collaboration. HFlow employs an evolutionary algorithm to automate the search for optimal workflows by mutating and crossing over their structures, prompts, and LLM backbones. This process is guided by human preferences to ensure rapid convergence, while a hierarchical experience memory enables the generalization of learned strategies. Extensive experiments on math and code generation benchmarks show HFlow surpasses other automated baselines by up to 27.34%, while achieving comparable performance to o1-preview at only one-fourth of the cost. Our work introduces a new paradigm for workflow design that produces cost-effective and adaptive solutions, better aligning automated agentic systems with dynamic human needs.

---

## 论文详细总结（自动生成）

# 论文总结：人机协作驱动的智能体工作流进化（HFlow）

## 1. 核心问题与整体含义

- **研究背景**：由多个 LLM 协作构成的"智能体工作流"（agentic workflow）已成为复杂问题求解的关键范式。从早期单智能体顺序执行，发展到结构化多智能体工作流（如 AutoGen、MetaGPT、GPTSwarm、AFlow 等），智能体设计的重要性日益凸显。
- **核心问题**：现有智能体工作流设计面临三大挑战：
  1. **高人工设计成本**：提示词与执行序列仍需人工探索，阻碍通用性与可扩展性。
  2. **低效的智能体搜索**：现有自动搜索多依赖蒙特卡洛树搜索等启发式方法，需长时间迭代反馈，导致高昂的 LLM API 成本与冗长搜索周期。
  3. **动态适应性差**：当前设计多为单向流程，无法在新环境中动态调整或理解人类隐性知识与偏好，且需重新初始化。
- **核心研究问题**：如何自动优化一组高效、低成本且适应人类需求的智能体工作流，为多样查询提供解决方案？
- **整体含义**：论文提出 **HFlow**，将工作流生成建模为一个由人类偏好引导、可学习历史经验的进化优化问题，试图为智能体编排建立"低成本、自适应"的新范式。

## 2. 方法论

### 2.1 核心思想
- 将智能体工作流的构建视为**搜索 + 进化**问题：通过交叉与变异操作，同时进化工作流的**高层结构**与**低层算子配置**，并由**人机协作反馈**引导收敛方向，由**分层经验记忆**实现跨任务泛化。

### 2.2 问题形式化
- **工作流定义**：工作流 $W=(\mathcal{N},E)$ 为有向无环图，节点 $N_i=(M_i,P_i,\theta_i)$ 表示算子（调用的 LLM、提示词、参数如 temperature），边 $E$ 定义数据流与拓扑结构。
- **搜索空间**：$S_{HFlow}=\{(\mathcal{N},E)\mid N\in S_{op},\ E\in S_{struct}\}$，即结构空间与算子空间的笛卡尔组合。
- **目标函数**：不再追求单一最优工作流 $W^*$，而是进化出多样且有效的种群：
  $$W^*=\arg\max_{W\in S_{HFlow}}\big(u(W,H,T)-\lambda\cdot c(W,T)\big)=\arg\max\big(p(W,T)+h(W,T)-\lambda\cdot c(W,T)\big)$$
  其中 $p(\cdot)$ 为任务性能、$h(\cdot)$ 为人类偏好、$c(\cdot)$ 为 API 成本、$\lambda$ 为权衡系数。

### 2.3 算法流程（Algorithm 1）
1. **种群初始化**：初始化算子池 $P^{(0)}_{op}$（CoT、Reflexion、Ensemble、Test、Custom 等）与结构池 $P^{(0)}_{struct}$（线性序列、生成-评审循环等基础拓扑，并用 LLM 分类器赋予 profile 标签）。
2. **基于检索的选择**：对查询 $q_t$，用标签嵌入的**余弦相似度** $S(W_i|q_t)=\frac{V(\tau_i)\cdot V(q_t)}{\|V(\tau_i)\|\|V(q_t)\|}$ 选出 Top-K 个最相关父代工作流。
3. **交叉与变异扩展**：
   - **交叉**：由 LLM 融合多个父代的结构与算子特征生成子代 $W_{child}$。
   - **结构变异** $\pi_s$：增删节点或边，改变拓扑。
   - **提示词变异** $\pi_p$：基于经验池中成功提示模板改写提示。
   - **LLM 变异** $\pi_l$：依据性能与成本在开源/闭源模型中替换骨干。
4. **人机协作评估**：对候选工作流执行并采集性能 $p$、偏好 $h$、成本 $c$ 三类指标，并维护**累积指标**（增量式更新 $\bar p_t(W_i)=\frac{\bar p_{t-1}(W_i)(n_t-1)+p(W_i,q_t)}{n_t}$）。
5. **种群更新（Pareto 支配）**：用多目标 Pareto 支配关系计算适应度 $F(W)=\sum_{W'\in P^{(t)}\cup W'_{child}}\exp\big(\frac{I(W',W)}{\phi\cdot I_{max}}\big)$，删除适应度最大（即被支配）的个体，保留 Pareto 前沿以维持多样性与成本-性能权衡。
6. **记忆更新**：将新经验写回分层记忆。

### 2.4 分层经验记忆
- **结构偏好记忆** $M_{struct}$：存储 $(W_i,q_j,H_{struct})$，指导初始化与结构变异。
- **提示偏好记忆** $M_{op}$：存储 $(W_i,q_j,H_{op})$，提供成功提示变体并跨任务复用。
- **LLM 经验记忆** $M_{LLM}$：记录不同算子语境下各 LLM 的正确性与成本，指导骨干选择。

## 3. 实验设计

### 3.1 数据集与场景
- **数学**：GSM8K、MATH（仅保留 Level 5 难度），指标为 solve rate。
- **代码生成**：HumanEval、MBPP，指标为 pass@1。
- **具身 AI**：ALFWorld，指标为成功率。
- 所有数据集按 **1:4** 划分训练/测试集。

### 3.2 对比方法（16 个基线）
- **手工单智能体**：Vanilla、CoT、ComplexCoT、Self-Consistency。
- **手工多智能体**：MultiPersona、LLM-Debate、LLM-Blender、DyLAN、AgentVerse、MacNet。
- **自动化工作流**：AutoAgents、GPTSwarm、ADAS、AgentSquare、AFlow、MASS。

### 3.3 实现细节
- 骨干模型：GPT-4o-mini 作为基础模型以保证公平；节点配置、工作流生成与答案合成使用 Claude-3.5-Sonnet、GPT-4o-mini、DeepSeek-V2.5、Qwen-2.5-72B、Llama-3.1-70B。
- **人类 oracle 由 GPT-4o 模拟**，整合三位人类专家与一个持续校准的自动智能体的洞见。

## 4. 资源与算力

- **论文未明确说明所用 GPU 型号、数量、训练时长或集群规模**。
- 文中仅提供了 **LLM API 成本**（美元）作为资源度量（Table 2）：HFlow 在 MATH 上成本 2.11 美元、MBPP 上 0.67 美元；对比 o1-preview 的 7.84/3.21 美元、DyLAN 的 16.86/8.79 美元（Qwen）等。
- 由于方法本身是"进化搜索 + API 调用"而非模型训练，其资源消耗主要体现在推理/搜索阶段的 API 开销，但论文未披露搜索迭代次数与总 token 量等细粒度算力信息。

## 5. 实验数量与充分性

- **主要性能实验**：5 个数据集 × 16 个基线（Table 1）。
- **成本分析**：在 MATH 与 MBPP 上对比 o1-preview、Vanilla、DyLAN、AFlow（Table 2）。
- **反馈影响消融**：8 种反馈设置（无反馈、随机、错误、分数、分数+摘要、分数+理由、多分数+摘要、多分数+理由）（Table 3）。
- **组件消融**：去除 LLM 经验、提示偏好池、结构偏好池三种记忆组件（Fig 5）。
- **进化效率实验**：在 MATH 训练/测试集上比较 HFlow 与 AFlow 随迭代的 solve rate 曲线（Fig 4）。
- **评价**：实验覆盖面较广（数学/代码/具身三类任务、多类基线、消融充分），整体客观。但存在公平性隐忧：MASS 非开源，对比基于其报告结果；ALFWorld 上 MASS 无结果；且人类反馈由 LLM oracle 模拟而非真实用户，可能引入偏差。

## 6. 主要结论与发现

- **性能领先**：HFlow 平均准确率提升 **12.34%**，相对基线最高提升 **27.34%**（ALFWorld 67.23%），在 GSM8K（94.03%）、MATH（57.20%）上表现突出。
- **成本优势**：以 **o1-preview 约 1/4 的成本**达到与之相当的性能（如 MBPP 上 84.75% vs 89.65%，但成本仅 0.67 vs 3.21 美元）；HumanEval 上以更轻量骨干超越使用 Gemini-1.5-pro 的 MASS。
- **搜索效率更高**：相比 AFlow，HFlow 收敛更快、最终 solve rate 更高，归因于人类 oracle 的高质量引导与经验记忆的累积学习。
- **反馈质量至关重要**：无反馈导致准确率下降近 10%；错误/随机反馈甚至低于基线；**细粒度多分数 + 理由（reason）反馈**效果最佳。
- **记忆组件关键性**：LLM 经验记忆影响最大，其次为结构偏好池——说明"选对 LLM"与"设计好高层架构"是成功的最关键因素。

## 7. 优点

- **新范式**：首次将智能体工作流设计明确表述为"人类偏好引导的进化优化问题"，把人类偏好作为关键信号纳入目标函数。
- **多目标 Pareto 优化**：用 Pareto 支配替代加权求和，避免为性能-成本冲突手工调参，保持解集多样性，防止早熟收敛。
- **分层经验记忆**：将结构、提示、LLM 三类知识分离存储与检索，提升跨任务迁移与适应性。
- **成本效益显著**：以极低成本逼近 o1-preview，且进化搜索为一次性投入、可被长期复用摊销。
- **消融设计细致**：反馈类型与记忆组件的消融揭示了各要素的贡献，结论有说服力。

## 8. 不足与局限

- **人类反馈的真实性**：论文自认依赖"人类专家 + 校准 LLM"的混合 oracle，LLM 代理可能无法完全捕捉真实用户反馈的多样性，未开展大规模真人研究验证泛化性。
- **算力信息缺失**：未报告 GPU 型号、数量、训练/搜索时长等关键资源信息，难以评估实际部署门槛。
- **部分基准提升有限**：HumanEval 上提升幅度较小（因基础模型已较强），说明优势并非在所有任务上都显著。
- **对比公平性存疑**：MASS 非开源，仅基于报告结果比较；ALFWorld 上缺乏 MASS 对照；不同方法骨干模型不完全一致（MASS 用 Gemini-1.5-pro）。
- **应用限制**：方法依赖多个闭源商用 LLM 的 API，存在成本与可用性风险；进化搜索的一次性成本在低频任务场景下可能难以摊销。
- **偏差风险**：以 GPT-4o 作为"人类 oracle"可能继承其固有偏好偏差，导致工作流朝特定方向收敛。

（完）
