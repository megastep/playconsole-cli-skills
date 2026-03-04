---
name: gpc-purchase-orders
description: Verify purchases, check subscription status, process refunds, and manage external transactions using gpc. Use when handling purchase verification or order management.
---

# Purchases & Orders

Use this skill when verifying purchases, checking subscription status, processing refunds, or managing external transactions.

## Purchase verification

### Verify a purchase

```bash
gpc purchases verify --product-id premium_upgrade --token PURCHASE_TOKEN --package com.example.app
```

### Check subscription status

```bash
gpc purchases subscription-status --product-id monthly_pro --token PURCHASE_TOKEN --package com.example.app
```

### Acknowledge a purchase

```bash
gpc purchases acknowledge --product-id premium_upgrade --token PURCHASE_TOKEN --package com.example.app
```

## Voided purchases

### List voided purchases

```bash
gpc purchases voided list --package com.example.app
```

## Orders

### Get order details

```bash
gpc orders get --order-id GPA.1234-5678-9012 --package com.example.app
```

### Get multiple orders

```bash
gpc orders batch-get --order-ids GPA.1234-5678-9012,GPA.9876-5432-1098 --package com.example.app
```

### Refund an order

```bash
gpc orders refund --order-id GPA.1234-5678-9012 --confirm --package com.example.app
```

## External transactions (alternative billing)

### Create external transaction

```bash
gpc ext-tx create --file transaction.json --package com.example.app
```

### Get external transaction

```bash
gpc ext-tx get --name transactions/12345 --package com.example.app
```

### Refund external transaction

```bash
gpc ext-tx refund --name transactions/12345 --confirm --package com.example.app
```

## Agent behavior

- Always verify purchase token validity before taking action.
- Require `--confirm` for refunds; never auto-confirm.
- Show order details before processing refunds.
- Use `gpc orders get` to inspect before `gpc orders refund`.

## Notes

- Purchase tokens come from the client app's billing library.
- Voided purchases include refunds, chargebacks, and revocations.
- External transactions are for apps using alternative billing (requires enrollment).
- `ext-tx` is the short alias for `external-transactions`.
