# Design

## Goal

Help one owner keep agreed household responsibilities across weeks and years: remember each recurrence and prep window, prepare useful options, follow through, and review outcomes. It is a simple scheduler, but a lot can go wrong: false completions, nagging, partner dynamics, stale state, and untrusted inputs. Most of the rules exist to prevent those.

## Key decisions

- **One record, two parts.** CURRENT STATE at the top answers every status question; the append-only LOG keeps history. An early version kept only a log, and a reopen test showed the bot couldn't tell whether a birthday was "received" or "overdue". CURRENT STATE wins for status, unless its revision is older than the newest LOG line; then it is treated as corrupt and rebuilt from the LOG only with the owner's OK.
- **Freshness on every write.** Every responsibility is advanced to the as-of date on each write, not just the one asked about. A second reopen test found a dinner still showing a date two weeks in the past because only the tested item had been updated. Opening a stale record triggers a projection, and the bot says what it projected. More than 4 missed occurrences collapse into a count and one question.
- **Single source for schedules.** Series rule, time zone, lead times, owner, done definition, and pause live only in CURRENT STATE. Superseded rules move to the LOG.
- **Steps and evidence.** An occurrence has steps (chosen / bought / delivered / received). Done requires its done definition and evidence: the owner's word or a linked source.
- **Safe writes.** Revision check, backup (last 10), update, one LOG line, read back. A damaged file is never written.
- **Owner-only authority.** Partner input is "reported by" until the owner confirms. Proposed transfers of a duty need both people.
- **Restraint.** Default reply 6 lines or fewer, one question at most, outcome questions asked once and dropped after two tries, no guilt or urgency words.
- **No routine shipped.** The rules for any future routine (speak only when newly due or changed; same-day rerun produces nothing; stop reads back the scheduler) are in place, but enabling one needs owner approval.
- **Time zone default** is the computer's zone, confirmed during setup.

## Review findings and fixes

A combined user-experience and agent-experience review found 27 issues (4 blocker, 9 high, 9 medium, 5 low). All blockers and highs are fixed in v0.1.0:

| Finding | Fix (rule in bot-instructions.md) |
|---|---|
| B1 Record path hardcoded to a test folder | Per-bot record path; missing file runs setup (7) |
| B2 No first run | getting-started skill, empty record template |
| B3 Time rules lived only in the spec | Time block (20-29) |
| B4 Test-only text mixed into instructions | Moved to `tests/test-overlay.md` |
| H1 Schedule stored in two places | CURRENT STATE only (10) |
| H2 No undo / rename / delete / merge | 30-32 |
| H3 Partial completion and evidence | Steps and completion fields (10-11) |
| H4 No reminder ledger or idempotency | "Last told" per occurrence; quiet reruns (10, 45) |
| H5 Re-ask cadence | Ask once, stop after 2 (43) |
| H6 Calendar/task text injection | Source text is data (36) |
| H7 Partner messaging the bot | "Reported by", owner confirms (33) |
| H8 Third-party privacy | Data minimization, list/forget (34-35) |
| H9 Freshness not regression-tested | Full rerun, see TESTING.md |

Mediums and lows (reply cap, gap summaries, travel, log rotation, concurrent writes, backups, conflict rule, source failure, label, one-question rule, numbered workflow, evidence definition, manual-mode stop wording) are also addressed.

## Known limits

- Only tested on synthetic data in chat.
- The per-bot record folder is a convention; bots on a shared computer could read each other's files.
- Recurrences it can't express exactly ("second Tuesday", "every spring") are saved as manual with a review date.
