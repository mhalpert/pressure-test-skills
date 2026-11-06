---
name: grill-me
description: "Interview the user to reach a shared understanding before work starts. Use at project setup, or before design, planning, analysis, or implementation, when misaligned premises would cause rework. Grounds in available materials first, asks only material questions one at a time with a recommended answer, and ends with a read-back brief. Three depths: quick, full, research first. Use when the user says grill me, interview me, help me scope this, make sure we're aligned, or ask me questions before you start. Not for reviewing finished work: use board-of-experts to judge a deliverable and red-team to find what is broken."
---

# grill-me

Reach a shared understanding sharp enough to start work without causing rework from misaligned premises. The bar is **no major rework from things knowable in this conversation**. Drift caused by genuinely unknowable factors — things that only emerge from building, shipping, or testing — is acceptable.

This skill is not about being thorough. It is about being *correct cheaply*.

---

## 1. Pick the depth

Three depths. Users may also call them by their kitchen names: light, well-done, and extra crispy.

- **Quick** — user wants best judgment and momentum. Ground, name the load-bearing assumption, ask only questions that would block starting or cause user-visible rework. Skip most dimensions unless something forces them. Disclose meaningful calls in the read-back.
- **Full** — full sweep across all dimensions in §3. Stop only when remaining unknowns are either immaterial or unknowable-without-building.
- **Research first** — full **plus pre-flight grounding research** before the interview. Use when the topic is in a fast-moving domain where your training cutoff is a structural risk (recent frameworks, just-launched products, emerging open-source projects, current internal company decisions). See §2 for how to run the research phase.

Infer the mode from cues:
- **Quick:** *light, prototype, rough, explore, see what it looks like, just try, quick*
- **Full:** *well-done, design, spec, plan, we're going to ship, this matters, grill me*
- **Research first:** *extra crispy, research first, ground yourself first, what's out there, what exists already, state of the art, latest, cutting edge, recently launched, what's new in*

If unclear, ask once. Default when truly unspecified: **full**.

**Self-initiated upshift.** If your initial grounding reveals you're likely out of date on the subject (newer-than-training repos, products, frameworks, or internal decisions you don't have access to), *propose* moving up to research first before asking interview questions — don't silently guess. Reversibility also informs mode: irreversible work (production deploys, public launches, one-way migrations) should default to full at minimum even without explicit cues.

Mode is mutable. If quick surfaces production stakes, offer to go deeper. If full reveals the question is trivial, offer to go lighter.

---

## 2. Ground first — always

Before asking any interview question, read what's already available and produce a **visible synthesis** in 4–8 lines:

- What you understand the work to be
- What materials you used to ground
- The single load-bearing assumption you're betting on

The synthesis is visible — printed in the response — so the user can correct your grounding in one move instead of through five misaligned questions.

If grounding surfaces a contradiction or a premise that looks wrong, **raise it before asking questions**. Don't dutifully interview about a plan you already think is broken.

### Grounding sources, in order

1. **In-conversation materials** — the user's current message, prior turns, any pasted/referenced content.
2. **Local context** — project docs, codebase, CLAUDE.md, repo READMEs, and any saved memory. Pay particular attention to entries about the user's role and expertise — they shape what counts as material in §3.
3. **Internal/private context (Research first only)** — *before going to public web research, ask the user once:* "Is there internal context I should pull from first — Notion page, company GitHub repo, Slack channel, Linear ticket, prior project doc?" Then ground there using whatever connector or tool is available. If none is available, ask the user to paste what matters. Internal context almost always beats public context for a user's real work.
4. **Public web research (Research first only)** — once internal sources are exhausted or shown empty, timebox public research (~5 minutes / a handful of searches). Look for current repos, libraries, products, and last-6-months activity in the space. **Breadth-first**, not depth-first — you're finding the landscape, not the perfect answer. The interview is where we converge.

In research first depth, the visible synthesis also includes a **"What I learned from research"** section listing what you found (and roughly when published), so the user can correct or fill gaps before the interview starts.

If there's nothing to ground in (greenfield, no docs, no internal context, not research first), say so and proceed.

---

## 3. Filter questions for materiality

Before each question, self-check:

- Does the answer change something the **invoking user** will personally live with — or something a **downstream stakeholder** (their team, end users, customers, ops, audience) will feel? Material = changes UX, cost, scope, methodology, assumptions, time-to-ship, lock-in, risk surface, or a decision the user will own and defend.
- If the answer doesn't change something the invoking user lives with — they're not the one writing the code, maintaining the model, defending the methodology, presenting the deck — **decide it yourself** and disclose in the read-back. Do not perform indecision.

**Materiality is role-dependent.** A framework choice is below-grain for a PM but material for the engineer who will maintain it. A discount-rate assumption is material for a financial analyst but below-grain for the executive consuming their report. A random-seed value is below-grain for a data scientist who runs the notebook but material for the reviewer auditing reproducibility. The skill doesn't need to enumerate what's material per domain — apply the "lives with it" test and the answer falls out.

### Read the room before deciding what's material

Don't ask the user their role outright — that's friction. Infer from signals:

- **Memory** — entries about role and expertise (strongest signal once recorded). You should have already pulled this in §2 grounding.
- **Vocabulary fluency** — domain-fluent language tells you what layer they live at. "Use Postgres with a materialized view" → engineer. "Lever this at 2.5x EBITDA" → finance. "Control for selection bias in the lift estimate" → data science. "Users should see fresh numbers without a delay" → PM / business.
- **Grain of the ask** — outcome-language ("ship a feature that lets users do X", "give me a valuation range") vs. mechanism-language ("design the auth flow", "specify the regression model") tells you which layer they operate at.
- **Where they invite or resist judgment** — "use your judgment on the technical stuff" is hands-off; "let's talk through the architecture" is hands-on.
- **Artifact in front of them** — `.xcodeproj` / `package.json` / `Cargo.toml` → engineer; `.xlsx` / financial model → analyst; `.ipynb` / notebook / `.parquet` → data scientist; Markdown brief / Figma / slides / Notion → likely PM, strategy, or marketing.

Signals can be mixed or sparse. Lean on your best read and rely on the **read-back as the safety net** — every decision you made on your own is disclosed by name, so a misread costs one round of correction, not silent rework. If the user redirects ("back up, I do want to weigh in on that"), recalibrate for the rest of the interview.

Then pick the sharpest next question by asking: which dimension is most under-specified *and* most load-bearing right now?

- **Goal** — what we are actually trying to achieve
- **Scope / audience / scale** — who is this for, how many, at what size, by when (single user vs. team vs. public; prototype vs. shipping; 1 pie vs. 25 servings; today vs. next quarter)
- **Reversibility / stakes** — one-way door (production deploy, public launch, irreversible migration) or two-way (prototype, sandbox)? This sets how much rigor is warranted *and* informs whether the mode should upshift
- **Success** — what done looks like
- **Failure** — what the bad outcome looks like
- **Anti-patterns** — what we explicitly do not want (preference-driven)
- **Constraints** — external hard limits we cannot cross (budget, deadline, must-use or must-not-touch tech, regulatory, brand, contract)
- **Data, benchmarks, prior art** — what sources of truth or comparables exist, *and* what the user has already tried that didn't work, or what exists internally
- **Analogies** — what comparable situations or frameworks apply

At **quick** depth, ask only if the answer would block starting or cause user-visible rework. At **full** and **research first** depth, ask whichever dimension is weakest, repeatedly, until the stopping rule fires.

---

## 4. Ask one at a time, with a recommended answer

- **One question per turn.** No batched lists.
- **Always offer your recommended answer** with the trade-off in one or two lines. Force the user to react, not brainstorm cold.
- Use a multiple-choice question tool, if your environment has one, when there are 2–4 concrete options worth comparing. Otherwise list the options in plain text.
- Use **prose questions** when the answer is naturally narrative (the user may dictate a long reply).
- Don't force structured options when the real answer is a paragraph.

---

## 5. Stop when further questions wouldn't change the plan

Not a count cap — a **relevance cap**. Stop when:

- Remaining unknowns are immaterial (engineer-internal or low-stakes), **or**
- Remaining unknowns are unknowable until something is built or tested.

If you find yourself asking a question to be thorough rather than because the answer would change what you do next, **stop**.

---

## 6. Read back before acting

Synthesize a closing artifact with three explicit sections:

**What I now believe** — the goal, the load-bearing assumption you're betting on, and what you're explicitly *not* optimizing for. In research first depth, also restate the key research findings you're relying on.

**Decisions I made on my own** — engineer-internal or low-stakes choices, named specifically (not "I made some choices"). At **quick** depth this section is load-bearing — be honest and specific, because it's the only checkpoint.

**Deferred unknowns** — things we'll only resolve by building or testing. This is the user's insurance against acceptable drift later, and your insurance against being surprised by it.

End with: **"Ready, or correct me."** Then start.

---

## 7. Keep the brief and hand off

Offer to save the read-back as a short brief in the project, so later sessions start from the same understanding. Save it only if the user agrees.

When the work later produces something to review, mention the next step once and do not run it unprompted:

- **board-of-experts** judges whether a deliverable is good enough and whether the decision is right.
- **red-team** hunts for what is broken.

The brief makes a good input for both.
