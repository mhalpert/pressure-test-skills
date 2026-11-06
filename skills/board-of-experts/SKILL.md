---
name: board-of-experts
description: "Convene a Board of Experts: a panel of 5-7 relevant, deliberately different expert personas, proposed to fit the deliverable, who review it independently and debate it over multiple rounds to judge whether it is good enough and whether the decision is right. Use for strategy memos, pitch decks, plans, proposals, investments, roadmaps, and go or no-go calls. Use when the user says board of experts, expert panel, get expert opinions, second opinion, is this a good idea, is this ready, or review this before it goes to leadership or investors. Not for hunting defects: use red-team when the user asks to red team, tear apart, poke holes in, or stress-test something. Not for scoping new work: use grill-me."
---

# Board of Experts

## What this is and why it works

Most reviews of an important decision fail in one of two ways. They reflect a single point of view, usually the author's, or they collapse into polite agreement. A **Board of Experts** is a panel of sharp, opinionated advisors who review the *same* materials **independently** and then **debate** each other.

The question this skill answers is: **is this good enough, and is it the right call?** The output that matters is the pattern. Where independent experts converge without coordinating, the signal is strong. Where they sharply disagree, the decision-maker has a fault line to resolve.

**State this caveat in every run.** When an AI runs this, the experts are personas from one model. They surface angles and gaps well, but they share priors. Weight their disagreements, and the points they reach independently, far more than their agreement. A human makes the final call.

## When to use it

Use it before a high-stakes or hard-to-reverse decision, or to make sure a deliverable can stand on its own before it goes out.

If the user says only "review this", ask one question: do they want a judgment on whether it is good and right (this skill), or a hunt for what is broken (red-team)?

## How to run it

### Step 0: Frame the review

Pin down and state back:

1. **The deliverable or decision under review.**
2. **Who it is for and what it must achieve.**
3. **The 1-3 guiding questions** the board must answer. If the user gave none, propose a set.

Assemble one **review packet** so every expert sees exactly the same material. Identical inputs make independent convergence meaningful.

### Step 1: Propose the panel

Identify the kind of deliverable, then propose 5-7 experts. Start from `references/panels.md`, and fit each seat to the specifics. Replace any starter seat that does not fit this deliverable or its stage. A seed-stage deck, for example, may not need a banker. For a business or strategy decision, `references/personas.md` has a complete panel.

The panel must pass two tests.

**Relevance: every seat must earn its place.** Each expert must be someone who would credibly be asked to review this deliverable, or who has a real stake in it. A florist or a dentist does not review a startup pitch deck. A VC, a banker, a technologist, a go-to-market lead and a customer do. Do not add a random outsider for novelty.

**Difference: no two seats may be interchangeable.** Compare the seats on five dimensions:

- **Role and context:** where they sit and what they have seen.
- **Expertise:** what they know that the others do not.
- **Agenda:** what they want to happen.
- **Incentive:** how they win or lose from this.
- **Problem-solving method:** how they reason, such as modeling numbers, reasoning from past cases, tracing systems, listening to customers, or testing assumptions.

Two seats that share an incentive and a method are one seat. Replace one. Two investors can both sit on a panel if they want different things, such as an early-stage VC seeking a large outcome and a banker seeking a clean, financeable story.

Every panel must also include:

- **A skeptic:** a seat whose job is disconfirmation.
- **Real conflict:** at least two seats whose incentives pull against each other.
- **An outside voice:** at least one seat from outside the author's side, such as a customer, a buyer, or the person who must carry out the work.

One seat can meet more than one of these requirements.

Show the proposed panel as a table, and mark required seats in the last column:

| Seat | Context and expertise | Agenda and incentive | Method | Why they belong |
|---|---|---|---|---|

Below the table, name the strongest seat you left out, so the user can swap it in. Ask the user to approve or swap seats, and also ask which depth they want (see Modes). Use a multiple-choice question tool if your environment has one, and plain text otherwise. If nobody can answer, for example in an automated run, proceed with the proposed panel and say so in the writeup.

Then write a short brief for each seat, in the style of `references/personas.md`: what they optimize for, what they always ask, their characteristic moves, and the bias to discount. Give each a first name so the debate is easy to follow.

### Step 2: Round 1, independent blind reviews

Each expert reviews the packet alone.

- **If sub-agents are available:** spawn one per persona, in parallel, in a single turn. Give each only its persona brief, the packet, and the guiding questions.
- **Otherwise:** adopt each persona in sequence, and write each review in full before starting the next. A later persona must not reference earlier ones. Say in the writeup that this is less independent.

Each Round 1 review returns, in character and citing specifics:

```
STANCE: <one line>
CONVICTION (1-5): <n>
ASSESSMENT: <2-4 sentences answering the guiding questions>
BIGGEST RISK: <one>
TOP CHANGE: <the single highest-value change>
```

Instruct every persona to reason from its own incentive and method, to disagree where it genuinely would, and never to validate to be polite.

### Step 3: Round 2, debate

Compile a tight digest of all Round 1 positions. Give it to each persona. Each responds:

```
MOVED BY: <whose point sharpened or changed their view, and how>
PUSH BACK: <whom they most disagree with, and the counter>
SHARPENED POSITION: <refined take on the guiding questions>
```

### Step 4: Round 3, converge and rule

Give each persona the state of the debate. Each closes with:

```
VERDICT: <per guiding question: Yes / Qualified yes / No, with a one-clause why>
NON-NEGOTIABLE: <the one change they insist on>
FAULT LINE: <where they land on the main disagreement>
```

### Step 5: Synthesize (moderator)

Step out of the personas and write the synthesis. Lead with what experts reached **independently** and with their **disagreements**, not a vote count. Preserve the sharpest dissent. A lone, well-argued "no" is often the most valuable line. Where a position follows from a persona's incentive, say so, so the reader can weigh it.

## Output format

```
# Board of Experts: [what was reviewed]
## The verdict in one line
## The panel (who sat, and what each one wanted)
## How it was run (guiding questions, rounds, independence method)
## The verdict (per guiding question; small table if useful)
## What the board validated
## Where they converged to sharpen it (punch list, ordered by leverage)
## The live disagreement(s) and how they resolved
## Dissent worth keeping
## Bottom line and recommended next steps
```

End every synthesis with the honest caveat. If the deliverable is close to final, mention once that red-team can hunt for what is still broken. Do not run it unprompted.

## Modes

- **Light:** Round 1 only, then synthesize. Use for low stakes or a quick read.
- **Standard (default):** Rounds 1-3. A seven-seat panel means about 21 separate reviews, so offer Light when the stakes are low.
- **Deep:** add a pre-mortem ("two years later this failed: why?") and require the board to steelman the rejected option before synthesis.

## Doing this well

- Identical inputs, independent reviews.
- Specificity beats vehemence.
- Discount pure contrarianism, including from the skeptic.
- Convergence is suggestive, not proof. The disagreements are where the thinking is.
- The human decides.
