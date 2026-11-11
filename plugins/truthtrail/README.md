# TruthTrail for Claude Code

When Claude asks you "A or B?" and you answer, that decision usually disappears into the chat. The ticket never changes, and later QA files a "bug" against behaviour you chose on purpose.

TruthTrail lets Claude **record those decisions itself**, next to your code in `.decisions/`.

## Install

In Claude Code, run these one at a time (not pasted together):

```
/plugin marketplace add truthtrail/claude-plugin
```

```
/plugin install truthtrail@truthtrail
```

## What you get

- **MCP tools:** `record_decision`, `list_decisions`, `why`, `check_branch`, `list_pending` and `resolve_pending`. Claude saves a decision right after you answer.
- **At session start:** Claude loads the decisions already made for the ticket in your branch name (e.g. `feature/JIRA-231-…`) and follows them.
- **Before Claude stops:** if you answered questions that were never recorded, Claude asks whether to record or dismiss each one.
- **Rules (skill):** record only behaviour a user or QA can see, never guess who approved, and mark guesses as assumptions.

Everything stays in your repo. No account, no server, no AI calls of our own.

## Also using Cursor or Copilot?

Run `npx truthtrail init` in the repo. It writes MCP config for Cursor (`.cursor/mcp.json`), Copilot (`.vscode/mcp.json`) and Claude Code (`.mcp.json`), and adds the rules to `AGENTS.md`.

If you use both this plugin and `init`, Claude Code shows the TruthTrail tools twice. Both work, but you can run `npx truthtrail init --no-mcp` to avoid the duplicate.

## More

- CLI and docs: https://www.npmjs.com/package/truthtrail
- License: MIT
