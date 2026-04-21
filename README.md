# playconsole-cli skills

A collection of Agent Skills for shipping with the [Play Console CLI](https://github.com/AndroidPoet/playconsole-cli) (`gpc`). These skills teach AI coding agents how to automate Google Play Console workflows — releases, metadata, monetization, testing, vitals, and more.

Skills follow the [Agent Skills](https://github.com/anthropics/agent-skills) format.

## Available Skills

### gpc-cli-usage

Guidance for running `gpc` commands — package resolution, profiles, project config, output formats, edit modes, and safety conventions.

**Use when:**
- You need the correct `gpc` command or flag combination
- You want to configure auth profiles or output formats

### gpc-release-flow

End-to-end release workflows — upload bundles, manage tracks, staged rollouts, promotions, halts, completions, and manual edits.

**Use when:**
- You need to upload a build and release it
- You're managing staged rollouts or promoting between tracks
- You need the manual edit lifecycle for atomic multi-step changes

### gpc-metadata-sync

Sync and manage store listings, images, and screenshots.

**Use when:**
- You're updating store metadata or localizations
- You need to upload screenshots or graphics
- You want optional per-file image upload progress with `--progress`
- You want to sync from a local directory structure

### gpc-monetization

Manage in-app products, subscriptions, base plans, and subscription offers.

**Use when:**
- You're creating or updating one-time products
- You need to manage subscription base plans and offers
- You want to activate, deactivate, or price subscription offers

### gpc-testing

Manage testing tracks, testers, tester groups, and internal app sharing.

**Use when:**
- You need to set up testing workflows
- You're adding or removing testers
- You want to share internal builds directly

### gpc-vitals

View vitals and grouped error-reporting commands — crashes, ANRs, startup, rendering, wakeups, wakelocks, memory, and issues.

**Use when:**
- You need to check app health and performance metrics
- You want to identify regressions after a release
- You're triaging crash or ANR rate issues

### gpc-build-lifecycle

Manage app bundles, legacy APKs, build processing, and deobfuscation uploads.

**Use when:**
- You're uploading builds in a CI/CD pipeline
- You need to wait for build processing to complete
- You want to upload ProGuard mappings or native debug symbols

### gpc-purchase-orders

Verify purchases, inspect subscription status, process refunds, and manage external transactions.

**Use when:**
- You need to verify a purchase token
- You're processing refunds or checking order details
- You're working with alternative billing external transactions

### gpc-review-management

List, filter, and reply to Google Play reviews.

**Use when:**
- You need to triage negative reviews
- You want to reply to user feedback
- You're monitoring review sentiment

### gpc-team-access

Manage Play Console users, app grants, roles, and revocations.

**Use when:**
- You need to grant or revoke developer access
- You're setting up roles for team members

### gpc-app-recovery

Create, target, deploy, and cancel app recovery actions for critical issues.

**Use when:**
- You're responding to a critical app issue
- You need to notify affected users about a fix

### gpc-device-management

Manage country availability, device tiers, device catalog views, report metadata, and draft-vs-live summaries.

**Use when:**
- You need to manage country targeting
- You're configuring device tier delivery
- You want to compare draft vs live state

## Installation

```bash
npx skills add AndroidPoet/playconsole-cli-skills
```

## Usage

Skills are automatically available once installed. The agent will use them when relevant tasks are detected.

**Examples:**

```
Upload my AAB to the internal track and wait for processing
```

```
Show me the crash rate for the last 7 days
```

```
List all 1-star reviews and help me draft replies
```

```
Create a new subscription with a monthly base plan and a free trial offer
```

```
Set up a staged rollout to production starting at 5%
```

## Skill Structure

Each skill contains:
- `SKILL.md` — Instructions for the agent

## License

MIT
