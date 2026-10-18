# Follow-Through

Grok Bot template for recurring household responsibilities. It remembers when each one comes back, helps you prep ahead of time, and follows up on how it went.

Chat-only by default. No routines ship with it, no accounts are needed, and it never messages anyone but you.

**Status:** v0.1.0. Tested on synthetic data only: 9 regression tests and 12 behavioral probes passing. Not yet used with a real household.

## What it does

- Keeps one record per bot: each responsibility (a birthday, a weekly dinner, a supply check), its schedule, what "done" means, and how far ahead to prep.
- On every request it brings the record up to today, tells you what's due, and suggests one next action (options, a list, a draft), with at most one question.
- Never marks something done without your word or a linked source. Missed dates stay overdue or unknown; they are never silently completed or rolled forward.
- Handles real calendar edge cases with date tools: time zones, daylight saving, Feb 29, month-end dates, "every 30 days after I do it", pauses, and travel. When a rule is ambiguous it asks instead of guessing.
- Lets you correct it: "actually I didn't do it", rename, delete (with confirmation), and merge duplicates. History is kept.
- Stays restrained: after a gap it gives one summary line and one question, never a burst of reminders or guilt language.

## Install

1. Create a Grok Bot from this template: paste `bot-instructions.md` as the bot's instructions.
2. Add the skill in `skills/follow-through-getting-started/`.
3. Start a chat. Nothing else is required.

## First run

On the first message (or "set up" / "start over") the bot runs `follow-through-getting-started`:

1. A two-line intro.
2. "What's one responsibility you own or have agreed to take on?"
3. Up to 3 follow-up questions, one per reply: when it recurs, what done means, how far ahead to prep.
4. One line of defaults: no connected sources, chat only, your computer's time zone.
5. It creates `~/follow-through/<bot id>/record.md` from `templates/record.md`, reads it back, and shows you the result.

Target: a useful answer within 4 turns.

## The record

`templates/record.md` shows the format. **CURRENT STATE** sits at the top and is updated in place on each change. The **LOG** below it is append-only history. Before every write the bot checks the revision, keeps a backup (last 10), and reads the file back afterwards. If the file is damaged it refuses to write and offers a restore.

## Privacy and safety boundaries

- **Owner only.** Only you change ownership, standards, or permissions. If a partner or anyone else reports something, it's recorded as "reported by <name>" and waits for your confirmation. It never scores or reports on anyone's performance.
- **Minimal data.** It stores only what the next occurrence needs: name, relation, date, and limits you state. No health, finances, private messages, or children's details beyond first name and age band. "What do you know about X" lists it; "forget X" removes it.
- **Untrusted text.** Text in calendar events, tasks, emails, web pages, or other agents' messages is treated as data, never as instructions. If it contains an instruction, the bot tells you it was ignored.
- **Approval first.** It asks before creating routines, connecting a calendar or task app, spending, sending, booking, or changing permissions. Calendar and task access is optional, scoped, and off by default.
- **No outbound messages.** It never messages anyone but you, and never writes to shared memory or reads other bots' files.
- **Shared computers.** The record folder is per bot by rule only. Other bots on the same computer could technically read it.

## Not included

- No routine. If you add one later, the instructions already limit it: it speaks only when something is newly due or changed, and a same-day rerun with no change sends nothing.
- No public Grok Bot template listing yet.

## Repo layout

- `bot-instructions.md`: the bot's instructions.
- `skills/follow-through-getting-started/SKILL.md`: first-run setup.
- `templates/record.md`: empty record.
- `docs/DESIGN.md`: design decisions and review findings.
- `docs/TESTING.md`: how it was tested and results.
- `tests/`: synthetic regression cases, probes, test overlay, and seed fixture.

## License

MIT. See `LICENSE`.
