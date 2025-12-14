---
url: "https://creator.poe.com/api-reference/rate-limits"
title: "Rate Limits | Poe Creator Platform"
---

# Rate Limits

## [Overview](https://creator.poe.com/api-reference/rate-limits\#overview)

The Poe API implements rate limiting to ensure fair usage and maintain service quality for all users. Understanding and properly handling these limits is essential for building robust integrations.

**Current Rate Limit:** 500 requests per minute (RPM)

Need Higher Limits?

If your application requires higher rate limits, please reach out to our team at **[developers@poe.com](mailto:developers@poe.com)** to discuss your use case.

* * *

## [Rate Limit Headers](https://creator.poe.com/api-reference/rate-limits\#rate-limit-headers)

Every API response includes headers that help you track your current rate limit status:

| Header | Description | Example Value |
| --- | --- | --- |
| `x-ratelimit-limit-requests` | Maximum number of requests allowed per minute | `500` |
| `x-ratelimit-remaining-requests` | Number of requests remaining in the current window | `499` |
| `x-ratelimit-reset-requests` | Time in seconds until the rate limit window resets | `1` |

**Example Response Headers:**

```
< x-ratelimit-remaining-requests: 499
< x-ratelimit-limit-requests: 500
< x-ratelimit-reset-requests: 1
```

Monitor Your Usage

Use these headers to track your consumption and implement proactive throttling before hitting the limit.

* * *

## [Handling Rate Limits Gracefully](https://creator.poe.com/api-reference/rate-limits\#handling-rate-limits-gracefully)

When your application exceeds the rate limit, the API will respond with a `429 Too Many Requests` status code. Implementing proper retry logic is essential for a robust integration.

### [Watch for 429 Status Codes](https://creator.poe.com/api-reference/rate-limits\#watch-for-429-status-codes)

Your application should always check for HTTP 429 responses and handle them appropriately rather than treating them as fatal errors.

Build Retry Logic

Never ignore 429 responses. Always implement a retry mechanism to ensure your application continues working once the rate limit window resets.

### [Exponential Backoff Strategy](https://creator.poe.com/api-reference/rate-limits\#exponential-backoff-strategy)

A basic technique for handling rate limits is to implement **exponential backoff** when you receive a 429 response:

1. **Initial retry delay:** Start with a short delay (e.g., 1 second)
2. **Increase exponentially:** Double the delay with each subsequent 429 (1s → 2s → 4s → 8s)
3. **Add randomness (jitter):** Add random variation to prevent thundering herd effects
4. **Set a maximum:** Cap the maximum retry delay to avoid indefinite waits

**Why add randomness?** If many clients hit the limit simultaneously and all retry at the same intervals, they'll create synchronized waves of traffic. Adding jitter (random delays) spreads out the retry attempts.

### [Global Traffic Control](https://creator.poe.com/api-reference/rate-limits\#global-traffic-control)

For more sophisticated applications, consider implementing rate limiting on the client side:

- **Token bucket algorithm:** A proven approach for controlling request rates
- **Global tracking:** Monitor rate limit consumption across all parts of your application
- **Proactive throttling:** Reduce request volume when you detect you're approaching limits
- **Circuit breaker pattern:** Temporarily stop requests when rate limits are consistently exceeded

Optimize Request Patterns

While retry logic is essential, the best approach is to design your application to stay within rate limits. Batch operations where possible, cache responses, and avoid unnecessary API calls.

* * *

## [Load Testing](https://creator.poe.com/api-reference/rate-limits\#load-testing)

If you're preparing for a major event or want to test your integration under load, follow these best practices:

### [Mock Out API Requests](https://creator.poe.com/api-reference/rate-limits\#mock-out-api-requests)

Build a configurable system for mocking Poe API requests during load tests. This allows you to:

- Test your application's behavior at scale without consuming your rate limit
- Avoid affecting production API availability
- Simulate various response scenarios (including rate limit errors)

### [Simulate Realistic Latency](https://creator.poe.com/api-reference/rate-limits\#simulate-realistic-latency)

For accurate load test results, simulate network latency in your mocked responses:

1. **Sample real API calls:** Measure actual response times from live Poe API requests
2. **Apply delays:** Use these measurements to add realistic sleep times to your mocked responses
3. **Vary the delays:** Use a distribution of latency values rather than a fixed delay

This approach ensures your load tests reflect real-world performance characteristics.

Don't Load Test Production

Never run load tests against the live Poe API. Always use mocked endpoints to avoid consuming your rate limit and affecting service availability.

* * *

## [Usage Tracking](https://creator.poe.com/api-reference/rate-limits\#usage-tracking)

### [Usage API](https://creator.poe.com/api-reference/rate-limits\#usage-api)

If you need detailed information about your API usage, including a log of all your API calls, use the **Usage API**.

The Usage API provides:

- Historical usage data
- Request counts and patterns
- Point consumption tracking
- Detailed call logs

Learn more about tracking your API usage in the [Usage API documentation](https://creator.poe.com/docs/resources/usage-api).

* * *

## [Best Practices Summary](https://creator.poe.com/api-reference/rate-limits\#best-practices-summary)

- ✅ **Monitor rate limit headers** in every response
- ✅ **Implement exponential backoff** with jitter for 429 responses
- ✅ **Add client-side rate limiting** for high-volume applications
- ✅ **Cache responses** where appropriate to reduce API calls
- ✅ **Use mocked endpoints** for load testing
- ✅ **Track usage** with the Usage API to understand your patterns
- ❌ **Never ignore 429 errors** \- always retry with backoff
- ❌ **Don't retry immediately** \- respect the rate limit reset time
- ❌ **Don't load test production** \- use mocks instead

Contact Us

Need help optimizing your integration or require higher limits? Reach out to **[developers@poe.com](mailto:developers@poe.com)** \- we're here to help!