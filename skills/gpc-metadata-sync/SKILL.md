---
name: gpc-metadata-sync
description: Sync and manage Google Play store listings, images, and screenshots using gpc. Use when updating store metadata, uploading screenshots, or syncing from local directories.
---

# Metadata Sync

Use this skill when you need to update store listings, manage screenshots and graphics, or sync metadata from local directories.

## Store listings

### List all locales

```bash
gpc listings list --package com.example.app
```

### Get a specific locale

```bash
gpc listings get --locale en-US --package com.example.app
```

### Update listing fields

```bash
gpc listings update --locale en-US \
  --title "My App" \
  --short-description "A short tagline" \
  --full-description "Full store description here" \
  --package com.example.app
```

### Sync from directory

```bash
gpc listings sync --dir ./metadata --package com.example.app
```

## Images and screenshots

### Image types

`phoneScreenshots`, `sevenInchScreenshots`, `tenInchScreenshots`, `tvScreenshots`, `wearScreenshots`, `featureGraphic`, `icon`, `tvBanner`, `promoGraphic`

### List images

```bash
gpc images list --locale en-US --type phoneScreenshots --package com.example.app
```

### Upload image

```bash
gpc images upload --locale en-US --type phoneScreenshots --file screenshot1.png --package com.example.app
gpc images upload --locale en-US --type featureGraphic --file feature.png --package com.example.app
gpc images upload --locale en-US --type icon --file icon.png --package com.example.app
```

### Delete specific image

```bash
gpc images delete --locale en-US --type phoneScreenshots --sha1 abc123 --package com.example.app
```

### Delete all images of a type

```bash
gpc images delete-all --locale en-US --type phoneScreenshots --package com.example.app
```

### Sync images from directory

```bash
gpc images sync --dir ./screenshots --package com.example.app
```

## Multi-language workflow

1. Export current listings:
```bash
gpc listings list --package com.example.app -o json > listings.json
```

2. Update each locale:
```bash
gpc listings update --locale ja --title "マイアプリ" --package com.example.app
gpc listings update --locale de --title "Meine App" --package com.example.app
```

3. Upload locale-specific screenshots:
```bash
gpc images upload --locale ja --type phoneScreenshots --file ja_screenshot1.png --package com.example.app
```

## Agent behavior

- Show current listing before overwriting (`gpc listings get --locale <locale>`).
- Confirm with user before bulk updates across multiple locales.
- Use `--dry-run` when syncing from directories if available.
- Validate image dimensions match Google Play requirements before uploading.

## Notes

- Google Play requires at least 2 phone screenshots per locale.
- Feature graphic must be 1024x500 pixels.
- Icon must be 512x512 pixels.
- Use `gpc listings sync --dir` for Fastlane-compatible directory structures.
