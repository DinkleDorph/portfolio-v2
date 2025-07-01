---
layout: ../../layouts/MarkdownProjectLayout.astro
title: 'Location Timeline'
description: 'Implemented a paginated activity timeline for customer locations, aggregating from multiple data sources.'
startDate: 2024-06-25
client: 'Kegshoe'
tags: ["Locations", "Timeline"]
images: [
    {
        url: 'src/assets/project-images/timeline.jpg',
        alt: 'Location timeline showing various events'
    },
    {
        url: 'src/assets/project-images/timeline-1.jpg',
        alt: 'Location timeline showing pagination button'
    },
]
---

### Location Timeline
We show an activity timeline on locations that includes events like CRM interactions, unit actions, and sales rep assignment changes. This timeline is paginated, and can be filtered by date range. This is useful for contextualizing separate types of events and compiling them into one coherent timeline, centered around locations (customer location pages are the customer profile basically).
