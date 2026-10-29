# InvestWeek9_AgentScheduler

Scheduled agent jobs for **Financial Eureka - MJK Version 1**, an educational equity-research pipeline that turns a trading session's US stock-market movers into one evidence-backed, one-page brief.

> For educational use only - not investment advice.

## Jobs

| Job | When (America/New_York) | What it does |
|---|---|---|
| Job 1 - At close | 5:30 PM, Monday-Friday, NYSE trading days only | Runs the full pipeline on the last closed session: gates, research, scoring, one-page report, pick log |
| Job 2 - Lunchtime trending | 12:30 PM (proposed), Monday-Friday, trading days only | Intraday snapshot table with a trending pick on top; no PDF |

Status: both prompts are drafted. Neither has run on a schedule yet.

## Rules in brief

- Numbers are fetched fresh in every run and calculated from raw fields; nothing is reused from an earlier run.
- No candidate is tagged or scored until it has been researched.
- Sources are ranked in tiers: first-party filings and exchange files, licensed data, major wires and redistributors, then everything else (corroboration only).
- One report slot per session date. A failed run writes a failure report naming the failed stage and the error.
- The pick log is write-only for the jobs and never influences selection.

## Pick log columns

`run_datetime, session_date, timing_mode, data_as_of, status, ticker, company, sector, move_type, score, stance_lean, qa_result, passes_used, font_size, prompt_version, snapshot_name, report_filename, failed_stage`

## Planned layout

```
docs/      specification and addenda
prompts/   Job 1 and Job 2 prompts
logs/      pick logs
```

## Open items

- Choose and verify the scheduler.
- First-night test of connector behavior after the close.
- Verify exchange, ETF and SPAC lookups against first-party reference files.
