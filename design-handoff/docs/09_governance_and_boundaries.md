# 09 — 与 Git、Knowledge/RAG、OpenSpec、Harness、企业研发的关系

## 各层职能不混为一谈

| 层 | 负责的权威信息 | 不应替代的东西 |
|---|---|---|
| SNL | 对外软件定义/契约、构成、步骤、审定状态、待决事项 | 源码实现、物理真值本身 |
| Source/Git | 真实源码、commit、diff、分支和历史 | 契约语义的人工审定 |
| Tests/Evidence | 已跑过的检查/基准/验证结果及可复现记录 | 所有输入正确性的全称证明 |
| Knowledge-as-Code/RAG | 可迁移理论、假设、证据、版本化通用知识 | 模块的有效公开契约 |
| Harness/Agent | 读取上下文、执行工具、局部修改、测试 | 用户控制权、准确性证明 |
| GUI/Graph | 呈现与导航、可选局部编辑 | 与 SNL 平行的另一份定义真值 |

## GitLab Knowledge / 飞书背景

用户既定研发体系中，飞书用于自由讨论、草稿、试错；成熟可复用的理论/经验/验证证据进入 GitLab Knowledge，具有 commit/Tag/MR，Agent/RAG 需按版本读取。SNL 可通过 `source_refs`、`evidence_refs`、`knowledge_version` 引用这些资料，**不能无版本地抓取冲突知识后当作当前批准契约**。

代码仓库中应保留与实现直接相关的接口/算法-源码映射和回归证据。SNL 项目可和代码同仓或独立仓，再通过锁定版本联系；这是集成选择而非语言语义强制。

## 与 OpenSpec 的交集和差别

OpenSpec 常用 `specs/` 当前规格、`changes/` 提案、delta/归档，强调持续变更共识。SNL 可以参考这种变更记录习惯，但重点还包括 Entity/Ownership、可机器分析的 I/O/Side-effects、Composition/Graph、Agent Context Bundle、Scope 和局部解构。因此**不能仅实现一种目录里的 Markdown 变更日志便宣称实现了 SNL**。

## 与 AI-Native 后端工作方式的关系

- 主 Agent 负责单上下文对接与总体验收，按需分派测试/实现任务，避免大量交叉上下文重复消耗。
- 讨论、假设、数学规约、离散、源代码实现映射与证据可以沿 SNL 的引用链并行建设；但 SNL 本身不等于求解器数学文档，也不强迫所有专业公式进入固定语言语法。
- AE 的可运行原型与 Workflow 并不自动成为公司可信资产。BAA/架构人应把业务可观察行为、边界、验收整理成 SNL/相关文档并逐步审查、重构与验证。
- 客户真实数据须先完成权限/脱敏/隔离；SNL CLI 原型测试优先使用合成数据。

## 开源与模型无关

收束器应可开源、独立 GUI/模型供应商，原则上允许不同 AI API/本地模型/Harness 消费 Agent Bundle。开源许可具体选型仍需人类确认；MVP 不必依赖在线模型或商业服务。
