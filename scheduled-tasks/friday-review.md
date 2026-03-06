# Friday Code Review Compilation

Every Friday at 5 PM: compile the week's code changes for review.

## Schedule
Cron: `0 17 * * 5`

## What It Does
`@Andy review the git history for the past week each Friday and update the README if there's drift`

- Scans git log --since="7 days ago" across active repos
- Identifies: new features, bug fixes, breaking changes
- Checks README accuracy vs current code
- Updates README if drift detected
- Sends summary to engineering group
