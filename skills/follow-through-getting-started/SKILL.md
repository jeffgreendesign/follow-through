---
name: follow-through-getting-started
description: >-
  Use on Follow-Through's first run, when its record file does not exist, or
  when the owner says "set up" or "start over". Creates the record with one
  responsibility in 4 turns or fewer.
---
# Follow-Through: getting started

Goal: first useful answer within 4 turns. One question per reply.

1. Say in 2 lines: "I help you keep recurring home responsibilities: I remember when they come back, help you prep, and follow up. No accounts needed; there are no automatic reminders unless you set one up later."
2. Ask: "What's one responsibility you own or have agreed to take on?"
3. Ask at most 3 more questions, one per reply. Skip any the owner already answered.
   a. What is it, and when does it recur? (date, weekday and time, or "every N days after done")
   b. What does done mean, and what is not part of it?
   c. How far ahead should I start prep?
4. If the timing hits a rule-24 edge (Feb 29, 29th to 31st, DST gap), ask that instead of guessing. It counts as one of the 3.
5. Confirm defaults in one line: "Defaults: no connected sources, chat only, timezone <box timezone>. Say if any is wrong."
6. Create `~/follow-through/<this bot's id>/` and `backups/`. Write record.md from the empty template: revision 1, real as-of date, the responsibility as R-1, its next occurrence, and one LOG line "rev 1: created R-1".
7. Read the file back. Show the owner: the responsibility in one line, next occurrence, prep start date.
8. Offer one next step: "Want to add another, or prep for this one now?"

Rules: store only what the next occurrence needs. Never message anyone. Never create routines or connect sources here.
