---
title: "OptiVerse: A Comprehensive Benchmark towards Optimization Problem Solving"
title_zh: OptiVerse：面向优化问题求解的综合基准
authors: "Xinyu Zhang, Boxuan Zhang, Yuchen Wan, Lingling Zhang, YiXing Yao, Bifan Wei, Yaqiang Wu, Jun Liu"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.150.pdf"
tags: ["query:llm-agent-or"]
score: 8.0
evidence: 面向大语言模型优化问题求解的综合基准，涵盖数学规划与组合优化
tldr: 现有针对大语言模型优化能力的评测多局限于数学规划与组合优化，覆盖面不足。本文提出OptiVerse基准，收录1000道覆盖随机优化、动态优化、博弈优化与最优控制等领域的题目，并划分三个难度等级。对22个大语言模型的实验显示，硬难度题目上性能急剧下降，即使先进模型也难以取得高分。该基准为评估与推动LLM在运筹优化问题求解上的能力提供了全面平台。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 293, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1618, \"height\": 904, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1597, \"height\": 554, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1620, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 806, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 808, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 806, \"height\": 540, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 803, \"height\": 280, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 804, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl150/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 805, \"height\": 466, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 772, \"height\": 109, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1623, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1660, \"height\": 676, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 756, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1657, \"height\": 1250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 792, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl150/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 739, \"height\": 343, \"label\": \"Table\"}]"
motivation: 现有LLM优化基准仅聚焦数学规划与组合优化，难以全面评估模型在复杂优化任务上的能力。
method: 作者构建包含1000道题目的OptiVerse基准，覆盖随机、动态、博弈优化与最优控制等被忽视领域，分三个难度等级。
result: 对22个大语言模型的评测显示，困难问题上性能急剧下降，先进模型也难以取得高分。
conclusion: OptiVerse为全面评测与推动大语言模型在运筹优化求解上的能力提供了标准化基准。
---

## Abstract
While Large Language Models (LLMs) demonstrate remarkable reasoning, complex optimization tasks remain challenging, requiring domain knowledge and robust implementation. However, existing benchmarks focus narrowly on Mathematical Programming and Combinatorial Optimization, hindering comprehensive evaluation. To address this, we introduce OptiVerse, a comprehensive benchmark of 1,000 curated problems spanning neglected domains, including Stochastic Optimization, Dynamic Optimization, Game Optimization, and Optimal Control, across three difficulty levels: Easy, Medium, and Hard. The experiments with 22 LLMs of different sizes reveal sharp performance degradation on hard problems, where even advanced models like GPT-5.2 and Gemini-3 struggle to exceed 27% accuracy. Through error analysis, we identify that modeling logic errors remain the primary bottleneck. Consequently, we propose a Dual-View Auditor Agent that improves the accuracy of the LLM modeling process without introducing significant time overhead. OptiVerse will serve as a foundational platform for advancing LLMs in solving complex optimization challenges.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：大语言模型（LLM）在推理、代码生成、数学推理等任务上表现突出，但复杂优化问题仍要求领域知识、数学建模能力和可执行求解实现。
- **现有基准的不足**：已有优化建模基准（如 NL4Opt、NLP4LP、OptiBench、OptMATH、MAMO、IndustryOR、CO-Bench 等）主要聚焦于**数学规划（MP）**和**组合优化（CO）**，系统性忽略了随机优化、动态优化、最优控制、博弈优化等重要领域。
- **论文目标**：提出 **OptiVerse**，一个覆盖六类优化领域、三个难度等级的综合性基准，用于系统评估 LLM 在优化问题求解中的能力边界。
- **整体含义**：论文不仅构建评测基准，还通过错误分析指出 LLM 失败的核心瓶颈是“建模与逻辑错误”，并提出 **Dual-View Auditor Agent（DVA-Agent）** 进行修复，推动 LLM 在运筹优化场景中的可靠应用。

## 2. 方法论

- **核心思想**：
  - 构建多领域、多难度、结构化文本输入的优化问题基准。
  - 采用“先数学建模、再生成代码、后沙盒执行”的求解范式。
  - 通过错误分析定位瓶颈，提出语义三角定位式审计代理，检测并修复“代码能运行但模型语义错误”的静默缺陷。

- **OptiVerse 构建流程**：
  - **Acquisition**：从权威教材、学术出版物、考研题、建模案例中收集问题，原始语料为 82 本书、26,702 页。
  - **Standardization**：使用 MinerU2.5 提取和结构化题目，保留表格、图形和文本描述。
  - **Translation and Verification**：由运筹学/应用数学方向博士生和硕士生审核、翻译并校验术语与数学符号。
  - **Quality Filtering**：排除可通过 5 分钟 Google 搜索直接获得答案的题目，降低数据污染。
  - **Classification**：按六领域和 Easy/Medium/Hard 三难度分类，最终保留 1,000 题。

- **六类优化领域**：
  - Mathematical Programming（MP）
  - Combinatorial Optimization（CO）
  - Stochastic Optimization（SO）
  - Dynamic Optimization（DO）
  - Optimal Control（OC）
  - Game Optimization（GO）

- **求解与评估流程**：
  - 模型接收问题 \(P\)，生成包含数学建模和可执行 Python 代码的响应 \(R = LLM(P)\)。
  - 抽取代码 \(C\)，在沙盒中执行，得到结果 \(O = Exec(C)\)。
  - 沙盒集成 `gurobi`、`casadi`、`pyomo`、`nashpy`、`scikit-opt`、`cvxpy`、`ortools`、`pulp`、`scipy` 等库。
  - 两阶段 LLM-as-judge：
    - 第一阶段：从执行输出中抽取答案 \(A = LLM_{extract}(O,R)=\{a_1,\dots,a_n\}\)。
    - 第二阶段：与标准答案 \(A^*\) 比较，允许相对误差 \(\epsilon=0.1\%\)。
    - 判定式：\(IsCorrect(A) \Leftrightarrow LLM_{judge}(A,A^*,\epsilon)\)。
    - 所有要求变量和目标准确才判为正确。

- **DVA-Agent 核心机制**：
  - **Requirement Extraction（Text-to-Math）**：从问题 \(P\) 和初始建模 \(M_{init}\) 中提取容易遗漏或误解的核心数学要求 \(R_{miss}\)。
  - **Blind Code Abstraction（Code-to-Math）**：不看原题，仅从代码反推其实际数学逻辑 \(M_{code}\)，减少确认偏差。
  - **Cross-Reference Analysis**：交叉比较原题、反推代码逻辑和缺失要求，生成差异集合 \(G\)。
  - **Refinement**：若 \(G=\emptyset\)，直接执行原代码；若 \(G\neq\emptyset\)，将差异作为修正指导，要求 LLM 修改建模逻辑和代码。
  - 该方法针对“代码成功执行但建模语义偏离问题意图”的静默语义错误。

## 3. 实验设计

- **基准**：OptiVerse，共 1,000 题。
  - 难度分布：Easy 300、Medium 400、Hard 300。
  - 领域分布：MP 36.7%、CO 23.8%、DO 14.6%、SO 12.0%、OC 7.8%、GO 5.1%。
  - 题目复杂度：平均问题 token 279.8，平均结果数 4.7；Hard 平均 369.3 token、6.83 个结果输出。
  - 对比现有基准：ComplexOR、NLP4LP、MAMO、IndustryOR、NL4OPT、OptiBench、OptMATH、CO-Bench 等。OptiVerse 的差异在于覆盖六领域、含表格/图、三难度、向量答案。

- **评估模型**：22 个 LLM，分为三类：
  - 开源非思考模型：Internlm3-8B、Mistral3-8B、Qwen3-8B/30B/235B-Instruct、Qwen3-Coder-30B、Qwen2.5-72B、DeepSeek-V3.2-Chat、Kimi-K2 等。
  - 开源思考模型：GPT-OSS-120B、Qwen3-8B/30B/235B-Thinking、DeepSeek-V3.2-Reasoner 等。
  - 闭源思考模型：Gemini-2.5-Flash/Pro、Gemini-3-Flash/Pro、Claude-4.5-Sonnet、o3、o4-mini、GPT-5.2 等。

- **推理配置**：
  - 采用 chain-of-thought 策略。
  - 强制“先数学建模，再生成代码”。
  - 代码抽取后在沙盒执行，输出最终结果。

- **评估设置**：
  - 使用 LLM-as-judge 两阶段评估。
  - 评估准确性测试使用 500 个样本。
  - 对比 Qwen3-235B-Instruct、Qwen3-235B-Thinking、DeepSeek-V3.2-Chat、DeepSeek-V3.2-Reasoner 后，选择 DeepSeek-V3.2-Chat 作为标准评估 LLM。

- **对比方法**：
  - DVA-Agent 与 Baseline、Chain of Experts（CoE）、OptiMUS 比较。
  - 使用 Qwen3-30B、Qwen3-235B、DeepSeek-V3.2 三类模型验证 DVA-Agent 的通用性和效率。

## 4. 资源与算力

- 论文**未明确报告训练算力**，包括 GPU 型号、数量、训练时长等。
- 该工作主要是**基准构建与推理评估**，不是模型训练研究。
- 文中提到：
  - 使用沙盒环境执行生成代码，集成多种优化求解库。
  - 使用 LLM-as-judge 进行答案抽取和验证。
  - 考虑成本与推理速度后，选择 DeepSeek-V3.2-Chat 作为标准评估 LLM。
- DVA-Agent 时间开销：
  - Qwen3-30B-Instruct：Baseline 6.1s，DVA-Agent 30.2s。
  - Qwen3-235B-Instruct：Baseline 11.8s，DVA-Agent 58.8s。
  - DeepSeek-V3.2-Chat：Baseline 15.7s，DVA-Agent 67.3s。
  - DVA-Agent 比 CoE、OptiMUS 更快，但仍显著高于原始 baseline。

## 5. 实验数量与充分性

- **主实验规模**：
  - 22 个 LLM 在 1,000 道题上评估。
  - 按 6 个领域和 3 个难度维度统计性能。
  - 可视为约 22,000 次问题求解推理。
- **错误分析实验**：
  - 对 9 个代表性模型进行人工错误类型标注。
  - 错误类型包括：建模与逻辑错误、参数与数据利用错误、可行性违反、最优性与数值错误、代码与语法错误。
- **DVA-Agent 实验**：
  - 3 个模型 × 3 个难度等级。
  - 对比 Baseline、CoE、OptiMUS。
  - 报告修改触发率：Qwen3-30B 为 23.6%，Qwen3-235B 为 32.3%，DeepSeek-V3.2-Chat 为 28.5%。
- **评估可靠性实验**：
  - 500 样本上比较 4 个 LLM 作为 judge 的评估准确率。
- **充分性判断**：
  - 覆盖模型数量多、领域广、难度分层清晰，实验规模较大。
  - 但未报告多次运行的方差、置信区间或统计显著性检验。
  - DVA-Agent 仅在 3 个模型上验证，未覆盖闭源模型。
  - 未与 ORLM、FOARL、SIRL 等微调方法进行
