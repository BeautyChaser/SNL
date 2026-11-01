# 单条可复制给 Codex 的综合 Prompt（无文件读取能力时也能用）

我要实现一个开源、模型/GUI 无关的 CLI 工具 `snl`（Windows 未来打包为 `snl.exe`），其核心设计为：

**SNL = Structured Natural Language = 面向大语言模型的人机协作契约式编程语言。** 它不是自然语言代替具体编程语言，也不是最初需求冻结后让 AI 机械执行。它是一套让人与 AI 在长期共同探索、批判、实验、实现、验证和反馈中逐步形成更正确的软件定义的基础设施（Living Specification）。人和 AI 都可增删改查、提案和修订 SNL；AI 负责起草复杂规约与实现/测试，人重点确认意图、输入输出、可检验性和重大变更。

**SNL-first, Graph-generated, GUI-optional**：多文件 SNL 文本是权威源；`validate/build → Contract IR → graph/pack/verify` 为派生产物，不能另造一套图形权威。SNL 应表达目标、Entity 与 Ownership、Capability/Component、Composition/Dependency、Workflow 步骤/分支/循环/异常、公开 I/O、前/后置条件、不变量、错误、副作用、验收/证据、问题状态、版本与审定范围；底层内部类、私有方法与算法实现由 AI 自由决定。契约白箱、实现黑箱、行为可观测、验证可追溯。

**活规约**：OPEN/DRAFT/APPROVED（具体命名可调整），不同条款允许局部审定；未审定修订不能自动覆盖有效基线；支持人机共同修改、change proposal、delta、结构/语义 diff、影响分析、证据、回滚；自然语言条件不可普遍机器证明，应标 REVIEW_REQUIRED。初始规约不保证正确。

**阶段性局部收束**：每次开发限定目标模块/文件夹、允许读写路径、非目标、输入输出和验收/停止条件，以测试/证据和 Git diff 收束随机性。Scope 检测并不等同 OS 沙箱，需要可信工作区/工具权限真正硬隔离。人负责关键判断，而不是亲手写每行规约。

**部分解构**：一个原始封闭 Workflow/Component 可以逐步提取 Capability/子 Workflow/实现单元；未拆部分长期 opaque，但整体仍可运行并被验证。人只治理实现单元边界，不必规范具体代码。采用报告式结构化自然语言/“面向 Agent 的多文件演讲稿”思想，用稳定步骤 ID 表示顺序、条件分支、合流、循环退出、异常，形成“规约步骤 ↔ 源码 ↔ 测试”映射，按 Agent 角色与上下文预算装配包。

**请直接实现 MVP**，而非停在架构设计：

1. 先检查当前仓库并保留已有代码。新仓库默认 Python 3.11+、`.snl.yaml`/YAML 安全子集、JSON Schema/语义检查（这些是候选实施方案，不是永久标准）。
2. 建立多文件定义与项目 manifest，支持 Entity/Capability/Component/Workflow 的最小语义与稳定 ID、source hash、状态、I/O、依赖、行为、验收。不要把无从判断的自然语言当成已验证机器逻辑。
3. 实现真实 `snl init/validate/build(IR)/graph(Mermaid 或 DOT)/pack(target,role,budget)/diff/scope-check` CLI。`verify/approve/impact` 可后续强化，但必须有真实诊断、规范化 JSON 输出、非零失败退出码，不能是永远成功的空壳命令。
4. `pack` 可依目标 Agent（Implementer/Tester/Architect）选择相关内容，保留关键精确条款、未决问题、来源与审定状态，预算不足不静默删除核心契约。
5. 用参数预处理（原始配置、补全规则、范围/一致性校验、来源追踪、缺失处理）和局部解构（旧黑箱 + 新提取 Capability）示范；工具保持领域无关。
6. 写 pytest/CLI E2E 正反测试：重复 ID、悬空引用、类型/端口不匹配、危险 YAML、分支风险、未审定内容误传播、确定性 IR、超预算告警、Git 越界修改、路径逃逸、跨 Windows/Linux 中文路径。
7. 输出真实代码、README/PowerShell 示例、运行后的测试结果、缺陷/未实现表、提议的下一阶段工作。对没有证据的安全、语义等价、业务验收和审批身份，明确说不支持或需人工复核。

请以一个可运行、可验证、能继续迭代的人机协作收束器原型作为第一阶段成果。若某个细节无定案，选择最小可逆实现并记录 proposal，不要擅自固化或扩大权限。
