# SNL · 结构化自然语言

**用持续演进的契约，让人与 AI 共同定义、实现和验证软件。**

[English](README.md) · [路线图](ROADMAP.md) · [参与贡献](CONTRIBUTING.md) · [讨论](https://github.com/BeautyChaser/SNL/discussions)

AI 写代码越来越快，但在持续开发中，意图、接口、假设、实现和验证证据怎样保持一致？SNL（Structured Natural Language）希望用可版本化的结构化自然语言，承载人与 AI 长期共同探索的软件定义。

它关注目标、Entity 与 Ownership、Capability / Component、Workflow、公开输入输出、依赖、副作用、验收、未决问题与审定范围。AI 参与起草、质疑、修订、实现和测试；人重点判断意图、公开行为和重大变更。

> **当前阶段：设计探索与社区共建。** 仓库已收录创始设计资料、候选示例和实施计划。目前没有可运行的 `snl` CLI，也没有已发布的语言标准。Python、YAML、具体字段和命令形式均为待实验的候选方案。

## 想解决的协作问题

- **规约会继续生长。** 初始想法可以不完整甚至错误，草案、实验、问题和已审定基线需要共同存在。
- **每轮开发有局部边界。** 指定目标、允许修改范围、输入输出、验收和停止条件，逐步收束不确定性。
- **判断要有证据。** 通过稳定 ID 关联“规约条款 ↔ 实现位置 ↔ 测试与审查记录”。
- **公开契约清晰，内部实现保留自由。** 治理到可验收的实现单元，不要求人写出每个类和算法。
- **支持渐进解构。** 从已运行的封闭模块逐步提取能力，保留并验证尚未拆分的部分。
- **上下文按任务装配。** 面向不同 Agent 角色和预算，保留必要契约、来源、状态及未决问题。

**SNL-first · Graph-generated · GUI-optional。** 多文件 SNL 文本是权威源，经过校验生成 Contract IR，再派生图和 Agent 上下文包；实现、测试与人的判断继续反馈到规约。

自然语言条款需要按可判定程度分别处理：结构校验、测试证据和人工复核具有不同含义。未来的 Scope 检测也需要配合实际工作区权限才能实现硬隔离。

## 从哪里开始

1. 阅读[定位与原则](design-handoff/docs/01_vision_and_invariants.md)和[参数预处理报告式示例](design-handoff/examples/parameter_preparation_report.md)。
2. 查看[活规约](design-handoff/docs/04_living_specification.md)、[局部作用域](design-handoff/docs/05_scoped_agent_operations.md)与[渐进解构](design-handoff/docs/06_partial_decomposition.md)。
3. 通过[决策台账](design-handoff/docs/10_decision_ledger.md)区分既有方向和候选实现，再选一个[开放问题](design-handoff/docs/11_open_questions.md)或[路线图任务](ROADMAP.md)。

## 欢迎一起思考与实验

欢迎带来 AI 辅助开发中的真实失败案例、对 SNL 的反例、语言设计建议、可复现实验、文档改进和小范围原型。不必先接受整套设计；帮助发现其代价和适用边界，同样是贡献。

- 开放讨论、提问与想法：[Discussions](https://github.com/BeautyChaser/SNL/discussions)。
- 可推进的问题、案例和任务：[Issues](https://github.com/BeautyChaser/SNL/issues)。
- 参与方式：[贡献指南](CONTRIBUTING.md)与[治理说明](GOVERNANCE.md)。中文和英文均可。

原始资料完整保存在 [design-handoff/](design-handoff/)，其 SHA-256 清单可追溯本次导入来源。包内要求“直接实现 MVP”的提示词供后续明确选择任务时使用；仓库当前的实际完成情况以本页和[路线图](ROADMAP.md)为准。详见[资料来源说明](docs/provenance.md)。

## 许可证

采用 [MIT](LICENSE) 许可证，欢迎使用、修改、分发与贡献。
