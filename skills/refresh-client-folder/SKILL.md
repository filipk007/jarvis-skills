---
name: refresh-client-folder
description: Refresh one client's six-file folder from a read-only HubSpot company, its onboarding ticket, and matching Gmail threads.
---

# Refresh one client folder

## Ask first

Ask Filip for the HubSpot company id if the message does not already contain one. A company URL is enough when it contains the id. Stop until you have it. Do not pick a company from a list of recent mail.

## Read

Use the connected HubSpot tools to read that company, its contacts, and onboarding tickets for that company. If more than one onboarding ticket matches, list the ticket ids and subjects and ask which one to use. If none match, continue and write `None recorded.` in the territory sections.

Use the connected Gmail tools to search the latest 20 threads to or from the contact email addresses on that company. Record the thread id and one sentence. Do not copy the raw body into the folder. Do not download attachments.

If HubSpot or Gmail cannot be read, write no files. Name the system that failed and stop.

## Write

Create `/Users/filipkostkiewicz/projects/jarvis-clients/` if it is missing. Write or update only:

`/Users/filipkostkiewicz/projects/jarvis-clients/<hubspot-company-id>-<slug>/`

`<slug>` is the company name in lowercase, with spaces turned into single hyphens, and any character that is not a letter, number, or hyphen removed. If a directory for that company id already exists, update it in place.

Write the six files named in `docs/superpowers/specs/2026-09-23-client-folder-csm-design.md`, with the headings that spec requires. The first refresh sets `status: onboarding`. A later refresh leaves an existing `status: proposal` or `status: handed-to-fulfillment` line as it is.

When mail contradicts the ticket, keep both statements and add one dated bullet to `decisions.md`. Do not delete a ZIP the ticket still contains.

## Check

From the jarvisbot repo, run:

```bash
python3 scripts/validate_client_folder.py /Users/filipkostkiewicz/projects/jarvis-clients/<hubspot-company-id>-<slug>
```

If it prints anything other than `ok`, paste those lines to Filip and do not call the refresh done.

Add one index line to this bot's `MEMORY.md`: company id, folder name, status, and today's date. Do not copy the client facts into `MEMORY.md`.
