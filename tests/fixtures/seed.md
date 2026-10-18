# CURRENT STATE
scenario: seed (read-only baseline; synthetic fixtures, fictional user Alex)
revision: 0
as of: 2027-05-22 (simulated)
timezone default: America/New_York

## Responsibilities
### R-B: Casey's birthday
- owner: Alex; helper: none
- done means: gift received, or Alex explicitly closes the occurrence with another outcome; excluded: purchasing authority (budget ceiling USD 40, advisory only)
- series: annual, June 12, date-only, no birth year (effective 2027-05-22)
- timezone: America/New_York; lead times: prep 21 days before, check unresolved delivery 7 days before, optional outcome check 1 day after
- pause: none
- people: Casey, Alex's adult sister, June 12, no stated limits
- preferences (confirmed, source, date): none confirmed; context only: Casey likes gardening (fixture, 2027-05-22); no confirmed gift preference
- temporary exceptions (until): none
- sources: none (no external task exists)
- next occurrence: R-B:2027-06-12 (Sat); prep due: 2027-05-22 (delivery check 2027-06-05; outcome check 2027-06-13)

#### Occurrences
- R-B:2027-06-12: status open
  - steps: choose gift: open, arrange delivery: open, receipt: open
  - completion: none
  - last told: none

### R-W: Thursday dinner
- owner: Alex; helper: none
- done means: plan, ingredients, dinner, leftovers, and cleanup for two adults; standard: simple meal, no elaborate cooking; excluded: none stated
- series: weekly Thursday 18:30 local (effective 2027-06-03)
- timezone: America/New_York; lead times: prep 2 days before, check one outcome question at the next agreed check-in after dinner
- pause: none
- people: two adults (Alex and partner), no stated limits
- preferences (confirmed, source, date): both adults eat vegetarian (fixture, 2027-05-22); no medical or allergy facts supplied
- temporary exceptions (until): none
- sources: mock calendar (fixture text, not a connected account), no conflict, last observed 2027-05-22
- next occurrence: R-W:2027-06-03 Thu 18:30; prep due: 2027-06-01

#### Occurrences
- R-W:2027-06-03: status open
  - steps: plan: open, ingredients: unknown, dinner: open, leftovers: open, cleanup: open
  - completion: none
  - last told: none

## Open proposals
- none

## Unresolved conflicts
- none

## Unknown
- ingredients on hand for R-W

## Permissions
- allowed: reasoning, draft options, proposed state deltas in chat
- not allowed: external writes, spending, messages, bookings, routines
- no connected accounts

# LOG
<!-- append-only; one line per write: rev N | date | change -->
rev 0 | 2027-05-22 (simulated) | seeded from PRD §6 fixtures (R-B, R-W; R-I is introduced only in T04). Synthetic only.
