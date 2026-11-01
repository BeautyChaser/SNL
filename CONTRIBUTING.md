# Contributing to SNL / 参与 SNL

SNL is an early exploration of how humans and AI can maintain a shared software definition. Ideas, criticism, and reproducible cases are as welcome as code. You can contribute in Chinese or English.

SNL 正处于早期探索阶段。真实案例、反例、问题和文档改进与代码同样有价值，欢迎中文或英文贡献。

## Choose a way to contribute

| Contribution | Start here | Useful detail |
| --- | --- | --- |
| An open question or alternative approach | [Discussions](https://github.com/BeautyChaser/SNL/discussions) | What assumption should we challenge? What would change your mind? |
| An AI-assisted development experience | [Experience report](https://github.com/BeautyChaser/SNL/issues/new?template=experience_report.yml) | Intent, observed behavior, expected behavior, and a minimal anonymized example |
| A language or governance proposal | [Design proposal](https://github.com/BeautyChaser/SNL/issues/new?template=design_proposal.yml) | Problem, examples, tradeoffs, affected contracts, and an experiment |
| A bounded implementation experiment | [Implementation task](https://github.com/BeautyChaser/SNL/issues/new?template=implementation_task.yml) | Target, allowed changes, acceptance checks, and unresolved choices |
| Documentation or translation | A focused pull request | Keep the English and Chinese entry points consistent where relevant |

## Before implementing a feature

Read the [roadmap](ROADMAP.md), [decision ledger](design-handoff/docs/10_decision_ledger.md), and relevant [open questions](design-handoff/docs/11_open_questions.md). For changes to public contracts, propose the problem and a small example in an issue before a large implementation. Small documentation fixes can go directly to a pull request.

Python 3.11+, safe YAML, and JSON Schema are candidates for the first CLI experiment. We have not adopted a permanent language syntax, runtime, or standard. The original handoff is under [design-handoff/](design-handoff/); its prompts describe future tasks.

## A useful pull request

1. Describe the concrete problem and expected behavior.
2. Keep changes within the proposed scope. Identify any public contract changes.
3. Include normal and failure examples for executable behavior, and run relevant checks.
4. Report exactly what ran and what remains unverified. Documentation-only changes should check links, examples, and terminology; they do not need invented runtime tests.
5. Update affected documents and references. Keep candidate choices and unresolved rules explicit.

There is no runnable CLI or established test suite in the initial repository. Installation and test commands should be documented only when their implementation exists.

## AI-assisted contributions

AI assistance is welcome. The person submitting a contribution is responsible for understanding and reviewing it. Explain AI involvement where it helps reviewers understand the work, and provide reproducible evidence for behavioral claims. Do not submit fabricated test results, approvals, or unsupported guarantees.

Use synthetic or anonymized examples that you have permission to share. Discuss ideas respectfully, explain disagreements, and avoid personal attacks. Maintainers may moderate abusive or irrelevant contributions.

## Licensing

By submitting a contribution, you agree to make it available under this repository's [MIT License](LICENSE). No separate CLA is required by the current project process. See [GOVERNANCE.md](GOVERNANCE.md) for how decisions are made.
