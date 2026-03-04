---
name: gpc-team-access
description: Manage team member access, roles, and permissions for Google Play Console using gpc. Use when granting or revoking developer access.
---

# Team Access Management

Use this skill when managing team member access, roles, and permissions.

## List team members

```bash
gpc users list --package com.example.app
gpc users list --package com.example.app -o table
```

## Grant access

```bash
gpc users grant --email developer@example.com --role releaseManager --package com.example.app
```

### Available roles

| Role | Description |
|------|-------------|
| `admin` | Full access to all features |
| `releaseManager` | Manage releases, tracks, and builds |
| `appOwner` | App-level ownership and settings |

## Revoke access

```bash
gpc users revoke --email developer@example.com --package com.example.app
```

## Agent behavior

- List current users before granting or revoking access.
- Confirm with user before revoking access (irreversible for that session).
- Use the least-privilege role that matches the need.

## Notes

- Access is managed per-app via the package name.
- Changes take effect immediately.
- Service account access is separate from user access.
