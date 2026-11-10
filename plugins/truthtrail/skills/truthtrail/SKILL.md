---
name: truthtrail
description: Use when implementing or testing a ticket in a repo that has .decisions/ — records product decisions and assumptions with npx truthtrail.
---
## TruthTrail: recording decisions

This repo records product decisions in `.decisions/`. Follow these rules.

**Find the ticket.** Take the ticket key from the branch name (e.g. `feature/JIRA-231-…`). If there is none, ask the user once.

**Tools.** If TruthTrail MCP tools are available (`record_decision`, `list_decisions`, `why`, `check_branch`, `list_pending`, `resolve_pending`), use them. Otherwise use the `npx truthtrail` commands below.

**Before you implement,** run `npx truthtrail list --ticket <KEY>` and follow the decisions it shows. Treat `rejected` ones as must-rework.

**Record a decision** with `npx truthtrail decide` when:
- the ticket is silent or ambiguous and your choice changes behaviour a user or QA can see;
- following the ticket would break something, so you changed the behaviour;
- you assumed something that changes visible behaviour (use `--type assumption`).

Do not record pure implementation details with no visible effect.

**Approver:** pass `--approver <name>` only if the user explicitly says who approved it. Never guess a name.

**Superseding:** if your decision replaces an older one, pass `--supersedes <id>`.

**When testing (QA):** before filing a defect, read the ticket and `npx truthtrail list --ticket <KEY>`. Behaviour that matches a decision is not a defect. If that decision is unconfirmed, report "needs confirmation" instead.
