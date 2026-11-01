# Codex 分阶段 Prompt — P0：最小 CLI 垂直闭环

你在 SNL 仓库工作。先读 `AGENTS.md`、`COMPACT_CONTEXT.md`、`implementation/00_scope_and_techstack.md`、`implementation/01_cli_contract.md`、`implementation/02_ir_and_schemas.md`、`implementation/04_acceptance_matrix.md`。真实检查仓库状态后，直接实现，不要只回答设计方案。

目标：`snl init/validate/build/graph/pack` 的可安装可测试闭环（如资源允许，同阶段加 `diff`、`scope-check`）。以最小 schema 解析多文件 `.snl.yaml`，保留中文自然语言与 source refs，生成稳定排序的 Contract IR、Mermaid/DOT 图及 target/role 定向 Agent Bundle。至少包含 Entity/Capability/Workflow/Component 的最小结构；先验证真实的可判定规则，对不可判定条件报告人工审查。

- **先检查**：现有依赖、测试、可复用模块、项目根目录和 Git 状态。
- **实现**：跨平台 Python 3.11+（若现有技术栈更适合则据实际调整）；安全 YAML；无 GUI/在线 LLM/电池求解器。
- **验证**：正常构建、重复 ID、悬空引用、类型不兼容、未审定条目、输出确定性、预算不足、危险 YAML 等正反测试。
- **输出**：真实 CLI 代码、安装指引、pytest 与运行日志/命令、对照验收矩阵的覆盖和未实现项。
- **原则**：SNL 是活契约，不是已经冻结的需求；YAML/字段是首轮候选；不伪称自然语言含糊已被自动证明。

必须在此轮结束前运行测试，报告事实性结果；失败时说明失败原因，不能把 TODO 或空函数报为完成。
