---
name: gpc-monetization
description: Manage one-time products, subscriptions, base plans, and subscription offers using gpc. Use when creating or updating the Play monetization catalog.
---

# Monetization

Use this skill for product catalog work under `products`, `subscriptions`, and `offers`.

## One-time products

```bash
gpc products list
gpc products get --product-id premium_unlock
gpc products create --product-id coins_100 --file product.json
gpc products create --product-id premium_unlock --title "Premium" --description "Unlock all features"
gpc products update --product-id coins_100 --file product.json
gpc products delete --product-id coins_100 --confirm
```

`gpc products list` supports pagination:

```bash
gpc products list --page-size 50
```

## Subscriptions and base plans

```bash
gpc subscriptions list
gpc subscriptions get --product-id monthly_pro
gpc subscriptions create --product-id monthly_pro --file subscription.json
gpc subscriptions base-plans list --product-id monthly_pro
gpc subscriptions base-plans create --product-id monthly_pro --file baseplan.json
gpc subscriptions pricing get --product-id monthly_pro --base-plan monthly
```

## Offers

```bash
gpc offers list --product-id monthly_pro --base-plan monthly
gpc offers get --product-id monthly_pro --base-plan monthly --offer-id free_trial
gpc offers create --product-id monthly_pro --base-plan monthly --file offer.json
gpc offers update --product-id monthly_pro --base-plan monthly --offer-id free_trial --file offer.json
gpc offers activate --product-id monthly_pro --base-plan monthly --offer-id free_trial
gpc offers deactivate --product-id monthly_pro --base-plan monthly --offer-id free_trial
gpc offers delete --product-id monthly_pro --base-plan monthly --offer-id free_trial --confirm
```

## Agent behavior

- List existing products or subscriptions before creating similar IDs.
- Use JSON files for subscriptions, base plans, and offers.
- Use `--confirm` explicitly for deletions.
- Model the hierarchy correctly: subscription -> base plan -> offer.
