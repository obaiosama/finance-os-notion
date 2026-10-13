# Finance OS

A finance operating system built in Notion with an automation layer on Make.com. It links accounts, transactions, expenses and subscriptions, so monthly budget pacing and upcoming renewals come from the data instead of being tracked by hand, and bank statements flow in through an intake pipeline that checks every file before it is accepted.

## What it does

- **Linked records.** Accounts, transactions, expenses and subscriptions are connected through Notion relations.
- **Rollups and formulas.** Rollups and Notion's Formulas 2.0 drive budget pacing, so monthly spending is compared with the budget automatically.
- **Renewal triggers.** Subscriptions have renewal triggers, so upcoming renewals are surfaced.
- **Reconciliation tracking.** The system tracks reconciliation of records against account activity.
- **Statement intake automation.** A Make.com scenario watches a Notion database for uploaded statement files and processes each one (details below).

## Statement intake pipeline

1. **Watch.** The scenario watches a Notion database for new or updated statement items.
2. **Pick the work.** It processes items that are new or that failed before, so failures are retried. Items already marked Done are skipped.
3. **Validate.** It checks that a file is attached and that the file name ends in .pdf. Anything else is marked Failed with a plain-language error such as "No File Uploaded" or "File Not PDF".
4. **Download and verify.** It downloads the file and confirms the content type really is a PDF. A download that is not a PDF is marked Failed with its own error.
5. **Catch duplicates.** It builds a fingerprint of the file and checks it against a data store, so the same statement is not processed twice.
6. **Write back.** Every outcome, success or failure, is written back to the Notion item with a status, an error message and a timestamp, so the Notion view always shows what happened.

## Design choices

- **One source of truth.** A record is entered once and the rest is derived from it through relations and rollups.
- **Derived numbers, not typed numbers.** Totals and pacing come from formulas, so they cannot drift from the underlying records.
- **Status lives where people look.** The automation reports results into Notion itself, so nobody has to open Make to find out why a file did not go through.
- **Fail loudly, retry safely.** Failures are labelled and retried, and a file fingerprint stops a retry or re-upload from creating duplicates.

## Stack

Notion (advanced relations, rollups, Formulas 2.0), Make.com, built with Claude
