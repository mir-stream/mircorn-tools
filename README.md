# mircorn-tools

Claude Code plugin marketplace.

## Plugins

### advisor-crew

Advisor/Implementer/Reviewer role system for Claude Code:

- **Advisor** — the main session. Focuses on judgment: requirements analysis, task decomposition, design decisions, briefs, verification, and final approval. Injected via a `SessionStart` hook so subagents never see (or misread) the role instructions.
- **implementer** — subagent that writes code and tests per the Advisor's brief. Never commits; goes `BLOCKED:` instead of improvising when the brief conflicts with reality.
- **reviewer** — adversarial reviewer (적대리뷰) spawned fresh each round. Tries to break the change; verdict is `PASS` / `NEEDS_CHANGES` with `file:line` findings and concrete failure scenarios.

Briefs must state the **intent** of a change; both subagents work against that intent, not just the letter of the instructions.

## Install

```
claude plugin marketplace add mircorn/mircorn-tools
claude plugin install advisor-crew@mircorn-tools
```

Disable per project with `.claude/settings.local.json`:

```json
{ "enabledPlugins": { "advisor-crew@mircorn-tools": false } }
```
