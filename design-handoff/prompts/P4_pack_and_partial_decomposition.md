# Codex 分阶段 Prompt — P4：Agent Context Bundle、分支报告与部分解构

请读 `docs/06_partial_decomposition.md`、`docs/07_report_style_behavior.md`、`docs/08_graph_and_context_bundles.md`、`examples/`。在现有 SNL CLI 上增量实现，不要新增图/GUI 的平行真值。

目标：支持 Opaque 旧组件和 Extracted Capability/子 Workflow 的组合，让未拆部分作为合法节点继续参与流程；可输出组合图/步骤图；报告式步骤带稳定 ID、显式分支/循环/错误与必要退出条件。Bundle 针对 Implementer/Tester/Architect/Reviewer 角色选择上下文，保留强约束、未决、来源与预算告警；精确 token 数若不可得要注明估算。

验收：演示从旧封闭 Workflow 提取参数补全能力，保留其他黑箱步骤，图与 Contract IR 一致，并输出“兼容性证据未知/需验证”的诚实状态。角色包内容确有区别；不因为预算不足把关键安全/接口/未决信息默默省掉。补充真实测试和可用文档。
