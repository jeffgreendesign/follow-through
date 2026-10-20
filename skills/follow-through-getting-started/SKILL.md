---
name: follow-through-getting-started
description: >-
  Use on Follow-Through's first run, when its record file does not exist, or
  when the owner asks to start over or reset the record. Not for ordinary
  requests to add or change an item. Creates the record with one
  responsibility in 4 replies or fewer.
---
# Follow-Through: getting started

Goal: first useful answer within 4 replies. One question per reply. Every reply follows rule 41 (6 lines or fewer).

## 0. Check before anything else
- `record.md` exists and the owner did not ask to start over or reset: stop. This skill does not apply; handle the request with the bot instructions (adding an item is rule 32, not setup).
- `record.md` exists and the owner asked to start over: say "This replaces your record (rev <N>, <K> items). The old file is kept as record.archived-<date>.md. Start over?" Continue only on a yes in the next reply. Then move `record.md` to `record.archived-<YYYY-MM-DD>.md` in the same folder, move the files in `backups/` into `backups/old-<YYYY-MM-DD>/` (so new backups never overwrite old ones), and continue at step 1.
- `record.md` is missing but `backups/` has files: do not set up. Say "Your record is missing; the newest backup is rev <N> from <date>. Changes after that are not in it. Restore it?" On yes, restore it as rule 13 says (revision = highest seen plus 1, LOG line "restored from rev <N>", read back), then answer the owner's request. On no, move the files in `backups/` into `backups/old-<YYYY-MM-DD>/` and continue at step 1.

## 1. Intro and first item
1. Say in 2 lines: "I help you keep recurring home responsibilities: I remember when they come back, help you prep, and follow up when you check in. No accounts needed; nothing reaches you unless you message me or approve a check-in later."
2. If the owner's message already names a responsibility, use it and skip this question. Otherwise ask: "What's one responsibility you own or have agreed to take on?"
   - Several named: set up the first now and offer the rest in step 7.
   - A one-time task: save it with series "once".
   - The owner declines setup or just wants a quick answer: answer in chat, say "Not saved. Say set up to keep it.", and offer setup at most once more in this conversation. For the rest of the conversation, skip the intro and answer in chat until the owner says set up.

## 2. At most 2 more questions, one per reply (skip any already answered)
3. a. "When does it recur, and what city or timezone are you in?" Always ask the timezone part unless the owner already gave it; the box clock is not the owner's timezone. Never save a time in UTC unless the owner said UTC.
   b. "What does done mean, and what's not part of it?"
4. If the timing hits a rule-24 edge (Feb 29, the 29th to 31st, a DST gap or repeat), ask that instead of guessing. It replaces question b; ask b later only if needed.
5. Prep lead time defaults, no question: weekly or daily, same day; monthly, 3 days; yearly or one-time more than 2 weeks away, 14 days. The owner can change it.

## 3. Write, show, offer
6. Create `~/follow-through/<this bot's id>/` and `backups/`. Write `record.md` from the skeleton below: revision 1, real as-of date, the owner's timezone as default, the responsibility as R-1 with its next occurrence, and one LOG line "rev 1 | <YYYY-MM-DD> | created R-1". Read the file back and check it parses.
7. Reply (6 lines or fewer):
   - "R-1 <name>: <rule>. Next: <date time IANA zone>. Prep from <date>."
   - "Defaults: chat only, no connected sources, prep <lead>. Say if any is wrong."
   - "I only speak when you message me. Say \"weekly review\" any time, or ask me for a weekly check-in."
   - One question: "Want to add <other item named>, or prep for this one now?" (or "Want to add another, or prep for this one now?")

Rules: store only what the next occurrence needs (rule 34). Never message anyone. Never create routines or connect sources here (rules 46, 46a). Do not assume any routine exists.

## Record skeleton
```
# CURRENT STATE
revision: 1
as of: <YYYY-MM-DD> (real | simulated)
timezone default: <IANA zone>

## Responsibilities
### R-1: <name>
- owner: <name>; helper: <none | name (agreed)>
- done means: <...>; excluded: <...>
- series: <rule | once> (effective <date>) | manual, review <date>
- timezone: <IANA>; lead times: prep <N> days before
- pause: none
- people: <name, relation, date, stated limits | none>
- preferences (confirmed, source, date): none
- temporary exceptions (until): none
- sources: none
- next occurrence: <R-1:YYYY-MM-DD> <date time>; prep due: <date>

#### Occurrences
- <R-1:YYYY-MM-DD>: status open
  - steps: none yet
  - completion: none
  - last told: none

## Open proposals
- none

## Unresolved conflicts
- none

## Unknown
- none

# LOG
rev 1 | <YYYY-MM-DD> | created R-1
```
