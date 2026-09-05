# Auction-Master Prompt Library

Use these prompts with the `Auction-Master` agent. Replace the bracketed values before sending a prompt.

## 1. Build a Complete Squad

> I have [TOTAL CREDITS] credits and need a squad of [SQUAD SIZE] players. Required composition: [NUMBER] batters, [NUMBER] bowlers, [NUMBER] wicketkeepers, and [NUMBER] all-rounders. My priorities are [TOP PRIORITIES], my risk tolerance is [LOW/MEDIUM/HIGH], and my constraints are [CONSTRAINTS]. Build a staged auction plan using the local data sources. Reserve at least 35% of the budget, assign provisional credit envelopes by role, identify three candidates per slot, and give target, stretch, and pass bid limits. Show the budget after each planned acquisition.

## 2. Powerplay Batters

> Rank the best powerplay batters for my squad. Define powerplay as overs 1–6 and use at least [MINIMUM BALLS] balls faced as the reliability threshold. Weight the ranking [RUN VOLUME]% for powerplay runs, [STRIKE RATE]% for strike rate, [SURVIVAL]% for runs per dismissal, and [CONSISTENCY]% for consistency. Return a top-10 table with runs, balls, dismissals, strike rate, runs per dismissal, confidence, and one risk for each player. Recommend the best target and the point at which I should pass.

## 3. Death-Over Batters

> Evaluate batters for a death-overs role using overs [DEATH-OVER RANGE]. I need a player who can score quickly without spending more than [MAX PLAYER CREDITS] credits. Use phase-specific runs, balls faced, strike rate, dismissal rate, and sample size. Separate proven candidates from small-sample candidates, rank the top eight, and recommend a target, stretch, and pass bid while preserving [RESERVE CREDITS OR RESERVE PERCENTAGE] for later rounds.

## 4. Powerplay Bowlers

> Find the best bowlers for overs 1–6. Rank them using [WICKET WEIGHT]% wicket threat, [ECONOMY WEIGHT]% economy, [CONTROL WEIGHT]% dot-ball or boundary prevention, and [WORKLOAD WEIGHT]% workload reliability. Use only metrics supported by the local data and define every denominator. Apply a minimum of [MINIMUM LEGAL BALLS] legal balls. Show primary options, fallback options, confidence, likely failure mode, and a bid ceiling that does not exceed [MAXIMUM CREDITS].

## 5. Death-Over Bowlers

> I need [NUMBER] death-overs bowlers for overs [DEATH-OVER RANGE]. Compare candidates on wickets, runs conceded, legal balls, economy, boundary prevention, and sample size. Penalize small samples and distinguish specialists from bowlers who only bowled a few death overs. Recommend the best combination of [NUMBER] players, explain whether two medium-cost options are better than one premium option, and retain at least 35% of the starting budget.

## 6. Wicketkeeper Evaluation

> Evaluate wicketkeeper candidates for a squad with [TOTAL CREDITS] credits. Batting requirements: [BATTING REQUIREMENT]. Keeping requirements: [KEEPING REQUIREMENT]. Do not infer wicketkeeper status from batting position or a fielder entry. First identify what keeping evidence exists in the data, then score batting fit and keeping value separately. Mark every candidate as confirmed, unverified, or unsupported, rank the shortlist, and recommend a bid only for candidates whose evidence supports the role.

## 7. All-Rounder Versus Specialists

> Compare these all-rounder candidates: [PLAYER NAMES], against specialist alternatives from the local data. My open roles are [OPEN ROLES], my remaining credits are [CREDITS], and I have [SLOTS] slots left. Evaluate batting and bowling independently, require meaningful samples in both disciplines, calculate replacement value versus specialists, and identify whether flexibility justifies the cost. Recommend the best purchase or the better two-player combination, including target, stretch, and pass decisions.

## 8. Live Auction Decision

> Update my auction plan after this purchase: [PLAYER BOUGHT] for [CREDITS SPENT] credits. Starting budget was [STARTING CREDITS]. Current squad: [CURRENT SQUAD]. Remaining slots and role gaps: [SLOTS AND GAPS]. Recalculate credits remaining, reserve credits, role coverage, maximum safe spend per remaining role, and the next three fallback candidates. Tell me whether my next action should be bid, wait, or pass, and explain the decision using the available evidence.

## 9. Value and Budget Sensitivity

> I am deciding between [PLAYER OR COMBINATION A] and [PLAYER OR COMBINATION B]. I have [CREDITS] credits remaining and need to fill [ROLE GAPS]. Compare their measured performance, sample size, role fit, replacement value, and budget impact. Run at least three scenarios: performance-first, balanced, and budget-preservation-first. Show when the recommendation changes and give a clear pass price for each option without inventing a market price.

## 10. Final Squad Audit

> Audit my proposed squad: [SQUAD LIST]. Starting credits: [STARTING CREDITS]. Credits spent: [SPENT CREDITS]. Remaining credits: [REMAINING CREDITS]. Rules and constraints: [RULES]. Check role coverage, phase coverage, duplicate strengths, major weaknesses, sample-size risks, unsupported role assumptions, and whether the 35% reserve rule is satisfied. Recommend no more than [NUMBER] changes, ordered by expected improvement per credit, and give the next action for each change.

## Prompting Notes

- Always provide the budget, remaining slots, role requirements, and constraints when asking for bid limits.
- Ask for a target, stretch, and pass bid instead of a single maximum price.
- Ask the agent to identify missing evidence when role status, availability, or auction price is not in the data.
- For a live auction, send the current squad and remaining budget after every purchase so the reserve and role envelopes can be recalculated.