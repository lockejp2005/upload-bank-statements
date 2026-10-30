# Upload bank statements to Tax Reaper

This Codex skill guides bank transaction exports and imports into Tax Reaper through computer use. It asks for exact dates and any other spending accounts, lets you complete bank login yourself, and checks the export format before uploading.

## Installation

Give Codex [this repository URL](https://github.com/lockejp2005/upload-bank-statements) and ask it to install the skill.

After installation, ask Codex to use `$upload-bank-statements`. Tell it which bank to start with and which Tax Reaper account should receive the statements. Codex will ask for any missing dates or account selections.

## How the workflow works

You log in to your bank and complete authentication yourself. Codex exports the selected accounts for the agreed date range, checks for existing imports, and uploads supported files to the specified Tax Reaper account. It checks processing and linked transactions before reporting completion.

The workflow requires Codex computer-use tools, access to the bank's export screen and a working Tax Reaper importer. Installing the skill does not connect accounts or start an upload. A pending upload is not a completed import.

## Skill files

The workflow is defined in [SKILL.md](SKILL.md). Codex display metadata is in [agents/openai.yaml](agents/openai.yaml). The repository contains no bank statements, credentials or account data.
