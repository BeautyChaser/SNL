# 12 — 历史讨论 → 可实施需求映射

> 这是按当前可回溯的历史讨论与持久设计要点重建的**主题覆盖图**，不是全部聊天逐字记录。重点是防止 Codex 漏掉“方法论/治理”和“CLI 具体能力”之间的关键连接。

| 历史主题 | 对应思想 | 已落实在本包中的位置 |
|---|---|---|
| 2026-10-23：收束式 AI 原生开发、契约白箱/实现黑箱、验证追溯 | 人评估和验收、AI 承接实现、验证证据可追溯 | `docs/01`、`docs/09`、`AGENTS.md` |
| 2026-10-28：SNL=面向 LLM 的契约式编程语言 | I/O、能力、所有权、副作用、异常、实现无关 | `docs/01`、`docs/02`、`docs/03` |
| 2026-10-28：SNL 与 YAML 的兼容性 | YAML 为候选载体，真正价值在契约语义及校验 | `docs/02`、`implementation/02`、`examples/` |
| 2026-10-28：Entity/Ownership、Capability/Component、Composition | 具名对象/拥有权、可复用能力、依赖/连线 | `docs/02`、`docs/06`、`implementation/02` |
| 2026-10-28：SNL-first / Graph-generated / GUI-optional | 规范文本为权威、IR/图/GUI 为投影 | `docs/01`、`docs/08`、`implementation/01` |
| 2026-10-28：开放 `snl.exe` 收束器 | CLI 校验、构建 IR、图、Agent 上下文包、验证 | `docs/08`、`implementation/00–04`、`prompts/` |
| 2026-10-28：Living Specification / CRUD / 局部审定 | 规约与实现共同演化，保留未决、审定、差异、影响 | `docs/04`、`prompts/P2`、`examples/change_proposal.yaml` |
| 2026-10-28：与 OpenSpec、Git/RAG+Knowledge 的关系 | 共识记录、代码知识版本、审批与有效定义分层 | `docs/09`、`docs/10` |
| 2026-10-28：封闭 Workflow 的渐进解构 | 30% 已拆/70% 黑箱仍运行，只规范到实现单元 | `docs/06`、`examples/modules/component.legacy.yaml`、`workflow.prepare.yaml` |
| 2026-10-29：面向 AI 的“多文件结构化演讲稿” | 角色、上下文预算、信息组织、反馈修订 | `docs/07`、`docs/08`、`COMPACT_CONTEXT.md` |
| 2026-10-29：像写报告一样描述模块行为 | 稳定步骤 ID、决策/分支/合流/循环、异常、验收 | `docs/07`、`examples/parameter_preparation_report.md` |
| 2026-11-01：阶段性局部作用域、减少随机性 | 指定文件夹/接口/验收/停止条件；权限/差异检查 | `docs/05`、`prompts/P3`、`examples/scope.yaml` |
| 2026-11-01：AI 参与规约撰写、人确认关键判断 | 避免 AI 仅执行、避免人工逐行写规范 | `AGENTS.md`、`docs/01`、`docs/04`、`docs/05` |

## 从方法论到原型的因果链

`人提出可能模糊的意图` → `AI 草拟多文件规约/备选假设` → `结构/语义检查与问题标注` → `人局部确认契约及可检测条件` → `锁定当下有效范围/版本` → `装配目标 Agent 的必要上下文` → `局部实现/探索` → `自动测试与人工验收` → `diff/impact/source↔evidence 追溯` → `继续修订、解构与知识沉淀`。

**不要误读**：不是一条永不回头的流水线；任何环节的失败或新证据可以反馈至较上层定义，产生新的草案和审定。
