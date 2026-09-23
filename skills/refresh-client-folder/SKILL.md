---
name: refresh-client-folder
description: Refresh one client's six-file folder from a read-only HubSpot company, its onboarding ticket, and the email engagements logged on that company.
---

# Refresh one client folder

## Ask first

Ask Filip for the HubSpot company id if the message does not already contain one. A company URL is enough when it contains the id. Stop until you have it. Do not pick a company from a list of recent mail.

## Read

Use HubSpot only. Read that company, its contacts, its onboarding tickets, and the email engagements already logged on the company. HubSpot activities are the mail record. Do not search Gmail when those engagements exist.

If more than one onboarding ticket matches, list the ticket ids and subjects and ask which one to use. If none match, continue and write `None recorded.` in the territory sections.

Put the company, contacts, ticket, and email engagements into one `COMPOSIO_MULTI_EXECUTE_TOOL` call. Do not call `COMPOSIO_REMOTE_WORKBENCH`. Do not run a shell search outside `/Users/filipkostkiewicz/projects/jarvis-clients/`. The folder contract is in this skill. Do not look for it on disk, and do not request access to Documents, Desktop, or Downloads.

For each logged email, keep the date, the sender address, and one sentence. Do not copy the raw body into the folder.

If HubSpot cannot be read, write no files. Name the failure and stop.

## Write

Create `/Users/filipkostkiewicz/projects/jarvis-clients/` if it is missing. Write or update only:

`/Users/filipkostkiewicz/projects/jarvis-clients/<hubspot-company-id>-<slug>/`

`<slug>` is the company name in lowercase, with spaces turned into single hyphens, and any character that is not a letter, number, or hyphen removed. If a directory for that company id already exists, update it in place.

Write these six files. Do not open another document to learn the headings.

`profile.md` has `# Profile`, `## Identity`, and `## Contacts`.
`onboarding.md` has `# Onboarding`, `## Territory request`, `## Property focus`, and `## Open questions`.
`communications.md` has `# Communications`, the sentence `Raw mail stays in Gmail.`, and `## Threads`. Under Threads, one bullet per HubSpot email: date, engagement id, sender, and one sentence.
`decisions.md` has `# Decisions`. If nothing changed, include `No decisions recorded yet.`
`territory.md` has `# Territory`, `## ZIPs`, `## Property types`, `## Exclusions`, and `## Source`. An empty section says `None recorded.`
`status.md` has `# Status` and, on the first refresh, the line `status: onboarding`. A later refresh leaves an existing `status: proposal` or `status: handed-to-fulfillment` line as it is.

When mail contradicts the ticket, keep both statements and add one dated bullet to `decisions.md`. Do not delete a ZIP the ticket still contains.

## Check

Run this command and no other search:

```bash
python3 /Users/filipkostkiewicz/projects/jarvisbot/.worktrees/client-folder-csm/scripts/validate_client_folder.py /Users/filipkostkiewicz/projects/jarvis-clients/<hubspot-company-id>-<slug>
```

If it prints anything other than `ok`, paste those lines to Filip and do not call the refresh done.

Add one index line to this bot's `MEMORY.md`: company id, folder name, status, and today's date. Do not copy the client facts into `MEMORY.md`.
