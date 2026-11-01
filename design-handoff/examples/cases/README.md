# 测试夹具制作要求

本包中的 `examples/snl.project.yaml`、`modules/` 是正常项目的**候选示例**。Codex 应在其真实 Schema 落定后建立以下**自动化正反 fixture**（不能凭手工想象测试通过）。

1. 修改 module 的 `id` 造成跨文件重复：`validate` 应返回 error，指出两处来源。
2. 在 `workflow.prepare.yaml` 写不存在的依赖 ID：返回 unresolved reference error。
3. 在数据流中将 `object` 输出连接到 `string` 输入：返回端口不兼容 error。
4. 写非法 YAML 或危险 object tag：安全解析失败，不执行任何代码。
5. 将 `OPEN` 条款误写为 Approved 并打包：工具必须显示状态/来源；不能将草稿自动批准。
6. 将 `S2` 的分支自然语言改成互相重叠：应标 review required，不能因为读起来合理就给 PASS。
7. 将 loop 的 exit/max_iterations 删去：应提示不保证终止。
8. 生成 IR 两次比较 SHA/字节，文本图输出保持相同。
9. 使用极小 pack 预算：强烈警告或失败，明确未携带条款。
10. Git 仓库中只准写 `src/parameter_preparation/`，却改动 `src/solver/`：`scope-check` 失败。
11. 测试 `../`、绝对路径、symlink 越界及 Windows 风格路径。
12. 部分解构表示中同时存在新 Capability 与 opaque Component，不能自动把未知回归等价设为 verified。

如样例字段需要微调以符合首次实现的 schema，必须同步修改 docs/examples/tests，并在提交说明里记录差异及为什么仍符合已确认 SNL 原则。不得悄悄删除业务语义以换取 Schema 通过。
