# A first example: preparing configuration

Imagine asking an AI to implement: “prepare the configuration and fill in missing values.” Several decisions are hidden in that sentence: whether explicit values may be replaced, which defaults are trustworthy, what to do with unresolved fields, and what counts as a successful result.

The SNL handoff explores this through a draft capability with stable ID `example.parameter_preparation`.

## Make the public behavior inspectable

| Part | Proposed contract |
| --- | --- |
| Inputs | Raw configuration and completion rules with traceable sources |
| Outputs | Normalized configuration and a report of field status, sources, and errors |
| Explicit valid value | Preserve it |
| Explicit invalid value | Report a located error according to the reviewed policy |
| Missing value with a trusted source | Fill it and record provenance |
| Missing required value without a trusted source | Report an unresolved field or failure |
| Open question | Which sources take priority when completion rules disagree? |

The proposed representation includes clauses such as:

```yaml
# Excerpt from the candidate example, not a finalized language schema.
contracts:
  postconditions:
    - id: POST-002
      statement: "合法显式值不被无依据的默认值覆盖"
      checkability: test
      test_refs: [T-KEEP-EXPLICIT-001]
```

This clause says that an explicit valid value is preserved. A `test_refs` entry names expected evidence; it does not mean the test exists or has passed. Natural-language business judgments may still require review.

Read the complete [candidate capability](../design-handoff/examples/modules/capability.prepare.yaml), [report-style behavior](../design-handoff/examples/parameter_preparation_report.md), and [project manifest](../design-handoff/examples/snl.project.yaml). These are design examples, with no runnable parser in this initial repository.

## Use a bounded experiment

A useful first implementation would declare the module it may change, implement the visible input/output behavior, and add cases for preservation, sourced completion, invalid values, and unresolved fields. Review can then compare the contract, Git diff, and actual results.

If an experiment reveals that defaults must be filled before a full consistency check, the AI can propose that revision with evidence. People review its consequences; the working draft and effective baseline stay distinguishable.

## Help challenge the idea

Does this contract prevent a mistake you have observed? Does it duplicate an existing test or interface definition? Which parts would become stale? Bring a minimal case to [Discussions](https://github.com/BeautyChaser/SNL/discussions) or open an [experience report](https://github.com/BeautyChaser/SNL/issues/new?template=experience_report.yml).
