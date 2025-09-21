Here is a **complete, detailed summary** of the "Introduction to DNS" page, including all key concepts and **real-world examples**:

***

### What is DNS?

The Domain Name System (**DNS**) is the internet’s “phonebook.” It translates **human-friendly domain names** (like `www.designgurus.com`) into **IP addresses** (like `198.47.25.1`) that computers use to find each other on the internet.

***

### Purpose and Importance of DNS

- **User-friendliness:** People can remember `google.com` more easily than its numeric IP.
- **Scalability:** DNS is distributed and hierarchical, letting it handle billions of records worldwide.
- **Flexibility:** Websites can change their IP addresses without affecting user access—just updating their DNS records is sufficient.
- **Load balancing:** DNS can direct users to the least busy or geographically nearest server, distributing client requests.

**Real-world example:** If Amazon adds servers in new regions, DNS can route Indian users to `amazon.in` servers located in India for speed.

***

### DNS Components and Terminology

#### 1. Domain Names, TLDs, and Subdomains

- **Domain names:** Readable addresses like `www.example.com`. Easier for humans than numeric IPs.
- **TLDs (Top-Level Domains):** Rightmost part, e.g., `.com`, `.org`, or country codes like `.us`, `.in`.
- **Subdomains:** Additional subdivisions, like `blog.example.com` or `shop.amazon.com`.

**Example:**  
For `deals.amazon.co.uk`:
- `amazon` is the domain,
- `.co.uk` is the country-code TLD,
- `deals` is a subdomain.

#### 2. DNS Servers: Root, TLD, Authoritative

- **Root servers:** Top of the DNS hierarchy. They direct requests to appropriate TLD servers (there are 13 clusters globally).
- **TLD servers:** Hold info for all domains within a specific TLD, such as `.com`, and forward to authoritative servers.
- **Authoritative name servers:** Hold the actual DNS records for domains—they know the real IP address.

**Example:**  
When you look up `openai.com`, your DNS query goes: root → `.com` TLD → OpenAI’s authoritative server (which returns OpenAI’s actual IP).

#### 3. DNS Resolvers

A **DNS resolver** is any component responsible for converting a domain into an IP address. There are several types, each with different responsibilities:

***

### Types of DNS Resolvers (With Examples)

#### 1. Stub Resolver
- **What:** Minimal software on your device.
- **How:** Knows which DNS server to ask, sends requests and waits for a reply.
- **Example:** Your iPhone using Google DNS (`8.8.8.8`). When you open Instagram, it asks the DNS server where `instagram.com` is.

#### 2. Recursive Resolver
- **What:** A DNS server doing all the work—it keeps asking other servers until it finds the answer.
- **How:** Checks its cache, then queries root, then TLD, then authoritative server if needed.
- **Example:** Your ISP’s DNS resolver or public DNS (Google, Cloudflare). Using Google DNS (`8.8.8.8`), it will try every layer to find `youtube.com`’s IP if it’s not in cache.

#### 3. Caching-Only Resolver
- **What:** Store answers for a time (“cache”) so repeated queries are much faster.
- **How:** Answers if it knows, otherwise forwards to an upstream resolver.
- **Example:** Your home router saves (caches) `netflix.com` after your first request, speeding it up for the whole family.

#### 4. Forwarder
- **What:** Sends all DNS queries to another server, doesn’t resolve them itself.
- **How:** Used in businesses to centralize DNS control.
- **Example:** A company network runs a forwarder that sends all DNS lookups to Cloudflare’s DNS so IT can log and filter outgoing queries.

#### 5. Iterative (Non-Recursive) Resolver
- **What:** Returns a referral if it doesn’t know the answer, telling the requester, “try there next.”
- **How:** Common in higher-level servers, rarely used by end-users.
- **Example:** An authoritative server for `university.edu` might tell you to ask another name server for `math.university.edu`.

***

### DNS Lookup: Step-by-Step

1. You type a domain (e.g., `example.com`) into your browser.
2. Your device’s stub resolver sends a request to a recursive resolver (ISP or public DNS).
3. If cached, you get an answer instantly.
4. If not, the recursive resolver queries root, TLD, and authoritative servers.
5. When found, the answer is cached and returned to you, and you connect to the website’s IP address.

***

### Visualizing the Resolution Chain

`User Device (Stub Resolver)` → `Recursive Resolver` → `Root Server` → `TLD Server` → `Authoritative Server` → **IP Address**

- Each step caches results for faster lookups later.

***

### Putting It All Together

- **Stub Resolver:** On your device, just sends queries.
- **Recursive Resolver:** Works to find answers, caching them along the way.
- **Caching-Only:** Routers or intermediate devices cache answers.
- **Forwarders:** Corporate servers centralize DNS management.
- **Iterative Resolver:** Passes along referrals, not full answers.

***

### Real-World Example Scenario

1. **Your laptop** (stub resolver) uses Google DNS (`8.8.8.8`).
2. You enter `www.example.com` in your browser.
3. The laptop sends this request to Google DNS (recursive resolver).
4. Google DNS first checks if it has the answer cached.
   - If yes, it replies instantly.
   - If not, it queries root → `.com` TLD → example.com’s authoritative server for the real IP.
5. Once found, Google DNS caches this for future requests and answers your laptop.
6. **Your laptop now connects to that IP**, and the site loads.  
**Bonus:** If your home router cached this after your previous visit, it answers instantly for any device in your house.

***

**Summary:**  
DNS translates names to IPs through a hierarchy of servers and resolvers. Each plays a unique role, with caching for speed and redundancy, flexible IP management for websites, and support for modern internet scale and reliability. Real-world uses: smart TVs, phones, corporate networks, and home routers all rely on these systems silently every day, letting people forget IP addresses forever.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/introduction-to-dns)

Here is a **detailed summary of the “DNS Resolution Process”** page, along with **real-world examples**:

***

### 1. Recursive and Iterative DNS Queries

**DNS resolution** is the process of converting a human-friendly domain name (like `www.amazon.com`) into its numeric IP address. There are **two types of DNS queries** involved in this process:

#### **Recursive Query**
- In a recursive query, a DNS resolver (like your ISP’s DNS or Google DNS) takes full responsibility for finding the answer to your request.
- If the server queried knows the answer, it returns it immediately.
- If not, the server itself queries other DNS servers on your behalf—moving through root, TLD, and authoritative servers—until it finds the answer, then returns the result to you.

**Real-world example:**  
When you type `www.spotify.com` into your browser at home, your device’s DNS query goes to your configured DNS resolver (maybe Google DNS). Google’s DNS server doesn’t tell you “ask someone else”—it finds the answer itself by querying the entire DNS hierarchy, then replies with the IP.

#### **Iterative Query**
- In an iterative query, the DNS resolver asks a server for the best answer it currently has.
- If the server does not know the full answer, it gives a referral—suggesting the next server the resolver should ask.
- The responsibility is distributed: the DNS resolver keeps querying the next referred server, “iterating” through the system until it gets the answer.

**Real-world example:**  
Suppose a corporate DNS resolver does not know the IP for `www.bbc.co.uk`. It asks a root server, which refers it to the `.uk` TLD server, which then refers it to the authoritative server for `bbc.co.uk`. The resolver follows each lead until it finds the answer.

***

### 2. DNS Caching and TTL (Time To Live)

To **speed up DNS lookups** and reduce unnecessary traffic, both resolvers (like your laptop, router, or Google DNS) and DNS servers **cache** previous DNS query results.

- Every DNS record has a **TTL (Time To Live)** — a number of seconds a record should be held in cache.
- When a request is made, the resolver first checks its cache. If the answer is there and the TTL hasn’t expired, it returns the cached IP instead of querying the DNS system.
- When the TTL expires, the cache entry is cleared, and a new query is made to ensure fresh, up-to-date information.

**Real-world example:**  
- If you visit `www.reddit.com` once, the IP mapping is cached on your router.
- If you or someone else visits again soon, the cached address is used for speed, unless the TTL has expired.
- When Reddit moves its site to a new IP, the change will only be seen by users making queries after the old cache’s TTL has expired—so updates don’t cause worldwide outages.

***

### 3. Negative Caching

Sometimes users request DNS records or domains that do **not exist**. Negative caching is the process of remembering these “not found” answers for a while.

- When a resolver confirms that a domain or record doesn’t exist, it caches this negative response, also for a TTL period.
- This means repeated queries for the same non-existent domain do not travel through the entire DNS hierarchy every time, reducing unnecessary traffic.

**Real-world example:**  
- If a typo such as `wwww.goggle.com` is entered, and no such domain exists, the negative response (domain not found) is cached.
- If your sibling enters the same typo, the resolver instantly returns “not found” without burdening root/TLD/authoritative DNS servers.

***

### In Short

- The DNS resolution process translates domain names to IPs using both recursive and iterative queries.
- DNS caching—with set TTLs—speeds up the lookup process and ensures reasonable freshness of results.
- Negative caching avoids wasting resources on repeated requests for domains or records that do not exist.

***

#### **Summary Table**

| Step                | Description                                                         | Real-World Example           |
|---------------------|---------------------------------------------------------------------|------------------------------|
| Recursive Query     | Resolver finds the answer by itself, querying many servers if needed| Typing `youtube.com` at home |
| Iterative Query     | Resolver gets referrals, asks each server in turn                   | Corporate DNS stepwise lookup|
| Caching & TTL       | Stores answers for later, TTL defines how long                      | Faster repeat visits, less load |
| Negative Caching    | Stores “not found” responses for TTL                               | Catches typos, reduces traffic |

***

**Conclusion:**  
DNS resolution efficiently maps names to IPs using intelligent query strategies and caching, reducing both latency and load on global infrastructure. Whether at home, school, or work, these mechanisms make internet navigation seamless, even handling errors gracefully.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/dns-resolution-process)

Here is a detailed summary of the page **DNS Load Balancing and High Availability**, including real-world examples:

***

### Overview

As the internet grows, **performance, reliability, and availability** of DNS become vital. To achieve these, the system uses several techniques to distribute traffic, prevent overload, and ensure smooth operation even if some servers fail.

***

### 1. Round-Robin DNS

- **What it is:** Multiple IP addresses are linked to one domain name. When a user requests the site, the DNS server rotates through these IPs—offering a different one to each query in turn.
- **Goal:** Spreads load among several servers to improve performance and uptime.
- **Limitation:** It doesn’t consider actual server load or client location, which can sometimes create uneven distribution or high latency.

**Real-world example:**  
A company’s website, `www.fashionstore.com`, maps to three backend servers’ IPs. Each new visitor is directed to a different server, helping handle traffic surges during sales. However, if one server is overloaded or offline, round-robin may still direct users to that problematic server.

***

### 2. Geographically Distributed DNS Servers

- **What it is:** DNS servers placed in different regions worldwide.
- **Goal:** Provides quicker responses to users by serving them from a nearby server. Boosts redundancy—if one server fails, others across the globe can serve traffic.
- **Benefit:** Minimizes latency and increases reliability in case of network problems or outages.

**Real-world example:**  
Global tech firms like Google and Facebook run DNS servers on multiple continents. Users in India resolve `google.com` via an Indian DNS server, while U.S. users are served from a U.S.-based server, ensuring faster load times.

***

### 3. Anycast Routing

- **What it is:** Multiple servers share the same IP. The network routes each request to the server that’s “nearest” (in terms of network distance or latency).
- **Goal:** Distributes queries, reduces latency, and provides automatic failover if a server becomes unreachable.

**Real-world example:**  
Public DNS services like **Cloudflare (1.1.1.1)** use anycast. When you use their DNS, your query is sent to the closest Cloudflare data center, ensuring fast and reliable DNS lookups. If one data center goes offline, your queries are automatically routed to the next closest one.

***

### 4. Content Delivery Networks (CDNs) and DNS

- **What it is:** CDNs are distributed networks of servers that cache and serve web content from locations close to end users.
- **How DNS fits in:** When you request content from a CDN-backed site, the CDN’s DNS chooses the best server for you (usually the nearest or least busy) and returns that IP, so you access the website quickly and efficiently.
- **Benefits:** Improved site load speed, reliability, protection against big traffic spikes (like product launches).

**Real-world example:**  
Media streaming platforms like **Netflix** depend on CDNs and DNS-based routing. When a user in Germany streams a movie, DNS ensures they get content from a German CDN server, speeding up load times and reducing the risk of service interruptions even if other CDN servers are down.

***

### Key Points

- **DNS Load Balancing** (using techniques like round-robin, anycast, and CDNs) spreads queries across multiple servers, avoiding overloads.
- **High Availability** is achieved with redundancy (multiple server locations) and auto-failover (anycast, global distribution).
- **Real-world**: These techniques let huge services like Amazon, Netflix, and Google load quickly and reliably for users everywhere—even during failures or traffic spikes.

***

**Summary:**  
DNS load balancing and high-availability strategies (round-robin DNS, geographically distributed DNS, anycast routing, and integration with CDNs) make websites fast, resilient, and accessible worldwide by directing users to the best and nearest resources, sustaining both uptime and speed under heavy and fluctuating loads.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/dns-load-balancing-and-high-availability)
