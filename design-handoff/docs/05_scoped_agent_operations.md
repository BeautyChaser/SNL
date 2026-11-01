# 05 — 阶段性局部作用域与随机性向确定性收束

## 最新明确加入的设计要求（2026-11-01）

一个复杂项目不应让 Agent 每次面对无限制的代码空间和修改权限。SNL 的每轮推进要有**阶段性的局部作用域**：可将工作限制到特定模块目录/文件夹，再结合目的、输入输出、可观察行为、可检测性/验收以及可停止的条件，把大模型的候选随机性逐步收束为可审计的局部结果。

**范围是阶段性的、可变的**：某阶段只改 `src/parameter_preparation/`，另一阶段经过审定后可以扩大或切换；不得暗自全仓重构。

## Scope Protocol 建议字段（MVP 候选）

- `objective`：本轮具体目标；`non_goals`：明确不做的事。
- `allowed_read_paths`、`allowed_write_paths`、`denied_paths`：相对于 Git/工程根目录的路径边界。
- `target_ids`：所处理的 SNL 模块/契约/步骤 ID。
- `permissions`：例如可 READ/ANALYZE/PROPOSE/WRITE/BUILD/TEST；变更架构/部署需另授权。
- `input_contract_refs` / `output_contract_refs`：这轮约束绑定到的公开接口。
- `acceptance_refs`：验收条件的测试与证据关联。
- `stop_conditions` / `escalation_conditions`：何时停止或请人批准。
- `base_revision`：比较本轮修改的 Git commit 或受信快照。
- `status`、`approved_by`（若审定），`change_id`（若提交变更）。

## 校验可做/不能做什么

`snl scope-check` 可以分析 Git diff（已跟踪文件及未跟踪新文件）、比较允许写路径、对 root 内路径标准化并拒绝 `..`、绝对越界、符号链接逃逸。跨 OS 路径分隔符和 Windows 大小写问题要测试。它属于**事前配置校验 + 事后更改检测**。

**不能保证**：单靠 YAML 中写一句限制或运行一个检测 CLI，就能技术性阻止拥有自由执行工具权限的 Codex 在范围外写文件。若需要强防护，应使用真正权限受限的工作区、容器/进程沙箱、只读挂载、工具权限、Git worktree、PR review；避免将声明式权限误宣传为沙箱。

## 人与 AI 的责任分配

AI 负责主动拟定详细规约、解释歧义、编写验证样例、更新引用、提出变更；人不必每行撰写，但应着重确认：目标意图是否对、输入输出与外部副作用是否合适、检查结果是否足以判断成功、何时可接受方向变更。这与“人只点一下批准、不读证据”同样不同。

## 可操作闭环

1. 选择模块/作用域与基线。
2. Agent 分析已有源码/契约，提出目标、分支方案及需要确认的行为。
3. 形成或修订局部 SNL + Acceptance；自动做结构/语义校验。
4. 在允许目录内实现与测试；记录 Source ↔ Contract ↔ Test。
5. `scope-check` + `validate` + 测试 + Git diff。越界必须阻断集成，必要时提案重新授权。
6. 人验收后按范围审定并更新基线；把不确定结论、失败假设留在版本历史。

**阶段性缩小/扩大的能力**是系统价值的一部分，不应退化为“项目初始化时有个静态 allowlist”。
