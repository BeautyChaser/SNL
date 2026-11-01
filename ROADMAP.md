# Roadmap / 路线图

This is a proposed research and implementation sequence. Unchecked items are not implemented. Scope and acceptance criteria can evolve through issues, experiments, and review.

这是待推进的研究与实现路线；未勾选内容尚未完成。欢迎通过案例、实验和讨论调整具体方案。

## Foundation · 开源协作起点

- [x] Import and verify the founding design handoff and candidate examples.
- [x] Add English and Chinese introductions, contribution guidance, and MIT licensing.
- [x] Define proposal, experience-report, and implementation-task templates.
- [ ] Collect real AI-assisted development failures and counterexamples.
- [ ] Agree on a small, observable experiment for the first CLI.

## P0 · A reproducible CLI vertical slice

Proposed flow: `init → validate → build → graph → pack`, with basic `diff` and `scope-check` as bounded follow-up slices if necessary.

- [ ] Load an explicit multi-file manifest with stable IDs and source hashes.
- [ ] Validate structure and supported references, ports, and types; report unsupported semantics explicitly.
- [ ] Produce deterministic Contract IR and a generated graph with source references.
- [ ] Build a target/role context bundle that retains status, open questions, and essential contracts; expose budget failures.
- [ ] Show structural differences and detect Git changes outside an allowed scope.
- [ ] Run positive and negative CLI tests on Windows and Linux, including UTF-8 paths.

**Completion evidence:** a runnable example, repeated builds with identical IR bytes, and expected failures for duplicate IDs, dangling references, unsafe input, and insufficient context budgets. Natural-language review requirements remain visible.

## P1 · Living specifications

- [ ] Model proposals, deltas, working views, and effective baselines.
- [ ] Keep unreviewed edits from silently replacing a reviewed contract.
- [ ] Track review scope and content hashes, and report affected dependencies.

**Completion evidence:** edit a reviewed contract as a draft, show the old effective baseline and proposed changes, and record an explicit review decision without claiming unverified approval identity.

## P2 · Scope and evidence

- [ ] Detect tracked and untracked changes, path traversal, and symlink escape cases.
- [ ] Connect contract and step IDs to implementation and verification evidence.
- [ ] Record scope versions, failed checks, and evidence gaps.

**Completion evidence:** permitted changes pass and out-of-scope changes fail; reports distinguish detection from operating-system isolation.

## P3 · Composition and gradual decomposition

- [ ] Represent branches, loops, exceptions, and explicit unresolved conditions.
- [ ] Keep an opaque component working alongside an extracted capability.
- [ ] Trace compatibility and regression evidence through the composition.

**Completion evidence:** a partial migration with both components represented; equivalence remains unknown where no evidence exists.

## P4 · Agent integration and distribution

- [ ] Compare implementer, tester, architect, and reviewer context views.
- [ ] Explore model adapters for context budgets and existing agent integrations.
- [ ] Publish installation guidance and reproducible distributions, including a Windows executable if justified.

**Completion evidence:** role-specific bundles preserve required constraints, and documented workflows run on supported platforms.

## Open research / 开放研究

Syntax and maintenance cost, trustworthy review, useful versus excessive formalization, context selection, interoperability, and measurable benefit to real development remain open. See the [open questions](design-handoff/docs/11_open_questions.md) and [original acceptance matrix](design-handoff/implementation/04_acceptance_matrix.md).
