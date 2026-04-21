---
name: gpc-review-management
description: List, filter, inspect, and reply to Google Play reviews using gpc. Use when triaging reviews or preparing developer responses.
---

# Review Management

Use this skill for review triage and replies.

## Review listing and inspection

```bash
gpc reviews list
gpc reviews list --min-rating 1 --max-rating 2
gpc reviews list --translation-lang en
gpc reviews get --review-id gp:AOqpTO... --translation-lang en
```

## Reply flow

```bash
gpc reviews reply --review-id gp:AOqpTO... --text "Thanks for the report. We shipped a fix in the latest version."
```

## Triage workflow

```bash
gpc reviews list --min-rating 1 --max-rating 3 -o table
gpc reviews get --review-id gp:AOqpTO...
```

## Agent behavior

- Draft reply text before sending it.
- Never auto-post review replies without user approval.
- Use translation when the review language is unclear or does not match the conversation.
- Do not suggest unsupported pagination flags such as `--start-index`.
