---
title: "API Options"
weight: 1
---

### [&#128279;](#api-options) API Options

All API endpoint definitions (described in [Defining API Endpoints](#defining-api-endpoints)) conform to the same structure so they can eventually be merged together during compilation. This dictates the top-level structure of the definition, which is rigid but useful. The attribute `opts` allows for optional configuration, extending endpoint definitions as needed. For most endpoints `opts` will be defined as an empty object. Currently supported options are as follows:

```typescript
export type ApiOptions = {
  readonly cache?: 'skip' | number | boolean | null | undefined;
  readonly load?: boolean | undefined;
  readonly throttle?: 'skip' | number | undefined;
  readonly contentType?: string | undefined;
}
```

- `cache`:
  - Only GET requests are cached.
  - GET requests are cached automatically, unless they are marked with `'skip'`.
  - Any non-GET request resets the cache for that same URL, as a mutation should have occured.
  - The minimum duration for caching a GET request is 180 seconds, unless specified by a number.
  - `null` will cache the response indefinitely.
- `load`: Forces a loading screen during transmission.
- `throttle`: Throttle the endpoint. The default rate limit is 10 requests per 10 seconds. A throttle of 60 would allow for 10 requests per minute; 1 would allow for 10 requests per second.
- `contentType`: Currently the only supported alternative content type is `octet-stream`, which is used for file uploads. 