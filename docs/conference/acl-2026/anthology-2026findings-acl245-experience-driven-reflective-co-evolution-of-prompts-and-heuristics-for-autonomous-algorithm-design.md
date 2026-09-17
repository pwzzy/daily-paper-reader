---
title: Experience-Driven Reflective Co-Evolution of Prompts and Heuristics for Autonomous Algorithm Design
title_zh: 经验驱动的提示与启发式反思式协同演化用于自主算法设计
authors: "Yihong Liu, Junyi Li, Hongyu Lu, Wayne Xin Zhao, Ji-Rong Wen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.245.pdf"
tags: ["query:llm-agent-or"]
score: 8.0
evidence: 大模型驱动的组合优化启发式算法自动合成
tldr: 组合优化长期依赖人工设计启发式，成本高且受限；已有用大模型迭代启发式种群的方法探索不足，易陷入局部最优。本文提出EvoPH框架，通过经验驱动的反思式提示与启发式协同演化，结合岛屿迁移模型与精英选择来维持种群多样性。该方法实现了组合优化算法的自主合成与优化，缓解了搜索停滞问题。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl245/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1416, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl245/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 797, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl245/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 803, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl245/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1411, \"height\": 512, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl245/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1486, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl245/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 696, \"height\": 434, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl245/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 1102, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl245/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1592, \"height\": 503, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl245/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 799, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl245/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1444, \"height\": 465, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl245/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1420, \"height\": 212, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl245/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1421, \"height\": 212, \"label\": \"Table\"}]"
motivation: 组合优化依赖人工设计启发式，而现有大模型迭代方法探索不足，易陷入局部最优。
method: 提出EvoPH框架，用反思式机制协同演化提示与启发式，并结合岛屿迁移与精英选择维持种群多样性。
result: 该框架实现了组合优化算法的自主合成与优化，有效缓解了启发式搜索的局部最优停滞。
conclusion: 表明大模型可驱动组合优化启发式的自主演化设计。
---

## Abstract
Combinatorial optimization has long been dominated by manually engineered heuristics, a paradigm requiring substantial expert intuition and implementation overhead. The advent of Large Language Models has disrupted this landscape, enabling the autonomous synthesis and optimization of algorithms. Recent approaches typically iterate on heuristic populations using LLMs as mutators; however, these strategies often suffer from limited exploration, leading to stagnation in local optima. To overcome this, we present the Experience-Driven Reflective Co- Evo lution of P rompt and H euristics ( EvoPH ) for autonomous algorithm design, a novel framework that couples an island migration model with elite selection to maintain population diversity. Uniquely, EvoPH co-evolves both the guiding prompts and the heuristics themselves, using a feedback loop driven by past experience to refine the search process. We demonstrate EvoPH’s efficacy on the Traveling Salesman and Bin Packing Problems. Our results show that EvoPH achieves superior accuracy compared to baselines, marking a significant step forward in LLM-aided algorithm design.

---

## 论文详细总结（自动生成）

## 一、论文核心问题与整体含义

- **研究动机**：组合优化问题（COPs）长期依赖人工设计启发式算法，需要大量领域专家直觉与实现成本；现实应用还常需针对不同流程和参数定制算法。
- **背景脉络**：遗传编程等自动启发式设计（AHD）方法受限于人工定义的变异算子；大语言模型（LLM）为代码生成与算法设计提供了新可能，但已有方法常使用固定提示或低效进化策略，探索不足，容易陷入局部最优。
- **关键痛点**：
  - 启发式种群进化探索有限，易停滞于局部最优；
  - 代码执行中的语法/逻辑错误会在后代中传播，造成重复失败和高计算开销；
  - 提示通常固定，无法根据执行反馈自适应调整。
- **论文含义**：提出 **EvoPH**，即经验驱动的反思式提示与启发式协同演化框架，让提示和可执行启发式算法共同进化，以更自主、更稳健地设计组合优化算法。

## 二、方法论：核心思想与关键技术

- **核心思想**：构建“启发式生成—评估—经验存储—反思—提示/策略演化”的闭环，将 LLM 作为语义变异算子，同时让指导 LLM 的提示也随经验进化。
- **总体流程**（Algorithm 1）：
  1. 初始化启发式 \(H_0\)、提示 \(P_0\)、策略池 \(S\)、数据 \(I\)；
  2. 初始化 \(K\) 个岛屿，每个岛屿维护自己的精英档案；
  3. 每轮迭代中，为每个岛屿选择父代启发式、采样进化策略、组合提示；
  4. LLM 生成子代启发式，执行评估，并将结果/错误分析写入经验库 \(E\)；
  5. 更新岛屿精英档案，演化提示；
  6. 每隔 \(\tau\) 轮执行岛屿迁移，最终返回最优启发式。

### 1. 启发式演化

- **生成**：LLM 在提示引导下，从精英库父代生成新候选算法。
- **经验总结**：执行有效则提取性能指标；执行失败则生成系统分析与报告；无论成败都蒸馏为结构化经验，用于后续反思。
- **岛屿精英选择**：
  - 将全局种群划分为 \(K\) 个相对独立的岛屿子种群；
  - 定义行为特征空间 \(F: H \to B\)，每个行为描述子 \(b\) 对应一个网格单元，存储该特征组合下最佳启发式；
  - 更新规则：  
    \[
    M_i(b_{\text{child}}) \leftarrow \max_g\{M_i(b_{\text{child}}), h_{\text{child}}\}
    \]
    即只有性能不劣于已有精英的子代才能替换；
  - 父代选择在探索与利用间平衡：探索时随机采样以保持多样性，利用时优先选择在多个描述子上稳定高质量的启发式。
- **岛屿迁移**：周期性将源岛屿精英迁入目标岛屿，与本地精英竞争，促进全局信息共享，避免早熟收敛。

### 2. 提示演化

- **Prompt Update**：根据启发式执行反馈，强化有效提示，改写或丢弃持续导致差结果的提示；提示从固定指令逐渐变为任务特定、可纠错的控制器。
- **Strategy Sampling**：预定义多种进化策略，如：
  - 参数修改；
  - 冗余移除；
  - 结构修改；
  - 启发式重写；
  - 完全重写。
  根据历史经验选择或组合策略，使提示与策略共同适应当前搜索状态。
- **最终提示**：由迭代更新的提示和采样得到的进化策略动态组合而成，既承载知识，也作为自适应控制器。

### 3. 与已有工作的区别

- 相比 EoH 的固定提示，EvoPH 引入经验驱动的提示进化；
- 相比 ReEvo 的 LLM 反思，EvoPH 支持提示与启发式协同演化；
- 相比 NeRM，无需辅助预测器；
- 相比 CALM，无需 LLM 微调，模型无关、更可扩展；
- 进化单元是可执行启发式代码，提示是辅助控制器，形成带延迟跨层信用分配的双层优化。

## 三、实验设计

- **数据集/场景**：
  - **TGB（TSP-Gurobi-Bench）**：基于 TSPLIB，转换为距离矩阵；用 Gurobi 求最优解，保留 58 个 600 秒内可解实例。
  - **BOB（BPP-Ortools-Bench）**：基于 BPPlib，选取 92 个实例；用 Google OR-Tools 求最优解。
- **评价指标**：相对误差  
  \[
  \text{Relative Error} = \frac{A_{\text{sol}} - O_{\text{sol}}}{O_{\text{sol}}} \times 100\%
  \]
  越低越好。
- **初始启发式**：
  - TSP：Christofides、2-opt、Nearest Insertion、Farthest Insertion、Nearest Neighbor、Random Insertion；
  - BPP：First Fit、Best Fit、Next Fit、Worst Fit。
- **对比方法**：BASE 初始启发式、FunSearch、EoH、mEoH、ReEvo、EvoPH。
- **实现设置**：Gemini-2.5-pro 作为主 LLM；temperature=0.8，top-p=0.95；\(T=20\) 轮，\(K=5\) 个岛屿；每个候选程序 600 秒超时；主实验使用固定随机种子，并额外用 5 个随机种子评估稳定性。
- **主要结果**：
  - TGB 上 EvoPH 显著降低相对误差：Christofides 20.64%→5.17%，2-opt 6.62%→4.20%，Nearest Insertion 19.54%→4.41%，Farthest Insertion 8.20%→4.05%，Nearest Neighbor 24.67%→4.41%，Random Insertion 9.43%→4.41%。
  - BOB 上同样提升：First Fit 4.90%→0.43%，Best Fit 28.13%→1.65%，Next Fit 5.61%→1.59%，Worst Fit 14.66%→1.65%。
- **消融实验**：在 TGB 上比较完整 EvoPH 与 w/o Strategy Sampling、w/o Prompt Evolution、w/o Island-Based Elites Selection，三者均导致性能下降。
- **进一步分析**：
  - 可执行性：带提示进化时生成可执行代码比例更高；
  - 收敛性：不同初始算法均表现为早期快速提升、后期稳定；
  - 随机稳定性：5 个随机种子下方差较低；
  - 模型规模：Qwen2.5-7B/14B 在 TSP 上有改进，14B 优于 7B；但在 BPP 上小模型基本停留在 BASE 水平，Gemini-2.5-Pro 仍显著更好；
  - 可扩展性：问题规模增大时相对误差较稳定，运行时间增长主要由可执行代码评估而非提示进化导致。

## 四、资源与算力

- 论文**未明确说明 GPU 型号、数量、训练时长或总能耗**。
- 方法本身不涉及 LLM 微调，主要依赖推理：
  - 主实验使用 **Gemini-2.5-pro**；
  - 模型规模鲁棒性实验使用 **Qwen2.5-7B-Instruct** 和 **Qwen2.5-14B-Instruct**；
  - 每候选程序执行超时 600 秒；
  - 进化配置为 \(T=20\) 轮、\(K=5\) 个岛屿；
  - 可扩展性附录报告了每轮运行时间分解，如 TSP 大规模下 LLM 生成约 50.9 秒/轮、反思+岛屿约 25.8 秒/轮、代码执行约 281.4 秒/轮。
- 局限中也指出：
