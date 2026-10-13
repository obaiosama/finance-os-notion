# Finance OS

A personal finance system built in Notion. It links accounts, transactions, expenses and subscriptions, so monthly budget pacing and upcoming renewals come from the data instead of being tracked by hand.

> **Scope, stated plainly.** This is a system I built for my own use and it is live: I use it myself. It is not a client project or a product I sell. I built it with Claude's help. It lives in Notion, so there is no application code in this repo, and I have not published the workspace or any of my financial data. This page documents the design.

## What it does

- **Linked records.** Accounts, transactions, expenses and subscriptions are connected through Notion relations.
- **Rollups and formulas.** Rollups and Notion's Formulas 2.0 drive the budget pacing, so monthly spending is compared with the budget automatically.
- **Renewal triggers.** Subscriptions have renewal triggers, so upcoming renewals are surfaced.
- **Reconciliation tracking.** The system tracks reconciliation of records.
- **Retry handling.** The automation side, built with Make.com, includes retry handling for failed steps.

## Design choices

- **One source of truth.** A record is entered once and the rest is derived from it through relations and rollups.
- **Derived numbers, not typed numbers.** Totals and pacing come from formulas, so they cannot drift from the underlying records.

## Stack

Notion (advanced relations, rollups, Formulas 2.0), Make.com, built with Claude
