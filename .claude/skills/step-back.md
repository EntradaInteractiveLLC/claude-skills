---
name: step-back
description: "When stuck on a coding/debugging problem, step back and generate 5 hypotheses ranked by likelihood before touching any code or proposing fixes. Prevents doom loops. Use when spinning on a bug, after 3 failed fix attempts, or when the problem is complex or intermittent."
keywords: debug, stuck, hypotheses, root cause, troubleshooting, step back, doom loop
allowed-tools: Read, Write, Edit, Bash, Test
source: https://github.com/EntradaInteractiveLLC/claude-skills
author: tevans@entradainteractive.com (@lordsnave on X)
---

# Step-Back Debugging Skill

## When to Activate This Skill
Use this skill automatically (or invoke with "/step-back") whenever:
- I'm spinning in circles / trying random fixes
- Previous attempts failed or created new issues
- The problem is complex, intermittent, or non-obvious
- I say "I'm struggling" or "keep failing to solve"
- I've tried 3+ fix attempts with the same symptom

## Core Instruction (Always Follow This Exact Workflow)
1. **Step Back** — Immediately stop any current fix attempts. Acknowledge: "Stepping back to avoid the doom loop."
2. **Generate 5 Hypotheses** — List exactly 5 distinct, plausible root causes. For each:
 - Write a clear mechanistic explanation (how/why it would cause the observed behavior).
 - Rate likelihood (1-10 scale) with a one-sentence justification based on the evidence so far.
 - Note what specific evidence would confirm or falsify it.
 - Categorize it (see Required Categories below).
3. **Prioritize & Plan** — Rank the 5 hypotheses from most to least likely. Suggest the minimal, targeted next step (logs, test, file inspection, reproduction) for the top 1-2 only. Do NOT propose code changes yet.
4. **Evidence-First Loop** — After I provide evidence or approve a step, re-evaluate only the relevant hypotheses. Update likelihoods and repeat until we have a confirmed root cause. If 3 attempts yield the same symptom, go back to Step 2 and generate 5 NEW hypotheses that assume your previous mental model is wrong.
5. **Only Then Fix** — Once a hypothesis is validated with evidence/reproduction:
 - Implement the minimal fix.
 - Verify the fix with the SAME evidence method that confirmed the bug.
 - If applicable, write a test that prevents regression.
 - Document the root cause and why the other hypotheses were wrong.

## Required Hypothesis Categories

Every set of 5 hypotheses MUST include at least one from each of these categories:

**Wrong location**: You are looking at or modifying the wrong thing entirely. The bug is in a different file, function, config, layer, or system than you think. The code you're changing isn't what's actually executing.

**Wrong assumption**: Your mental model of how the system works is incorrect. A guard, condition, cache, or indirection means the code path is different from what you expect. Something you believe is true about the environment, state, or data flow is false.

**Wrong evidence**: The symptom is misleading you. The error message points somewhere other than the real cause. You're reading stale output, cached results, or a different copy than you think.

**Mandatory Hypothesis #3**: "My change is not taking effect at all." This MUST always be one of your 5 hypotheses. It is the #1 cause of "I changed it but nothing happened." Check: Is there a cache, build artifact, intermediate layer, deployment step, or restart required between your edit and the running system? Is the file you edited actually the one being used?

## Verification Checklist (Mandatory After Every Fix Attempt)

After any fix attempt, ALWAYS verify before declaring success:
- Was the change actually saved and applied? (read it back, check timestamps)
- Did the change reach the running system? (rebuild, redeploy, restart, cache clear - whatever applies)
- Is the observed behavior actually different now? (use the same diagnostic that revealed the bug)
- If ANY of these checks fail, your fix was not applied. Do not try a different fix - figure out why this one didn't take effect.

## Bail-Out Rule

If you have tried 3 fix attempts and the symptom is identical each time, you are modifying the wrong thing. STOP. Return to Step 2 and generate 5 completely new hypotheses that assume your entire mental model of the problem is incorrect. Consider:
- Am I editing the right file / the right system?
- Is this code even in the path that's executing?
- Is there a cache, layer, proxy, or intermediary between my edit and what's running?
- Is the error actually coming from where I think it is?

## Output Format (Strict)
Always respond in this structure:

**Step Back Acknowledged**
**Top 5 Hypotheses**
1. [Category: X] [Hypothesis] — Likelihood: X/10 — Justification: ...
 Confirmation evidence: ... | Falsification: ...

**Prioritized Investigation Plan**
- Start with Hypothesis #X because...
- Next action: [specific, minimal command/test/log request]

Never skip steps 1-3. Never jump straight to a fix.
