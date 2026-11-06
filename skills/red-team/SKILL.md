---
name: red-team
description: "Run a red team: a small team of relevant, deliberately different attackers independently hunt for gaps, bugs, and holes in logic in anything concrete enough to break, such as a product, plan, document, deck, or video. Returns one ranked list of evidence-backed defects with severity, location, and fix, with an optional fix and re-review loop. Use when the user says red team, tear this apart, poke holes in this, stress-test this, find what's broken, what did I miss, or where does this fail. Reviews plans, products, and documents; it is not a security penetration test. Not for judging overall quality or a decision: use board-of-experts. Not for scoping new work: use grill-me."
---

# Red Team

## What this is

A red team exists to find what is broken before someone else does. It answers one question: **where does this break?**

It does not decide whether the idea is good. It does not balance strengths against weaknesses. Each attacker works alone, there is no debate, and a moderator merges the results into one ranked list.

**State this caveat in every run.** The attackers are simulated by one model. Their findings are directional, and they share blind spots. A clean result does not prove the work is sound.

## When to use it

Use it on anything concrete enough to break: a working product, a near-final video, a plan, a memo, a deck.

If the user says only "review this", ask one question: do they want a hunt for what is broken (this skill), or a judgment on whether it is good and right (board-of-experts)?

## Safety rules

These rules apply unless the user explicitly says otherwise:

- Review read-only. Do not change live data or production systems.
- Do not make paid calls or send anything to anyone.
- Do not print secrets.
- Apply fixes only with the user's approval.

## How to run it

### Step 0: Frame the attack

Pin down and state back:

1. **The target:** what exactly is under attack, and its scope.
2. **Its job:** who it is for and what it must do.
3. **The evidence:** the real thing wherever possible. Use the running product, the screens, the actual frames, or the full document, not a summary of them.
4. **What counts as failure:** what "broken" means here.

Do not give attackers your own critique or the author's defense. Both anchor the review.

### Step 1: Pick the attackers

Propose 3-5 attackers. Start from `references/attackers.md`, and fit each one to the target. Replace any starter attacker who does not fit.

The team must pass two tests.

**Relevance: every attacker must earn a place.** Each must be someone who would credibly use, judge, or attack this target. A florist or a dentist does not attack a startup pitch deck, unless florists or dentists are its customers. A naive newcomer is relevant only when newcomers are part of the real audience.

**Difference: no two attackers may be interchangeable.** Compare them on five dimensions:

- **Role and context:** where they sit and what they have seen.
- **Expertise:** what they know that the others do not.
- **Agenda:** what they want to happen.
- **Incentive:** how they win or lose if this fails.
- **Attack method:** how they try to break it.

Two attackers that share an incentive and a method will find the same things. Replace one.

Every team must also include:

- **A real user or audience member:** someone from the group the target serves.
- **A specialist:** someone who knows how this kind of thing usually fails.
- **A logic checker:** someone who tests claims, assumptions, and internal consistency. Another attacker can fill this seat if their attack method already tests claims and logic.

One attacker can meet more than one of these requirements.

Show the team as a table, and mark required seats in the last column:

| Attacker | Context and expertise | Agenda and incentive | Attack method | Why they belong |
|---|---|---|---|---|

Below the table, name the strongest attacker you left out, so the user can swap them in. Ask the user to approve or swap attackers. Use a multiple-choice question tool if your environment has one, and plain text otherwise. If nobody can answer, for example in an automated run, proceed with the proposed team and say so in the report.

### Step 2: Independent attacks

- **If sub-agents are available:** spawn one per attacker, in parallel, in a single turn. Give each only its brief, the evidence, and the safety rules.
- **Otherwise:** adopt each attacker in sequence, and write each report in full before starting the next. A later attacker must not reference earlier ones. Say in the report that this is less independent.

Each attacker stays in character and returns ranked findings, at most 10:

```
FINDING: <the defect in one sentence>
EVIDENCE: <the quote, screen, timestamp, number, or step that shows it>
LOCATION: <where it is>
SEVERITY: Critical / High / Medium / Low
WHO IT HURTS: <who feels this, and how>
FIX: <the smallest change that resolves it>
```

Then each attacker adds one line: **KEEP: the one thing that must not change.** This stops fixes from destroying what works.

Tell each attacker: report only real problems. If you find nothing serious, say so. Do not invent problems to look useful.

### Step 3: Merge and verify (moderator)

Step out of the attackers and write one list:

1. **Drop** any finding with no evidence.
2. **Verify** each Critical and High finding against the evidence yourself. Mark any you could not verify.
3. **Merge** duplicates, and record who found each one. A defect found by two attackers independently ranks higher.
4. **Rank** by severity, then by how many people it hurts.

Severity scale:

- **Critical:** the target fails at its job, or causes real harm.
- **High:** a main path or central claim fails for many people.
- **Medium:** a real problem with a workaround, or one that affects few people.
- **Low:** polish.

## Output format

```
# Red Team: [target]
## Bottom line (the worst problem, in one sentence)
## The team (who attacked, and how)
## Findings (table: rank, severity, finding, evidence, location, found by, fix)
## Patterns (root causes behind several findings)
## Dropped or unverified findings
## Keep (what the attackers said must not change)
## Not tested (what this review could not reach)
```

End every report with the caveat. Do not give an overall score or a verdict on the idea. If the user needs that judgment, mention once that board-of-experts can do it, and do not run it unprompted.

## Optional: fix and re-review loop

Offer this after the report. Run it only if the user agrees.

1. Agree which findings to fix, and record any declined finding with a reason.
2. Make the fixes, or let the user make them.
3. Give the same attackers the changed target and the list of fixes.
4. Each attacker confirms each fix and rates the target: **ready to ship, yes or no**, with reasons.
5. Stop when every attacker says yes, or after 3 loops.

## Doing this well

- Test the real thing. A review of a description finds description problems.
- One specific, evidenced defect beats ten vague concerns.
- Say what you could not test.
- The human decides what to fix.
