\# Codex — Environment Notes



> This document covers notes for running the Production Code Guidelines in a Codex environment.

> For the general workflow, see \[`SKILL.md`](../../SKILL.md).



\## AGENTS.md Core Constraints Block

Append the following to `AGENTS.md` (or your system instruction setup) to restrict Codex batch execution behaviors:



```markdown

\## Core Constraints

\- Every code generation or modification task must adhere to `skills/production-code-guidelines/SKILL.md`.

\- Match local conventions and make the smallest surgical change that solves the request.

\- Defend only at trust boundaries; do not add speculative guards or speculative null checks in trusted code.

\- Fail fast rather than mask bad state with hidden recovery paths.

