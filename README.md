# Paylocity Manager Assignment Processor

A single-page browser tool that converts Synergy's InterCompany changes export into a Paylocity-ready manager assignment import file for Catch Health (company 361966).

## How to use

1. Open `ManagerAssignmentProcessor.html` in any modern browser — no install or server needed.
2. Drop or select the `Changes_[MM-DD-YYYY].xlsx` file.
3. Review the summary. If validation passes, click **Download** to save the output file.

## What it does

| Step | Detail |
|---|---|
| Reads | `Changes_[MM-DD-YYYY].xlsx` — 19-column InterCompany sheet |
| Filters | Only rows with company code `361966` (Catch) are included; others are reported and skipped |
| Validates | Blocks processing if any row's Department Description is Andvaris, Medix, Nulogic, or People Share |
| PayGroup | Populated for past/current start dates; blanked for future dates — except when uploading on a Wednesday and the start date falls within the same Sun–Sat week |
| Output | `Catch_Manager Assignments_[date].xlsx` — 501-column Paylocity import template |

## Column mapping

| Field | Source column (0-based) | Destination column |
|---|---|---|
| Co | 9 | 0 |
| ID | 10 | 1 |
| Record Type | 11 | 2 |
| Supervisor Co | 15 | 46 |
| Supervisor | 12 | 47 |
| Reviewer Co | 16 | 49 |
| Reviewer | 13 | 50 |
| Cost Center 1 | 17 | 51 |
| Cost Center 2 | 18 | 52 |
| PayGroup | 14 | 61 |

## Files

- `ManagerAssignmentProcessor.html` — the entire app (HTML + JS, uses SheetJS via CDN)
- `template.xlsx` — empty 501-column Paylocity import template (reference only, not tracked in repo)

## Notes

- No data leaves the browser — all processing is done client-side.
- The output date is parsed from the input filename (`MM-DD-YYYY`), falling back to today's date.
