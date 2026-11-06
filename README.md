# Break Test

**An evidence-first reliability skill for coding agents.**

Break Test helps a coding agent find realistic ways a project's build or test suite can fail, reproduce each failure, and apply the smallest safe fix — keeping a fix only when both the reproduction and the project gate pass against the recorded baseline.

## Start here

- [`SKILL.md`](SKILL.md) — complete skill; source of truth
- [`QUICKSTART.md`](QUICKSTART.md) — short setup and usage guide

## Core workflow

**Isolate → Map → Baseline → Probe → Reproduce → Fix → Verify → Report**

Break Test is designed for coding agents with shell and file access. Git is required for the default isolated-worktree workflow; the full skill documents a non-Git fallback.

## Design principles

- Reproduce before reporting.
- Protect the user's checkout and local environment.
- Make the smallest change that removes the demonstrated cause.
- Verify both the reproduction and the project gate against baseline.
- Never weaken tests to manufacture a green result.
- Report observed evidence, inferences, skipped probes, and remaining risks separately.

## Important

Break Test does not promise exhaustive coverage or guarantee that a project is bug-free. It reports the probes actually run and the risks that remain. Read the full skill before using it on a project, especially the confirmation requirements for external services, long-running probes, and projects without version control.
