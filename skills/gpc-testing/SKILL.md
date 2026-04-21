---
name: gpc-testing
description: Manage testing tracks, testers, tester groups, and internal app sharing using gpc. Use when setting up or operating Play testing workflows.
---

# Testing

Use this skill for internal releases, tester assignment, and internal app sharing.

## Internal testing

```bash
gpc testing internal list
gpc bundles upload --file app.aab --track internal
gpc bundles wait --version-code 42
```

## Internal app sharing

`internal-sharing upload` accepts either `.apk` or `.aab`:

```bash
gpc testing internal-sharing upload --file app.aab
```

## Testers

```bash
gpc testing testers list --track beta
gpc testing testers add --track beta --emails "qa@example.com,pm@example.com"
gpc testing testers add --track beta --emails-file testers.txt
gpc testing testers remove --track beta --emails "qa@example.com"
```

Tester changes can use edit submission control:

```bash
gpc testing testers add --track beta --emails-file testers.txt --edit-mode=stage
```

## Tester groups

```bash
gpc testing tester-groups list
```

The CLI treats tester groups as informational only; management still happens through Google Groups.

## Agent behavior

- Use `--emails` or `--emails-file`; do not invent singular `--email` flags.
- Use internal app sharing for fast distribution outside the normal track flow.
- Show current tester state before bulk add or remove operations.
