---
title: "OPT-BENCH: Evaluating LLM Agent on Large-Scale Search Spaces Optimization Problems"
title_zh: OPT-BENCH：评估LLM智能体在大规模搜索空间优化问题上的能力
authors: "Xiaozhe Li, Jixuan Chen, Xinyu Fang, Shengyuan Ding, Haodong Duan, Qingwen Liu, Kai Chen"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=FYke66uUU1"
tags: ["query:llm-agent-or"]
score: 8.0
evidence: 面向LLM智能体大规模搜索空间与NP优化问题评测的基准与端到端框架
tldr: LLM智能体能否在超大搜索空间中通过迭代反馈优化复杂解仍待系统检验。OPT-BENCH汇集20个Kaggle机器学习任务与10个经典NP问题，并提出OPT-Agent端到端框架，模拟人类推理持续生成和改进解。该基准系统评测了LLM的迭代优化能力，揭示了其在复杂优化问题上的潜能与不足，为智能体优化研究提供标准测试环境。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM智能体在超大搜索空间上的迭代优化能力缺少系统性基准，现有任务覆盖不足。
method: 集成ML与NP优化任务构建OPT-BENCH，并设计OPT-Agent框架以反馈驱动方式迭代生成与精化解。
result: 通过大规模评测展示了LLM智能体在多种优化问题上的表现与局限。
conclusion: 为评估LLM智能体的黑盒优化能力提供公开基准与可参照的端到端框架。
---

## Abstract
Large Language Models (LLMs) have demonstrated impressive capabilities in solving a wide range of tasks. However, their ability to iteratively optimize complex solutions by learning from previous feedback remains underexplored. To address this gap, we introduce \textbf{OPT-BENCH}, a comprehensive benchmark designed to evaluate LLM agents on large-scale search space optimization problems. OPT-BENCH includes 20 real-world machine learning tasks sourced from Kaggle and 10 classical NP problems, providing a diverse and challenging environment for assessing LLMs on iterative reasoning and solution refinement.
To facilitate rigorous evaluation, we present \textbf{OPT-Agent}, an end-to-end optimization framework that emulates human reasoning by generating, validating, and iteratively improving solutions through the use of historical feedback. Through extensive experiments involving 17 state-of-the-art LLMs from 7 model families, including reasoning models, general models, and open-source models ranging from 3B to 72B parameters, we demonstrate that incorporating historical context significantly enhances optimization performance across both ML and NP tasks. However, this benefit remains limited, as even with the latest models, a gap still persists compared to human expert performance.
All datasets, code, and evaluation tools will be open-sourced to foster further research in advancing LLM-driven optimization and iterative reasoning.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

大型语言模型（LLM）已在各类自然语言与推理任务上展现出强大能力，但其**在超大搜索空间中进行迭代优化**的能力——即根据历史反馈不断改进复杂解——尚未被系统性研究。现有评测多聚焦一次性回答或简单推理，缺少对"智能体能否像人类一样，在多次尝试中通过试错逐步逼近更优解"的标准化测试环境。

为此，论文提出 **OPT-BENCH**：一个专为评估 LLM 智能体在大规模搜索空间优化问题上的迭代推理与解精细化能力而设计的综合性基准，旨在填补该方向上的评测空白。

---

## 2. 方法论

论文提出 **OPT-Agent**，一个端到端优化框架，模拟人类推理的"生成—验证—迭代改进"循环。

**核心思想：**
- 将优化过程建模为历史反馈驱动的迭代流程；
- 智能体不仅依赖当前解，还显式利用过去尝试中的反馈信息（如验证结果、错误模式、指标变化）来指导后续解的生成；
- 模拟人类专家在黑盒优化场景中的工作方式，不依赖梯度或领域内部结构。

**算法流程（文字描述）：**
1. 初始解生成：LLM 根据任务描述与目标函数生成一个候选解；
2. 验证与评分：由环境/评测器对解进行客观打分（如 Kaggle 任务中的指标，NP 问题中的约束满足度或目标值）；
3. 反馈构建：将历史解、得分、失败信息等组织为结构化上下文；
4. 迭代改进：LLM 读取包含历史反馈的上下文，生成新的候选解；
5. 循环执行第 2–4 步，直至达到预算上限（迭代次数/时间）或收敛。

该框架可作为通用评测协议，兼容不同 LLM 后端，无需针对特定模型调整。

---

## 3. 实验设计

**Benchmark 组成：**
- **20 个真实世界机器学习任务**：均来自 Kaggle 竞赛，覆盖分类、回归等场景，涉及大规模特征/超参数搜索空间；
- **10 个经典 NP 问题**：包括如旅行商、图着色、约束满足等经典组合优化问题。

上述任务共同构成 OPT-BENCH，为评测 LLM 智能体提供了多样化且具有挑战性的环境。

**评测的模型：**
- 共 **17 个先进 LLM**，来自 **7 个模型家族**；
- 覆盖**推理模型**、**通用模型**和**开源模型**；
- 模型规模跨度从 **3B 到 72B 参数**。

**对比方式：**
- 主要对比指标为各模型在 OPT-BENCH 上的优化性能；
- 考察有无历史反馈上下文对优化效果的影响；
- 与人类专家表现进行对比作为上限参照。

---

## 4. 资源与算力

论文文本中**未明确说明**所使用的 GPU 型号、数量、训练/推理时长或总计算量等具体算力资源信息。因此无法评估其资源消耗层面上的成本与可行性。若需要该信息，需查阅论文完整版本或附录。

---

## 5. 实验数量与充分性

**实验规模：**
- 30 个优化任务（20 ML + 10 NP）；
- 17 个不同 LLM；
- 覆盖推理型、通用型与开源型模型，规模从 3B 至 72B；
- 关键实验变量为是否注入历史反馈上下文（即验证 OPT-Agent 设计的核心假设）。

**充分性与客观性评估：**
- **积极方面**：任务多样性高（ML 现实数据 + NP 经典问题）、模型覆盖面广、参数区间宽，保证了结论具有一定的泛化性；
- **公平性**：采用统一评测框架，各模型在同一协议下运行，有利于横向比较；NP 问题有客观最优性度量，ML 任务有标准竞赛指标，评估相对客观；
- **不足方面**：文本摘要中未显示消融实验（如迭代次数的影响、反馈类型的影响、不同的上下文组织方式等），也未报告不同初始化的敏感性、单次运行随机性下的方差控制手段。因此，实验"是否充分"在完整论文层面可能更强，但就摘要层面而言存在信息缺口，尤其是缺乏人类专家对比的详细数值和统计显著性分析。

---

## 6. 主要结论与发现

1. **历史反馈显著提升优化性能**：在 ML 与 NP 两类任务上，加入历史上下文均一致性地改善了 LLM 智能体的优化效果。
2. **该提升存在上限**：即使使用最新的强模型，其优化能力与人类专家之间仍有明显差距，说明 LLM 驱动的迭代优化尚未成熟。
3. **OPT-BENCH 可作为标准评测工具**：能有效区分不同 LLM 在迭代优化上的能力差异，为后续研究提供参照。
4. 开源数据集、代码与评测工具，以推动 LLM 驱动的优化与迭代推理研究。

---

## 7. 优点

- **填补基准空白**：首次系统性地将 Kaggle 真实 ML 任务与 NP 经典问题统一纳入 LLM 迭代优化测评，贴近实际应用需求。
- **端到端评估协议**：OPT-Agent 提供统一的标准化流程，降低评测中的实现偏差，提高可比性。
- **模型覆盖广**：同时涵盖推理模型、通用模型与开源模型（3B–72B），可揭示不同架构/训练策略下的能力差异。
- **强调迭代而非单步推理**：抓住 LLM 智能体在真实应用中"多轮改进"这一核心场景，评测维度更具生态效度。
- **结果透明度高**：与人类专家的差距被明确报告，为领域发展设定量化追赶目标。

---

## 8. 不足与局限

- **算力细节缺失**：未报告运行所需的 GPU 时间与资源，使复现成本难以预估。
- **实验描述有限**：摘要层面未见消融、不同反馈策略对比、错误分析与迭代预算敏感性分析，正文可能是评判完整性的关键。
- **人类专家对比方式不明**：如何定义和获取"人类专家表现"（例如是 Kaggle 获奖提交还是人工调优的基线）可能影响比较公平性。
- **黑盒优化的固有局限**：LLM 在搜索空间极大且性能面崎岖的问题上可能陷入局部最优，基准未提及如何缓解或度量这类问题。
- **任务代表性受限**：尽管涵盖 ML 与 NP 任务，但尚未覆盖连续控制、设计优化、科学发现等其他重要优化场景；Kaggle 任务也偏重表格型和超参数学习，可能存在数据偏差。
- **成本可扩展性问题**：迭代过程中多次 LLM 调用引入高推理延迟与费用，对于 72B 等大模型的端到端实用性可能构成瓶颈，论文摘要未讨论这一现实约束。

---

（完）
