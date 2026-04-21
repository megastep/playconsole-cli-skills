---
name: gpc-metadata-sync
description: Sync and manage Google Play store listings, images, and screenshots using gpc. Use when updating store metadata, uploading screenshots, or syncing local store assets.
---

# Metadata Sync

Use this skill for listings and image assets.

## Listings

```bash
gpc listings list
gpc listings get --locale en-US
gpc listings update --locale en-US --title "My App"
gpc listings sync --dir ./metadata
```

Use edit control when batching or deferring review:

```bash
gpc listings update --locale en-US --title "My App" --edit-mode=stage
gpc listings sync --dir ./metadata --edit-mode=open
```

## Images

```bash
gpc images list --locale en-US --type phoneScreenshots
gpc images upload --locale en-US --type phoneScreenshots --file screenshot1.png
gpc images upload --locale en-US --type phoneScreenshots --file screenshot1.png --progress
gpc images delete --locale en-US --type phoneScreenshots --id IMAGE_ID
gpc images delete-all --locale en-US --type phoneScreenshots
```

Sync behavior:

```bash
gpc images sync --dir ./screenshots
gpc images sync --dir ./screenshots --progress
gpc images sync --dir ./screenshots --replace
gpc images sync --dir ./screenshots --edit-mode=stage
```

`gpc images upload` and `gpc images sync` support optional upload progress output via `--progress`. `gpc images sync` appends by default. Use `--replace` to clear each discovered `locale/type` pair before upload.

## Directory-driven workflow

```bash
gpc listings sync --dir ./metadata --edit-mode=open
gpc images sync --dir ./screenshots --replace --edit-mode=open
gpc edits validate --edit-id EDIT_ID
gpc edits commit --edit-id EDIT_ID --edit-mode=stage
```

## Agent behavior

- Read current listing state before overwriting a locale.
- Prefer sync commands when the repo already has metadata directories.
- Do not refer to image deletion by checksum or SHA; the CLI deletes by `--id`.
- Do not claim the CLI validates Play image dimensions automatically.
