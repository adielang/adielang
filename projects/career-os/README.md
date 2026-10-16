# Career OS — AI Job Application Tracker

**Status:** Discovery / MVP design  
**Parent initiative:** AI Job Search Orchestrator  
**Project type:** Applied AI engineering / personal productivity / portfolio case study

## Problem

Job applications, CV versions, recruiter conversations, salary expectations, and follow-up dates can become fragmented across email, chat, and files. The result is duplicated effort, missed follow-ups, and poor visibility into the application pipeline.

## Objective

Build a privacy-conscious, human-in-the-loop job application tracking workflow that keeps structured records in one place and delegates repeatable coordination tasks to an AI agent.

## Proposed architecture (not yet implemented)

```text
                  +--------------------------+
                  | Notion: Application DB   |
                  | source of truth          |
                  +------------+-------------+
                               ^
                               | API (authenticated)
                               v
                  +------------+-------------+
                  | Hermes Agent             |
                  | validation + orchestration|
                  +------------+-------------+
                               |
                +--------------+--------------+
                |                             |
        Telegram input/alerts         Email metadata (future)
```

- **Notion:** structured application records and kanban/table views.
- **Hermes Agent:** propose and eventually apply approved status updates, schedule follow-up checks, and summarize opportunities.
- **Telegram:** convenient manual capture and controlled notifications.
- **Python / Notion API:** adapter, schema validation, idempotency, logging, and error handling.

## MVP scope

1. Create a private Notion `Job Applications` database.
2. Track position, company, job URL, priority, stage, applied date, follow-up date, compensation target, CV version, and next action.
3. Add a first manually verified opportunity and distinguish `To Apply` from `Applied`.
4. Implement a read-only Notion API integration.
5. Enable validated updates with explicit confirmation and an audit trail.
6. Add Telegram commands and reminders only after the API workflow has passed tests.

## Suggested application pipeline

`Saved → To Apply → Applied → Screening → Interview → Assessment → Offer → Accepted`

`Rejected` and `Withdrawn` are separate terminal outcomes.

## Acceptance criteria

- One authoritative record per application (company + role + requisition ID).
- Updates are visible from Notion across devices.
- The agent never marks an application as submitted without evidence or user confirmation.
- Sensitive records stay in a private Notion workspace; the public repo uses synthetic data only.
- Follow-up notifications are deduplicated and are not confused with status changes.
- Error paths, permission scopes, and human approval rules are documented.

## Delivery plan

| Milestone | Deliverable | Status |
| --- | --- | --- |
| M1 — Foundation | Notion database and views | Planned |
| M2 — First opportunity | Manually verified record | Planned |
| M3 — API integration | Read-only adapter and validation | Planned |
| M4 — Controlled write | Approved status changes and audit log | Planned |
| M5 — Agent workflow | Telegram ingestion and follow-up reminders | Planned |
| M6 — Evaluation | Failure cases, metrics, demo, lessons learned | Planned |

## Portfolio evidence to collect

- Problem statement and product requirements
- Architecture and API permission design
- Synthetic test dataset and repeatable integration tests
- Demonstration screenshots with private information removed
- Reliability/quality measurements and lessons learned

> **Privacy note:** Actual job applications, contacts, emails, salary data, and CVs will not be published in this repository. This README documents the intended project, not a shipped system.
