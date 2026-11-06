# Break Test — Quick Start

Break Test is a coding-agent skill for finding realistic ways a project's build and test suite can fail, reproducing each failure, and making only small fixes that are verified against the original baseline.

## What it does

1. **Isolates the work.** Uses a separate Git worktree and branch by default so probes do not disturb the user's checkout.
2. **Maps the build.** Records the toolchain, CI commands, services, and the commands that define the project's build/test gate.
3. **Records a baseline.** Runs the untouched gate three times to distinguish existing failures from regressions.
4. **Probes realistic failure modes.** Checks clean-checkout behavior, lockfile/install integrity, generated-code drift, toolchain and configuration assumptions, test order and flakiness, timezone/locale/platform behavior, network access, permissions, resource limits, and dependency health.
5. **Reproduces before reporting.** A suspected issue is not presented as a confirmed finding until a command reproduces it and its output is observed.
6. **Applies minimal fixes.** Each candidate fix is checked against its reproduction and the baseline. Fixes that weaken tests or make the gate less trustworthy are not retained.
7. **Reports the evidence.** The report includes commands, observed output, findings, applied/rejected fixes, remaining risks, and probes that were not run.

## Run it

1. Add the complete `SKILL.md` to your coding agent's skills directory or make it available to the agent using that tool's skill-loading mechanism.
2. Open the target repository in an agent that has shell and file access.
3. Ask the agent: **“Run Break Test on this project.”**
4. Review the isolation plan and answer any confirmation questions. In particular, the skill requires confirmation before probes that could contact real external services, unusually long probes, or work on a project without version control.
5. Review the final evidence report and each separate fix commit.

## Important safety and trust boundaries

- The default workflow keeps probes and fixes in an isolated worktree; the user's checkout is not the test playground.
- Local-only files such as `.env` and credentials are not copied without confirmation and must never be committed.
- Probes that may reach deployments, production databases, paid APIs, publishing systems, email, or messaging require explicit approval.
- A green test run alone does not prove a suspected issue was fixed. The reproduction must pass too.
- The skill does not claim exhaustive coverage. Skipped probes and unverified risks are reported explicitly.

## Compatibility

The skill is designed for coding agents with shell and file access. Git is required for the default workflow; a non-Git fallback is documented in the full skill.

**Use the full `SKILL.md` as the source of truth.** This quick start is an introduction, not a replacement for the complete procedure.
