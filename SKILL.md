---
name: conseil-agents
description: Runs a council of Claude subagents with distinct roles (independent answers, anonymized cross-review, synthesis) for a hard question, a plan or a decision.
---

# Agent Council

A variant of Karpathy's LLM Council: instead of different models, each role is a Claude subagent with an isolated context. Use this skill when Gab says "run it by the council", "council", or asks for an in-depth review of a question, plan, piece of code or decision.

## Roles (4 by default, 3 if the question is simple)

1. **Expert**: answers on substance with the best technical or domain competence and proposes the solution they judge soundest.
2. **Devil's advocate**: looks for flaws, hidden assumptions, edge cases and reasons the obvious solution would fail.
3. **Verifier**: checks facts, logic, figures and sources; flags anything unverifiable or uncertain.
4. **Pragmatist**: assesses feasibility, cost, time and risk; proposes the simplest version that works.

## Stage 1: independent answers

- Launch all subagents in the same turn, in parallel, with the Agent tool.
- Each agent receives only: the full question, the useful context, its role, and the instruction to answer in 300 words maximum, structured, with a confidence level (low, medium, high).
- No agent sees the others' answers.

## Stage 2: anonymized cross-review

- Replace roles with labels A, B, C, D in random order.
- Relaunch each agent in parallel with the labeled answers (its own included, without telling it which one) and ask for: a ranking from strongest to weakest, the most serious error spotted, and any point everyone missed.
- Limit each response to 150 words.

## Stage 3: synthesis

The main model acts as chairman:

- aggregate the rankings and identify real agreements and disagreements;
- settle each disagreement with a short justification;
- never smooth over a serious objection from the Devil's advocate or the Verifier: if it holds, it changes the conclusion.

## Output format

1. **Verdict**: the recommended answer in one to three sentences, with a confidence level.
2. **Why**: the 3 main reasons.
3. **Remaining risks**: what the council could not resolve.
4. **Divergences**: one line per notable disagreement, with who was wrong and why.
5. **Next action**: a single concrete step.

## Rules

- Address the user as Gab.
- Always give a single final recommendation.
- Limit the number of agents and the length of exchanges to preserve the subscription quota; do not run a second round unless explicitly asked.
- If the question is trivial or simply factual, answer directly without the council and say so in one sentence.
