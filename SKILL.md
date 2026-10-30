---
name: upload-bank-statements
description: Use Codex computer use to download bank transaction exports for an explicit date range and upload them to Tax Reaper, with user-controlled bank login and coverage of other spending accounts. Use when the user asks to import bank statements or spending history into Tax Reaper.
---

## Purpose and scope

Complete the bank export and Tax Reaper import through the browser using the available Codex computer-use tools. Use the current tool documentation and observed page state rather than fixed coordinates or assumed bank menus. Keep the workflow limited to viewing accounts, exporting transactions and importing the selected files. Creating or editing this skill is not authorization to run it against bank accounts.

## Establish dates, accounts and destination

Ask which bank and account to use, the exact inclusive start and end dates, and whether the user has any other spending accounts or credit cards to include. Ask this directly even if only one bank is currently visible, unless the user has already answered. Include relevant joint accounts only when the user selects them. Account nicknames or masked identifiers are sufficient; do not request full account numbers in chat.

Resolve phrases such as “last month”, “this year” or “tax year” into explicit calendar dates and obtain the user's answer before exporting. State dates in an unambiguous form such as 1 July 2026 to 31 July 2026. Do not infer a financial year from the current date. Keep independent preparation moving while waiting, but do not treat elapsed time as an answer.

Establish the Tax Reaper destination, including whether it is the local app or a hosted account. Do not guess a production URL or switch destinations without authorization. Confirm which logged-in Tax Reaper account will receive the files. A local page can still send files to configured cloud storage and processing services; do not describe localhost as local-only storage.

## Open the bank and hand over login

Use the bank's official site, verified from the user's URL, existing tab or official source. Open the selected bank in the user's requested browser, or an available browser when none is specified. Make the tab visible for login. Ask the user to log in themselves and finish their bank's authentication, including MFA. Do not ask them to paste passwords, recovery codes or one-time codes into chat. If they are already signed in to the intended account, continue without requiring a fresh login.

Wait for the user to finish, then read the current page state and identify the selected account. If authentication expires, hand control back again. Do not attempt transfers, payments, account changes or security changes. Avoid capturing login screens or exposing balances and account identifiers in progress messages.

## Export the selected period

Find the account's transaction export or download control. Prefer a native CSV export; use another format that the current Tax Reaper importer accepts when CSV is unavailable. A bank's PDF statement download is different from a transaction export. Look for the transaction-history export before concluding the bank cannot provide a supported file.

Set the exact requested dates and confirm the visible account and date controls before downloading. Check whether the bank uses inclusive or exclusive date boundaries. Prefer posted transactions; report pending or unavailable periods rather than inventing missing records. Repeat for each explicitly selected spending account and credit card.

Keep one export per account and, when practical, per calendar month because Tax Reaper asks for a statement month. For a range spanning several months, export each month's intersection with the requested range. Do not silently upload an entire quarter or year under the current month. If the bank only offers a broader export, explain the mismatch and resolve the import period before submission.

Save downloads to a private local task folder, with descriptive names containing a bank label, account nickname and date range. Do not put statements in a Git repository, public artifact or shared folder. Retain the original export. Do not rename a PDF or HTML file to CSV to bypass validation.

## Check the import format

Read the current Tax Reaper upload screen for accepted formats and limits. The local implementation inspected on 30 October 2026 accepted CSV, XLSX, XLS, OFX, QFX, QIF and TXT, with a 10 MB limit. It did not accept PDF. These are a starting point, not a promise about a future deployment.

When repository access is available, verify changed requirements in `tax-reaper/apps/web/src/features/reaper-cloud/components/StatementImport.tsx`, `tax-reaper/apps/api/src/app/api/cashflow/statement-upload/route.ts` and `tax-reaper/packages/core/src/features/transactions/statementMimeType.ts` relative to Digital HQ. Use browser-visible requirements when the source is unavailable.

Inspect the downloaded file locally without printing transaction contents into chat. Check that it is nonempty, is the actual export rather than a login/error page, contains transaction dates, descriptions and amounts or debit/credit columns, and matches the selected account and period. Preserve signs, currency, date meaning and debit/credit direction. Do not impose invented CSV column names when the native export is supported. If conversion is necessary, establish the importer's actual requirements and preserve the original; do not infer missing amounts or ambiguous dates. If only PDF is available, report the unsupported format and agree on a conversion path before creating financial records from it.

## Upload and verify

Before selecting the file in Tax Reaper, ensure authorization covers those statements and that specific destination. An explicit request to upload the selected accounts and period to the established Tax Reaper account is sufficient; do not ask repeatedly. If the destination or data scope was not authorized, prepare the exports first, then ask a concrete question identifying the account labels, dates, files and receiving Tax Reaper account. Do not transmit the statements until answered.

Check Manage statements for existing imports covering the same files, accounts and dates. If a matching import exists, inspect its status and linked transactions before uploading again. Do not assume deduplication is guaranteed. Preserve existing pending jobs and avoid duplicate retries when the previous submission outcome is uncertain.

Use the bank statement upload flow rather than receipt or expense spreadsheet import. Select the verified export, set its correct statement month and any available account fields, and submit once. Track the resulting job through processing. Uploaded, pending and queued do not mean completed.

For local Tax Reaper, check that the API, configured queue and upload workers are available. The web app and API can run while upload workers are disabled. If processing is blocked, report the actual state and diagnose the existing job rather than reuploading. Do not change remote infrastructure or process an unrelated queue backlog merely to complete one import.

After completion, inspect linked Cashflow transactions and the covered dates. Compare transaction count and representative dates and debit/credit direction against the export. Investigate material count differences, skipped rows and parser warnings before claiming success. Do not automatically change claimability or approve deductions as part of statement import.

Stop repeated submissions after a failed or uncertain attempt until its job state is understood. If a job remains pending, fails, or needs attention, report that accurately with the next concrete action. Keep financial details out of screenshots unless they are necessary for the user's requested review, and never publish them to an external preview service.

## Finish

Report which account labels and date ranges completed, the observed import counts, any omitted accounts or dates, and any jobs still pending or requiring attention. Provide the private local download location when useful. Do not delete originals or stored statements without a separate user instruction. Keep the response concise and distinguish verified imports from merely downloaded or submitted files.
