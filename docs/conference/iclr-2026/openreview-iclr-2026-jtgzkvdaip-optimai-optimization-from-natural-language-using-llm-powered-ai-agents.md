---
title: "OptimAI: Optimization from Natural Language Using LLM-Powered AI Agents"
title_zh: OptimAI：基于大语言模型智能体的自然语言优化求解
authors: "Raghav Thind, Youran Sun, Ling Liang, Haizhao Yang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=JtgZkVdAIP"
tags: ["query:llm-agent-or"]
score: 10.0
evidence: 基于LLM的智能体将自然语言优化问题转化为数学形式并选择求解器
tldr: 自然语言优化问题建模常依赖专家手工完成，门槛高且难以自动化。OptimAI提出由大模型智能体担任建模员、规划员和编码员的分工框架，将文字描述自动转化为数学规划并生成可执行求解代码。在多个基准问题上的实验显示，该方法显著优于现有最先进系统。该工作验证了LLM智能体端到端完成运筹优化建模与求解的可行性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 自然语言描述的优化问题需要专家手工建模和选出求解器，人工门槛高且难自动化。
method: 提出OptimAI，以formulator将自然语言转成数学规划，以planner规划高层求解策略，并由coder等智能体生成代码执行求解。
result: 在自然语言优化问题基准上获得优于当前最先进方法的表现。
conclusion: 验证了LLM驱动的多角色智能体能够端到端自动完成优化建模与求解。
---

## Abstract
Optimization plays a vital role in scientific research and practical applications. However, formulating a concrete optimization problem described in natural language into a mathematical form and selecting a suitable solver to solve the problem requires substantial domain expertise.
We introduce OptimAI, a framework for solving Optimization problems described in natural language by leveraging LLM-powered AI agents, and achieve superior performance over current state-of-the-art methods.
Our framework is built upon the following key roles:
(1) a formulator that translates natural language problem descriptions into precise mathematical formulations;
(2) a planner that constructs a high-level solution strategy prior to execution; and 
(3) a coder and a code critic capable of interacting with the environment and reflecting on outcomes to refine future actions.
Ablation studies confirm that all roles are essential; removing the planner or code critic results in $5.8\times$ and $3.1\times$ drops in productivity, respectively.
Furthermore, we introduce UCB-based debug scheduling to dynamically switch between alternative plans, yielding an additional $3.3\times$ productivity gain.
Our design emphasizes multi-agent collaboration, and our experiments confirm that combining diverse models leads to performance gains.
Our approach attains 88.1\% accuracy on the NLP4LP dataset and 82.3\% on the Optibench dataset, reducing error rates by 58\% and 52\%, respectively, over prior best results.

---

## 论文详细总结（自动生成）

# 《OptimAI：基于大语言模型智能体的自然语言优化求解》论文总结

## 1. 核心问题与研究动机

- **核心问题**：自然语言描述的优化问题，如何自动转化为可求解的数学形式并选择合适求解器？
- **研究背景**：优化在科学研究和实际应用中至关重要，但将自然语言问题描述建模为数学规划、并匹配合适的求解器，通常依赖运筹学专家的手工参与，门槛高、成本大，难以自动化。
- **关键矛盾**：自然语言（用户能轻易表达需求）与数学规划（求解器需要的形式化输入）之间存在巨大的语义鸿沟，而传统自动化方法很难跨越这一鸿沟。
- **出发点**：与通用问题求解不同，NLP驱动的优化求解需要同时解决“建模正确性”和“求解可行性”双重挑战——错误的问题描述、错误的模型假设、错误的求解策略都会导致结果失败。

## 2. 论文提出的方法论

### 核心思想
提出 **OptimAI**——基于 LLM 驱动的多智能体（Multi-Agent）协作框架，将优化问题求解拆解为多个职责明确的角色，通过智能体间的分工与协作，端到端地将自然语言描述自动转化为可执行的求解代码。

### 关键角色设计

| 角色 | 职责 |
|------|------|
| **Formulator（建模员）** | 将自然语言问题描述翻译为准确的数学规划形式（目标函数、约束、变量等） |
| **Planner（规划员）** | 在代码执行前预先构建高层求解策略，选择合适的求解方法或求解器 |
| **Coder（编码员）** | 将数学规划和求解策略转化为可运行代码，并与环境交互执行 |
| **Code Critic（代码评审员）** | 检查执行反馈，对失败结果进行反思，指导后续代码修正 |

### 关键技术细节

- **多智能体协作流程**：模型先由 Formulator 完成数学化表达，Planner 在“动手写代码之前”先设计求解路线，再由 Coder 生成代码、Critic 审阅反思，形成闭环迭代优化。
- **UCB 调试调度（UCB-based Debug Scheduling）**：引入强化学习/在线学习中的 UCB（Upper Confidence Bound）策略，在多个备选方案之间**动态切换**，而不是死板地执行单一计划。实验表明，这一调度机制额外带来 **3.3 倍**生产率提升——其本质是对“探索（尝试不同策略）与利用（坚持有效策略）”的平衡。
- **模型异构组合**：设计上有意强调多智能体可由**不同模型**承担不同角色。作者认为不同模型的组合可带来性能增益，实验证实了这一设计选择。

### 文本化流程说明

```
自然语言问题描述
      ↓
[Formulator] → 数学规划（形式化表达）
      ↓
[Planner] → 高层求解策略
      ↓
[Coder + Code Critic] → 迭代生成/修正求解代码
      ↓
（UCB调度动态管理不同策略的调试切换）
      ↓
输出：可执行的求解代码 + 求得的优化解
```

## 3. 实验设计

### Benchmark 数据集

| 数据集 | 说明 | OptimAI准确率 |
|--------|------|--------------|
| **NLP4LP** | 自然语言线性规划问题标准基准 | **88.1%** |
| **Optibench** | 更广泛的优化问题评测集 | **82.3%** |

### 对比方法

- 对比对象为当前最先进的（State-of-the-Art）基线方法。
- 效果提升幅度以“错误率降低”表述：在 NLP4LP 上相比先前最佳结果错误率降低了 **58%**；在 Optibench 上错误率降低了 **52%**。

### 消融实验（Ablation Study）

- **去掉 Planner**：生产率下降 **5.8 倍**——说明预规划（先想后做）的不可替代性。
- **去掉 Code Critic**：生产率下降 **3.1 倍**——说明反思/反馈闭环对错误修正至关重要。
- **去掉 UCB 调度（固定单一计划）**：生产率下降 **3.3 倍**——说明动态在备选策略间切换比固守一个方案更高效。
- **同构 vs. 异构模型组合实验**：验证了“不同模型扮演不同角色”比“单一模型承担所有角色”更有优势。

## 4. 资源与算力

- **论文正文（摘要可见部分）未明确说明**所使用的 GPU 型号、数量、总训练/推理时长、能源开销或成本预算等计算资源信息。
- 从方法特征推断：该方法基于 LLM 推理（尤其若后端调用商用大模型 API），主要开销可能在大量 agent 协作和代码迭代执行上，但具体数值**无法从现有信息获知**。
- 如果重点是解决 NLP→优化 的建模与求解问题，而非模型训练，则算力可能集中在推理和多轮生成上，但这一点属于推测，论文并未给出透明的算力/成本记录。

## 5. 实验数量与充分性评估

- **可确认实验组数**：至少涵盖（1）两个标准数据集上的主结果；（2）至少 3 组消融（去 Planner、去 Critic、去 UCB 调度）；（3）模型组合策略对比实验。实验组数在多智能体框架类论文中属于常规水平。
- **实验设计质量**：消融内容针对核心创新点（Planner 的存在、Critic 的反省能力、UCB 调度机制），每个角色都验证了必要性，设计逻辑清晰、归因合理。
- **有效性指标**：采取"错误率降幅"作为衡量，比单纯报准确率更能反映相对提升幅度。
- **局限之处**：
  - 摘要未给出与基线的详细对比表格（如每个方法的组件配置是否对齐），公平性细节无法从现有内容核验；
  - 未见跨领域泛化实验（如连续优化、混合整数规划、非线性问题等在 Optibench 内部的组织细节）；
  - 未见大规模压力测试或真实业务场景的应用示范。
- **总体判定**：实验具备框架内各模块必要性验证的完整性，但受限于仅能看到摘要层面信息，正文中更丰富的实验细节（例如每类问题子集的表现差异）无法纳入评估。

## 6. 主要结论与发现

1. **端到端可行**：LLM 驱动的多角色智能体协作能够端到端地完成“自然语言 → 数学建模 → 求解代码 → 答案”的全流程自动化。
2. **性能显著领先**：OptimAI 在 NLP4LP 上达到 88.1% 准确率、Optibench 上达到 82.3%，错误率相对先前最佳降低约 6 成。
3. **预规划至关重要**：Planner 角色（执行前先做高层规划）在求解流程中是最大的单一贡献者（去除后损失最重）。
4. **反馈闭环不可或缺**：Critic 提供的结果反思与迭代机制是保障模型修正错误的关键环节。
5. **动态调度优于固定策略**：UCB 调试调度让系统能依据不同方案的实时表现灵活切换，胜过静态执行单一方案。
6. **多样性本身是一种优势**：异构模型组合（不同 LLM 承担不同角色）优于同构配置，说明框架能从模型多样性中获益。

## 7. 论文优点

- **问题选题切中痛点**：自然语言优化建模的自动化是运筹学与 AI 交叉领域的真实需求，研究价值明确。
- **模块化角色分工设计**：将复杂问题拆解为 Formulator（建模）、Planner（规划）、Coder（编码）、Critic（评审）四个清晰逻辑单元，职责解耦、思路富有工程美感。
- **“先规划再执行”的设计有别于主流**：许多现有 LLM 求解框架直接让模型生成代码，缺少显式的策略规划层，OptimAI 的这一设计具有明显差异化亮点。
- **UCB 调度具有理论支撑**：将经典在线决策算法引入 LLM agent 调试流程，是算法层面的创新性迁移。
- **消融因果清楚，效率度量有说服力**：以“×倍生产力变化”来汇报消融损失，直观传达不同模块的实际价值大小。
- **诚实标注细节**：包括该论文具体状态，便于阅者结合审稿意见客观判断其学术定位。

## 8. 不足与局限

- **信息可获取度限制**：本总结基于的仅为论文摘要和元数据；完整正文的算法伪代码、提示词模板、基线实现细节、错误分析等关键内容无法在本总结中展开评估。尤其是该论文在 ICLR 2026 中被拒稿（标注为 Rejected），这一事实通常指向审稿人在方法新颖性或实验说服力上提出了重要异议，需要结合具体审稿意见（如投稿系统讨论或社区公开评审）来判断其学术实质贡献边界。仅基于摘要信息难以确知审稿人指出的是哪些具体问题。
- **缺乏失败案例分析**：摘要未透露 OptimAI 在哪些类型的问题上仍然失败——这恰恰是帮助读者理解应用边界最重要的信息。
- **实验信息不透明**：基准数据集的规模、问题的类型构成、求解器的选取范围与配置、成功判定的标准等细节均未在可见内容中说明。
- **回答格式的可靠性问题**：准确率虽高，但“最终答案正确”与“数学建模本身正确”是否等价（例如答案碰巧正确而模型写错/约束缺失）不得而知。
- **对 API/商业模型的隐性依赖**：若依赖闭源 LLM，该方法在可复现性、稳定性和推广成本上均可能受限。
- **成本与效率的平衡未说明**：多智能体协作 + 迭代调试意味着多轮 LLM 调用，现有摘要并未提供单问题求解的平均成本、平均迭代轮数或延迟指标。
- **计算资源的透明性缺失**：论文未报告训练/推理算力投入，这在依赖基线公平复现的环境（如另一个团队对比或复现代价极高场景）中是一种信息缺口。
- **应用场景覆盖有限**：方法主要面向线性/数学规划类问题，对于非线性、随机优化、大规模实际决策场景的适应能力仍有待验证。

---

（完）
