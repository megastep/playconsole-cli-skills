---
name: gpc-cli-usage
description: Guidance for using the Play Console CLI (gpc) — package resolution, profiles, project config, output formats, edit submission modes, and safety conventions. Use when asked to run or design gpc commands.
---

# GPC CLI Usage

Use this skill when you need the right `gpc` command shape, global flags, or setup flow.

## Resolve package and profile first

`gpc` can get the package name from several places. Prefer the most local source already present in the project:

```bash
gpc init --package com.example.app
gpc auth login --credentials ~/.config/gpc/service-account.json --name work --default-package com.example.app
gpc auth current
```

Package resolution order is effectively:
- `--package`
- `GPC_PACKAGE`
- current profile default package
- nearest `.gpc.yaml`

If none are set, add `--package` explicitly.

## Command discovery

Confirm the real command tree before composing anything non-trivial:

```bash
gpc --help
gpc bundles --help
gpc tracks update --help
gpc testing testers add --help
```

## Global flags

Common global flags:
- `--package`, `-p`
- `--profile`
- `--output`, `-o` with `json`, `table`, `minimal`, `tsv`, `csv`, `yaml`
- `--pretty`
- `--quiet`, `-q`
- `--debug`
- `--timeout`
- `--dry-run`
- `--edit-mode` with `live`, `stage`, `open`

Default output is JSON. Use `-o table` for human review and JSON for piping.

```bash
gpc apps list -o table
gpc reviews list -o json | jq .
gpc tracks list --pretty
```

## Edit-backed mutations

Many mutating commands support edit submission control. Prefer `--edit-mode` over legacy compatibility flags:

```bash
gpc bundles upload --file app.aab --track production --edit-mode=stage
gpc listings sync --dir ./metadata --edit-mode=open
gpc edits commit --edit-id EDIT_ID --edit-mode=stage
```

Compatibility aliases still exist during rollout:
- `--stage`
- `--commit=false`

Prefer not to introduce those in new examples unless you are maintaining old scripts.

## Auth and setup

Recommended setup paths:

```bash
gpc setup --auto
gpc auth list
gpc auth switch --name work
gpc doctor
gpc doctor --verbose
```

Useful environment variables:
- `GPC_PACKAGE`
- `GPC_PROFILE`
- `GPC_OUTPUT`
- `GPC_EDIT_MODE`
- `GPC_TIMEOUT`
- `GPC_CREDENTIALS_PATH`
- `GPC_CREDENTIALS_B64`

## Agent behavior

- Prefer examples that work with a configured package instead of always repeating `--package`.
- Add `--package` explicitly when there is no evidence that a default package is configured.
- Use `--dry-run` before destructive operations when supported.
- Use `--confirm` explicitly for destructive commands; never simulate confirmation with shell tricks.
