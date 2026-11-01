# 03 — 阶段性实施路线与完成标准

目标是**先建立一个运行闭环，再逐步扩展语义和治理**，而非第一天建立宏大平台。主 Agent 默认先推进 P0；其余阶段可在后续 Codex 会话按独立 Prompt 增量实现。

## P0 — 最小能用的收束器（首轮必须优先）

交付：Python 可安装包、CLI 入口、项目 manifest/多文件 parser、Schema/基本语义校验、Contract IR、一个确定性 graph、一个 target/role pack、基本 diff 与范围检查（资源不足时后两者可分次交付，不能伪装成功）、examples/pytest/README。

退出门槛：能从多文件 SNL 源码 `validate → build → graph → pack` 全流程成功，并在重复 ID、悬空引用、端口类型错误、无授权路径修改等反例上有正确失败/警告；输出可复现且有源追溯。

## P1 — 强化活规约与差异影响

交付：Proposal/Delta、working/baseline view、局部审定范围记录、有效版本内容哈希、结构差异的影响传播、未审定条目“不得静默生效”检查；对批准真实性模型的界限保持诚实。

退出门槛：对一个已批准契约做 AI 草案修改，运行时仍能识别旧有效基线，显示未批准差异及相关依赖；新批准操作需显式审定证据，不能由 Agent 自动替签。

## P2 — Scope + 开发回写的工程闭环

交付：路径白/黑名单、Git diff（tracked/untracked）越界检测、symlink/Windows 路径处理、Scope 的版本记录、步骤 ↔ 实现 ↔ 测试/evidence 引用与结果读取。

退出门槛：Agent 试图越界改文件的模拟测试被可靠检测；授权变更通过；输出报告明确“不等于 OS 沙箱”。

## P3 — 组合、行为报告与部分解构

交付：更完整的 branch/loop/exception IR 与诊断；Opaque + Extracted Component/Workflow 组合表示；Graph 渲染可显示部分拆分和黑箱；兼容性和测试证据可追溯。

退出门槛：同一组合中已拆部分与未拆黑箱都存在，接口完整，图与 IR 一致，取消不经验证的“等价已证明”断言。

## P4 — Agent Context/开源工具产品化

交付：多 Agent Role profile、确定性打包与预算/截断策略、CI JSON 消费接口、安装包与 Windows `snl.exe` 打包指引（如需可发布构建）、帮助文档、示例工程。

退出门槛：Implementer/Tester/Architect 目标包内容有显著且合理差异，预算不足显式报警，命令跨 Windows/Linux 实测，公开 API/文档/版本一致。

**注意**：P0 应已提供基础 Scope、Diff、局部状态与 Pack 闭环；后续阶段是强化而非把 SNL 的核心理念拖到未来才实现。可根据实际工作量调整阶段边界，但不得只用图或 Prompt 欺骗验收。
