# 04 — 验收矩阵（可直接转 pytest / CLI E2E）

每个 Case 都应在测试中具有名称、输入 fixture、预期退出码/诊断与证据。某项尚未实现时标记 `NOT_IMPLEMENTED`，不可声称通过。

| ID | 用例 | 期望 | 重要阶段 |
|---|---|---|---|
| A-01 | 全新项目 `snl init` | 生成合法 manifest 与样例，非空目录不静默覆盖 | P0 |
| A-02 | 多文件正常解析 | 产出至少 Entity、Capability、Workflow/Component 的唯一 ID | P0 |
| A-03 | 同一个 ID 在两个文件中重复 | validate error，定位两个文件 | P0 |
| A-04 | 格式错误/缺必需键/危险 YAML Tag | 安全拒绝，非零退出，不运行代码 | P0 |
| A-05 | 引用不存在的 Capability/步骤 | error，列出来源 ID/缺失目标 | P0 |
| A-06 | 类型不兼容的端口连线 | error；未定义类型的部分标 review/unsupported | P0 |
| A-07 | 组合图生成 | 图节点/边来自 IR，可按稳定 ID 溯源 | P0 |
| A-08 | 同输入连续 build 两次 | IR byte-for-byte 相同（去除非核心日志） | P0 |
| A-09 | 针对目标的 pack | 必要 I/O、契约、依赖、状态、source refs 都存在；不注入无关模块 | P0 |
| A-10 | Pack 预算不足 | 明确失败或强警告，列出被省略内容；不默默丢强约束 | P0 |
| A-11 | 草案/未决/待审定内容 | 不能被输出或标识成 approved；含 review-required | P0/P1 |
| A-12 | 结构 diff | 展示 added/removed/modified，可能影响的下游引用及未知影响 | P0/P1 |
| A-13 | 未获批的草案修订已有生效契约 | baseline 不被静默覆盖；可查询差异 | P1 |
| A-14 | 部分条款批准/其余 OPEN | 局部 status 准确，整体不误判 approved | P1 |
| A-15 | 文件外路径 `../secrets` 或 symlink escape | 目录/作用域检查拒绝 | P0/P2 |
| A-16 | Git 修改范围内与范围外各 1 个文件 | 输出清晰越权列表、非零退出 | P0/P2 |
| A-17 | Workflow 自然语言分支重叠风险 | 不假装证明互斥，标 review-required | P0/P3 |
| A-18 | Workflow 无限循环或无出口 | 结构诊断或要求退出上限 | P0/P3 |
| A-19 | 旧封闭模块局部抽取 | 保留 opaque + extracted 两种节点、明确合同与黑箱状态 | P3 |
| A-20 | “旧新行为等价”缺少测试证据 | status unknown/review，绝不返回 verified true | P3 |
| A-21 | 角色不同的 pack | Implementer/Tester/Architect 视图内容有差异且都可追踪 | P4 |
| A-22 | CLI Windows/Linux + 中文 UTF-8 | 正常导入中文说明及导出 JSON/MD | P0/P4 |
| A-23 | 静态校验虽通过但验收证据缺失 | 报未验证而非科学意义上的 PASS | P0/P2 |
| A-24 | 跨文件引用存在循环 | 诊断区分类型引用与无终止执行环；避免一概拒绝 | P3 |
| A-25 | Agent 欲自动批准业务规则 | 工具/工作流拒绝无证据自批准（或明确不提供审批功能） | P1 |

## 必须给出一次真实 E2E

在临时工作目录中导入 `examples/`，执行 `validate`、`build`、`graph`、`pack`、至少一次预期失败校验，并运行自动测试；保存执行命令、退出码、生成文件与摘要。不能将“测试预计通过”写成“测试通过”。

## 实验性而非被承诺的能力

- 任意自然语言语义等价；
- 完全静态证明分支互斥/穷尽；
- 不经沙箱的 Agent 文件写入阻止；
- 未经身份认证的人类审定证明；
- 数值求解器的物理精度保证；
- 跨模型精确 token 数量。

这些是后续研究问题，必须和可验收的 CLI 能力分开。
