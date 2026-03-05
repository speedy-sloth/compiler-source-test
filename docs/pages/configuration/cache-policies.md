# Configure Cache Policies

This guide walks you through setting up browser and CDN cache policies for your Magnolia PaaS public instance.

## Prerequisites

- Access to the Magnolia PaaS cockpit
- A deployed public instance
- Familiarity with [how the CDN works](../overview/index.md)

## Step 1: Open the Cache Configuration Panel

Navigate to your environment in the cockpit and select the **Caching** tab. You will see separate sections for browser caching and CDN caching.

## Step 2: Configure Browser Cache-Control

Browser cache headers determine how long a visitor's browser retains a local copy. Set the `max-age` value in seconds:

```yaml
cache_control:
  public: true
  max_age: 3600        # 1 hour for standard pages
  s_maxage: 86400      # 24 hours at CDN edge
```

For static assets like CSS and JavaScript, longer TTLs are appropriate since these files are typically fingerprinted:

```yaml
static_assets:
  cache_control:
    public: true
    max_age: 31536000   # 1 year
    immutable: true
```

## Step 3: Configure CDN Surrogate-Control

The `Surrogate-Control` header controls caching at the CDN layer independently of browser caching. This allows you to cache aggressively at the edge while keeping browser caches short:

```yaml
surrogate_control:
  max_age: 86400         # CDN caches for 24 hours
  stale_while_revalidate: 3600  # serve stale for 1 hour while refreshing
```

## Step 4: Define Cache Exclusion Rules

Some paths should never be cached. Add exclusion patterns for personalized or dynamic content:

```yaml
exclusions:
  - /api/*
  - /dam/jcr:*
  - /.auth/*
```

## Step 5: Verify Your Configuration

After saving, use the **Cache Inspector** in the cockpit to verify headers on specific URLs. You should see both `Cache-Control` and `Surrogate-Control` headers in the response.

If content appears stale after changes, see [Purging](../troubleshooting/purging.md) to invalidate the CDN cache.

![Cache configuration panel](images/burp.jpg)
