# Cache Header Reference

Complete reference of cache-related HTTP headers supported by the Magnolia PaaS CDN layer.

## Response Headers

| Header | Type | Description |
|--------|------|-------------|
| `Cache-Control` | Standard | Controls browser caching behavior |
| `Surrogate-Control` | CDN | Controls CDN edge caching, stripped before reaching the browser |
| `X-Cache` | Diagnostic | Indicates whether the response was a CDN cache hit or miss |
| `X-Cache-TTL` | Diagnostic | Remaining TTL in seconds for the cached object |
| `Vary` | Standard | Specifies which request headers affect caching |

## Cache-Control Directives

| Directive | Example | Description |
|-----------|---------|-------------|
| `public` | `Cache-Control: public` | Response can be cached by any cache |
| `private` | `Cache-Control: private` | Response is specific to one user, not cacheable by CDN |
| `max-age` | `max-age=3600` | Maximum time in seconds the response is considered fresh |
| `s-maxage` | `s-maxage=86400` | Overrides `max-age` for shared caches (CDN) |
| `no-cache` | `Cache-Control: no-cache` | Must revalidate with origin before serving cached copy |
| `no-store` | `Cache-Control: no-store` | Must not cache the response at all |
| `immutable` | `Cache-Control: immutable` | Indicates the response body will not change |
| `stale-while-revalidate` | `stale-while-revalidate=60` | Serve stale content while fetching a fresh version |

## Surrogate-Control Directives

The CDN processes `Surrogate-Control` headers and removes them before forwarding the response to the browser. This allows different caching strategies at each layer.

```
Surrogate-Control: max-age=86400, stale-while-revalidate=3600
Cache-Control: max-age=300
```

In this example, the CDN caches for 24 hours but the browser only caches for 5 minutes.

See [Configure Cache Policies](cache-policies.md) for step-by-step setup instructions.

<!-- include: @shared/example.md -->
