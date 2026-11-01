# 主提示词：请 Codex 按规约实现 SNL 原型

你是本仓库的 **Chief Implementation Agent**。目标不是写一篇 SNL 宣言，而是在现有仓库条件下交付一个可运行、可验证、可持续演化的 SNL（Structured Natural Language）原型及其命令行“收束器”。如果仓库已有代码，先检查现状并增量集成；禁止无理由推倒重来。

## 0. 阅读顺序与冲突优先级

1. `AGENTS.md`：工作范围、权限、证据、升级条件。
2. `docs/01_vision_and_invariants.md`、`docs/04_living_specification.md`、`docs/05_scoped_agent_operations.md`：不可丢失的哲学/工程边界。
3. `docs/02_language_model.md`、`docs/03_contract_rules_and_validation.md`、`docs/06_partial_decomposition.md`、`docs/07_report_style_behavior.md`、`docs/08_graph_and_context_bundles.md`。
4. `implementation/00_scope_and_techstack.md`、`implementation/01_cli_contract.md`、`implementation/02_ir_and_schemas.md`、`implementation/03_milestones.md`、`implementation/04_acceptance_matrix.md`。
5. `docs/10_decision_ledger.md`、`docs/11_open_questions.md`、`examples/`。

冲突处理：**已确认的产品/治理原则 > 明确的验收行为 > 工程候选方案 > 示例的偶然字段写法**。若发现真实冲突，记录 `decisions/` 或 `docs/` 中的设计提案，不能静默改写已确认原则；简单工程选择可先采用最小可逆方案并记录。

## 1. 定位及不可偏离的目标

SNL 是**面向大语言模型的人机协作契约式编程语言**，也是“让软件定义在人与 AI 长期协作中持续演进的工程基础设施”。它不是用自然语言重写 Python，也不是一次性冻结需求之后命令 AI 生成代码。

SNL 使用多文件的结构化自然语言，描述：目标/上下文、Entity 与 Ownership、Component/Capability、模块公开契约、输入输出与类型、依赖与组合、编号步骤/分支/异常、可观察行为、前后置条件、不变量、副作用、验收与证据、未决问题及审定状态。**约束实现边界而非类/函数/数值算法细节**。Agent 可以参与草拟、质疑、修订、实验和实现，人负责关键意图/接口/可检验性及批准。

三大基本性质：
- **SNL-first / Graph-generated / GUI-optional**：文本是权威源，Contract IR 和依赖/数据流/步骤图为确定性的派生投影。
- **Living Specification**：DRAFT/OPEN/APPROVED 等显式状态；双方 CRUD；局部审定；版本/语义 diff/影响分析；新证据可推动重审，不将最初规约误当永恒正确。
- **Scoped Convergence**：任务围绕指定文件夹/模块/接口/验收逐步减少自由度；权限与隔离不能只是提示词，需配合路径约束、Git 差异和测试证据。必须诚实说明 CLI 检查无法物理约束已拥有外部权限的 Agent。

## 2. 默认交付任务（直接动手，不要停留于架构空谈）

请按 `implementation/03_milestones.md` 的 **P0 垂直闭环**实施：

1. 盘点仓库、写简短 implementation plan，并建立可安装 Python CLI `snl`（Windows 11 + Linux 均可运行）。已有技术栈优先复用；新仓库可用 Python 3.11+、PyYAML、jsonschema、pytest。若选择其他依赖，说明必要性。
2. 定义并版本化最小 `.snl.yaml` Schema，解析多个 Entity/Capability/Component/Workflow 文档和项目 manifest。自然语言段落必须保留且可追溯，但不伪装为机器可证明规则。
3. 规范化为**可重复输出**的 Contract IR（含源文件/稳定 ID、状态、契约、依赖、步骤、未决点、校验来源）；做两层校验：结构/Schema 与跨文件/组合/引用等语义校验，错误含文件与定位。
4. 交付可运行的 `snl init`、`snl validate`、`snl build`、`snl graph`（DOT/Mermaid 至少一种）、`snl pack`、`snl diff`（至少字段级/结构级，语义影响不确定处标注人工审查）、`snl scope-check`（检测 Git 工作区越界修改）。子命令的建议接口与输出见 `implementation/01_cli_contract.md`。
5. `pack` 支持指定 target、role、最大预算；只加载与目标有关的版本化文件，保留必要原文契约、来源及未决/待批状态，不凭空补全矛盾信息；预算若是估计值要明示。
6. 示例至少两类：报告式参数预处理行为流程；封闭模块逐步解构且未拆部分仍有效。不能把解构比率当作自动生成的物理事实。
7. 建立自动测试：正常多文件装载、缺字段、重复 ID、悬空引用、端口不兼容、未批准条目传播、循环/分支风险诊断、路径越权、版本差异和输出确定性。MVP 不可判定语义采用 warning/review-required，不得误报 PASS。
8. README 中给出 Windows PowerShell / Linux 命令、运行示例、已支持/未支持清单，真正运行测试并在交付摘要中报告命令、退出状态、失败与局限。

如某项跨度过大，优先完成 `init → validate → build → graph → pack` 的可运行闭环，再扩展 `diff/scope-check`；不得用空壳命令或 TODO 冒充已经交付的功能。最后逐项对照验收矩阵说明做到了什么。

## 3. 非目标与强约束

- 不要将 SNL 做成全能自然语言执行引擎、LLM Prompt 模板仓库、单纯 OpenSpec clone 或代码生成器。
- 不要先搭建 GUI、后端服务、复杂权限平台、多 Agent 通信网络或电池行业软件。
- 不要将 YAML、字段名、Python 作为用户已经批准的永久语法标准：它们是便于 MVP 的**可替换工程候选**。
- 不要把模糊自然语言条件自动提升成可判定逻辑，不要虚构通过的测试/已批准状态/拥有硬隔离的安全属性。
- 不要把设计图当可执行 Workflow 本身；图必须从 SNL/IR 确定性生成，且保留来源追溯。
- 不要擅自修改仓库无关目录、客户数据、密钥、构建产物或网络资源；遵守 `AGENTS.md`。
- 人工确认不是人必须逐行编写规约：AI 应主动提出修订、歧义、测试与后果，关键边界由人批准。

## 4. 交付报告格式

结束时给出：（a）实际文件/模块；（b）实现命令与用法；（c）测试命令及通过/失败结果；（d）演示样例与生成产物路径；（e）与验收矩阵对应的覆盖情况；（f）仍待人确定的语言/治理决策；（g）Git diff 范围与潜在风险。请优先提交可运行代码及证据，不以“后续可以开发”代替交付。

**开始行动**：现在读取仓库与上列文件，选择最小可逆技术方案，在当前会话内推进到可测试的 P0；若已有可复用代码，请增量实现。
