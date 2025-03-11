# Caching

Next.js improves your application's performance and reduces costs by caching rendering work and data requests. This page provides an in-depth look at Next.js caching mechanisms, the APIs you can use to configure them, and how they interact with each other.

## Overview

Here's a high-level overview of the different caching mechanisms and their purpose:

| **Mechanism** | **What** | **Where** | **Purpose** | **Duration** |
| --- | --- | --- | --- | --- |
| Request Memoization | Return values of functions | Server | Re-use data in a React Component tree | Per-request lifecycle |
| Data Cache | Data | Server | Store data across user requests and deployments | Persistent (can be revalidated) |
| Full Route Cache | HTML and RSC payload | Server | Reduce rendering cost and improve performance | Persistent (can be revalidated) |
| Router Cache | RSC Payload | Client | Reduce server requests on navigation | User session or time-based |

By default, Next.js will cache as much as possible to improve performance and reduce cost. This means routes are **statically rendered** and data requests are **cached** unless you opt out. The diagram below shows the default caching behavior: when a route is statically rendered at build time and when a static route is first visited.

[caching-overview.avif](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/caching-overview.avif)

Caching behavior changes depending on whether the route is statically or dynamically rendered, data is cached or uncached, and whether a request is part of an initial visit or a subsequent navigation. Depending on your use case, you can configure the caching behavior for individual routes and data requests.

[**Request Memoization**](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/Request%20Memoization%201b2aeacbb29981a2abc1f334e41bece7.md)

[Data Cache](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/Data%20Cache%201b2aeacbb29981389260fe493dc39137.md)

[**Full Route Cache**](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/Full%20Route%20Cache%201b2aeacbb2998180ad63f7b56f5795ad.md)

[**Router Cache**](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/Router%20Cache%201b2aeacbb299814cb23adf3a16dc9dc9.md)

[**Cache Interactions**](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/Cache%20Interactions%201b2aeacbb299815f98bcc18f2fee6a7a.md)

[APIs](Caching%201b2aeacbb299812880a2eb1b6d17b6ea/APIs%201b2aeacbb299812baba4cbdd8a7e0265.md)