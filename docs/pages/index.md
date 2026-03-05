# CDN Overview

The Content Delivery Network (CDN) layer in Magnolia PaaS sits between the public internet and your author/public instances. It caches rendered pages and static assets at edge locations worldwide, reducing latency for end users and offloading traffic from your origin servers.

## How the CDN Works

When a visitor requests a page, the CDN checks its edge cache first. If a cached copy exists and hasn't expired, the CDN serves it directly without contacting your Magnolia instance. This is a cache hit. If no cached copy exists or it has expired, the CDN forwards the request to your origin server, caches the response, and serves it to the visitor. This is a cache miss.

The CDN respects two distinct sets of cache headers: browser cache headers (`Cache-Control`) that tell the visitor's browser how long to cache locally, and CDN cache headers (`Surrogate-Control`) that tell the CDN itself how long to cache at the edge. These operate independently, giving you fine-grained control over caching behavior at each layer.

## When to Use CDN Caching

CDN caching is most effective for content that changes infrequently and is accessed by many users. Public-facing marketing pages, product catalogs, and documentation are ideal candidates. Personalized content, authenticated pages, and rapidly changing data should bypass the CDN cache or use very short TTLs.

See [Cache Policies](configuration/cache-policies.md) for detailed configuration instructions and [Headers](configuration/headers.md) for the full reference of supported headers.
