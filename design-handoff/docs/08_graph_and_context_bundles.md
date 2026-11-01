# 08 — Contract IR、图投影、Agent Bundle 与 CLI 收束器

## Contract IR 的地位

SNL 源文件是可读写的定义权威，**Contract IR 是从某个版本的 SNL 解析/校验后生成的标准化机器投影**。IR 应具有确定排序、显式版本、稳定 ID、来源指针和未决/批准状态，供 graph、pack、diff、后续 GUI 消费。不要让 IR 独立成为第二套需要手动维护的权威源。

## 图与数据流投影

应按需要生成：

- Structure/Architecture：Entity、Capability、Component/Workflow 的层次与依赖。
- Composition/Data-flow：节点、公开端口、数据传递、调用/所有权方向。
- Behavior：带步骤 ID 的顺序/分支/合流/循环/异常图。
- Impact（逐步实现）：变更 ID 会影响哪些模块、接口/测试、潜在兼容性风险。

MVP 可以先用 DOT/Mermaid 文本输出；不要让图渲染依赖必须安装的 GUI。对没有具体边的自然语言步骤，输出可见的“未连接/待确认”而不是臆造边。

## Agent Bundle 的目的

`snl pack --target <id> --role <agent-role> --max-tokens <budget>` 将一个**具体版本**的相关契约按目标打包，不盲扫所有文件。Agent Bundle 不是随意摘要，至少应包含：

- 目标模块/步骤、当前状态、已审定公开接口、必要前后置/验收条件；
- 所依赖的可访问模块的**必要摘要 + 源指针**、数据流/副作用边界；
- 本轮 Scope、允许修改目录、禁止越权条件；
- 未决问题、冲突、疑似需升级的变化及审定版本/sha；
- 预期证据输出：测试、diff、实现映射、停止/升级条件；
- target/role/profile/预算估计与遗漏告警。

对不同 Role 分配内容：Implementer 优先放输入/输出/局部结构、代码位置和验收；Architect 更侧重依赖/影响；Tester 更侧重 invariant/异常/验证案例；Reviewer 更侧重 diff/证据/开放问题。

## 预算与信息完整性

优先保留不可压缩的精确定义：ID、类型、数字约束、权限、验收、例外、待决冲突和来源。可在预算不足时降级为“依赖摘要”，但不得以简写抹掉已批准条件，也不可把未知写成已知。若装不下所有必须内容，应该失败/告警并列出被截断的源及影响，不能静默提交一个看似完备的上下文。

Token 数量可能需要模型专用 tokenizer 才能精确计数。MVP 可提供明确标记的保守估计；不能宣称跨模型精确。建议支持确定性顺序和相同输入/版本产出相同 bundle 的测试。

## 典型 CLI 演化路径

`snl init → snl validate → snl build → snl graph → snl pack → Agent 实现/测试 → snl verify/impact/diff → 人批准基线`。

`validate / graph / build / pack / verify` 在早期讨论中是收束器目标命令；`diff / scope-check / impact / approve` 是为活规约和最新局部范围需求增补的合理命令方案。具体子命令拼写及参数不视为语言的核心不可变约束。
