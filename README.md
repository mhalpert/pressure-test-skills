# pressure-test-skills

Three free Claude skills for finding the problems in your work before they cost you. Each skill does one job at a different stage.

| Stage | Skill | Question it answers | What you get |
|---|---|---|---|
| Before you start | `grill-me` | Do we understand this the same way? | A shared-understanding brief |
| Before you decide or send | `board-of-experts` | Is this good enough, and is it the right call? | A verdict, a punch list, and the strongest dissent |
| Before you ship or commit | `red-team` | Where does this break? | A ranked list of defects and fixes |

Use one, or use them in order. Each skill suggests the next one but never runs it on its own.

## Install in Claude Code

Run these two commands in your terminal:

```bash
claude plugin marketplace add mhalpert/pressure-test-skills
```

```bash
claude plugin install pressure-test@pressure-test-skills
```

Then start a new Claude Code session.

## Install in claude.ai or the Claude desktop app

1. Download `grill-me.zip`, `board-of-experts.zip` and `red-team.zip` from the latest release.
2. Upload each file under Customize > Skills.
3. Turn each skill on.

## grill-me

Use this to set up a project. Claude reads what is available, tells you what it thinks the work is, and then interviews you one question at a time. Each question comes with a recommended answer. Claude skips anything that would not change the plan.

- **Say:** "grill me", "interview me", "help me scope this"
- **Or run:** `/pressure-test:grill-me`
- **Depths:** Quick, Full, Research first
- **You get:** agreed goals, the decisions Claude made alone, and the unknowns left open

## board-of-experts

Use this to judge a deliverable or a decision. Claude proposes 5 to 7 experts suited to what you are reviewing, and you approve or swap them. The experts review independently, debate each other, and each gives a verdict. A moderator then writes up where they agreed and where they split.

- **Say:** "convene the board of experts", "get expert opinions", "is this ready for leadership?"
- **Or run:** `/pressure-test:board-of-experts`
- **Depths:** Light (1 round), Standard (3 rounds), Deep (adds a pre-mortem)
- **You get:** a verdict per question, a ranked punch list, and the disagreements you must decide

A seven-seat Standard board runs about 21 separate reviews, so use Light when the stakes are low.

## red-team

Use this to find what is broken in anything concrete enough to break: a product, plan, document, deck or video. Claude proposes 3 to 5 attackers, and you approve or swap them. Each attacker works alone and must back every finding with evidence. A moderator verifies and merges the findings into one ranked list.

- **Say:** "red team this", "tear this apart", "poke holes in this", "stress-test this"
- **Or run:** `/pressure-test:red-team`
- **Optional loop:** you fix the issues, the attackers re-review and rate it ready to ship, for up to 3 loops
- **You get:** ranked defects with severity, location and fix, plus what must not change

The red team reviews read-only by default and applies fixes only with your approval. It covers plans, products and documents. It is not a security penetration test.

## How the panels are chosen

The value of a review comes from who is in the room. Both `board-of-experts` and `red-team` pick their members with two tests:

- **Relevant:** every member must be someone who would credibly review, use or attack this work. A florist does not review a startup pitch deck.
- **Different:** no two members may be interchangeable. They must differ in role, expertise, agenda, incentive and problem-solving method.

A pitch deck might get an early-stage VC, a growth equity investor, a banker, a technologist, a go-to-market lead, a customer and a skeptic. Each one wants something different from it, and that conflict is the point.

## Which skill do I need?

| You want to... | Use |
|---|---|
| Get aligned before work starts | `grill-me` |
| Know whether a plan is the right call | `board-of-experts` |
| Know whether a deliverable is ready | `board-of-experts` |
| Find bugs, gaps or holes in the logic | `red-team` |

If you just say "review this", Claude asks whether you want a judgment or a defect hunt.

## What to expect

The experts and attackers are personas from one model, so they share blind spots. Trust their disagreements more than their agreement. A clean result does not prove the work is sound. You make the final call.

## License

MIT
