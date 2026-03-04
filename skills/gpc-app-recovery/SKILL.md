---
name: gpc-app-recovery
description: Create, deploy, and manage app recovery actions for Google Play using gpc. Use when responding to critical app issues that require user-facing recovery.
---

# App Recovery

Use this skill when creating or managing recovery actions for critical app issues.

## List recovery actions

```bash
gpc recovery list --package com.example.app
```

## Create recovery action

```bash
gpc recovery create --file recovery.json --package com.example.app
```

## Deploy recovery action

```bash
gpc recovery deploy --recovery-id abc123 --confirm --package com.example.app
```

## Cancel recovery action

```bash
gpc recovery cancel --recovery-id abc123 --confirm --package com.example.app
```

## Add targeting

```bash
gpc recovery add-targeting --recovery-id abc123 --file targeting.json --package com.example.app
```

## Recovery workflow

1. Identify the issue via vitals:
```bash
gpc vitals crashes --days 1 --package com.example.app
```

2. Create recovery action:
```bash
gpc recovery create --file recovery.json --package com.example.app
```

3. Add targeting for affected versions:
```bash
gpc recovery add-targeting --recovery-id $RECOVERY_ID --file targeting.json --package com.example.app
```

4. Deploy:
```bash
gpc recovery deploy --recovery-id $RECOVERY_ID --confirm --package com.example.app
```

## Agent behavior

- Always check vitals before recommending recovery actions.
- Show recovery action details before deploying.
- Require explicit `--confirm` for deploy and cancel operations.
- Never deploy recovery actions without user approval.

## Notes

- Recovery actions notify affected users about the issue.
- Use targeting to limit the recovery to specific app versions or devices.
- See `gpc-vitals` skill for monitoring crash rates.
