---
name: gpc-vitals
description: Monitor Android Vitals metrics — crashes, ANRs, startup time, rendering, wakeups, and memory using gpc. Use when checking app health or performance.
---

# Android Vitals

Use this skill when monitoring app health metrics, crash rates, ANR rates, or performance indicators.

## Overview

```bash
gpc vitals overview --package com.example.app
gpc vitals overview --days 28 --package com.example.app
```

## Individual metrics

### Crash rate

```bash
gpc vitals crashes --package com.example.app
gpc vitals crashes --days 7 --package com.example.app
```

### ANR rate

```bash
gpc vitals anr --package com.example.app
gpc vitals anr --days 7 --package com.example.app
```

### Slow startup

```bash
gpc vitals slow-start --package com.example.app
```

### Slow rendering (jank)

```bash
gpc vitals slow-rendering --package com.example.app
```

### Excessive wakeups

```bash
gpc vitals wakeups --package com.example.app
```

### Stuck wakelocks

```bash
gpc vitals wakelocks --package com.example.app
```

### Low memory killer

```bash
gpc vitals memory --package com.example.app
```

## Error tracking

### View error counts

```bash
gpc vitals errors --package com.example.app
gpc vitals errors --days 7 --package com.example.app
```

### List grouped error issues

```bash
gpc vitals errors issues --package com.example.app
```

## Health check workflow

Run a full health assessment:

```bash
gpc vitals overview --days 7 --package com.example.app -o table
gpc vitals crashes --days 7 --package com.example.app -o table
gpc vitals anr --days 7 --package com.example.app -o table
```

## Agent behavior

- Default to `--days 7` for recent trends, `--days 28` for overall health.
- Use `-o table` when presenting to user; `-o json` for data processing.
- Flag metrics that exceed Google Play's bad behavior thresholds:
  - Crash rate > 1.09%
  - ANR rate > 0.47%
- Compare before/after a release to detect regressions.

## Notes

- Vitals data uses Play Developer Reporting API v1beta1.
- Data may have 24-48 hour delay.
- Upload ProGuard mappings (`gpc deobfuscation upload`) for readable crash stacks.
- See `gpc-build-lifecycle` skill for deobfuscation upload.
