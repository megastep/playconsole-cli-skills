---
name: gpc-app-recovery
description: Create, target, deploy, cancel, and inspect Play app recovery actions using gpc. Use when responding to critical production incidents with user-facing recovery.
---

# App Recovery

Use this skill for production incident response via recovery actions.

## Commands

```bash
gpc recovery list
gpc recovery create --file recovery.json
gpc recovery add-targeting --recovery-id 123 --file targeting.json
gpc recovery deploy --recovery-id 123 --confirm
gpc recovery cancel --recovery-id 123 --confirm
```

`recovery-id` is numeric.

## Suggested workflow

```bash
gpc vitals overview --days 7
gpc recovery create --file recovery.json
gpc recovery add-targeting --recovery-id 123 --file targeting.json
gpc recovery deploy --recovery-id 123 --confirm
```

## Agent behavior

- Check current app health context before recommending recovery.
- Show the draft recovery and targeting inputs before deployment.
- Require explicit approval for deploy and cancel.
