---
name: gpc-monetization
description: Manage in-app products, subscriptions, base plans, and subscription offers using gpc. Use when creating or updating monetization catalog.
---

# Monetization

Use this skill when managing in-app products (one-time purchases), subscriptions, base plans, or subscription offers.

## In-app products (one-time)

### List products

```bash
gpc products list --package com.example.app
gpc products list --page-size 50 --package com.example.app
```

### Get product details

```bash
gpc products get --product-id premium_upgrade --package com.example.app
```

### Create product

```bash
gpc products create --product-id premium_upgrade \
  --title "Premium Upgrade" \
  --description "Unlock all features" \
  --package com.example.app
```

### Create from JSON file

```bash
gpc products create --product-id premium_upgrade --file product.json --package com.example.app
```

### Update product

```bash
gpc products update --product-id premium_upgrade \
  --title "Premium Upgrade v2" \
  --package com.example.app
```

### Delete product

```bash
gpc products delete --product-id premium_upgrade --confirm --package com.example.app
```

## Subscriptions

### List subscriptions

```bash
gpc subscriptions list --package com.example.app
gpc subscriptions list --max-results 100 --package com.example.app
```

### Get subscription

```bash
gpc subscriptions get --product-id monthly_pro --package com.example.app
```

### Create subscription

```bash
gpc subscriptions create --product-id monthly_pro --file subscription.json --package com.example.app
```

## Base plans

### List base plans for a subscription

```bash
gpc subscriptions base-plans list --product-id monthly_pro --package com.example.app
```

### Create base plan

```bash
gpc subscriptions base-plans create --product-id monthly_pro --file baseplan.json --package com.example.app
```

### Get pricing

```bash
gpc subscriptions pricing get --product-id monthly_pro --base-plan p1m --package com.example.app
```

## Subscription offers

### List offers

```bash
gpc offers list --product-id monthly_pro --base-plan p1m --package com.example.app
```

### Get offer details

```bash
gpc offers get --product-id monthly_pro --base-plan p1m --offer-id free_trial --package com.example.app
```

### Create offer

```bash
gpc offers create --product-id monthly_pro --base-plan p1m --file offer.json --package com.example.app
```

### Update offer

```bash
gpc offers update --product-id monthly_pro --base-plan p1m --offer-id free_trial --file offer.json --package com.example.app
```

### Activate / deactivate offer

```bash
gpc offers activate --product-id monthly_pro --base-plan p1m --offer-id free_trial --package com.example.app
gpc offers deactivate --product-id monthly_pro --base-plan p1m --offer-id free_trial --package com.example.app
```

### Delete offer

```bash
gpc offers delete --product-id monthly_pro --base-plan p1m --offer-id free_trial --confirm --package com.example.app
```

## Agent behavior

- Always list existing products/subscriptions before creating to avoid duplicates.
- Confirm with user before deleting products (irreversible).
- Use `--confirm` flag explicitly for destructive operations.
- Show current state before and after updates.

## Notes

- Products and subscriptions require active base plans to be purchasable.
- Use JSON files for complex product definitions with multiple fields.
- Subscription hierarchy: Subscription → Base Plan → Offer.
