---
name: gpc-device-management
description: Manage supported devices, device statistics, device tier configs, country availability, and reports using gpc. Use when working with device targeting or distribution settings.
---

# Device Management & Distribution

Use this skill when managing device support, device tiers, country availability, or accessing reports.

## Devices

### List supported devices

```bash
gpc devices list --package com.example.app
```

### Device usage statistics

```bash
gpc devices stats --package com.example.app
gpc devices stats --package com.example.app -o table
```

## Device tier configuration

### List device tier configs

```bash
gpc dt list --package com.example.app
```

### Get config details

```bash
gpc dt get --config-id 123 --package com.example.app
```

### Create device tier config

```bash
gpc dt create --file tier-config.json --package com.example.app
```

## Country availability

### List current availability

```bash
gpc availability list --track production --package com.example.app
```

### Update countries

```bash
gpc availability update --track production \
  --countries US,CA,GB,DE,FR,JP \
  --confirm \
  --package com.example.app
```

### Include rest of world

```bash
gpc availability update --track production \
  --countries US,CA,GB \
  --include-rest \
  --confirm \
  --package com.example.app
```

## Reports

### List available reports

```bash
gpc reports list --package com.example.app
```

### Show report types

```bash
gpc reports types --package com.example.app
```

## Download statistics

### Download counts

```bash
gpc stats downloads --package com.example.app
```

### Download sources

```bash
gpc stats sources --package com.example.app
```

## Compare draft vs live

```bash
gpc diff --package com.example.app
gpc diff --section listings --package com.example.app
```

## Agent behavior

- Show current availability before modifying country targeting.
- Use `--confirm` for availability updates.
- Use `-o table` for device stats when presenting to user.
- `dt` is the short alias for `device-tiers`.

## Notes

- Device tier configs enable delivering different APKs/assets to different device groups.
- Country availability is per-track (different tracks can target different countries).
- Use `gpc diff` to review changes before committing an edit.
