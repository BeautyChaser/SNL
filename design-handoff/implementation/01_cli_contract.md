# 01 — CLI 行为契约（命令拼写为候选稳定接口）

推荐包名/入口：`snl`，`snl --version`，`snl --help`。入口支持 `--format text|json`，错误既有 human-readable 信息也有 machine-readable diagnostic。所有命令必须使用明确 project/工作目录路径，不能默默覆盖任意文件。

| 命令 | 最小输入 | 成功输出 | 失败/边界 |
|---|---|---|---|
| `snl init DIR` | 不存在/空目录 | 示例 manifest、模块 SNL、README，退出 0 | 目录非空则拒绝或要求显式参数，不静默覆盖 |
| `snl validate PROJECT` | 项目 manifest | diagnostics：结构 + 静态语义；可 JSON | malformed YAML、重复 ID、缺失引用、端口不匹配使退出非零；不可判定语义是 review |
| `snl build PROJECT --out OUT` | 通过最小结构检查的源文件 | 确定排序的 Contract IR JSON、源指针与状态 | fatal error 不写伪完整 IR；需要允许草案视图但标明它非已批准基线 |
| `snl graph PROJECT --format mermaid --out OUT` | IR/有效项目 | 按定义导出的图，稳定 ID 与 source ref | 不凭空补不存在的边，不强制依赖图形软件 |
| `snl pack PROJECT --target ID --role ROLE --budget-tokens N --out OUT` | 指定模块/角色/预算 | Agent Bundle MD/JSON、审定/未决/预算/来源信息 | 目标缺失或必需契约超预算时失败或强警告，不静默截去关键约束 |
| `snl diff --base IR_A --head IR_B` | 两份同版本可比较 IR | added/removed/modified/renamed-candidate、受影响依赖与 review 标记 | 不能声称已完成自然语言语义等价证明 |
| `snl scope-check SCOPE --base-ref REV` | scope 规则 + Git 项目 | 本轮修改文件清单及越界项 | 非 Git 工程、路径逃逸、越界修改须明确报错或失败 |

下一阶段或增量实现：`snl verify`（验证结果与测试引用对照、可选受控测试执行）、`snl impact`、`snl approve`、`snl migrate`。这些命令应由真实需求/测试驱动补齐，**不要实现永远只返回 success 的空壳**。

## JSON 建议结果格式

```json
{
  "ok": false,
  "project": "example.project",
  "source_revision": "content-sha-or-git-ref",
  "diagnostics": [
    {
      "code": "SNL-REF-001",
      "severity": "error",
      "message": "Unresolved capability reference",
      "source_path": "modules/workflow.prepare.snl.yaml",
      "definition_id": "example.prepare_workflow",
      "step_id": "S2",
      "related_refs": ["example.missing_capability"]
    }
  ]
}
```

建议一致退出码：`0`=命令成功（warning 可存在），`2`=输入/语义校验失败，`3`=环境/运行异常；如仓库约定不同请统一记录。JSON stdout 仅结构化结果，其他日志写 stderr，便于 CLI 被 Agent/Harness 调用。

## 可复现命令（完成后 Codex 需亲测、根据实现调整）

```bash
python -m pip install -e '.[dev]'
snl validate examples/snl.project.yaml --format json
snl build examples/snl.project.yaml --out .snl-out/contracts.json
snl graph examples/snl.project.yaml --format mermaid --out .snl-out/graph.mmd
snl pack examples/snl.project.yaml --target example.parameter_preparation --role implementer --budget-tokens 5000 --out .snl-out/agent.md
snl diff --base tests/fixtures/baseline_ir.json --head .snl-out/contracts.json
pytest -q
```

**命令列表为期望契约，非已存在的命令**。缺少 fixture 时先创建真实测试 fixture，再对文档示例命令做修正；不要为演示写空壳。
