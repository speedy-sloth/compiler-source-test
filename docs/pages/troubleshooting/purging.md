# Purging the CDN Cache

When you publish content changes in Magnolia, the CDN may continue serving stale cached versions until the TTL expires. Cache purging lets you invalidate specific URLs or entire path patterns immediately.

## Purge a Single URL

1. Open the **Caching** tab in your environment
2. Enter the full URL path (e.g., `/travel/destinations/paris`)
3. Click **Purge**
4. The CDN removes the cached version at all edge locations within 30 seconds

## Purge by Pattern

To invalidate multiple URLs at once, use a wildcard pattern:

1. Enter a path pattern (e.g., `/travel/destinations/*`)
2. Click **Purge All Matching**
3. All cached URLs matching the pattern are invalidated

## Full Cache Purge

A full purge removes every cached object for your environment. Use this sparingly as it causes a temporary spike in origin traffic while the CDN repopulates its cache.

```bash
# Via CLI
magnolia-cli cache purge --environment production --all
magnolia-cli cache purge --environment production --test
```

## Automatic Purge on Publish

Magnolia PaaS can automatically purge relevant URLs when content is published. Enable this in the environment settings under **Cache > Auto-Purge**. The system uses the content path mapping to determine which URLs to invalidate.

For an understanding of how caching works in general, see [CDN Overview](../overview/index.md). For header configuration, see [Cache Policies](../configuration/cache-policies.md).
