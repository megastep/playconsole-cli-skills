---
name: gpc-team-access
description: Manage Play Console users, app grants, roles, and revocations using gpc. Use when granting or revoking developer access.
---

# Team Access

Use this skill for `users` workflows.

## List users

`gpc users list` does not require an app package:

```bash
gpc users list
gpc users list -o table
```

## Grant and revoke app access

Grant and revoke are package-specific:

```bash
gpc users grant --email developer@example.com --role releaseManager
gpc users revoke --email developer@example.com --confirm
```

Supported role values:
- `admin`
- `releaseManager`
- `appOwner`

## Agent behavior

- List current users before changing access.
- Use the least-privilege role that satisfies the request.
- Require explicit approval before revoking access.
- Do not claim every `users` command needs `--package`; only grant and revoke do.
