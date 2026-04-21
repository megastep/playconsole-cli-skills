---
name: gpc-build-lifecycle
description: Manage Android app bundles, legacy APKs, build processing, and deobfuscation uploads using gpc. Use when uploading builds, checking processing state, or uploading mapping and symbol files.
---

# Build Lifecycle

Use this skill for artifact upload, processing checks, and crash symbolication inputs.

## Bundles

```bash
gpc bundles upload --file app.aab --track internal
gpc bundles list
gpc bundles find --version-code 42
gpc bundles wait --version-code 42 --timeout 10m --interval 15s
```

Edit submission control:

```bash
gpc bundles upload --file app.aab --track production --edit-mode=stage
gpc bundles upload --file app.aab --track production --edit-mode=open
```

## APKs

`apks` still exists for legacy flows, but prefer bundles for new work.

```bash
gpc apks upload --file app.apk --track internal
gpc apks list
```

## Deobfuscation

```bash
gpc deobfuscation upload --version-code 42 --file mapping.txt --type proguard
gpc deobfuscation upload --version-code 42 --file symbols.zip --type native-code
```

## Typical CI flow

```bash
gpc bundles upload --file app.aab --track internal
gpc bundles wait --version-code 42 --timeout 10m
gpc deobfuscation upload --version-code 42 --file mapping.txt --type proguard
gpc tracks promote --from internal --to beta
```

## Agent behavior

- Prefer AAB unless the user explicitly needs APK.
- Upload mapping or native symbols immediately after the matching version is available.
- Use `gpc bundles wait` in CI when later steps depend on Play processing finishing.
- Use duration syntax like `10m` or `30s` for wait flags.
