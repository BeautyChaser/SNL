# Codex 分阶段 Prompt — P3：阶段性 Scope / 越权检测 / 验证回写

请读 `docs/05_scoped_agent_operations.md`、`AGENTS.md`、`implementation/04_acceptance_matrix.md`，在当前代码上增量实现。

目标：Scope 随每个任务或阶段指定目标目录、允许读写路径、禁止路径、target SNL IDs、接口/验收/stop conditions 和 Git base revision；`scope-check` 识别 tracked/untracked changes，阻止 `..`、绝对越界、symlink escape、输出位置逃逸；Windows/Linux 处理一致。实现“规约条款/步骤 ID ↔ 源码位置 ↔ 测试 ID ↔ 证据状态”的机器可读引用与缺失检查。

必须声明 scope-check 只是静态/后验检查，不等于操作系统或 Codex Tool 级权限隔离。请模拟一次合法修改和一次非法越界修改，运行测试/命令并展示实际输出；不允许为了通过测试而跳过 symlink/路径规范化问题。
