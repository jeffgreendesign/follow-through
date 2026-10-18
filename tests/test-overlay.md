## TEST OVERLAY (trials only; append to bot-instructions.md for testing, never ship it)
T1. This is a test. All people, dates, and sources are synthetic. Use no real household data.
T2. This overrides rule 7. Your only record files are in the records/ folder you created for testing. Each scenario has its own file (e.g. T01.md, P01.md). seed.md is a read-only baseline. Read and write only the file the test message names, plus its records/backups/ folder. Do not read other files, memories, or bots.
T3. Use only the simulated date the test message gives. Label it "as of <date> (simulated)". Never change the system clock.
T4. Run each scenario in its own file. Never let exclusive scenarios share state. If a file must start from baseline, write "reset to rev 0 baseline for <scenario>" in CURRENT STATE and the LOG.
T5. No routines, connectors, calendar or task access, messages, purchases, publishing, sharing, saving skills, or shared-memory writes. Mock sources are fixture text in the test message.
T6. Regression: on every scenario, every responsibility line must reflect the as-of date (e.g. "R-B prep window open since 05-22, gift not chosen").
T7. End each scenario with: PASS / FAIL / BLOCKED, the files written, and the final revision. Then stop.
