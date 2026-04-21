---
name: gpc-purchase-orders
description: Verify purchases, inspect subscription status, acknowledge purchases, process refunds, and manage external transactions using gpc.
---

# Purchases And Orders

Use this skill for post-purchase support and billing operations.

## Purchases

```bash
gpc purchases verify --product-id premium_upgrade --token PURCHASE_TOKEN
gpc purchases subscription-status --product-id monthly_pro --token PURCHASE_TOKEN
gpc purchases acknowledge --product-id premium_upgrade --token PURCHASE_TOKEN
gpc purchases voided list
gpc purchases voided list --start-time 2026-04-01T00:00:00Z --end-time 2026-04-21T00:00:00Z
```

## Orders

```bash
gpc orders get --order-id GPA.1234-5678-9012
gpc orders batch-get --order-ids GPA.1234-5678-9012,GPA.9876-5432-1098
gpc orders refund --order-id GPA.1234-5678-9012 --confirm
```

## External transactions

Both command names work:

```bash
gpc external-transactions create --file tx.json
gpc ext-tx get --name "apps/com.example/externalTransactions/TX_ID"
gpc ext-tx refund --name "apps/com.example/externalTransactions/TX_ID" --confirm
```

## Agent behavior

- Inspect the order before refunding it.
- Use `--confirm` explicitly for refunds.
- Treat voided purchase time filters as RFC3339 input.
- Prefer the full `external-transactions` name in new examples and mention `ext-tx` as an alias.
