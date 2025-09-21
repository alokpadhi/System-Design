Here is a **detailed summary** of the "Introduction to Caching" page, complete with **real-world examples**:

***

### What is Caching?

**Caching** is a technique where a high-speed storage layer is placed between an application and the original data source (like a database, file system, or remote service). When the application needs data:
- It first checks the cache.
- If the data is present (a cache hit), it’s returned immediately.
- If the data isn’t present (a cache miss), it’s fetched from the primary source, returned to the application, and also stored in the cache for future use.

**Goal:**  
Caching aims to **reduce the need to fetch data repeatedly from slower or more expensive data sources**, resulting in faster performance and lower latency.

***

### Types of Data Cached

- **Web pages:** Frequently visited web content can be kept close to users for fast loading.
- **Database queries:** Reused query results can be quickly retrieved.
- **API responses:** Common API requests can be instantly fulfilled.
- **Media:** Images and videos are cached to avoid repeated downloads.

***

### Methods of Implementing Caching

- **In-memory caching:** Stores data in the computer’s RAM (very fast, but more expensive storage).
  - *Real-world example:* Redis or Memcached for storing session data in web applications so user info is retrieved instantly.
- **Disk caching:** Uses storage drives to keep information that can’t fit in RAM.
  - *Real-world example:* Operating systems cache files on disk so repeated access doesn’t require reading from slower hard drives or the network.
- **Database caching:** Keeps hot/frequently-used records inside the database itself to speed up recurring queries.
  - *Real-world example:* E-commerce sites caching popular product listings for faster search.
- **CDN caching:** Stores content on distributed servers globally to serve data quickly to users based on their location.
  - *Real-world example:* Netflix uses CDN caches for popular movies, storing them in servers near major cities so users experience instant playback.

***

### Key Caching Terminology

**1. Cache:**  
A temporary storage for fast access to data or computation results.

**Real-world example:**  
Your browser stores website images in a cache, so websites you visit often load instantly on subsequent visits.

**2. Cache hit:**  
A requested item is found in the cache.

**Example:**  
Opening a news article for the second time in the same session and getting it loaded instantly.

**3. Cache miss:**  
A requested item is not found, so it is fetched from the source and then cached.

**Example:**  
Clicking on a new product page on Amazon you haven’t visited before. The data is fetched from the database, then cached for faster access if you or others return soon.

**4. Cache eviction:**  
Removing data from the cache (to make room, or based on eviction policies like LRU, LFU).

**Example:**  
If your phone runs out of storage space for cached Instagram posts, the oldest cached images are deleted first.

**5. Cache staleness:**  
Cached data becomes outdated compared to the original data source.

**Example:**  
You check the score of a live match on a sports app. If the app’s cache hasn’t updated recently, you might see an old score until the app fetches a fresh result.

***

**Summary:**  
Caching is vital for speeding up applications and reducing the cost of repeated data access. Used correctly, it provides faster results for end-users, saves bandwidth, and decreases load on primary data sources. Real-world implementations are everywhere—from web browsers and mobile apps to e-commerce, streaming, and content delivery across the globe.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/introduction-to-caching)

Here is a detailed summary of the "Why is Caching Important?" page, with real-world examples for each concept:

***

### Why is Caching Important?

**Caching** is essential in software engineering because it greatly enhances system performance and user experience by efficiently storing and serving frequently accessed data. Here are the main reasons caching is considered so critical, with real-world scenarios for each:

***

#### 1. Reduced Latency

- **Explanation:** Cache stores data closer to the application or user. Retrieving data from this fast-access layer is much quicker than reaching all the way to the original source (like a remote database or web service).
- **Real-world example:**  
  When you revisit a website on your browser, images and CSS files load instantly because they’re cached locally, making page load times almost immediate compared to the first visit.

***

#### 2. Improved System Performance

- **Explanation:** Caching reduces how often applications need to fetch or compute data from the main source, which is usually much slower than the cache.
- **Real-world example:**  
  Social media platforms like Instagram cache your feed and media in their apps. Scrolling back through your timeline is smooth and fast because recently viewed posts are cached, decreasing load on Instagram’s servers.

***

#### 3. Reduced Network Load

- **Explanation:** Since cached data is fetched locally, there’s less need to request it over networks. This minimizes the bandwidth used and eases congestion.
- **Real-world example:**  
  Streaming platforms such as Netflix or YouTube use CDN (Content Delivery Network) caches near users. When lots of people in the same city watch the same video, it streams from a local cache rather than using international bandwidth for every viewer, greatly reducing internet backbone traffic.

***

#### 4. Increased Scalability

- **Explanation:** By reducing the number of requests to the original data source, caching lightens the load on those primary systems. This enables the system to serve many more users simultaneously without getting overwhelmed.
- **Real-world example:**  
  During major online sales (like Amazon Prime Day), product info and prices are cached heavily. Instead of millions of users hitting the central database, they get results instantly from distributed caches, preventing site crashes.

***

#### 5. Better User Experience

- **Explanation:** Faster response times mean users feel the application is more responsive. Quick-loading apps keep users engaged and satisfied.
- **Real-world example:**  
  Mobile banking apps show your recent transactions instantly after login, thanks to caching. Instead of always querying the mainbank server, many transactions are loaded from a secure local cache, giving you immediate feedback.

***

**Summary:**  
Caching drives speed, scalability, and efficiency across modern software—from web browsing and social media to e-commerce and video streaming. Without caching, apps would be slower, less reliable, and more expensive to run, compromising both user experience and provider scalability.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/why-is-caching-important)

Here’s a detailed summary of the "Types of Caching" page with real-world examples for each caching technique:

***

### 1. In-Memory Caching

- **What it is:** Data is stored directly in a computer’s RAM, providing the fastest access speed.
- **Where it’s used:** Frequently accessed data that fits in memory, such as API responses, user sessions, or web page fragments.
- **Technologies:** Memcached, Redis.
- **Real-world example:**  
  E-commerce sites use Redis to cache popular product listings or shopping cart data, allowing instant retrieval as users browse.

***

### 2. Disk Caching

- **What it is:** Data is saved to the computer’s hard disk, which is slower than RAM but still much faster than querying remote sources.
- **Where it’s used:** Caching data too large for memory or data that should persist after application restarts, like database queries and files.
- **Real-world example:**  
  Operating systems like Windows and macOS cache recently opened files on disk so when you reopen them, they load much quicker.

***

### 3. Database Caching

- **What it is:** Caching frequently accessed database information within the database system itself, often by storing query results.
- **Where it’s used:** Multi-user apps where many people access the same data, like dashboards and analytics tools.
- **Real-world example:**  
  Instagram may cache user profile data or post counts to avoid recalculating these values for every viewer.

***

### 4. Client-Side Caching

- **What it is:** Data is cached on the user’s device, like in a browser or a mobile app.
- **Where it’s used:** Storing static resources (images, CSS, JS) or frequent API payloads locally.
- **Real-world example:**  
  When you revisit Facebook or Twitter, your browser loads logos, scripts, and styles from cache instead of downloading them again, speeding up site load times.

***

### 5. Server-Side Caching

- **What it is:** Frequently requested data or computed results are cached by application servers.
- **Where it’s used:** Improving server response time with full-page caching, fragment caching, or object caching.
- **Real-world example:**  
  News sites cache homepage content during high-traffic events, delivering static HTML to all visitors rather than regenerating it for each request.

***

### 6. CDN (Content Delivery Network) Caching

- **What it is:** Content is cached on a geographically distributed network of servers, bringing it closer to end-users worldwide.
- **Where it’s used:** Static files for large, global websites to minimize latency (like images, videos, downloads).
- **Real-world example:**  
  Netflix and YouTube use CDN caching so when millions watch the same video, it’s instantly served from the nearest city rather than a distant data center.

***

### 7. DNS Caching

- **What it is:** Results of domain lookups are cached by your device or DNS server.
- **Where it’s used:** Reducing DNS query times when repeatedly accessing the same website.
- **Real-world example:**  
  If your laptop recently visited `amazon.in`, it caches the mapping of `amazon.in` to its IP address; re-opening the site doesn’t need a new DNS lookup.

***

Since direct images cannot be taken from the page, here’s a conceptual illustration to help you visualize where these caches exist:

```
[User]
   |
   |--- Client-side Cache (browser/app)
   |--- DNS Cache
   |
[Internet]
   |
   |--- CDN Cache
   |
[Web/App Server]
   |
   |--- Server-Side Cache
   |--- In-Memory Cache (RAM)
   |--- Disk Cache
   |--- Database Cache
   |
[Primary Database/Source]
```

***
**What and Where to Cache**
![What and where to cache](https://raw.githubusercontent.com/alokpadhi/System-Design/refs/heads/main/Grokking%20System%20Design%20Fundamentals/docImages_642240028314cd6463f3e5e2_img_a3734b0-aad6-e1cc-516d-f3dedc3188ca.svg))
**Summary**:  
Different caching types—spanning memory, disk, database, client/server, CDN, and DNS—are chosen based on data access patterns and requirements. They all speed up performance, cut latency, and deliver a much faster and smoother user experience. Real-world applications include everything from faster webpage loads to snappy video streaming and reliable domain lookups.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/types-of-caching)

Here is a detailed summary of the "Cache Replacement Policies" page, along with real-world examples for each policy:

***

### Why Do We Need Cache Replacement Policies?

When a **cache becomes full**, we need a policy to determine which item to remove to make space for new data. The effectiveness of a cache strongly depends on the replacement policy used.

***

### Common Cache Replacement Policies

#### 1. Least Recently Used (LRU)

- **How it works:** Removes the item that hasn’t been accessed for the longest time.
- **Assumption:** Recently accessed items are more likely to be accessed again.
- **Real-world example:**  
  Smartphone app switcher – The last-used apps are kept in memory, while the ones you haven’t opened in a long time get evicted first. If you keep jumping between Instagram and WhatsApp, but haven’t opened Twitter in hours, Twitter will get closed to save RAM.

***

#### 2. Least Frequently Used (LFU)

- **How it works:** Removes the item that is used the least number of times.
- **Assumption:** Items accessed frequently are more likely to be needed again.
- **Real-world example:**  
  News app home screen cache – Articles you tap on most often are kept ready for instant access, while rarely opened articles are cleared from cache to make room for trending or frequently visited news.

***

#### 3. First In, First Out (FIFO)

- **How it works:** Removes the oldest-added item in the cache, regardless of how often or recently it’s been accessed.
- **Assumption:** Oldest items are least likely to be useful.
- **Real-world example:**  
  Video streaming buffer – The oldest video frames buffered get discarded first as new frames arrive, regardless of which ones you might have replayed.

***

#### 4. Random Replacement

- **How it works:** Randomly selects any item in cache for removal when space is needed.
- **Assumption:** Good for unpredictable access patterns; no assumptions about future access.
- **Real-world example:**  
  In some hardware caches of CPUs, a random line is evicted when full since the cost of maintaining usage statistics outweighs extra hit rates for certain workloads.

***

### Comparison and Trade-offs

- **LRU and LFU** tend to give better performance because they leverage access patterns; however, they need additional data structures to track access times or counts, making them more complex to implement.
- **FIFO and Random** are easier to implement but generally do not perform as well on workloads with locality or repetition.

**Summary Table:**

| Policy | Strengths | Weaknesses | Best For |
|---|---|---|---|
| LRU | Adapts to recent trends; good hit rate | More complex; needs tracking access order | Apps with temporal locality (e.g., browsers) |
| LFU | Captures long-term popularity | Even more complex; needs frequency counters | Trending data (e.g., news feeds) |
| FIFO | Simple; predictable | May evict popular items too soon | Streaming, circular buffers |
| Random | Simple | Unpredictable performance | Environments where simplicity > accuracy (low-memory hardware) |

***

**Conclusion:**  
Choosing the right cache replacement policy depends on your use case. LRU and LFU are very effective when access patterns are predictable, while FIFO and random may be selected for simplicity in some systems. Real-world systems often use LRU for both operating system file caches and application-level caches.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/cache-replacement-policies)

Here’s a **detailed summary** of the "Cache Invalidation" page, featuring real-world examples for each concept:

***

### What is Cache Invalidation?

**Cache invalidation** ensures that the data in a cache stays fresh and does not become stale or inconsistent with the underlying data source. When the original (source) data changes, mechanisms are needed to update or remove cached versions so that users see the latest information.

***

### Why is Cache Invalidation Important?

1. **Ensures Data Freshness:**  
   Cached content must be updated after the underlying data (e.g., product price changes in a database). Otherwise, users might get outdated info.

   *Example:*  
   An e-commerce site changes the price of a TV. If the cached price isn’t invalidated, shoppers may see the wrong price, leading to confusion or financial losses.

2. **Maintains Consistency:**  
   Multiple caching layers can present conflicting data if not properly invalidated.

   *Example:*  
   News apps with local cache and CDN cache—if one isn’t invalidated after an article update, users in different regions might see inconsistent headlines.

3. **Balances Performance and Accuracy:**  
   Effective strategies (like TTL, event-based triggers) aim to keep data fresh while taking advantage of cache speed.

   *Example:*  
   A social network uses short cache times for trending feeds, ensuring relevance with minimal server strain.

4. **Reduces Errors and State Mismatch:**  
   Serving stale data can result in errors, such as showing out-of-stock items or expired offers.

   *Example:*  
   Ticket booking apps need real-time inventory refresh; old cached availability can mislead customers and overbook seats.

***

### Cache Invalidation Schemes

#### 1. Write-through Cache
- **Data is written to both cache and permanent storage simultaneously.**
- **Consistent, but write-latency is higher.**
- *Example:*  
   Banking systems: balance updates are immediately written to both fast cache and persistent storage, ensuring up-to-date records even in case of failures.

#### 2. Write-around Cache
- **Data is written to storage only, bypassing the cache.**
- **Reduces cache pollution by infrequently accessed items, but new reads may miss the cache and be slower.**
- *Example:*  
   Logs or analytics systems: write events to storage straight away, since most events may never be read again soon.

#### 3. Write-back Cache
- **Data is written to the cache and confirmed to the client. Storage is updated later, often when eviction is needed.**
- **High speed for writes but risks data loss if cache fails.**
- *Example:*  
   Offline document editors: save edits instantly to cache, syncing to cloud storage after a delay or on closing the document.

#### 4. Write-behind Cache
- **Similar to write-back, but data is written to storage at set intervals (batching updates).**
- **Boosts performance, but data loss risk during crashes.**
- *Example:*  
   Point of Sale (POS) systems: process purchases offline, batching updates to the central server every few minutes.

***

### Cache Invalidation Methods

#### **Purge**
- Instantly removes cached data for a specific item or set.
- *Example:*  
   After updating a product image, purge its old cached version to force retrieval of the new image upon the next request.

#### **Refresh**
- Forces a re-fetch of a resource from the origin and updates the cache.
- *Example:*  
   A site admin requests a “refresh” of a blog post after editing, ensuring all readers get the updated version.

#### **Ban**
- Flags cached items as invalid using rules or patterns. Not deleted immediately, but marked for replacement on next access.
- *Example:*  
   Invalidate all items in `/deals/*` category after a sale ends, so every matching product page is treated as stale and refreshed upon next request.

#### **TTL (Time-to-live) Expiration**
- Automatically expires cached items after a set time.
- *Example:*  
   DNS records cached for an hour; after TTL expires, cache will re-query origin DNS server for any update.

#### **Stale-While-Revalidate**
- Serves stale content instantly, while updating the cache in the background.
- *Example:*  
   Blogs using this approach serve the old version immediately but quietly fetch the new post, so next user gets the fresh version—great for minimizing wait time.

***
![cache invalidation methods](https://raw.githubusercontent.com/alokpadhi/System-Design/refs/heads/main/Grokking%20System%20Design%20Fundamentals/docImages_64224412a763c048c9763975_img_750dd4f-1d6b-0512-3744-353a8ffed1dd.svg)
**Summary:**  
Cache invalidation is essential to keep systems correct and up to date. Techniques like purge, refresh, ban, TTL expiration, and stale-while-revalidate let developers choose the best balance of speed and accuracy, and ensure users always get the latest or at least “fresh enough” content. Real-world apps—from e-commerce and news to banking—depend on effective cache invalidation to avoid confusion and maintain reliability.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/cache-invalidation)

Here is a **detailed summary** of the "Cache Read Strategies" page, including **real-world examples** for each approach:

***

### 1. Read-Through Cache

- **How it works:**  
  In a read-through cache, the application requests data from the cache, not directly from the data store (like a database).  
  - If the data is **in the cache** (cache hit), it’s returned right away.
  - If it’s **not in the cache** (cache miss), the cache itself retrieves the data from the data store, updates the cache, and returns the data to the application.

- **Benefits:**  
  - Simplifies application code (app only interacts with cache, never with the database directly).
  - Ensures cache and data store remain consistent.
  - Improves performance, especially when cache misses are infrequent.

- **Real-world example:**  
  - **Amazon product pages:** When you view a product, Amazon’s application queries the cache. If the product details aren’t there, the cache fetches them from the main database, stores them for next time, and returns the details for display.

***

### 2. Read-Aside Cache (Cache-Aside or Lazy-Loading)

- **How it works:**  
  Here, the application **is responsible** for interacting with both the cache and the data store.
  - The app first checks the cache for data.
  - **If the data is present** (cache hit), the app uses it.
  - **If not** (cache miss), the app retrieves the data from the data store, puts the data into the cache, and then uses it.

- **Benefits:**  
  - Greater control over cache usage and update logic.
  - The application can decide when and how often to update the cache.
  - If the cache system fails, the application can still directly access the database, ensuring system availability.

- **Real-world example:**  
  - **Social media feeds:** A user’s timeline isn’t always cached because it changes with every login or action. When a user logs in, the application checks the cache. If nothing is found for this user, it queries the backend service, stores the result in cache, and serves it to the user.

***

### Summary Table

| Strategy          | Who loads cache on miss? | Code Complexity | Reliability | Example Scenario               |
|-------------------|-------------------------|-----------------|-------------|-------------------------------|
| Read-Through      | Cache library/system     | Low             | High        | Product/current prices lookup  |
| Read-Aside        | Application itself       | Higher          | Highest     | User-specific dynamic timelines|

***

**Conclusion:**  
Both read-through and read-aside cache strategies are widely used to improve data retrieval speed. Read-through centralizes cache management for consistency, while read-aside lets applications maintain control and resilience, making them especially valuable for dynamic or rapidly changing data. Systems like e-commerce platforms, news sites, and social networks all leverage these strategies for better performance and scalability.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/cache-read-strategies)


