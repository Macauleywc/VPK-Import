# CLAUDE.md — VPK Import Tool

## What this repo is
A single-page HTML/JS app that converts customer delivery schedules into Qargo TMS import files. Parsers exist per-customer for schedule formats that differ in layout.

## Known parsers / customers
- Instarmac
- SAM Mouldings
- VPK
- EuroPool (added recently — verify against the EuroPool customer's actual schedule format if extending it further)

## Deployment
- Netlify site: `vpkimport` (site ID `b53d30ae-bfdf-4f39-b366-98e29d5c7b78`)
- Live at https://vpkimport.netlify.app
- GitHub: repo backing this Netlify site (confirm exact repo name/owner on first clone if not already known)

## Standing rules — always follow these without being asked

1. **Each customer's parser is isolated** — a fix or format change for one customer (e.g. Instarmac) should not alter parsing logic for another (e.g. SAM Mouldings) unless the bug is genuinely shared. Check before generalising a fix across parsers.
2. **Output must be a valid Qargo TMS import file** — validate the output structure/format matches what Qargo expects, not just that the HTML/JS runs without error.
3. **Brand colours: Orange, Black, Grey — never blue**, consistent with other PLG-branded tools.

## Validation — required before any commit

Run `node --check <file>` on every changed file. Where possible, test the parser against a real (or realistic sample) delivery schedule for that customer before pushing — parser bugs are often only visible against actual data, not just syntax.

## Deploy workflow

1. Edit directly in this cloned repo.
2. `node --check` on each changed file.
3. `git add`, commit with a clear message naming the customer/parser affected (e.g. `Fix EuroPool parser date column offset`).
4. `git push origin main`.
5. Netlify auto-builds and publishes from the linked GitHub repo. Confirm at https://vpkimport.netlify.app; hard-refresh (Ctrl+Shift+R) if needed.

## Don't
- Don't share parser logic across customers without confirming the underlying schedule formats actually match.
- Don't skip `node --check`.
- Don't assume a parser fix is "done" until tested against real sample data for that customer.
