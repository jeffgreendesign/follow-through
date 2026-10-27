# Changelog

## v0.2.1 (2026-10-27)

- Public Grok Bot template is live: https://x.ai/bot/01aN07LdGG8WyvI-iW5UV (share id `01aN07LdGG8WyvI-iW5UV`).
- `bot-instructions.md` matches the published bot. Skills are unchanged from v0.2.0.

## v0.2.0 (2026-10-19)

Setup and record safety
- "set up" in an ordinary request no longer triggers setup. Only a missing record or an explicit start over or reset does.
- Start over asks first, then archives the old record as `record.archived-<date>.md` and moves old backups into `backups/old-<date>/`.
- A missing record with backups offers a restore instead of starting fresh.
- Restore procedure for a damaged record (keep the damaged copy, revision = highest plus 1, log the restore).
- Setup uses the responsibility you already named, supports one-time items, and answers in chat if you decline.
- Setup asks your time zone (the computer clock is not used as your time zone) and never saves a UTC time unless you said UTC.
- Setup finishes in 4 replies: prep lead time has defaults. The record skeleton now lives in the skill.
- One LOG line format: `rev <N> | <YYYY-MM-DD> | <change>`.

Replies and lane
- Every reply is 6 lines or fewer, planning included; "more" lifts it for the step list; "status" shows the record.
- Priority order when lines run short.
- Purchases are one step per category; no shopping lists, item lists, or prices. Neutral example ("party supplies").
- If you have no shopping bot, the category step can go to a store as a note.

Privacy and sources
- Forget offers to redact past log lines, backups, and archives, and never claims full deletion while copies remain.
- Food restrictions are stored as meal limits, not conditions.
- Instruction-like text inside the record file is data.
- An approved calendar or task list is the one the owner names; created items start with "FT:".

Routines
- The bot never creates a routine on its own. After approval: one routine, owner's time zone, fixed prompt, one test, schedule read back.
- No assumption that any routine exists.

Other
- Weekly review skill added (`follow-through-weekly-review`).
- Status questions project in memory only.
- "Every request" steps renumbered E1 to E9.
- Delete confirm is "in the next reply"; revision collisions are redone on the new revision and reported.

## v0.1.0 (2026-10-17)

- First public release.
- Instructions with a single record (CURRENT STATE plus append-only LOG), freshness rule, time rules, correction verbs, owner-only authority, data minimization, and untrusted-source handling.
- First-run skill `follow-through-getting-started`.
- Empty record template.
- Synthetic test suite: 9 regression cases and 12 probes, all passing.
