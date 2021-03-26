---
title: "How to deal with cache stampede in MySQL"
published: true
---

The **Cache stampede** problem (also called dog-piling, cache miss storm, or cache choking) is not a big problem for small scale systems but is a common headache for large scale applications with millions of requests. It has the potential to bring down the entire system in a matter of seconds.

<img width="80%" src="https://1.bp.blogspot.com/-v087GjnruQM/Xx5OUkhr9qI/AAAAAAAB2QE/Cec2qzUeqnQ39IUtOq0jlt6S1Knwma53wCLcBGAsYHQ/d/1_Gl4ajUBKwY6uZxlT84x4GQ.png" />

## What is Cache Stampede
Consider an item that is expensive to generate, and is cached. When the cache expires, the application usually regenerates the item and writes to the cache, and continue as normal. Under very high load, when the cached item expires, multiple requests will get a cache miss and all of them will try to regenerate the cache simultaneously, which will cause a high load in the database.

Cache Stampede can occur with any cache including MySQL query cache, or any external cache like Redis or Memcached. It is ok to ignore this problem when your application is small scale but very important to address the issues as you scale up. 

Cache stampede can be seen as random spikes in the CPU usage of your database server.

## Solutions
#### Optimize query
Optimizing database queries is something that needs to be done in any case. When a cache stampede occurs, it is important for the query to finish faster. All requests will start piling up on the database until the first query is finished. If the query finishes faster, the impact of stampede will reduce. 

#### Locking
Before regenerating the cache after a cache miss, make sure to get a lock to regenerate the cache. You can put a special value in the cache indicating that it is being updated so that all other requests can wait rather than starting to regenerate it.

Locking can cause starvation and hung requests which is much better than a stampede but still can cause performance degradation. You can try out other solutions like having a stale value in cache until the regeneration is complete.

This solution is not possible for MySQL query cache, as MySQL takes care of cache invalidation and regeneration but can be implemented in other external caches that you implement.

#### Pre-Populate the cache
With this solution, you are making sure that a cache-miss never occurs, and thereby no cache-stampede. This works best when there are few hot cache entries that cause the problem. Consider a cache item that expires every 30 minutes. You can run a cache refresh every 25 minutes so that you never get a cache-miss.

The disadvantage is that you'll have to maintain an external process for regenerating cache.

#### Probabilistic early expiration
With this solution, processes recompute the value on their own before the expiration of the cache. But each process makes its own independent decision whether to recompute the cache or not, based on some parameters or random values. The probability of recomputation increases as it gets closer to the expiration of the cache value. This can still cause multiple processes generating cache simultaneously, but much less than that of a stampede.

## Read more
- [Cache Stampede (Wikipedia)](https://en.wikipedia.org/wiki/Cache_stampede)
- Facebook outage due to cache stampede : <https://www.facebook.com/notes/facebook-engineering/more-details-on-todays-outage/431441338919>