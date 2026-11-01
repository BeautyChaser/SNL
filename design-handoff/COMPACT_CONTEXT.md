# SNL 压缩上下文（适合新 Codex 会话）

**定义**：SNL (Structured Natural Language) 是面向大语言模型、由人和 AI 协作维护的**契约式编程语言**与**持续演进的软件定义基础设施**。不是自然语言取代底层代码，不是“先冻结需求→AI 自动生成”的单向过程。它通过契约、版本、权限、验证证据把发散探索逐步收束为可审核、可复现的软件行为。

**权威链条**：多文件 SNL 规范文本（source of truth）→ 结构/语义验证 → Contract IR → 衍生依赖图/组合图/行为步骤图 → 目标 Agent 上下文包 → Agent 局部实现/测试 → 证据与反馈回写 SNL。GUI 可选。Git 管版本，知识库/RAG 提供可引用的外部知识，但不取代有审定状态的 SNL 定义。

**对象模型**：Entity/Ownership（身份、状态、生命周期、写权限）+ Capability（公开可观察能力、I/O、异常、副作用、契约）+ Component（组合与封装）+ Workflow（顺序/分支/循环/异常/数据流）+ Dependency/Composition + Acceptance/Evidence。*代码实现*保持黑箱；*契约*白箱；*行为*可观察；*验证*可追溯。架构图由文本投影，非独立手工权威。

**Living Specification**：人和 AI 均可 CRUD、讨论、实验；状态含 OPEN/DRAFT/APPROVED（具体枚举待规范化），支持局部审定、Proposal/Delta、版本/语义 diff、影响分析、撤回及复核。未审定不能自动替代生效契约；AI 不能自称拥有业务批准权。初始规约可以不完整甚至错误。

**Scoped Convergence**：每轮围绕指定目录、模块、约束、I/O、验收推进；AI 负责尽可能多的规约起草、维护、测试推导，人确认关键意图、接口和可检测性。路径白名单、Git diff、权限与隔离工作区共同治理；单一 CLI 无法保证 Agent 绝不越权。

**行为写法**：像多文件结构化演讲稿/报告，先说明目标受众/Agent/上下文，再用稳定 ID 逐条表达步骤、条件分支、合流、循环退出、异常和验收。对不确定性做显式标记，禁止模糊判断冒充机器真值；维护“步骤 ↔ 代码 ↔ 测试”映射。

**可持续解构**：一个原始封闭 Workflow/Component 可逐渐拆成 Capability/子 Workflow/实现单元，未拆部分仍保持 opaque 并可运行；人只治理到实现单元边界，不需介入每个类或函数。黑箱与新能力通过契约/适配器并存。

**CLI 目标**：开源、跨平台、独立于模型与 GUI 的 `snl`/`snl.exe`，核心 `init / validate / build(IR) / graph / pack / verify`，并逐步支持 `diff / scope-check / approve/impact`。MVP 选 YAML 1.2 兼容的 `.snl.yaml` + Schema/semantic validators 是**候选实施方案**，不是被宣布唯一语法；任何未被证明的自然语言约束必须标注人工审查或测试验证。

**行业适配**：先做领域无关 CLI，以参数准备+电池工作流/渐进解构为案例；不是直接开发 PyBaMM/MOOSE 求解器。先交付一条可运行的最小闭环，自动化测试为准，保留开放问题并让软件定义继续生长。
