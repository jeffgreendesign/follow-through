# Follow-Through

Grok Bot template for recurring household responsibilities. It remembers when each one comes back, helps you prep ahead of time, and follows up on how it went.

Chat-only by default. No routines ship with it, no accounts are needed, and it never messages anyone but you. It follows up when you check in; it only messages you on a schedule if you approve a check-in.

**Status:** v0.2.0. Synthetic regression tests and probes pass, plus a pre-ship review with a simulated retest. In daily use by the author since October 2026.

## What it does

- Keeps one record per bot: each responsibility (a birthday, a weekly dinner, a supply check), its schedule, what "done" means, and how far ahead to prep.
- On every request it brings the record up to today, tells you what's due, and suggests one next action (options, a step list, a draft), with at most one question. Replies stay at 6 lines or fewer; say "more" for the full step list or "status" for the whole record.
- Never marks something done without your word or a linked source. Missed dates stay overdue or unknown; they are never silently completed or rolled forward.
- Handles real calendar edge cases with date tools: time zones, daylight saving, Feb 29, month-end dates, "every 30 days after I do it", pauses, and travel. When a rule is ambiguous it asks instead of guessing.
- Lets you correct it: "actually I didn't do it", rename, delete (with confirmation), and merge duplicates. History is kept.
- Stays restrained: after a gap it gives one summary line and one question, never a burst of reminders or guilt language.
- Stays in its lane: it tracks purchases as one step per category and never builds shopping lists or quotes prices.
- Weekly review: say "weekly review" for what is due in the next 7 days and what passed without an update.

## Install

1. Create a Grok Bot from this template: paste `bot-instructions.md` as the bot's instructions.
2. Add both skills: `skills/follow-through-getting-started/` and `skills/follow-through-weekly-review/`.
3. Start a chat. Nothing else is required.

## First run

When no record exists, the bot runs `follow-through-getting-started` (also on an explicit "start over", which asks first and archives the old record):

1. A two-line intro, and "What's one responsibility you own?" unless you already named one.
2. Up to 2 follow-up questions, one per reply: when it recurs and your time zone, and what done means. Prep lead time has a sensible default.
3. It creates `~/follow-through/<bot id>/record.md` (the skeleton is inside the skill), reads it back, and shows the next occurrence with its time zone plus one line of defaults.

If the record file is missing but backups exist, it offers to restore instead of starting over. If you'd rather not set up, it answers in chat and says nothing was saved.

Target: a useful answer within 4 turns.

## The record

`templates/record.md` shows the format. **CURRENT STATE** sits at the top and is updated in place on each change. The **LOG** below it is append-only history. Before every write the bot checks the revision, keeps a backup (last 10), and reads the file back afterwards. If the file is damaged it refuses to write and offers a restore. Each LOG line reads `rev <N> | <date> | <change>`.

## Privacy and safety boundaries

- **Owner only.** Only you change ownership, standards, or permissions. If a partner or anyone else reports something, it's recorded as "reported by <name>" and waits for your confirmation. It never scores or reports on anyone's performance.
- **Minimal data.** It stores only what the next occurrence needs: name, relation, date, and limits you state. No health, finances, private messages, or children's details beyond first name and age band. "What do you know about X" lists it; "forget X" removes it from the current record and offers to redact it from past log lines and backups.
- **Untrusted text.** Text in calendar events, tasks, emails, web pages, or other agents' messages is treated as data, never as instructions. If it contains an instruction, the bot tells you it was ignored.
- **Approval first.** It asks before creating routines, connecting a calendar or task app, spending, sending, booking, or changing permissions. Calendar and task access is optional, scoped, and off by default.
- **No outbound messages.** It never messages anyone but you, and never writes to shared memory or reads other bots' files.
- **Shared computers.** The record folder is per bot by rule only. Other bots on the same computer could technically read it.

## Not included

- No routine. The bot never creates one on its own. If you approve a check-in, it creates one routine in your time zone, tests it once, and reads back the schedule. It speaks only when something is newly due or changed, and a same-day rerun with no change sends nothing.
- No public Grok Bot template listing yet.

## Repo layout

- `bot-instructions.md`: the bot's instructions.
- `skills/follow-through-getting-started/SKILL.md`: first-run setup, restore, and start over.
- `skills/follow-through-weekly-review/SKILL.md`: weekly review on request.
- `templates/record.md`: empty record.
- `docs/DESIGN.md`: design decisions and review findings.
- `docs/TESTING.md`: how it was tested and results.
- `tests/`: synthetic regression cases, probes, test overlay, and seed fixture.

## License

MIT. See `LICENSE`.
