---
name: gpc-testing
description: Manage beta testing, internal test builds, tester groups, and internal app sharing using gpc. Use when setting up or managing testing workflows.
---

# Testing & Beta Management

Use this skill when managing testers, tester groups, internal test builds, or internal app sharing.

## Internal test builds

### List internal test builds

```bash
gpc testing internal list --package com.example.app
```

### Upload for internal sharing

```bash
gpc testing internal-sharing upload --file app.aab --package com.example.app
```

## Testers

### List testers on a track

```bash
gpc testing testers list --track beta --package com.example.app
```

### Add tester by email

```bash
gpc testing testers add --track beta --email tester@example.com --package com.example.app
```

### Add testers from file

```bash
gpc testing testers add --track beta --file testers.csv --package com.example.app
```

### Remove tester

```bash
gpc testing testers remove --track beta --email tester@example.com --package com.example.app
```

## Tester groups

### List tester groups

```bash
gpc testing tester-groups list --package com.example.app
```

## Typical beta workflow

1. Upload build to internal track:
```bash
gpc bundles upload --file app.aab --track internal --package com.example.app
```

2. Wait for processing:
```bash
gpc bundles wait --version-code 42 --package com.example.app
```

3. Add testers:
```bash
gpc testing testers add --track internal --email qa@example.com --package com.example.app
```

4. Promote to beta when ready:
```bash
gpc tracks promote --from internal --to beta --package com.example.app
```

5. Add external testers:
```bash
gpc testing testers add --track beta --file beta-testers.csv --package com.example.app
```

## Agent behavior

- Confirm tester additions on production tracks.
- Show current tester list before bulk operations.
- Use internal track for initial testing, beta for wider distribution.

## Notes

- Internal app sharing generates a direct download link (no review required).
- Testers CSV should contain one email per line.
- Use `gpc-release-flow` skill for promoting builds between tracks.
