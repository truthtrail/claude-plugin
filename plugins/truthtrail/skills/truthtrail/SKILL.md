---
name: truthtrail
description: Use when implementing or testing a ticket in a repo that uses TruthTrail — records product decisions and assumptions with npx truthtrail.
---
## TruthTrail: recording decisions

This repo records product decisions with TruthTrail: in `.decisions/`, or, when you are logged in (`npx truthtrail login`), on the TruthTrail server and the Jira ticket, where the reporter confirms or rejects them. Follow these rules.

**Find the ticket.** Take the ticket key from the branch name (e.g. `feature/JIRA-231-…` or `ABC-1234/login`). If there is none, ask the user once and remember it with `set_ticket` (or `npx truthtrail ticket <KEY>`). TruthTrail shows the ticket's title; if it doesn't match the task, stop and ask the user for the right ticket. To fix a decision recorded on the wrong ticket, use `move_decision` (or `npx truthtrail move <id> <KEY>`).

**Tools.** If TruthTrail MCP tools are available (`record_decision`, `list_decisions`, `why`, `check_branch`, `list_pending`, `resolve_pending`, `withdraw_decision`, `set_ticket`, `move_decision`), use them. Otherwise use the `npx truthtrail` commands below.

**Before you implement,** run `npx truthtrail list --ticket <KEY>` and follow the decisions it shows. Treat `rejected` ones as must-rework: change the code, then record a new decision with `--supersedes <id>`.

**Record a decision** with `npx truthtrail decide` when:
- the ticket is silent or ambiguous and your choice changes behaviour a user or QA can see;
- following the ticket would break something, so you changed the behaviour;
- you assumed something that changes visible behaviour (use `--type assumption`). Anything you chose without the user answering is an assumption, even a well-reasoned one; use `decision` only for what the user answered or told you. If you add details the user didn't choose, record them as a separate assumption.

Do not record pure implementation details with no visible effect.

**Approver:** pass `--approver <name>` only if the user explicitly says who approved it. Never guess a name.

**Superseding:** if your decision replaces an older one, pass `--supersedes <id>`.

**When testing (QA):** before filing a defect, read the ticket and `npx truthtrail list --ticket <KEY>`. Behaviour that matches a decision is not a defect. If that decision is unconfirmed, report "needs confirmation" instead.
