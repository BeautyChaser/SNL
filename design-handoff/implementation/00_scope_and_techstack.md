# 00 — MVP 范围与工程选型（给 Codex 的可逆默认）

## 要验证的核心假设

是否能把**多文件结构化自然语言**中的稳定契约、依赖、状态、步骤和开放问题解析为 IR，并持续通过 CLI 校验、图投影、目标上下文装配、差异/作用域检查支持人机共同修改，而不把“自然语言含糊”变成虚假的确定性？

## 最小架构

- `parser/loader`：按项目 manifest 读取指定文件，安全 YAML 解析，追踪源文件和内容 SHA。
- `schema`：版本化 Schema 与模型约束，拒绝未知 major version。
- `semantic`：ID/引用、类型/端口、Workflow 步骤/循环诊断、未批准内容传播。
- `ir`：保持 source refs 的规范化 Contract IR，确定输出。
- `graph`：从 IR 生成 DOT/Mermaid 等文本图。
- `pack`：target/role/budget 选择上下文与来源/状态告警。
- `diff`：IR 版本的结构差异；标记高风险人工影响复核。
- `scope`：git changed files + 白名单/拒绝列表检查、路径逃逸检测。
- `cli`：统一文本/JSON 诊断、退出码。
- `tests/examples`：可运行正反样例与 CLI E2E。

新仓库优先 Python 3.11+、PyYAML safe_load、jsonschema、pytest；可用 Typer 或标准 argparse，但不要堆重型框架。CLI 要能 `pip install -e .` 然后 `snl --help`，能在 Windows PowerShell 与 Linux Shell 正常工作。若源仓库已有成熟语言/结构，评估后复用，避免“为遵守候选技术栈”重写。

## 明确暂不做

- LLM 在线服务/模型接口和自动生成真实业务代码；
- GUI、UE Blueprint、可视化编辑器和复杂网络服务；
- 完整通用自然语言逻辑证明器、通用动态运行时；
- 商业级可信审批身份和权限平台；
- 自动爬取知识库、公司飞书/GitLab、真实客户数据；
- 电池仿真求解器本体、参数辨识流程的运行实现；
- Windows exe 的二进制发行流水线（可作为后续里程碑）。

## 风险防护

- 模板/规约文件不得触发任意 Python、shell 或 YAML object 构造。
- 默认只读解析；生成文件时不能覆盖不属于输出目录的用户内容。
- CI/测试不需要网络或密钥。
- Windows 的路径大小写、反斜杠、UTF-8 中文、相对路径与 symlink 要有测试。
- 任何未实现的语义检查必须暴露为 `unsupported` / `review_required`，不得在 README 中宣称已验证。
