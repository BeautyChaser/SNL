# Codex 分阶段 Prompt — P2：Living Specification / Delta / 局部审定

在 P0/P1 已实现代码上扩展；阅读 `docs/04_living_specification.md`、`docs/10_decision_ledger.md`、`docs/11_open_questions.md`。

目标：实现 working/baseline 分离的真实版本逻辑；提案与 ADD/MODIFY/REMOVE/RENAME 变化记录；结构差异及受影响模块/测试分析；局部审定和未审定条款不可静默生效。**绝不**把 AI 自动推测写成由人批准，Git commit/status 字段也不自动等于可信业务批准。可先用需人工复核的状态与带 hash 的审核记录，并在文档准确界定可信程度。

请用完整样例证明：对已经批准的参数预处理接口写一份 AI 提议修订，未批准前 `baseline` 仍旧；`working` 能展示拟议差异、需要重新检查的依赖；真实批准后再记录新基线。添加回归测试并报告证据。若审批身份无法可信实现，提供“记录与校验候选审批信息”，而非安全保证。
