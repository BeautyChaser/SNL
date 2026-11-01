# Founding sources and repository status / 资料来源与仓库状态

## Sources

On 2026-11-01, the founder supplied:

- `SNL_Codex_PromptPack_2026-11-01.zip` — 37 files, including a manifest for 36 other files.
- `ONE_SHOT_PROMPT.md` — byte-identical to the copy inside that archive, verified by SHA-256.

The archive was imported under [design-handoff/](../design-handoff/) with its file bytes and internal layout preserved. All 36 recorded file sizes and SHA-256 hashes matched [manifest.json](../design-handoff/manifest.json) during import. The ZIP itself and duplicate standalone prompt are not needed in version control.

The source package describes itself as a reconstructed design handoff, not a verbatim archive of every prior chat. Its historical decisions should be read with that limitation. This repository does not claim independent access to the underlying ChatGPT conversations.

## Current decisions

The founder requested a public GitHub repository under `BeautyChaser` to develop SNL openly and invite other developers to examine AI-assisted software development. The founder selected the MIT License on 2026-11-01.

These current decisions resolve the handoff's earlier open question about licensing. The historical package is preserved rather than retroactively rewriting its manifest or decision records.

## Instructions versus present scope

The handoff contains agent instructions and prompts for implementing a substantial CLI MVP. They are archived task material. Importing them does not mean the MVP has been requested, implemented, tested, or released in this repository's initialization step.

The initial repository establishes project context, examples, a proposed roadmap, and contribution channels. Executable functionality must be developed in later scoped contributions and supported by actual evidence. See [README.md](../README.md), [ROADMAP.md](../ROADMAP.md), and the current root [AGENTS.md](../AGENTS.md).

## 中文说明

原始资料包为过往讨论的整理摘要，不能视作完整聊天逐字记录。`design-handoff/` 保留导入时的原始内容与哈希清单，因此其中“许可证待定”等历史表述保持原样；当前采用 MIT 的决定以仓库根目录的许可证和治理说明为准。

包内的“直接实现 MVP”提示词是后续任务参考。本次仓库初始化已建立资料、社区入口与路线图；尚未交付 CLI、测试套件或最终语法标准。
