---
title: "OPT-BENCH: Evaluating the Iterative Self-Optimization of LLM Agents in Large-Scale Search Spaces"
title_zh: OPT-BENCH：评估大模型智能体在大规模搜索空间中的迭代自优化
authors: "Xiaozhe Li, Jixuan Chen, Xinyu Fang, Shengyuan Ding, Haodong Duan, Qingwen Liu, Kai Chen"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1417.pdf"
tags: ["query:llm-agent-or"]
score: 4.0
evidence: 评估大模型智能体在大规模搜索空间的自优化
tldr: 大模型虽具备推理与工具使用能力，但其能否依据动态环境反馈持续改进解仍缺乏研究。本文提出OPT-BENCH基准，结合20个机器学习任务评估智能体在大规模搜索空间中的迭代自优化能力，考察感知、推理与记忆等认知要素。该工作为衡量智能体的自优化能力提供了标准化测试平台。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1672, \"height\": 630, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1644, \"height\": 1155, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1577, \"height\": 1023, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1569, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1671, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 786, \"height\": 978, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1417/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1514, \"height\": 1005, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1638, \"height\": 1055, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1635, \"height\": 995, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1643, \"height\": 264, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1640, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1645, \"height\": 272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1633, \"height\": 726, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1638, \"height\": 369, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1417/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1644, \"height\": 237, \"label\": \"Table\"}]"
motivation: 大模型智能体能否在动态反馈下持续改进解尚不清楚，缺乏相应评测基准。
method: 提出OPT-BENCH基准，结合20个机器学习任务评估智能体在大规模搜索空间中的迭代自优化能力。
result: 该基准从感知、推理与记忆角度揭示了智能体在自优化任务中的表现与局限。
conclusion: 为评估大模型智能体的持续自优化能力提供了标准化平台。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable capabilities in reasoning and tool use. However, the fundamental cognitive faculties essential for problem-solving—perception, reasoning, and memory—remain the stable core of intelligence. Unlike memorizing specific patterns, humans succeed in novel environments by applying these intrinsic faculties to adapt and optimize. Yet, whether LLMs possess this essential capacity—namely, the ability to continuously refine solutions in response to dynamic environmental feedback—remains underexplored. To address this challenge, we introduce OPT-BENCH , a benchmark for evaluating self-improvement capabilities in large-scale search spaces. By combining 20 machine learning tasks with 10 classic NP-hard problems, OPT-BENCH provides a rigorous setting to assess whether agents can adapt through intrinsic self-reflection rather than rote tool application. We further propose OPT-Agent , a framework that emulates human-like cognitive adaptation. It operates via a general perception–memory–reasoning loop, iteratively refining solutions based on environmental feedback. Through extensive experiments on 19 LLMs from 7 model families, including reasoning models, general models, and open-source models ranging from 3B to 235B parameters, we demonstrate stronger models are more effective at leveraging feedback signals for self-improvement. However, this upper-bound adaptability remains fundamentally constrained by the models’ base capacity, and even the most advanced LLMs still fall short of human expert performance.

---

## 论文详细总结（自动生成）

# OPT-BENCH 论文结构化总结

## 1. 核心问题与整体含义（研究动机与背景）

- **研究动机**：LLM 在推理与工具使用上表现优异，但智能的核心并非"记忆特定模式"，而是**感知（perception）、推理（reasoning）、记忆（memory）**这三项稳定认知能力，使人类能在新环境中适应与优化。作者追问：LLM 是否具备**迭代自优化（iterative self-optimization）**能力，即依据动态环境反馈持续改进解？
- **现有空白**：主流基准（MMLU、BIG-bench、MATH、GSM8K、HumanEval、NP-HardEval 等）多为**一次性、开环（one-shot, open-loop）**评测，只考察单次生成正确性，忽视"从经验中学习"的过程；即便有 CoT，也仅评估瞬时推理而非自适应学习。
- **Agent 类基准**（AgentBench、WebShop、WebArena、MLE-Bench）侧重"能否完成任务/跑通代码"，而非"能否随时间优化指标"。
- **整体含义**：作者提出 **OPT-BENCH**，把评测焦点从"agent 能否运行代码"转向"agent 能否演化解（evolve the solution）"，为衡量 LLM 自优化能力提供标准化平台。

## 2. 方法论

### 2.1 OPT-BENCH 基准设计
- 共 **30 个任务**，刻意并列两种反馈景观：
  - **20 个真实机器学习任务**（来自 Kaggle）：连续参数优化空间，反馈是"噪声但有方向"的梯度（如验证精度）。
  - **10 个经典 NP-hard 问题**（图着色、哈密顿回路、背包、最大团、集合覆盖、TSP 等）：离散组合空间，约束脆弱、易陷局部最优。
- 每个样本包含：任务描述、数据规格（CSV/JSON）、提交格式、**初始解（Cold Start，功能可用但次优）**、环境反馈机制、人类/专家基线。
- **人类专家基线**：ML 用 Kaggle 金牌解；NP 用启发式算法（如模拟退火）作为"推理上限"代理。
- ML 初始解由 AIDE 生成并经 4 名博士级专家精修；NP 有效性由 `validation.py` 规则脚本强制（二元 Valid/Invalid + 具体错误信息）。

### 2.2 OPT-Agent 工作流（核心思想）
- 受 AlphaEvolve 与认知 CoT 启发，实现**感知–记忆–推理循环**，不依赖复杂 prompt 工程，包含三种动作：
  - **Drafting（初始化）**：生成初始假设——ML 合成 Python 训练脚本；NP 直接用演绎推理构造离散结构（强制依赖内部规划而非代码解释器）。
  - **Improving（精化）**：有效解出现时触发，检索历史上下文（历史代码/路径、指标、反馈趋势），ML 用归纳推理调超参/架构，NP 尝试在保约束下精化解结构。
  - **Debugging（纠错）**：环境返回失败信号（运行错误/约束违反）时触发，分析错误日志诊断并修复，考察自纠错能力。

### 2.3 评价指标（公式以文字说明）
- **Win Count（反馈效用）**：OPT-Agent 优于 Random Rollout（无记忆盲测基线）的任务数，衡量是否真正在学习。
- **Improvement Rate (IR)**：`IR(α,β) = (1/n) Σ αi/βi`，α 为优化后指标、β 为基线值（初始解或无记忆生成）；IR>1.0 表示有效利用反馈。
- **Expert Gap (EG)**：为消除 30 个任务量纲差异，用相对归一化 `Score_norm = (M_current − M_initial) / (M_expert − M_initial)`，衡量自优化填补初始解与专家解之间差距的程度。
- **Buggy Rate**：无效解（语法错误/约束违反）比例，下降说明 agent 在学会满足结构约束。

## 3. 实验设计

- **Benchmark**：OPT-BENCH（20 ML + 10 NP，共 30 环境）。
- **被测模型**：**19 个 LLM，7 个模型家族**，参数 3B–235B，含：
  - 专有模型：gpt-4o-2024-08-06、gpt-4.1、gpt-o3-mini、gemini-2.0-flash、claude-3-5-sonnet、claude-3-7-sonnet、grok-3、Deepseek-V3.1-Thinking、Qwen3-235B-Thinking/Instruct。
  - 开源模型：InternLM3-8B、Qwen2.5-3B/7B/14B/32B/72B-Instruct、Qwen3-8B/30B-A3B/32B。
- **对比基线**：
  - **下界 Random Rollout**（无历史上下文的无记忆生成）。
  - **上界 Human Expert**（Kaggle 金牌解 / NP 启发式最优）。
- **实验维度**：
  - 优化步数：**5 / 10 / 20 步**（ML 表1、NP 表2）。
  - **温度消融**：T = 0 / 0.2 / 0.8（ML 表3、NP 表4）。
  - **Draft vs Refine 设置消融**（附录表5）：从零生成 vs 基于历史精化。
- **环境**：ML 用标准 CPU（4 核 32GB RAM）；NP 用 2 核 16GB RAM；专有模型走 API，开源模型（3B–72B）走 LMDeploy 部署。

## 4. 资源与算力

- **文中未明确说明训练算力**（无 GPU 型号、数量、训练时长）。这符合作者定位——OPT-Agent 是**推理时（inference-time）评测框架**，不涉及模型训练。
- 仅提及评测运行环境：ML 任务 4 核 CPU / 32GB RAM，NP 任务 2 核 CPU / 16GB RAM；专有模型通过 API 访问，开源模型通过 LMDeploy 部署。**具体的 GPU 部署规模、并发数、总推理耗时均未报告**。

## 5. 实验数量与充分性

- **实验组数（粗估）**：
  - 主实验 2 大表（ML 表1、NP 表2）× 19 模型 × 3 个步数档 = 大量组合。
  - 温度消融 2 表（各 3 个代表模型 × 3 温度）。
  - Draft/Refine 消融 1 表（3 模型 × 3 步数）。
  - 另有优化轨迹可视化案例（ML 自行车需求、NP 哈密顿回路）。
- **充分性评价**：
  - **优点**：覆盖模型数量多、规模跨度大（3B–235B）、家族多样，含推理模型与通用模型对比；步数 + 温度 + Draft/Refine 多维度消融，主结论有交叉验证支撑。
  - **不足**：
    - 每类任务仅 **30 个环境**，样本量偏小，作者在 Limitations 中亦承认。
    - 温度消融仅选 3 个代表模型，代表性有限。
    - **公平性/客观性**：指标设计（归一化 EG、IR）考虑了量纲差异，基线（无记忆盲测 + 专家上界）设置合理，整体较客观；但人类专家基线在 NP 上用启发式算法近似，与真实人类专家推理存在偏差。

## 6. 主要结论与发现

- **连续 ML 域：强模型有效充当"归纳优化器"**。gpt-4o 在 20 步达 18/2 Win Count；gpt-4.1 的 IR 达 2.15，说明性能提升来自历史驱动的定向精化而非随机波动。
- **自优化的"规模定律"**：模型越大越能利用历史反馈（Qwen2.5-72B EG 0.45 vs 7B 0.20），存在**认知阈值**——小模型把复杂错误轨迹当噪声，大模型涌现多步归纳能力。
- **推理模型 > 通用模型**：推理模型（如 gpt-o3-mini 达最高 ML EG 0.65；Deepseek-V3.1-Thinking 在 NP 达 0.00 Buggy Rate 与最高 EG≈0.79），CoT 对细粒度优化与全局拓扑一致性至关重要。
- **离散 NP 域：反馈效率悖论**。Win Count 更均衡（gpt-4o 仅 4/6），离散错误信号（如"Invalid Cycle"）缺乏方向梯度，自优化退化为"带记忆的随机搜索"；小模型遭遇**可行性瓶颈**（Buggy Rate ~0.80），无法建立有效基线。
- **关键认知分歧**：ML 中 LLM 能单调改进；NP 中反馈常触发**剧烈跳变**——模型倾向丢弃整个历史重新生成，而非像人类那样局部修补（如修一条断边）。
- **温度效应**：连续域 T=0 最优（严格利用反馈）；离散域 T=0.2 常降低 Buggy Rate（适度探索跳出局部陷阱），T=0.8 破坏逻辑一致性。
- **人类差距**：即便最强 LLM 也难达人类专家上界，当前"自优化"本质是**受模型固有推理深度约束的局部搜索机制**。

## 7. 优点

- **问题定位新颖**：从"能否完成任务"转向"能否演化解"，直击 LLM 自适应学习这一未被充分探索的认知能力。
- **基准设计精巧**：连续（ML）+ 离散（NP）双景观并列，构成对归纳/演绎两种推理模式的交叉检验，避免单一任务偏差。
- **框架简洁且认知合理**：OPT-Agent 的 perception–memory–reasoning 循环不依赖繁复 prompt 工程，能干净地隔离"是否真正利用反馈"这一变量。
- **指标体系严谨**：引入归一化 Expert Gap 解决跨 30 个异质任务的量纲问题，IR 与 Win Count 分别刻画学习效率与反馈效用，指标互补。
- **实验覆盖广**：19 模型 / 7 家族 / 3B–235B，含专有与开源、推理与通用模型，结论具较强泛化说服力。
- **诊断性分析深入**：通过优化轨迹可视化揭示"ML 单调改进 vs NP 跳变重置"的行为差异，解释性强。

## 8. 不足与局限

- **环境规模有限**：仅 30 个任务，作者自述未来需扩展至更大更多样的环境集以提升鲁棒性。
- **模型覆盖缺口**：因资源限制未纳入 Gemini 3、GPT-5.2、Claude 4.5 等最新 SOTA，结论的时效性可能受限。
- **人类基线代理化**：NP 任务用启发式算法代替真实人类专家，可能低估或扭曲真实人类推理上限，影响 EG 的解释力。
- **算力与效率信息缺失**：未报告推理成本、GPU 部署细节、总耗时，难以评估方法的实际部署可行性与经济性。
- **指标潜在偏差**：IR 依赖基线选择（初始解或无记忆生成），不同基线会显著改变结论；NP 域部分任务 Win Count 接近随机，统计显著性未做检验。
- **训练/推理对齐限制**：作者推测推理模型在 NP 域改进有限，可能受 RL 对齐约束抑制长程探索，但未做深入验证。
- **应用限制**：OPT-Agent 本质是局部搜索机制，难以处理需要全局规划与高层推理的复杂组合优化，距离真正的自主优化尚有差距。

（完）
