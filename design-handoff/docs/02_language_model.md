# 02 — 概念语义模型与候选文件载体

## 语言三层

1. **表示层 (Syntax/Carrier)**：版本化、多文件、便于人阅读和 Agent 编辑的结构化自然语言。候选载体 `.snl.yaml` / YAML 1.2 子集；YAML 是可替换的媒介，并非 SNL 的核心原创点。
2. **契约语义层 (Semantics)**：Entity、Ownership、Capability、Component、Composition、Workflow、输入输出、可观察行为、权限、副作用、不变量、错误及依赖兼容性。
3. **验证/治理层 (Verification/Governance)**：结构校验、跨文件语义检查、审定状态、上下文选择、测试和人类复核证据、变更/影响追溯。

**重要**：用 YAML 声明文本并不会神奇地使描述可执行或无歧义。类型/条件/断言是否机器可验证要逐项标记。

## 概念对象

| 概念 | 责任 | 必要语义 |
|---|---|---|
| `Project` | 将多文件定义装配成指定视图 | ID、schema 版本、源文件集合、可审定基线、输出位置 |
| `Entity` | 长期身份、状态与生命周期、访问边界 | 唯一 ID、Owner、可读/可写权限、状态/不变量、事件 |
| `Ownership` | 谁负责状态真值与写入授权 | 对某 Entity/属性/副作用的责任主体；显式权限，不依赖推测 |
| `Capability` | 可复用公开行为/接口 | 输入输出、契约、外部副作用、异常、验收与依赖 |
| `Component` | 具边界的组合/封装单元 | 公开接口、内部调用能力、数据流、隐藏实现、契约兼容 |
| `Workflow` | 业务/算法步骤拓扑 | 顺序、分支、合流、循环/退出、失败与数据传递 |
| `Dependency/Composition` | 连接公开能力并校验兼容性 | 源/目标 ID、端口、类型、拥有权/权限/前置条件 |
| `Contract` | 对外行为的可检验定义 | Preconditions、Postconditions、Invariants、Errors、Side Effects |
| `Acceptance/Evidence` | 判断目标实现是否通过的证据链 | 测试引用、检查类型、验证状态、来源版本 |
| `Decision/Issue` | 记录尚无共识的定义 | OPEN/DRAFT/APPROVED 状态、责任、影响与依据 |

### Ownership 原则

Entity 负责身份与（可能是可变的）状态，Capability/Component 声明读写/调用权。对有状态数据优先采用清晰单一写责任、通过公开契约访问；若允许多写者须有明确协调规则，不应由 Agent 自行假定无冲突。`Owner` 不等于写在文本里的某个人名，更不是操作系统安全凭据；它是软件结构与治理概念。

### Capability 与 Component

Capability 描述 *能做什么*（public boundary），Component 描述 *组合了什么*（encapsulation），Workflow 描述 *如何组织执行次序与分支*（composition/flow）。三者不要强行等同底层函数类。可独立提供 Capability，也可将其封装进不同 Workflow。SNL 不需强迫层次永远固定。

## 候选文档字段（MVP 可简化）

每个定义建议具有：`snl_version`、`kind`、`id`（全局稳定、跨文件唯一）、`title`、`status`、`intent`/`description`、`interface`、`contracts`、`dependencies`、`behavior`、`acceptance`、`open_questions`、`source_refs`。Entity/Workflow 等只需各自适用字段。

附加治理属性建议：`provenance`（source path、Git SHA、作者/提出者）、`owner`、`scope`、`review`、`change_id`、`evidence_refs`。**示例字段是设计起点，不代表已定语法标准**。

## 多文件与唯一性

- 每份定义可独立编辑、审核、定位；project manifest 只列出明确许可的规范文件，不盲扫整个机器。
- ID 是语义身份，文件名是文件位置；重命名文件不应导致 ID 全体变化。
- 允许引用其他定义，引用要解析且类型/端口匹配；循环引用不总是非法，但无限制的调用/执行循环必须报错或需要控制规则。
- 推荐将复杂业务说明拆成模块级文档与细节段落；Agent Bundle 只提取有关内容，避免重复加载全库。
- 解析器需明确 YAML 版本/子集，不允许任意反序列化或执行标签；默认禁用隐式代码执行、外部引用自动下载。

## 与 JSON、YAML、图的关系

YAML/JSON 是载体，SNL 语义规范提供契约的内涵；JSON Schema 检查结构，Semantic Validator 检查实体身份/权限/组合，测试与审查确认行为。Graph 是 IR 的 deterministic projection；可导出 DOT 或 Mermaid，后续 GUI 仅为编辑器/投影视图。业务的 `project.json/flowchart.json/condition.json` 可以成为 SNL 描述/验证的外部目标，却不是强制的 SNL 本体语法。
