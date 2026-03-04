---
name: gpc-release-flow
description: End-to-end release workflows for Google Play — upload bundles, manage tracks, staged rollouts, promotions, and halts. Use when uploading builds or managing releases.
---

# Release Flow

Use this skill when you need to upload a build, publish to a track, promote between tracks, or manage rollouts.

## Preconditions

- Auth configured (`gpc doctor` passes).
- New version code for each upload.
- Always pass `--package` explicitly.

## Upload and release

### Upload AAB to a track

```bash
gpc bundles upload --file app.aab --track internal --package com.example.app
```

### Upload with release notes and commit

```bash
gpc bundles upload --file app.aab --track beta \
  --release-notes "Bug fixes and improvements" \
  --release-notes-lang en-US \
  --commit \
  --package com.example.app
```

### Upload with staged rollout

```bash
gpc bundles upload --file app.aab --track production \
  --rollout 0.1 \
  --package com.example.app
```

## Track management

### List tracks

```bash
gpc tracks list --package com.example.app
```

### Get track details

```bash
gpc tracks get --track production --package com.example.app
```

### Update track release

```bash
gpc tracks update --track production \
  --version-code 42 \
  --status completed \
  --rollout-percentage 1.0 \
  --package com.example.app
```

## Promote between tracks

```bash
gpc tracks promote --from internal --to beta --package com.example.app
gpc tracks promote --from beta --to production \
  --rollout-percentage 0.05 \
  --package com.example.app
```

## Staged rollout

### Gradual increase

```bash
gpc tracks update --track production --rollout-percentage 0.05 --package com.example.app
gpc tracks update --track production --rollout-percentage 0.20 --package com.example.app
gpc tracks update --track production --rollout-percentage 0.50 --package com.example.app
```

### Complete rollout (100%)

```bash
gpc tracks complete --track production --package com.example.app
```

### Halt rollout

```bash
gpc tracks halt --track production --package com.example.app
```

## Manual edit lifecycle

Use when you need precise control or multiple changes in one commit:

```bash
# 1. Create edit session
gpc edits create --package com.example.app

# 2. Make changes (upload, update tracks, etc.)
gpc bundles upload --file app.aab --package com.example.app

# 3. Validate before committing
gpc edits validate --edit-id $EDIT_ID --package com.example.app

# 4. Commit all changes atomically
gpc edits commit --edit-id $EDIT_ID --package com.example.app
```

## Wait for bundle processing

```bash
gpc bundles wait --version-code 42 --timeout 600 --interval 30 --package com.example.app
```

## Agent behavior

- Always confirm the target track before uploading.
- Use `--dry-run` when available for production releases.
- Show `gpc tracks get --track <track>` output before and after changes.
- For production, prefer staged rollout starting at 5% over full release.

## Notes

- Use `gpc tracks list` to discover available tracks (internal, alpha, beta, production, custom).
- Release notes support `--release-notes-lang` for locale-specific notes.
- `--commit` on upload auto-commits the edit; omit for manual edit lifecycle.
