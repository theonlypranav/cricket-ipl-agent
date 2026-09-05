---
name: "Auction Evaluation Workflow"
description: "Use when evaluating cricket auction candidates, ranking batters, bowlers, wicketkeepers, or all-rounders, building a squad, setting bid limits, or managing auction credits incrementally from local data sources."
---

# Auction Evaluation Workflow

Use this instruction with Auction-Master. Build the strongest feasible squad without spending the available credits in one move.

## Staged Workflow

1. **Capture requirements:** total credits, squad size, role quotas, team or overseas limits, venue or phase priorities, scoring rules, and risk tolerance. Ask only for requirements that could change the decision; otherwise state assumptions.
2. **Inspect evidence:** check schemas, missing values, duplicate records, naming consistency, date range, and sample size before ranking.
3. **Apply hard filters:** remove candidates failing explicit role, team, availability, budget, or roster constraints.
4. **Build a broad shortlist:** keep at least three candidates per required slot when possible; label primary, fallback, and speculative options.
5. **Set a bid ceiling:** base it on role fit, confidence, replacement quality, and remaining squad needs. Do not invent market prices.
6. **Spend incrementally:** recommend an opening bid or bid band, not an automatic maximum. After every purchase, recalculate credits, slots, role coverage, and fallbacks.
7. **Pass when marginal value falls:** do not chase a player when the next bid reduces flexibility more than it improves the squad.

## Credit-Control Policy

Unless the user provides different rules:

- Reserve at least **35%** of starting credits for the late auction and unforeseen gaps.
- Spend no more than **25%** of starting credits on one player unless the player fills a scarce, high-confidence requirement and concentrated risk is accepted.
- Create role-specific credit envelopes before bidding. Transfer credits only when a role is filled or its fallback pool is demonstrably strong.
- Never spend reserve credits on a speculative candidate.
- Use three bid states: **target**, **stretch**, and **pass**.
- After each purchase report credits spent, credits remaining, percentage remaining, slots left, role gaps, and the next fallback.
- Prefer two complementary players over one expensive player when their combined marginal value is higher and the squad remains balanced.

## Role Evaluation Logic

Normalize metrics within the relevant candidate pool, state weights, and enforce a minimum sample. Never rank on one metric alone.

### Batters

Evaluate runs and phase-specific runs, strike rate with its denominator, runs per dismissal or average, phase fit, and consistency across matches or seasons. Default score: **40% phase runs, 30% strike rate, 20% survival, 10% consistency**. For a pure finisher, shift weight from survival to death-overs strike rate.

### Bowlers

Evaluate wickets or wickets per legal ball, economy using runs conceded and legal balls, dot-ball and boundary prevention, phase fit, and workload. Default score: **35% wicket threat, 30% economy, 20% phase fit, 15% control or workload reliability**. A high wicket rate from a tiny sample is speculative.

### Wicketkeepers

Evaluate batting with the batter model and keeping evidence separately: catches, stumpings, dismissals, or explicit keeper metadata. Do not infer keeper status from a fielder appearance or batting position. If keeper evidence is absent, label the recommendation unverified and lower confidence. When both dimensions exist, default to **60% batting fit and 40% keeping value**.

### All-rounders

Evaluate batting and bowling independently, then combine only with reliable identity and role evidence. Measure dual contribution, replacement value versus specialists, lineup flexibility, and risk of a part-time sample. Default score: **40% batting, 40% bowling, 20% flexibility or replacement value**. Require meaningful samples in both disciplines or classify the player as part-time.

## Scoring and Bid Logic

Use:

`fit score = weighted role metrics - risk penalty`

Penalize small samples, missing role confirmation, inconsistent names, unavailable economics, and proxy metrics. Do not convert fit directly into credits without a budget model.

Use:

`bid ceiling = role envelope x fit confidence x scarcity adjustment`

Fit confidence is high, medium, or low and reflects evidence quality. Scarcity adjustment is valid only when few credible fallbacks remain. Show sensitivity when the answer changes under different weights.

## Required Output

Return:

1. **Decision:** next player or action, with target, stretch, and pass prices only when a budget is supplied.
2. **Shortlist:** rank, role, measured metrics, sample size, fit, confidence, and fallback status.
3. **Budget state:** spent, remaining, reserved, slots left, and role gaps.
4. **Why:** scoring logic and requirements satisfied.
5. **Risk:** the most likely failure mode.
6. **Next move:** next candidate or bid trigger.

## Evidence Boundaries

- Use `most_runs_average_strikerate.csv` for aggregate batting comparisons.
- Use `deliveries.csv` for custom batting, bowling, phase, dismissal, and ball-level calculations.
- Use `matches.csv` for match, venue, result, and player-of-the-match context.
- Use `teamwise_home_and_away.csv` for team venue splits, not individual player skill.
- Inspect `Players.xlsx` before relying on its sheets or columns; its schema is not assumed.
- Do not invent prices, availability, injuries, roles, salaries, current-season facts, or keeper status.
- Separate observed metrics, derived metrics, assumptions, and inference.
