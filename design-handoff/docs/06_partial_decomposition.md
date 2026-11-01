# 06 — 从封闭原型到可治理单元：持续局部解构

## 背景与目标

应用工程师可能交付一个已可运行的单体 `main.py`、封闭 Workflow、示意流程图、外部输入/输出和参考结果。后端架构工作不是一口气将其逐行拆成原子函数，而是**先保证有可验证的整体行为，再逐步提炼公开契约与复用能力**。

典型演变：

1. `LegacyOpaqueWorkflow`：内部未知或不规整，但拥有有限的 I/O、错误与观察结果。
2. 选一个稳定边界，例如 `ParameterPreparation`，定义 Capability/Component、接口、来源和测试。
3. 新能力代替原始模块中的一部分，剩余部分仍以 `OpaqueAdapter` 持续存在；用边界连接并验证结果等价或差异可解释。
4. 若进一步发现公共能力，再从封闭部分提取新的能力；必要时保留多个阶段长期共存。
5. 人负责实现单元层的结构、权限和验收，Agent 决定类、方法、实现和优化细节。

## SNL 应能表达

- `decomposition_status: opaque | partial | composed`（候选标签）。
- 原组件和提取模块的稳定 ID、来源版本及已拆/未拆部分的**明确引用**。
- 保留黑箱适配模块（可为整段、子 Workflow 或实现单元），而不是未完成就删掉旧模块。
- `public_contract`、`adapter/compatibility_contract`、`data_bindings`、`evidence_refs`、已替换能力与未替换行为。
- `migration/change_id` 与 `verified_equivalence: yes/no/unknown`，不可凭主观观感宣称完全等价。

“已拆 30%、剩余 70%”只是解释**长期部分解构是合法系统状态**的例子，不是 SNL 必须计算代码百分比的度量。输出能力图应能显示 Opaque/Extracted 角色，明确未替换部分仍真实参与执行。

## 不要过度绑定电池行业

当前典型使用场景是电池工业软件后端、以 Application / Workflow / Capability / Solver Adapter 等边界组织研发。某些流程可有分子/原子两级 Workflow，业务层也可编排更高层流程；这些是领域架构规则，**不是所有 SNL 工程必须遵守的语言层级规定**。

SNL 能表达模型/求解器接口和验证，但核心工具不直接内置 PyBaMM、MOOSE、COMSOL 求解器，也不内置电池参数含义。通过示例证明可描述即可。

## 失败风险

- 只有结构图，没有旧新行为对照与验收；
- 迁移时强制把未拆模块虚构成已拆模块；
- 把“能力黑箱”解释为“没必要定义 I/O/错误/副作用”；
- Agent 在局部实现时擅自重构全局架构；
- 接口契约虽能解析但真实代码行为和图不一致。
