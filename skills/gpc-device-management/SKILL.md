---
name: gpc-device-management
description: Manage country availability, device tier configs, device catalog views, report metadata, and draft-vs-live summaries using gpc.
---

# Device Management And Distribution

Use this skill for availability, device tiers, devices, reports, and diff summaries.

## Devices

```bash
gpc devices list
gpc devices stats
```

`devices stats` is a lightweight overview, not a full Play export.

## Device tiers

Prefer the full command name in new examples:

```bash
gpc device-tiers list
gpc device-tiers get --config-id 123
gpc device-tiers create --file tier-config.json
```

`gpc dt` remains an alias.

## Country availability

```bash
gpc availability list --track production
gpc availability update --track production --countries US,CA,GB --confirm
gpc availability update --track production --countries US,CA,GB --include-rest=false --confirm
gpc availability update --track production --countries US,CA,GB --edit-mode=stage --confirm
```

`--include-rest` defaults to `true`. Set it to `false` when you want only the listed countries.

## Reports and diff

```bash
gpc reports list
gpc reports list --type installs
gpc reports types
gpc diff
gpc diff --section listings
gpc diff --section tracks
```

`reports` is informational metadata about available report types, not a report downloader.

## Agent behavior

- Show current availability before changing country targeting.
- Use `--confirm` for availability updates.
- Treat `diff` as a summary of current draft or live state, not a full textual diff.
- Do not use `gpc stats` for app statistics; that command is for CLI download stats.
