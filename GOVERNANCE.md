# Governance / 项目治理

SNL begins as a maintainer-led open-source exploration. [BeautyChaser](https://github.com/BeautyChaser) is the founding maintainer. This document describes the initial process, which can evolve as contributors join.

SNL 初期由创始维护者 BeautyChaser 维护。欢迎社区共同提出问题、挑战假设、设计实验和评审实现；随着参与者增加，治理方式可继续修订。

## How decisions happen

1. Discuss a problem or experience in Discussions or an issue.
2. Turn a concrete alternative into a proposal with examples, scope, tradeoffs, and observable acceptance criteria.
3. Run a bounded experiment when evidence is needed.
4. The maintainer reviews the contribution and records the outcome through the issue or pull request. Rejected or deferred proposals should retain their reasoning.
5. Update the relevant design record when adopting a public contract or changing a founding principle.

Small, reversible implementation choices can be documented in a pull request. Changes to public semantics, reviewed baselines, licensing, or governance need an explicit maintainer decision. Contributors can question existing choices and offer counterexamples.

## What has been decided

- The project is public and open to community participation.
- Repository contributions use the [MIT License](LICENSE), selected by the founder on 2026-11-01.
- The [founding decision ledger](design-handoff/docs/10_decision_ledger.md) records prior design directions and candidate choices as a historical handoff.

The handoff's historical status labels do not make every schema field a standard. A Git commit or an AI-generated `APPROVED` label does not independently prove business approval. New decisions should identify their scope, rationale, evidence, and corresponding issue or pull request.

## Review and participation

Use evidence and concrete examples to resolve disagreements where possible; retain unresolved questions where evidence is insufficient. Both Chinese and English are welcome. The English and Chinese repository introductions should describe the same capabilities and project maturity.

Maintainers may close duplicates, request a narrower contribution, or moderate abusive content. There is no promise of response times or implementation deadlines. Changes to this process should be proposed publicly in the repository.
