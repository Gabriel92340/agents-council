# agents-council

A Claude Code skill that runs a council of Claude subagents with distinct roles, inspired by Karpathy's LLM Council. No API key needed: it runs inside Claude Code on your existing subscription.

## How it works

1. **Independent answers**: Expert, Devil's advocate, Verifier and Pragmatist answer in parallel, each in an isolated context.
2. **Anonymized cross-review**: answers are relabeled A, B, C, D and each agent ranks them and flags the worst error.
3. **Synthesis**: the main model acts as chairman and returns one verdict, remaining risks, divergences and a next action.

## Install

```
git clone https://github.com/Gabriel92340/agents-council ~/.claude/skills/conseil-agents
```

Or per project:

```
git clone https://github.com/Gabriel92340/agents-council .claude/skills/conseil-agents
```

## Use

In Claude Code, say: `run it by the council: <your question>`.

## Notes

- Same model for every role, so errors can be correlated; the gain comes from role and context diversity plus critique.
- Uses 3 to 4 subagents and a single round to preserve subscription quota.
