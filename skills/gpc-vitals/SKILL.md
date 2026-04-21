---
name: gpc-vitals
description: View Android vitals and error reporting commands with gpc, including crashes, ANRs, startup, rendering, wakeups, wakelocks, memory, and grouped issues.
---

# Android Vitals

Use this skill for Play Developer Reporting API workflows.

## Core commands

```bash
gpc vitals overview --days 28
gpc vitals crashes --days 7
gpc vitals anr --days 7
gpc vitals slow-start --days 28
gpc vitals slow-rendering --days 28
gpc vitals wakeups --days 28
gpc vitals wakelocks --days 28
gpc vitals memory --days 28
gpc vitals errors --days 28
gpc vitals errors issues
```

## Common usage patterns

For recent regressions:

```bash
gpc vitals overview --days 7 -o table
gpc vitals crashes --days 7 -o table
gpc vitals anr --days 7 -o table
```

For broader health checks:

```bash
gpc vitals overview --days 28
```

## Agent behavior

- Use `--days 7` for post-release checks and `--days 28` for broader trends.
- Prefer `-o table` when presenting results directly to a user.
- Pair vitals triage with `gpc deobfuscation upload` guidance when stack symbolication is relevant.
- Do not overstate thresholds or computed interpretations that the CLI itself does not return.
