<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into your **DevEvent** Next.js App Router project. Here's a summary of all changes made:

- **`instrumentation-client.ts`** (new): Initializes PostHog client-side using the Next.js 15.3+ `instrumentation-client` convention. Configured with a reverse proxy (`/ingest`), exception capture for error tracking, and debug mode in development.
- **`next.config.ts`** (updated): Added reverse proxy rewrites so PostHog requests route through your own domain (`/ingest/*` → PostHog), reducing the chance of ad-blocker interception. Also set `skipTrailingSlashRedirect: true` as required by PostHog.
- **`components/ExploreBtn.tsx`** (updated): Added `posthog.capture("explore_events_clicked")` to the existing button `onClick` handler.
- **`components/EventCard.tsx`** (updated): Converted to a client component (`"use client"`) and added `posthog.capture("event_card_clicked", { event_title, event_slug, event_location, event_date })` on the card link click.
- **`.env.local`** (new): Created with `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` — automatically added to `.gitignore`.

## Events tracked

| Event name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the "Explore Events" CTA button on the homepage hero | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks an event card to view event details (captures title, slug, location, date) | `components/EventCard.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard**: [Analytics basics](https://us.posthog.com/project/400779/dashboard/1518640)
- **Insight**: [Explore Events button clicks over time](https://us.posthog.com/project/400779/insights/Dc6hnFUz)
- **Insight**: [Event card clicks over time](https://us.posthog.com/project/400779/insights/93ABSMQ9)
- **Insight**: [Most popular events by clicks](https://us.posthog.com/project/400779/insights/ukh7tlTr)
- **Insight**: [Homepage to event detail funnel](https://us.posthog.com/project/400779/insights/SV0WwYiZ)
- **Insight**: [Event clicks by location](https://us.posthog.com/project/400779/insights/R5HlYXbZ)

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
