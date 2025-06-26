---
layout: ../../layouts/MarkdownProjectLayout.astro
title: 'In-House Subscriptions'
startDate: 2025-06-25
endDate: 2025-06-25
images: [
    {
        source: 'external',
        url: 'https://picsum.photos/400/300',
        alt: 'Lorum Picsum'
    },
]
tags: ["Subscriptions", "Payments", "Billing", "Stripe"]
---

### In-House Subscriptions
We used to rely on Stripe as the source of truth for customer subscriptions and billing. We had some manually billed customers, but they had to be managed in a hacky way to work around the limitations of the Stripe-based system.

I designed and built a Kegshoe owned subscription system that decoupled payment processing and billing from subscriptions. Subscriptions are properly modelled within Kegshoe. They have payment platform types, which change how the customer's setup flow, subscription management interface, and billing works.

The customer onboarding process includes a setup link that takes the user through the first-time account setup. They enter and review details, then proceed to payment. If they are paying through Stripe, they are taken to a Checkout session. If manually billed, they can start using the platform immediately. We model the setup links as their own entity, so they can includes presets for subscription details and locks for certain fields that were agreed to during the sales and agreements phase.

Before, the subscription management page was limited; it only supported keg tracking subscriptions (not CRM or equipment tracking, which are separate features).

Includes Stripe checkout, improved setup flow, multiple subscription types supported on plan page
