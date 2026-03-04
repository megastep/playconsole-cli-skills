---
name: gpc-build-lifecycle
description: Manage Android app bundles, APKs, build processing, and debug symbol uploads using gpc. Use when uploading builds, checking build status, or uploading ProGuard mappings.
---

# Build Lifecycle

Use this skill when uploading builds, waiting for processing, managing APKs/bundles, or uploading deobfuscation files.

## Bundles (AAB)

### Upload bundle

```bash
gpc bundles upload --file app.aab --track internal --package com.example.app
```

### List uploaded bundles

```bash
gpc bundles list --package com.example.app
```

### Find bundle by version code

```bash
gpc bundles find --version-code 42 --package com.example.app
```

### Wait for processing

```bash
gpc bundles wait --version-code 42 --package com.example.app
gpc bundles wait --version-code 42 --timeout 600 --interval 30 --package com.example.app
```

## APKs (legacy)

### Upload APK

```bash
gpc apks upload --file app.apk --package com.example.app
```

### List APKs

```bash
gpc apks list --package com.example.app
```

## Deobfuscation files

### Upload ProGuard mapping

```bash
gpc deobfuscation upload --version-code 42 --file mapping.txt --type proguard --package com.example.app
```

### Upload native debug symbols

```bash
gpc deobfuscation upload --version-code 42 --file symbols.zip --type native-code --package com.example.app
```

## CI/CD build pipeline

Typical CI flow:

```bash
# 1. Upload bundle
gpc bundles upload --file app.aab --track internal --commit --package com.example.app

# 2. Wait for processing
gpc bundles wait --version-code $VERSION_CODE --timeout 600 --package com.example.app

# 3. Upload ProGuard mapping for crash symbolication
gpc deobfuscation upload --version-code $VERSION_CODE --file mapping.txt --type proguard --package com.example.app

# 4. Promote to beta
gpc tracks promote --from internal --to beta --package com.example.app
```

## Agent behavior

- Always use AAB format over APK (APK upload is deprecated).
- Upload deobfuscation files immediately after build upload.
- Use `gpc bundles wait` in CI to block until processing completes.
- Show bundle list after upload to confirm success.

## Notes

- AAB is required for new apps; APK support is for legacy apps.
- ProGuard mappings enable readable crash stacks in Android Vitals.
- Native debug symbols enable symbolicated native crash reports.
- See `gpc-release-flow` skill for track promotion after upload.
