---
description: Check Bugsly cron monitors, uptime monitors, crash-free rate and event usage (read-only)
---

Check the health of a Bugsly project. Project (may be empty): $ARGUMENTS. This is read-only: change nothing and do not call `get_checkout_url`.

1. Call `list_projects` and pick the project (ask if several and none named).
2. Call `list_monitors` and `list_uptime_monitors`. For anything failing or late, call `get_monitor` or `get_uptime_status`.
3. Call `get_crash_free` (30 days by default) and `get_usage`.
4. Summarise failing or late monitors first, then uptime, crash-free sessions and users, and event usage against the plan limit, exactly as returned. If crash-free percentages are null, no sessions have been ingested yet: say so.
