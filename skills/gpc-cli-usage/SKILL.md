---
name: gpc-cli-usage
description: Guidance for using the Play Console CLI (gpc) — flags, output formats, auth profiles, pagination, and safety conventions. Use when asked to run or design gpc commands.
---

# GPC CLI Usage

Use this skill when you need to run or design `gpc` commands for Google Play Console workflows.

## Command discovery

Always confirm commands and flags before running:

```bash
gpc --help
gpc tracks --help
gpc bundles upload --help
```

## Flag conventions

- Use explicit long flags: `--package`, `--track`, `--output`.
- No interactive prompts; destructive operations require `--confirm`.
- Short aliases: `-p` (package), `-o` (output), `-q` (quiet).

## Output formats

Default output is minified JSON. Available formats:

```bash
gpc apps list -o json          # Default, machine-readable
gpc apps list -o table         # Human-readable columns
gpc apps list -o yaml          # YAML format
gpc apps list -o csv           # CSV for spreadsheets
gpc apps list -o tsv           # Tab-separated
gpc apps list -o minimal       # Compact output
gpc apps list --pretty         # Pretty-print JSON
```

Use `--pretty` for debugging. Use `-o json` (default) for automation and piping to `jq`.

## Authentication

### Configure a profile

```bash
gpc auth login --credentials /path/to/service-account.json --name myprofile --default-package com.example.app
```

### Switch profiles

```bash
gpc auth list
gpc auth current
gpc auth switch --name otherprofile
```

### Environment variables for CI

| Variable | Purpose |
|----------|---------|
| `GPC_CREDENTIALS_PATH` | Path to service account JSON |
| `GPC_CREDENTIALS_B64` | Base64-encoded credentials |
| `GPC_PACKAGE` | Default package name |
| `GPC_PROFILE` | Default auth profile |
| `GPC_OUTPUT` | Default output format |

### Diagnostics

```bash
gpc doctor              # Check config, credentials, API access
gpc doctor --verbose    # Detailed diagnostic output
```

## Global flags

| Flag | Short | Description |
|------|-------|-------------|
| `--package` | `-p` | App package name (or `GPC_PACKAGE`) |
| `--output` | `-o` | Output format (json, table, yaml, csv, tsv, minimal) |
| `--pretty` | | Pretty-print JSON |
| `--quiet` | `-q` | Suppress non-essential output |
| `--debug` | | Show API requests/responses |
| `--dry-run` | | Preview without applying changes |
| `--timeout` | | Request timeout (default 60s) |
| `--profile` | | Auth profile name |

## Safety

- Use `--dry-run` before destructive operations.
- Use `--confirm` flags explicitly; never pipe `yes` into commands.
- Check `gpc doctor` before troubleshooting auth issues.

## Agent behavior

- Always pass `--package` explicitly unless `GPC_PACKAGE` is confirmed set.
- Prefer `--output json` for parsing; use `--output table` when showing results to the user.
- Run `gpc doctor` first if auth errors occur.
