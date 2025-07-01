---
layout: ../../layouts/MarkdownProjectLayout.astro
title: 'ERP Integration'
description: 'Led the technical design and implementation of an integration with the leading brewery ERP provider to import and sync resources across platforms.'
startDate: 2025-06-25
endDate: 2025-06-25
client: 'Kegshoe'
tags: ["OAuth", "Integration", "ERP"]
images: [
    {
        url: 'src/assets/project-images/ekos-integration-page.jpg',
        alt: 'Kegshoe dashboard showing integrations page'
    },
    {
        url: 'src/assets/project-images/ekos-setup.jpg',
        alt: 'Kegshoe dashboard showing ERP integration setup page'
    },
]
---

### ERP Integration with Ekos
We sync customer and storage locations, products, and product batches 1-way from Ekos to Kegshoe. This saves headache of updating the same resources on two platforms for our customers who also use Ekos. We also send unit scans to Ekos, which they use for inventory and invoicing purposes.

Building OAuth client implementation to connect to them, they connect to our OAuth server. On auth connection success, we add a message to Rabbit queue and a consumer picks it up. Each message has an action type and other data to tell the consumer what to do with it. The consumer pulls the resources from the Ekos API and performs a de-duplication algorithm with existing Kegshoe records. The user reviews and makes any necessary changes to these matches through the dashboard and submits. This process repeats for each resource type, then the integration setup is considered complete. We expose an API for Ekos to send resource creations, updates, and deletions to stay in sync after the initial import/setup step.

### De-duplication/matching algorithm
Assignment problem. Algorithm for Ekos integration. Had to de-dupe/determine matches between external records and internal records.

Standardize keys for matching. Estimate memory usage before choosing which algorithm to use. If too many combinations, use local greedy assignment, which is less optimal global result. If not going to run out of memory by using global greedy, use that. Go through one by one and compute score based on a scoring function (name string token similarity, location coordinates), then if the score is within the "possible match" threshold, store it in score matrix (array). If it's not above the threshold, don't assign anything to that location in the score matrix (sparse matrix). This saves space.

After scoring is complete, assign matches based on best score. Remove from pool of available matches, until all external records have been matched with existing internal records, or no matches found and they are to be created internally.
