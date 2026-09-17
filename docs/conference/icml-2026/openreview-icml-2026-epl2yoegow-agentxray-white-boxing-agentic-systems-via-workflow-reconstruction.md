---
title: "AgentXRay: White-Boxing Agentic Systems via Workflow Reconstruction"
title_zh: AgentXRay：通过工作流重建实现智能体系统白盒化
authors: "Ruijie Shi, Houbin Zhang, Yuecheng Han, Yuheng Wang, Jingru Fan, Runde Yang, Yufan Dang, Huatao Li, Dewen Liu, Yuan Cheng, Chen Qian"
date: 2026-04-30
pdf: "https://openreview.net/pdf/7cf3481e1a69e3585ab912a046ded8ea0968e629.pdf"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 将智能体系统与智能体工作流的组合优化结合
tldr: 已部署的智能体系统往往以黑盒形式运行，内部工作流不透明，导致难以解释与控制。论文提出智能体工作流重建任务，旨在仅凭输入输出访问合成一个可解释的替代工作流，并将该任务建模为链式工作流空间上关于离散智能体角色与工具调用的组合优化问题，用搜索框架求解。实验表明该方法能逼近黑盒系统行为。其贡献在于把组合优化引入智能体系统白盒化，提升可解释性与可控性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 许多已部署的智能体系统内部工作流不透明，用户难以解释和控制其行为。
method: 提出智能体工作流重建任务，将合成替代工作流形式化为链式空间中离散角色与工具调用的组合优化问题，用搜索框架求解。
result: 仅凭输入输出访问即可合成可解释的替代工作流，逼近黑盒系统的行为。
conclusion: 为智能体系统的白盒化、可解释与可控提供了组合优化的新视角。
---

## Abstract
Large Language Models have shown strong capabilities in complex problem solving, yet many agentic systems remain difficult to interpret and control due to opaque internal workflows.
While some frameworks offer explicit architectures for collaboration, many deployed agentic systems operate as black boxes to users.
We address this by introducing Agentic Workflow Reconstruction (AWR), a new task aiming to synthesize an explicit, interpretable stand-in workflow that approximates a black-box system using only input--output access.
We propose AgentXRay, a search-based framework that formulates AWR as a combinatorial optimization problem over discrete agent roles and tool invocations in a chain-structured workflow space.
Unlike model distillation, AgentXRay produces editable white-box workflows that match target outputs under an observable, output-based proxy metric, without accessing model parameters.
To navigate the vast search space, AgentXRay employs Monte Carlo Tree Search enhanced by a scoring-based Red-Black Pruning mechanism, which dynamically integrates proxy quality with search depth.
Experiments across diverse domains demonstrate that AgentXRay achieves higher proxy similarity and reduces token consumption compared to unpruned search, enabling deeper workflow exploration under fixed iteration budgets.

---

## 论文详细总结（自动生成）

> 说明：提供的 PDF 提取文本实际为 OpenReview 的浏览器验证页面，未包含论文正文；以下总结主要依据题录元数据、摘要及结构化字段。涉及具体数据集、算力、实验组数等正文细节处，将明确标注“未提供/无法判断”。

## 1. 核心问题与整体含义

- **研究动机**：大语言模型在复杂问题求解中表现强，但许多已部署的智能体系统内部工作流不透明，用户难以解释和控制其行为。
- **核心问题**：已部署智能体系统常以黑盒形式运行，只能观察输入与输出，无法查看内部角色分工、工具调用和协作流程。
- **整体含义**：论文提出 **Agentic Workflow Reconstruction, AWR** 新任务，目标是在仅有输入—输出访问的条件下，合成一个显式、可解释、可编辑的替代工作流，以逼近黑盒智能体系统的行为。
- **定位差异**：不同于模型蒸馏，AgentXRay 不访问模型参数，而是产出白盒工作流；其重点不是复制模型权重，而是重建可读、可改的智能体流程。
- **应用价值**：为智能体系统的白盒化、可解释性、可控性和审计提供新路径，也可用于理解、复现或改进已有黑盒智能体系统。

## 2. 方法论：核心思想与关键技术

- **任务形式化**：将 AWR 建模为 **链式工作流空间上的组合优化问题**。搜索空间由离散的智能体角色和工具调用组成，目标是找到一条替代工作流，使其在输出层面尽可能接近黑盒系统。
- **核心思想**：在无法访问模型参数的前提下，仅利用输入—输出访问，通过搜索算法合成一个可解释的 stand-in workflow。
- **评价方式**：使用 **基于输出的代理指标** 衡量候选工作流与黑盒系统输出的相似度。该指标是可观察的，不需要内部参数或真实工作流标签。
- **搜索框架**：提出 **AgentXRay**，一种基于搜索的框架，在链式工作流空间中探索离散角色与工具调用的组合。
- **MCTS 增强**：使用 **蒙特卡洛树搜索** 导航巨大的组合搜索空间，平衡探索与利用，逐步构建和评估候选工作流。
- **Red-Black Pruning**：引入 **基于评分的红黑剪枝机制**，动态整合代理质量与搜索深度，剪除低潜力分支，从而在固定迭代预算下进行更深的工作流探索。
- **算法流程概述**（据摘要可概括为）：
  - 初始化搜索树，节点对应部分链式工作流或候选工作流；
  - 扩展节点时加入离散角色或工具调用；
  - 用输出代理指标评估候选工作流质量；
  - 通过 MCTS 选择高潜力分支继续搜索；
  - 用 Red-Black Pruning 根据评分和深度动态剪枝；
  - 最终输出可编辑的白盒工作流。
- **输出特点**：结果是显式、可解释、可编辑的工作流，而非黑盒模型或仅蒸馏出的学生模型。

## 3. 实验设计

- **场景/领域**：摘要称实验覆盖 **diverse domains**，即多个不同领域，但未提供具体数据集名称、领域列表或任务类型。
- **Benchmark**：论文将 AWR 本身作为新任务；评价依赖输入—输出访问和 **output-based proxy metric**。是否构建了公开 benchmark、具体指标定义如何，摘要未说明。
- **对比方法**：摘要明确与 **unpruned search** 对比，即未使用 Red-Black Pruning 的搜索版本。
- **评价指标**：
  - **Proxy similarity**：替代工作流与黑盒系统输出的代理相似度；
  - **Token consumption**：token 消耗；
  - **Iteration budget**：固定迭代预算下的搜索能力；
  - **Workflow exploration depth**：工作流探索深度。
- **其他基线**：摘要提到“不同于模型蒸馏”，但未说明实验中是否与蒸馏方法、其他工作流重建方法或人工设计流程进行对比。因此，外部基线信息不足。

## 4. 资源与算力

- 提供的摘要与元数据中 **未提及 GPU 型号、数量、训练时长、推理成本或集群规模**。
- 由于方法强调仅通过输入—输出访问黑盒系统，可能主要涉及搜索与调用开销，但论文是否报告 token 成本之外的算力细节，当前材料无法确认。
- 结论：**算力资源信息未提供，无法评估其计算效率与可复现成本。**

## 5. 实验数量与充分性

- 从现有材料只能确认：
  - 进行了跨多个领域的实验；
  - 进行了剪枝与未剪枝搜索的对比；
  - 报告了代理相似度与 token 消耗等结果。
- **具体实验组数未提供**：无法知道使用了多少数据集、多少黑盒系统、多少种工作流结构、多少轮重复实验。
- **消融实验**：至少包含 Red-Black Pruning 与 unpruned search 的消融式比较，但其他组件如 MCTS、评分函数、深度项等的单独消融未在摘要中说明。
- **充分性与公平性**：
  - 仅凭摘要无法判断实验是否充分；
  - 缺少外部强基线、统计显著性检验、随机种子、方差报告等信息；
  - 若只与 unpruned search 对比，可能存在“内部对比充分、外部对比不足”的问题；
  - 代理指标本身是输出层面的近似，公平性取决于指标设计，但当前材料未给出细节。

## 6. 主要结论与发现

- AgentXRay 能够在仅有输入—输出访问的情况下，合成可解释的替代工作流，逼近黑盒智能体系统的行为。
- 与未剪枝搜索相比，AgentXRay 获得 **更高的代理相似度**，同时 **降低 token 消耗**。
- 在固定迭代预算下，Red-Black Pruning 使搜索能够进行 **更深的工作流探索**。
- 论文将智能体系统白盒化问题转化为链式工作流空间上的组合优化问题，为可解释性与可控性提供了新视角。
- AWR 任务本身具有独立价值：它强调从黑盒行为反推可编辑工作流，而不是仅做输出模仿或模型蒸馏。

## 7. 优点

- **任务定义新颖**：提出 Agentic Workflow Reconstruction，将黑盒智能体系统的理解问题形式化为工作流重建问题。
- **黑盒实用性强**：只依赖输入—输出访问，不要求模型参数或内部日志，更贴近真实部署场景。
- **产出白盒可编辑**：生成的是显式工作流，可解释、可修改，优于仅得到另一个黑盒模型。
- **组合优化视角清晰**：把离散角色与工具调用纳入链式工作流空间，便于用搜索方法求解。
- **搜索效率设计有针对性**：MCTS 加 Red-Black Pruning，结合代理质量与搜索深度，在固定预算下提升探索深度并减少 token 消耗。
- **跨领域验证**：摘要声称覆盖多个领域，若属实，说明方法具有一定通用性。

## 8. 不足与局限

- **正文缺失导致无法完整验证**：当前 PDF 文本仅为 OpenReview 验证页，无法核对方法公式、实验表格、附录和复现细节。
- **评价指标局限**：仅使用 output-based proxy metric，可能只能保证输出行为近似，不能保证内部角色、工具调用和协作机制与真实黑盒系统一致。
- **工作流空间限制**：方法假设链式工作流空间，可能难以覆盖真实智能体系统中的分支、循环、多智能体图结构或动态调度。
- **黑盒访问假设限制**：若黑盒系统输出不可靠、存在随机性、或被限制调用频率，重建质量可能下降。
- **实验覆盖不明**：数据集、领域数量、任务难度、黑盒系统类型均未提供，无法判断泛化能力。
- **基线与公平性不足**：摘要仅明确对比 unpruned search，缺少与模型蒸馏、行为克隆、人工设计、其他工作流搜索方法的系统比较。
- **资源与复现信息不足**：未报告算力、随机种子、重复次数、显著性检验和代码可用性，复现成本与稳定性未知。
- **潜在滥用风险**：逆向重建黑盒智能体工作流可能被用于模仿、规避控制或侵犯系统知识产权，论文是否讨论伦理与安全约束未在现有材料中体现。

（完）
