---
name: gpc-release-flow
description: End-to-end release workflows for Google Play — upload bundles, manage tracks, staged rollouts, promotions, halts, completions, and manual edits. Use when uploading builds or managing releases.
---

# Release Flow

Use this skill for uploads, promotions, staged rollouts, and advanced edit control.

## Preconditions

```bash
gpc doctor
gpc tracks list
```

Assume the package comes from `--package`, a profile default, `GPC_PACKAGE`, or `.gpc.yaml`. Add `--package` only if needed.

## Upload a bundle

```bash
gpc bundles upload --file app.aab --track internal
gpc bundles upload --file app.aab --track production --edit-mode=stage
gpc bundles upload --file app.aab --track production --edit-mode=open
```

Release notes and production rollout on upload:

```bash
gpc bundles upload \
  --file app.aab \
  --track production \
  --release-notes "Bug fixes and performance improvements" \
  --release-notes-lang en-US \
  --rollout 10
```

`gpc bundles upload --rollout <n>` expects a percent from `0` to `100`.

## Track operations

```bash
gpc tracks get --track production
gpc tracks promote --from internal --to beta
gpc tracks halt --track production
gpc tracks complete --track production
```

For `gpc tracks update`, staged rollout requires both rollout percentage and `inProgress` status:

```bash
gpc tracks update \
  --track production \
  --version-code 42 \
  --status inProgress \
  --rollout-percentage 10
```

If you omit `--status inProgress`, the CLI defaults to `completed`.

## Manual edit lifecycle

Use manual edits only when you need to batch multiple edit-backed changes:

```bash
gpc edits create
gpc listings sync --dir ./metadata --edit-mode=open
gpc images sync --dir ./screenshots --edit-mode=open
gpc edits validate --edit-id EDIT_ID
gpc edits commit --edit-id EDIT_ID --edit-mode=stage
```

## Processing and symbolication

```bash
gpc bundles find --version-code 42
gpc bundles wait --version-code 42 --timeout 10m --interval 15s
gpc deobfuscation upload --version-code 42 --file mapping.txt --type proguard
```

## Agent behavior

- Prefer `bundles` over `apks`.
- Prefer `--edit-mode` over legacy `--stage` or `--commit=false`.
- Show current track state before changing production.
- For production, prefer staged rollout over immediate 100% rollout unless the user asks otherwise.
