# Code From Spec

**Code From Spec** is a methodology where code is a generated
artifact, not the source of truth. The source of truth is a
hierarchy of specification files. To change behavior, you change
the spec and regenerate. You never edit generated code directly.

This methodology is designed for AI agent participation at every
stage — writing specs, managing versions, detecting staleness,
running resyncs, and generating code.

---

## How it works

Specifications are organized as a tree. Each node adds precision
to its parent — business intent at the root, implementation
contracts at the leaves. Only leaf nodes generate code.

```
spec/
└── payments/
    └── fees/
        ├── calculation/   ← leaf → generates code
        └── rounding/      ← leaf → generates code
```

Every spec node is a Markdown file with a YAML frontmatter carrying
a `version` integer. When a node changes, its version increments.
Dependents that reference an outdated version are **stale** and
must be reviewed and regenerated.

---

## Methodology files

| File | Purpose |
|---|---|
| [`framework/CODE_FROM_SPEC.md`](framework/CODE_FROM_SPEC.md) | Overview and resync procedure |
| [`framework/SPECIFICATIONS.md`](framework/SPECIFICATIONS.md) | Spec tree structure and node format |
| [`framework/VERSIONING_AND_STALENESS.md`](framework/VERSIONING_AND_STALENESS.md) | Versioning rules and staleness conditions |
| [`framework/EXTERNAL_DEPENDENCIES.md`](framework/EXTERNAL_DEPENDENCIES.md) | External dependency format |
| [`framework/AGENT_SPEC_STALENESS.md`](framework/AGENT_SPEC_STALENESS.md) | Agent instructions: spec staleness |
| [`framework/AGENT_CODE_STALENESS.md`](framework/AGENT_CODE_STALENESS.md) | Agent instructions: code staleness |
| [`framework/AGENT_CODE_GENERATION.md`](framework/AGENT_CODE_GENERATION.md) | Agent instructions: code generation |

---

## Tools

| Repository | Description |
|---|---|
| [spec-staleness-check](https://github.com/CodeFromSpec/spec-staleness-check) | CLI tool that automates spec staleness verification |

---

## Versioning

`main` is the development branch. Released versions live in
dedicated branches (`v1`, `v2`, ...) and receive only bugfix
commits. Breaking changes always produce a new version branch.

To fetch a specific version of the methodology, use the raw URLs
from the appropriate branch:

```
https://raw.githubusercontent.com/CodeFromSpec/.github/v1/framework/CODE_FROM_SPEC.md
https://raw.githubusercontent.com/CodeFromSpec/.github/v1/framework/SPECIFICATIONS.md
```
