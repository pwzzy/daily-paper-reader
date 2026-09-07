---
title: Efficient and Interpretable Multi-Agent LLM Routing via Ant Colony Optimization
title_zh: 基于蚁群优化的高效可解释多智能体大语言模型路由
authors: "Jiaquan Zhang, Xudong Wang, Chaoning Zhang, Chenghao Li, Qigan Sun, Sung-Ho Bae, Peng Wang, Ning Xie, Jie Zou, Yang Yang, Heng Tao Shen"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ojUhmgIS7o"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 用蚁群优化元启发式解决LLM多智能体系统的任务路由问题，连接运筹优化与智能体编排
tldr: 多智能体大语言模型系统中的任务路由缺少透明度，且难以适应动态资源受限环境。AMRO将智能体交互建模为函数有向图，利用信息素驱动的节点更新和自适应信息素衰减机制，借鉴蚁群算法实现高效可解释的任务路由优化。该方法把运筹优化中的蚁群元启发式与LLM多智能体系统结合，用于提升系统状态感知和路由决策能力。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM多智能体系统在动态资源受限环境中任务路由缺乏透明性、自适应性以及对系统状态的感知。
method: 提出AMRO，通过函数有向图建模智能体交互，利用信息素驱动的节点更新与自适应衰减机制完成路由优化。
result: 蚁群启发式更新机制可提升多智能体任务路由的效率和可解释性，改善系统状态感知能力。
conclusion: 表明蚁群等运筹优化方法能够改善LLM多智能体系统的任务分配与动态协作。
---

## Abstract
The instruction-following and semantic understanding capabilities of large language models (LLMs) serve as the core competence of Multi-Agent Systems (MAS), enabling collective strategy coordination. However, task routing in MAS remains a critical performance bottleneck, especially in dynamic and resource-constrained environments. Existing LLM-based routing approaches often suffer from limited transparency, static allocation strategies, and insufficient system state awareness. To address these challenges, we propose AMRO: Ant colony inspired Multi-agent Routing Optimization. AMRO models agent interactions as a function-based directed graph, utilizing a pheromone-driven node update mechanism and an adaptive pheromone decay strategy to achieve real-time perception and response to environmental changes, thereby continuously optimizing routing assignments. This approach significantly enhances routing efficiency and overall system performance, while the pheromone-guided path selection offers strong interpretability for the routing process. We conduct extensive experiments on five public benchmark datasets. The results show that AMRO achieves an average improvement of 1.97\% in pass@1 accuracy over the baseline and demonstrates superior efficiency and robustness under high concurrency. These findings indicate that AMRO provides an efficient and interpretable solution to the routing problem in LLM-based MAS.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 核心问题与整体含义

- **背景动机**：大语言模型（LLM）的指令遵循与语义理解能力是多智能体系统（MAS）实现集体策略协调的核心。然而，在多智能体系统中，**任务路由（task routing）** 已成为关键的性能瓶颈，尤其是在**动态、资源受限**的环境中。
- **现有问题**：基于 LLM 的路由方法普遍存在三大缺陷：
  - 透明性不足：路由决策过程不清晰、难以解释；
  - 策略静态化：分配策略不能随环境变化动态调整；
  - 系统状态感知缺乏：对智能体实时负载、能力和状态缺乏感知。
- **整体意义**：本文尝试将运筹优化中的**蚁群优化元启发式**引入 LLM 多智能体任务路由，连接了运筹优化与智能体编排两个领域，为动态协作中的任务分配提供了新的解决思路。

## 2. 方法论：AMRO（Ant colony inspired Multi-agent Routing Optimization）

- **核心思想**：模拟蚂蚁觅食时通过信息素通信、正反馈和挥发机制寻找最优路径的过程，将智能体路由选择建模为信息素引导的路径搜索。
- **关键技术细节**：
  - **函数有向图建模**：将智能体之间的交互关系建模为一个基于函数的**有向图**，图中节点表示智能体（或其功能模块），边表示调用/交互关系；
  - **信息素驱动的节点更新机制**：每个节点（智能体）维护与路由选择相关的信息素浓度。当某个路由路径成功完成任务时，相应路径上的信息素被增强，从而引导后续请求向高效智能体聚集；
  - **自适应信息素衰减策略**：为避免陈旧信息素导致路由僵化，信息素会随时间衰减，且衰减速率可根据环境动态调整，从而实现**实时感知并响应环境变化**，持续优化路由分配。
- **算法流程（文字化）**：
  1. 输入一个任务请求；
  2. 根据当前函数有向图和各边的信息素浓度计算路由概率，选择下一跳智能体；
  3. 智能体执行子任务，并将结果返回；
  4. 根据任务完成质量（如正确性、响应时间）更新该路径上的信息素；
  5. 对所有信息素执行自适应衰减，并重复上述过程直到任务完成或达到最大步数。
- **可解释性来源**：信息素引导的路径选择可以直观地反映出哪些智能体在近期任务中表现更优、为何选择某条路径，因此路由过程具备较强的解释性。

## 3. 实验设计

- **数据集/场景**：文中提到在**五个公开基准数据集**上进行了广泛实验。
- **任务类型**：从摘要推测为涉及多智能体协作的问答/任务完成类基准（具体数据集名称未在摘要中列出，正文未提供）。
- **对比方法**：摘要仅称与“baseline”比较，并未列出具体基线方法名称。结合其提到的“LLM-based routing”，基线可能包含基于 LLM 的静态路由、启发式路由或随机路由等，但**无法从摘要确认**。
- **评估指标**：
  - 主要使用 **pass@1 准确率**；
  - 同时评估了**效率**与**鲁棒性**（尤其在高并发场景下）。

## 4. 资源与算力

- 论文的摘要和元数据中**未提及任何算力信息**，包括 GPU 型号、数量、训练/推理时长、能耗等。
- 因此无法评估其实验的计算成本与可复现性。这是信息呈现上的一个缺口。

## 5. 实验数量与充分性

- **实验数量**：摘要仅声称在五个公开基准上测试，并提到高并发场景下的评估。未提及消融实验、敏感性分析、不同任务类型的细分等。
- **充分性判断**：
  - 由于缺少具体数据集说明、基线明细、误差/方差报告和详细实验设置，目前能看到的实验规模**不够充分透明**；
  - 单一的 pass@1 指标可能无法全面反映路由的延迟、成本、任务成功率、鲁棒性等维度；
  - 没有说明多个随机种子的重复实验或统计显著性检验，因此难以判断结果的稳定性与客观性；
  - 因此，虽然 5 个基准提供了一定的多场景验证，但从公开信息看实验的**完整性、公平性和可复现性尚需正文补充**。

## 6. 主要结论与发现

- **效率提升**：相比基线，AMRO 在 pass@1 准确率上**平均提升 1.97%**；
- **鲁棒性**：在**高并发场景**下表现出更优的效率和鲁棒性；
- **可解释性**：信息素引导的路径选择使路由过程更透明、更易解读；
- **综合意义**：表明蚁群等运筹优化方法可以有效改善 LLM 多智能体系统中的任务分配与动态协作，提供高效且可解释的路由解决方案。

## 7. 优点

- **跨领域融合创新**：将蚁群优化（运筹学中的成熟元启发式）与 LLM 多智能体系统结合，思路新颖，拓宽了智能体路由优化的技术路线；
- **动态自适应能力强**：通过自适应信息素衰减，系统能感知环境变化并及时调整路由策略，缓解了静态策略的缺陷；
- **可解释性突出**：信息素机制天然提供路径选择的可视化依据，避免了传统深度强化学习或黑盒路由不可解释的问题；
- **高效性**：蚁群优化的分布式、正反馈特性有助于在高并发下快速收敛到优质路由；
- **多基准验证**：在 5 个公开数据集上进行评估，具有一定的泛化验证广度。

## 8. 不足与局限

- **信息不透明**：提供的摘要信息过少，缺少方法细节、伪代码、复杂度和正式定义；
- **基线不明确**：未列出可比方法的名称与版本，无法判断比较的公平性；
- **实验细节缺乏**：没有说明各个数据集的具体任务特性、规模、评估协议、指标计算方式；
- **消融缺失**：未见对信息素更新、衰减策略、图构建方式等核心组件的消融实验，无法确认各部件贡献；
- **算力未报告**：无法评估实际部署成本；
- **应用限制**：蚁群算法本身的参数敏感性和收敛速度问题未被讨论；MAS 的拓扑结构和智能体异质性对方法效果的影响也尚未显式分析；
- **指标单一**：pass@1 仅衡量最终正确性，没有覆盖路由延迟、资源消耗、智能体负载均衡等关键性能维度；
- **综述性内容**：以上局限部分源于可获取文本仅为摘要和元数据，正式论文中的完整实验和讨论可能会弥补部分不足，但截至当前信息，上述评估缺口确实存在。

（完）
