# 02 — 建议 Schema 与 Contract IR 契约

## 版本策略

候选初始 schema：`snl_version: "0.1"`。每次 SNL 文档解析必须明确版本；拒绝不支持的 major，minor 未知字段按可配置严格度处理，避免无声吞掉关键条款。`kind` 至少支持 `Entity/Capability/Component/Workflow` 作为文档主体，Project 单独 manifest。

## 项目 Manifest（建议）

`project_id`、`snl_version`、`spec_files`（有序/规范化文件路径列表）、可选 `scope_file`、`baseline_ref`、`context_profiles`、`output_dir`。项目加载必须限制读取范围到 manifest 所属目录或显式授权根，不能接受路径逃逸。

## 模块声明（建议）

- 通用：`snl_version/kind/id/title/status/intent/source_refs/open_questions`；
- Entity：`owner`、`state`、`invariants`、`exposes`；
- Capability：`interface.inputs`/`outputs`（每个有 `name/type/required/description` 等）、`contracts`、`errors`、`side_effects`、`acceptance`；
- Component：`interface`、`uses`/`dependencies`、`composition`、`encapsulation`；
- Workflow：`interface`、`behavior.steps`（稳定 ID 与 step kind）、`dependencies`、`data_flows`、`acceptance`。

**优先实现固定类型少、规则清楚的垂直切片**，再扩展表达式。自然语言 `statement`/`description` 应保留，不能丢弃未知语义后宣称检查完成。

## Contract IR（建议）

```json
{
  "ir_version": "0.1",
  "source_format_version": "0.1",
  "project_id": "example.project",
  "view": "working",
  "definitions": [
    {
      "id": "example.parameter_preparation",
      "kind": "Capability",
      "status": "DRAFT",
      "source": {"path": "modules/capability.prepare.snl.yaml", "sha256": "..."},
      "interface": {"inputs": [], "outputs": []},
      "contracts": [],
      "dependencies": [],
      "steps": [],
      "acceptance": [],
      "open_questions": []
    }
  ],
  "edges": [],
  "diagnostics": []
}
```

字段具体可根据实现调整，重要的是**结构分层、确定性、版本、稳定 ID、源追溯、状态与待决点不丢**。

## 重要的确定性细节

- 相同输入 bytes + 相同版本的解析器 + 相同配置应生成相同 IR 核心字节内容（统一 UTF-8 / newline / 排序 / JSON 编码）；动态时间戳放日志 sidecar 而非内容核心。
- Reference resolution 使用完整 `id`，对文件名、序号/行数的变化更稳健；错误定位包含 path + ID + 可得到的 step ID。
- 统一规范化路径，不输出绝对个人路径到跨机器 IR 中；源内容 sha256 可用于审查范围和缓存。
- Approval 有独立事实来源/审定者与版本哈希；单纯 `status: APPROVED` 的 YAML 字样不能构成可信审批审计，但首版可以用**标注状态**并明确“未验证审批真实性”。
- Scope 的 `owner` 与 Entity 的 `owner` 语义不同，不能将状态写权限等同磁盘权限。

## 同源图与 Context Pack

Graph 的每个节点/边应能指到 IR 的 definition ID / step ID 与原始源路径；Bundle 按 target 与依赖距离筛选并保留重要合同条款。输出要显示 `view=working/baseline` 和 `status`，并对每个未决必要项标出 `REVIEW_REQUIRED`。

## MVP 退化策略

不可判定的中文条件原样放 IR，但不求值；`checkability: review`。端口类型仅做明确已支持的形式检查。无法自动判断单位兼容、业务约束、引用的证据真实性时给出 unsupported/review，不凭猜测通过。
