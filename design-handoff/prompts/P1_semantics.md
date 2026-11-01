# Codex 分阶段 Prompt — P1：契约语义与精细验证

请在既有可运行 SNL CLI 基础上扩展，勿重写 P0。阅读 `docs/02_language_model.md`、`docs/03_contract_rules_and_validation.md`、`docs/07_report_style_behavior.md`、`implementation/04_acceptance_matrix.md`。先运行现有测试并报告基线。

任务：强化 Entity/Ownership 与 Capability/Component/Workflow 的引用、端口、读写权限、错误、副作用、分支/循环的静态检查；为每条条款引入机器可判定/test-backed/review-required 分类。对自然语言条件仅检查结构一致性，不能宣称自动证明互斥/覆盖；如引入受限表达式，只支持白名单语法，不执行任意 Python。

提供：可版本化 Schema、诊断 code/severity/source/step、稳定 ID 到测试/代码的追踪结构、错误/边界 fixture；输出验证矩阵覆盖与未实现语义清单。结构和语义检查应可由 CLI/CI 独立运行，所有新增功能有自动测试。
