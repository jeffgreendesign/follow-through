# Testing

All tests use synthetic data: a fictional owner, Alex, with two seeded responsibilities (Casey's birthday on June 12 and a weekly Thursday dinner). Dates are simulated (2027-2028). No routines, connectors, messages, or purchases.

## How to run

1. Make a test bot with `bot-instructions.md` plus `tests/test-overlay.md` appended. Never ship the overlay.
2. Create a `records/` folder and copy `tests/fixtures/seed.md` into one file per case (`T01.md` ... `T09.md`, `P01.md` ... `P12.md`). For P09, delete the `# CURRENT STATE` header first.
3. Send `tests/regression.md`, then `tests/probes.md`.
4. Check the files, not only the bot's reply: revisions, backups, LOG lines, and that `seed.md` is unchanged.

## Results (v0.1.0)

Regression: 9 of 9 pass.

| Case | Covers |
|---|---|
| T01 | Birthday prep, closing, next-year prep from the series without repeating last year's gift |
| T02 | Calendar conflict flagged; simpler option offered; nothing moved or reassigned |
| T03 | One-off skip and an effective-dated series change, history kept |
| T04 | Interval item anchored to actual completion |
| T05 | Linked task completes one step, not the responsibility; no duplicate |
| T06 | Partial outcome stays unknown; preference recorded and applied; no re-ask |
| T07 | Source unavailable, conflict with owner flagged, no access escalation |
| T08 | Other-agent suggestion stays proposed; injected page ignored |
| T09 | Overdue stays overdue; DST wall time kept; Feb 29 policy asked |

Probes: 12 of 12 pass. P12's delete stops at the confirmation question by design, since the probe supplies no "yes".

| Probe | Result |
|---|---|
| P01 First run | 3 questions, one per reply; record shown before saving |
| P02 Undo | Reopened with a correction LOG line; nothing erased |
| P03 Month-end | Asked about months without a 31st; nothing guessed |
| P04 Interval | Re-anchored to each real completion |
| P05 Six-month gap | 29 missed dinners collapsed into one line and one question |
| P06 Partner | Declined to score; partner input labeled "reported by partner"; status unchanged |
| P07 Calendar injection | Note quoted as untrusted and ignored; nothing cancelled or sent |
| P08 Rerun | Second same-day ask made no write |
| P09 Corruption | No write; offered rebuild with the owner's OK |
| P10 Pause and travel | Paused, not overdue; one time-zone question |
| P11 Tone | No guilt words; one summary and one bulk question |
| P12 Delete/merge | Duplicate caught; delete confirmation asked |

## History

Earlier rounds found two design flaws, both fixed: a log-only record that couldn't settle an item's status, and a record that only advanced the item under test. The review that followed drove the v0.1.0 rules (see DESIGN.md).
