---
name: gpc-review-management
description: List, filter, and reply to Google Play reviews using gpc. Use when managing user reviews or responding to feedback.
---

# Review Management

Use this skill when listing reviews, filtering by rating, or replying to user feedback.

## List reviews

```bash
gpc reviews list --package com.example.app
gpc reviews list --max-results 50 --package com.example.app
```

### Filter by rating

```bash
gpc reviews list --min-rating 1 --max-rating 2 --package com.example.app    # Negative reviews
gpc reviews list --min-rating 4 --max-rating 5 --package com.example.app    # Positive reviews
```

### With translation

```bash
gpc reviews list --translation-lang en --package com.example.app
```

### Paginate

```bash
gpc reviews list --max-results 20 --start-index 0 --package com.example.app
gpc reviews list --max-results 20 --start-index 20 --package com.example.app
```

## Get specific review

```bash
gpc reviews get --review-id abc123 --package com.example.app
gpc reviews get --review-id abc123 --translation-lang en --package com.example.app
```

## Reply to review

```bash
gpc reviews reply --review-id abc123 --text "Thank you for your feedback!" --package com.example.app
```

## Review triage workflow

1. List low-rated reviews:
```bash
gpc reviews list --min-rating 1 --max-rating 3 --translation-lang en --package com.example.app -o table
```

2. Inspect specific reviews:
```bash
gpc reviews get --review-id $REVIEW_ID --package com.example.app
```

3. Reply to each:
```bash
gpc reviews reply --review-id $REVIEW_ID --text "We're sorry about this issue. We've fixed it in the latest update." --package com.example.app
```

## Agent behavior

- Show reviews in table format for readability.
- Draft reply text and show to user before sending.
- Never auto-reply to reviews without user approval.
- Use `--translation-lang en` when reviews may be in other languages.

## Notes

- Only the latest developer reply is visible on the store.
- Replying to a review replaces any previous reply.
- Google Play may auto-translate replies for users in other locales.
