# Introduction to Load Balancing
A detailed introduction to **load balancing** in system design, explaining its purpose, working, and practical application:

***

### What is Load Balancing?
- **Load balancing** distributes incoming network or application traffic evenly across multiple servers, ensuring no single server is overwhelmed.
- Its main goals are to maximize **availability** (system remains up and running), **reliability**, and **performance** (fast response times) by avoiding overloading and single points of failure.

***

### How Load Balancers Work (with Example)
1. **Request Reception:** The load balancer receives a request from a user or client.
2. **Server Selection:** It uses a pre-set algorithm (e.g., round robin, least connections) to choose the best backend server based on capacity, active connections, response times, or even location.
3. **Forwarding:** The load balancer forwards the request to the selected server.
4. **Processing:** The server processes the request and generates a response.
5. **Response Relay:** The server’s response is sent back to the load balancer, which then sends it to the original requester.

**Example:**  
Suppose an e-commerce site receives hundreds of simultaneous checkout requests during a big sale. A load balancer is placed between users and the web servers:
- It distributes those requests among several web servers instead of letting any one server get crowded, ensuring shoppers experience fast checkouts, minimal errors, and the whole system remains available—even if one server fails.

***

### Key Concepts and Terms
- **Load Balancer:** Device/software that distributes requests using rules/algorithms.
- **Backend Servers:** The pool of servers that handle actual request processing.
- **Load Balancing Algorithm:** Logic used to pick which server will handle each request.
- **Health Checks:** Routine tests by the load balancer to confirm server health—unhealthy servers are temporarily removed.
- **Session Persistence:** Keeping all of a user’s requests on the same server for consistency (important for logged-in sessions or shopping carts).
- **SSL/TLS Termination:** The load balancer handles SSL decryption, freeing backend servers from that processing load and centralizing security.

***

### Where Load Balancers Are Used
- **Between users and web servers**
- **Between web servers and application/cache servers**
- **Between platform layers and databases**

***

Load balancing is a foundation for scaling services and maintaining a resilient, efficient, and user-friendly system in modern distributed web architectures.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/introduction-to-load-balancing)

# Load balancing Algorithms
This page provides an **in-depth breakdown** of all the major load balancing algorithms, their mechanics, advantages, disadvantages, specialized scenarios, and concrete examples for each. Here’s a systematic, highly detailed summary:

***

### 1. **Round Robin**
- **Mechanism:** Requests are assigned to backend servers in a strict cycle—server 1, then server 2, and so on; wraps back to the start after the last server.
- **Advantages:** Simple to implement; ensures even, predictable distribution across homogeneous servers.
- **Disadvantages:** Does not consider actual server load; failing servers (if not health-checked) still get traffic; session persistence not guaranteed.
- **Example:**  
  Imagine 4 servers (A, B, C, D) and 8 client requests. Request flow: A, B, C, D, A, B, C, D—each gets exactly 2.  
- **Use Case:** Static web servers, image/CDN servers, where nodes are equal and requests are stateless.

***

### 2. **Least Connections**
- **Mechanism:** Assigns new requests to the server currently handling the fewest active connections; dynamically adapts as traffic and connections change.
- **Advantages:** Dynamically reacts to real-time load; prevents servers from being overwhelmed when some requests take longer.
- **Disadvantages:** Requires real-time connection tracking; less effective with highly volatile request completion times.
- **Example:**  
  Suppose servers A, B, C have 2, 4, and 4 connections each; the next request is always routed to A.
- **Use Case:** Long-lived web sockets, long-polling APIs, chat systems.

***

### 3. **Weighted Round Robin**
- **Mechanism:** Each server is assigned a “weight” proportional to its capacity. Servers with higher weights receive more requests in the cycle.
- **Advantages:** Supports heterogeneous server environments; simple proportional request division.
- **Disadvantages:** Needs manual/effective weight assignment; not adaptive to dynamic resource changes.
- **Example:**  
  Assume server A (weight 4), B (2), C (1). Out of 7 requests, A gets 4, B gets 2, C gets 1.
- **Use Case:** Data centers/mixed environments with varying physical or VM resources.

***

### 4. **Weighted Least Connections**
- **Mechanism:** Like least connections, but servers have weights—some can handle more connections than others before being considered overloaded.
- **Advantages:** Combines capacity awareness and real-time load adaptation; great for hybrid instances.
- **Disadvantages:** Requires up-to-date metrics and fine-tuned weights; more complex than plain least connections.
- **Example:**  
  If A’s weight is 2x B, A can have twice the connections before being balanced away from.
- **Use Case:** Multi-cloud or hybrid apps where server resources differ day-to-day.

***

### 5. **IP Hash**
- **Mechanism:** Uses a hashing function on the client’s IP to map consistently to a specific server.
- **Advantages:** Excellent for session persistence; no external state management required.
- **Disadvantages:** Imbalanced distribution if IPs are unevenly allocated; server removal/addition disrupts assignments.
- **Example:**  
  User with IP X hashes to server B, so all repeat requests from X hit server B.
- **Use Case:** User-specific experience (shopping carts, gaming sessions).

***

### 6. **Least Response Time**
- **Mechanism:** Continuously tracks backend response times. New requests are sent to the server with the lowest average or most recent response time.
- **Advantages:** Highly dynamic—focuses on servers actually performing best right now; optimal for user experience.
- **Disadvantages:** If response time fluctuates, requests may spike to “temporarily faster” servers.
- **Example:**  
  Servers report 20ms, 30ms, and 50ms; next request goes to the 20ms server.
- **Use Case:** Real-time bidding, trading, and microservice APIs with strict SLAs.

***

### 7. **Random**
- **Mechanism:** Each request is randomly assigned to any server in the pool.
- **Advantages:** Easy to implement, no traffic analysis or metrics needed; offers probabilistic fairness over time.
- **Disadvantages:** Short-term imbalances possible; no session stickiness, may ignore backend health.
- **Example:**  
  With servers A–E, random assignments over 1000 requests will approach 20% distribution per node.
- **Use Case:** Test or staging environments, highly dynamic transient systems.

***

### 8. **Least Bandwidth**
- **Mechanism:** Tracks current bandwidth consumed by each server and sends new requests to the least-used server.
- **Advantages:** Specializes in bandwidth-heavy scenarios (video, file serving); prevents congestion.
- **Disadvantages:** Requires exact bandwidth tracking, which is resource-intensive.
- **Example:**  
  In video streaming, new viewers are routed to servers with the most free bandwidth (not overloaded by active streams).
- **Use Case:** Streaming platforms, CDNs, content-rich media apps.

***

### 9. **Custom Load**
- **Mechanism:** Operators define any metric (CPU, memory, application load, business criteria) and the load balancer uses that for distribution.
- **Advantages:** Tailored to specific business or technical needs; highly flexible.
- **Disadvantages:** Hardest to maintain and optimize; risk of bad metrics causing worse-than-random balancing.
- **Example:**  
  E-commerce site may use a composite metric—CPU < 50%, checkout queue size < 10.
- **Use Case:** Large-scale, continually evolving distributed architectures in big tech.

***

**Summary Table (Sample)**

| Algorithm                | Adapts to Load | Session-Aware | Requires Weights | Manual Tuning | Sample Application    |
|--------------------------|:-------------:|:-------------:|:----------------:|:-------------:|----------------------|
| Round Robin              |       ✗       |       ✗       |        ✗         |       ✗       | Static web content   |
| Least Connections        |       ✓       |       ✗       |        ✗         |       ✗       | Chat/websocket apps  |
| Weighted Round Robin     |       ✗       |       ✗       |        ✓         |       ✓       | Mixed servers        |
| Weighted Least Conn.     |       ✓       |       ✗       |        ✓         |       ✓       | Hybrid cloud         |
| IP Hash                  |       ×       |       ✓       |        ✗         |       ✗       | Stateful sessions    |
| Least Response Time      |       ✓       |       ✗       |        ✗         |       ✗       | Real-time APIs       |
| Random                   |       ✗       |       ✗       |        ✗         |       ✗       | Testing              |
| Least Bandwidth          |       ✓       |       ✗       |        ✗         |       ✗       | Video/CDN            |
| Custom                   |      ✓/✗      |      ✓/✗      |      ✓/✗         |       ✓       | Custom apps          |

The choice of algorithm impacts performance, reliability, and user experience. For example:
- **Round Robin**: Good for stateless, uniform tasks.
- **Least Connections**: Vital when some users stick around longer (live chat).
- **IP Hash**: Needed when users must always hit the same backend (login sessions).
- **Least Bandwidth/Response Time**: Required for media streaming and latency-sensitive apps.

By considering your system’s needs and the algorithm’s strengths, you achieve optimal utilization, lowest latency, and high reliability.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/load-balancing-algorithms)

# Uses of Load Balancing
Here is a detailed summary of the uses of load balancing, with examples:

***

**1. Improving Website Performance**
- **How:** Distributes incoming web traffic among multiple servers to ensure no single server is overwhelmed.
- **Example:** During a holiday sale, an e-commerce site receives a huge spike in visitors. The load balancer spreads these requests across multiple servers, so each server loads pages quickly and users get a fast experience.

***

**2. Ensuring High Availability and Reliability**
- **How:** If one server fails, the load balancer reroutes traffic to working servers, preventing downtime.
- **Example:** A banking app uses several servers. If one fails, the load balancer redirects all user transactions to healthy servers, so customers keep using the service without interruption.

***

**3. Scalability**
- **How:** Makes it simple to add (or remove) servers as demand changes, without altering the whole system.
- **Example:** A video streaming platform becomes more popular, so new servers are added behind the load balancer, smoothly handling increased user demand.

***

**4. Redundancy**
- **How:** Maintains duplicate copies of data and services across several servers, protecting against data loss or outages.
- **Example:** An online storage service keeps user files copied across multiple servers; if one fails, users can still access their data from another.

***

**5. Network Optimization**
- **How:** Distributes network traffic over multiple paths and links, preventing congestion.
- **Example:** A large company uses several internet connections, and the load balancer divides traffic between them, improving speed and reliability for all users.

***

**6. Geographic Distribution**
- **How:** Directs user traffic to the data center closest to them, minimizing latency.
- **Example:** A global company has data centers in the US, Europe, and Asia. Users are routed to the nearest center, ensuring they access services quickly.

***

**7. Application Performance**
- **How:** Assigns dedicated resources to different apps, preventing them from affecting each other.
- **Example:** An enterprise assigns separate server groups (via the load balancer) to email, file storage, and collaboration apps, so each gets the right resources for high performance.

***

**8. Security**
- **How:** Helps defend against DDoS attacks by distributing large volumes of requests, making it much harder to overwhelm a single server.
- **Example:** A news site facing a DDoS attack relies on the balancer to spread malicious traffic across many servers, reducing the risk of being completely knocked offline.

***

**9. Cost Savings**
- **How:** Optimizes use of hardware, cutting costs on infrastructure and energy.
- **Example:** A small business using cloud servers only pays for what it uses; load balancing lets them run on fewer instances during quiet times, saving money.

***

**10. Content Caching**
- **How:** Some load balancers can cache and directly serve static files (like images or videos), bypassing main servers.
- **Example:** In streaming services like Netflix, popular shows are cached at the load balancer so millions of viewers can be served quickly without overwhelming backend servers.

***

**Summary:**  
Load balancing is crucial for system performance, reliability, scalability, security, cost efficiency, and smooth user experiences in modern web and networked applications.

[ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/uses-of-load-balancing)

# Load balancer Types

Here is a detailed summary of the types of load balancers with examples:

***

### 1. **Hardware Load Balancing**
- **Description:** Uses dedicated physical devices with specialized hardware (like ASICs or FPGAs) to distribute network traffic.
- **Pros:** High performance, built-in security and monitoring features, handles large volumes.
- **Cons:** Expensive, requires expert maintenance, scalability is limited to hardware capabilities.
- **Example:** A large e-commerce website uses a hardware load balancer to spread web traffic across many servers so customers always get fast page loads—even during Black Friday.

***

### 2. **Software Load Balancing**
- **Description:** Load balancing done with software running on standard servers or VMs using software algorithms.
- **Pros:** Affordable, flexible, simple to scale by adding resources, cloud-friendly.
- **Cons:** Lower peak performance, takes system resources, needs frequent updates.
- **Example:** A growing startup uses software load balancers on cloud VMs to manage increased traffic to their app.

***

### 3. **Cloud-based Load Balancing**
- **Description:** Managed as a service by cloud providers—offered on-demand, easy to scale, pay-per-use.
- **Pros:** Highly scalable, managed by cloud vendor, cost-effective, no need to maintain hardware.
- **Cons:** Vendor lock-in risk, limited customization, full reliance on the provider.
- **Example:** A mobile app offloads all load balancing to AWS Elastic Load Balancer, automatically adapting to spikes from new app launches.

***

### 4. **DNS Load Balancing**
- **Description:** Distributes users via DNS by resolving domain names to multiple IP addresses.
- **Pros:** Simple, no special hardware needed, good for basic failover or global load distribution.
- **Cons:** Not real-time—DNS caching/propagation delays, no server health awareness, can't handle sessions well.
- **Example:** A content delivery network (CDN) directs users worldwide to the nearest server via DNS—so video loads faster, no matter the user’s location.

***

### 5. **Global Server Load Balancing (GSLB)**
- **Description:** Combines DNS with health checks and advanced policies to route traffic to the best or healthiest geographic region or data center.
- **Pros:** Global availability, advanced failover, user gets best-performing region, supports custom routing.
- **Cons:** Complex, higher management, relies partly on DNS limitations.
- **Example:** A multinational retailer uses GSLB to keep its website up, redirecting users in Europe to a resilient EU data center if the primary US site fails.

***

### 6. **Hybrid Load Balancing**
- **Description:** Mixes multiple balancing methods (hardware, software, cloud, DNS) to optimize performance, flexibility, and reliability.
- **Pros:** Highly adaptable, harnesses strengths of several approaches, can grow with business needs.
- **Cons:** Most complex to set up and manage, may require multi-disciplinary expertise, can cost more.
- **Example:** A large streaming platform mixes hardware in data centers, software in cloud, and DNS balancing for global audience management.

***

### 7. **Layer 4 (Transport Layer) Load Balancing**
- **Description:** Works at TCP/UDP (OSI Layer 4)—routes requests using IP and port without inspecting content.
- **Pros:** Fast, efficient, works for many protocol types, handles lots of connections.
- **Cons:** Can't make decisions based on app-level (HTTP) data, limits session handling.
- **Example:** An online game routes all player connections based on IP/port to the least-busy server for real-time gameplay.

***

### 8. **Layer 7 (Application Layer) Load Balancing**
- **Description:** Makes routing decisions using application-level data (HTTP methods, cookies, URLs).
- **Pros:** Supports advanced rules (session persistence, SSL offload, content-based routing), excellent for apps or microservices.
- **Cons:** Slower/more resource-intensive (deep traffic inspection required), setup can be complex.
- **Example:** A microservices-based web app uses Layer 7 balancing to route user actions (like /login, /cart, /orders) to the correct dedicated backend service.

***

**Conclusion:**  
The best choice of load balancer depends on required performance, control, and infrastructure flexibility. Real-world systems often use a combination to meet changing user demands, ensure uptime, and support rapid growth.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/load-balancer-types)

# Stateless vs. Stateful Load Balancing

Here is a detailed summary of stateless vs. stateful load balancing, including examples:

***

### **Stateless Load Balancing**
- **How it works:**  
  The load balancer does not record or maintain any information about each client’s session. Every incoming request is treated independently. Routing decisions are based only on the request details (such as IP address, URI, headers) and the current state of backend servers.
- **Pros:**  
  - Fast, simple, highly scalable  
  - No session memory or synchronization needed  
- **Cons:**  
  - Cannot guarantee that requests from the same client are always sent to the same server  
  - Not suitable where session state/persistence is required
- **Example:**  
  A web application lets users search for nearby restaurants. A stateless load balancer directs each request to any server available (based on user location or other logic), making no attempt to send repeat requests from the same user to the same server.

***

### **Stateful Load Balancing**
- **How it works:**  
  The load balancer maintains session information for each client. Each client is assigned to a specific backend server for the duration of their session, and all subsequent requests are routed to the same server.
- **Pros:**  
  - Enables session persistence (“sticky sessions”)  
  - Ensures that session data like login state, user preferences, or cart contents remain available to the user
- **Cons:**  
  - More complex, may require additional overhead and storage  
  - Harder to scale horizontally; session migration or replication may be needed if a server fails

**Two Main Approaches in Stateful Load Balancing:**
- **Source IP Affinity:**  
  The balancer routes all requests from a specific client IP to the same server.  
  - *Example*: Corporate users all behind the same static IP will always connect to the same web server.  
  - *Limitation*: Fails if the client IP changes frequently (e.g., in 4G/5G mobile networks).
- **Session Affinity (Sticky Sessions):**  
  Requests are tracked using a session ID, often via a cookie or URL parameter. The balancer uses this session ID to always route the user to their assigned backend server, regardless of changes in their IP address.  
  - *Example*: E-commerce site uses sticky sessions so all of a given shopper’s requests reach the server holding their shopping cart and login state, even as the user moves locations.

***

### **Summary**
- **Stateless** load balancing is best for services where requests are not dependent on session data (e.g., most public APIs, static site delivery).
- **Stateful** load balancing is essential for applications needing continuity or personalization, such as logged-in dashboards, e-commerce shopping carts, or collaborative apps. The right choice depends on your application’s nature and session requirements.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/stateless-vs-stateful-load-balancing)

# High Availability and Fault Tolerance
Here is a detailed summary of the "High Availability and Fault Tolerance" page, including examples:

***

### **Redundancy and Failover Strategies for Load Balancers**
- **Active-passive configuration:**  
  - One load balancer (active) handles all traffic; another (passive) is on standby ready to take over if the active one fails.
  - **Example:** An e-commerce site uses an active-passive setup: if the primary load balancer goes down during a sale, the backup instantly takes over, so users experience zero downtime.
  - *Pros:* Simple, reliable, but passive resource is idle during normal operation.
- **Active-active configuration:**  
  - Multiple load balancers operate at the same time and traffic is spread among them using DNS or another balancer layer.
  - **Example:** A global video streaming service uses several load balancers in different data centers. If one fails, the others keep handling traffic—users don’t notice any issue.
  - *Pros:* Better resource utilization; increased fault tolerance.

***

### **Health Checks and Monitoring**
- **Health checks:**  
  - Load balancers perform regular tests to check if backend servers are available and performing well.
  - If a backend server fails health checks, the balancer removes it from the pool to prevent downtime and bad user experiences.
- **Monitoring:**  
  - Tracking performance metrics (response times, error rates, resource usage) of load balancers to catch problems early.
  - **Example:** An alert is triggered if a load balancer’s error rate spikes, so engineers can fix issues before they affect users.
- **Alerting and incident response:**  
  - Having processes and tools to notify the right people as soon as problems occur, ensuring rapid problem resolution.

***

### **Synchronization and State Sharing**
- **Centralized configuration management:**  
  - Tools like etcd, Consul, or ZooKeeper manage and synchronize settings across multiple balancer instances.
  - **Example:** A multinational service uses ZooKeeper to ensure all load balancers share the same knowledge of backend server status and routes.
- **State sharing and replication:**  
  - For stateful/session-aware balancers, session and config data must stay in sync across all instances (using databases, distributed cache like Redis, or built-in mechanisms).
  - **Example:** Sticky session info is stored in Redis so whichever load balancer instance handles a session, it knows where to route requests.

***

**In summary:**  
Redundancy, effective health checks, centralized management, and robust monitoring mean that if any single component fails, traffic seamlessly shifts and the system keeps running. This is critical for modern, always-on applications (retail, streaming, banking) that cannot afford downtime.Here is a detailed summary with examples:

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/high-availability-and-fault-tolerance)

# Scalability and Performance

Here is a detailed summary of the "Scalability and Performance" page, with examples:

***

### **Horizontal and Vertical Scaling of Load Balancers**

- **Horizontal Scaling**:  
  - Adds more load balancer instances to manage increased demand.
  - Especially used in *active-active* configurations (all instances process traffic together).
  - Achieved via DNS load balancing or a hierarchy of load balancers.
  - **Example**: A popular music streaming service gets more users, so more load balancer VMs are added across data centers. Each instance participates in routing requests, preventing bottlenecks.

- **Vertical Scaling**:  
  - Increases resources (CPU, RAM, network) of a single load balancer instance so it can handle more traffic.
  - Limited by hardware/resource maximums.
  - **Example**: A growing SaaS tool upgrades its load balancer’s cloud VM from 2-core to 16-core for better throughput, but at some limit horizontal scaling becomes necessary.

***

### **Connection and Request Rate Limits**

- Load balancers can enforce limits on the number of open connections and the rate of requests per source (IP, domain, or URL).
- Prevents overload and keeps performance consistent.
- Also helps mitigate DoS attacks and greedy client monopolization.
- **Example**: An online gaming API allows only 100 simultaneous connections per IP, so no single user can crash the system or disrupt global gameplay.

***

### **Caching and Content Optimization**

- Load balancers can cache static content (images, CSS, JS) directly, reducing backend load and speeding up responses.
- Advanced balancers also support content optimization: compressing images, minifying scripts, reducing bandwidth.
- **Example**: An online retailer serving millions of product images benefits from caching at the load balancer—return users see immediate page loads, and origin servers get fewer requests.

***

### **Impact of Load Balancers on Latency**

- Each load balancer adds a network hop, introducing some latency (usually minimal).
- To reduce this:
  - **Geographical distribution:** Deploy balancers close to users to minimize request distance.
    - *Example*: A global video platform deploys load balancers in US, Europe, and Asia for localized user bases.
  - **Connection reuse:** Use keep-alive/persistent connections between balancers and backends to avoid constant reconnections.
    - *Example*: Streaming services maintain open connections for high-throughput video, lowering connection overhead.
  - **Protocol optimizations:** Use HTTP/2, QUIC, or similar to squeeze out performance gains.
    - *Example*: News sites adopt HTTP/2 via their balancer for faster, parallel load of dozens of article assets.

***

**Summary:**  
By focusing on the right mix of horizontal and vertical scaling, connection/request limiting, intelligent caching, and latency optimization, load balancing infrastructure can maintain high performance and reliability for applications even under heavy and global user demand.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/scalability-and-performance)

# Challenges of Load Balancers

Here’s a detailed summary of the **challenges of load balancers**, including practical examples and remedies:

***

### 1. **Single Point of Failure**
- **Challenge:** If there is only one load balancer, its failure affects the entire system—users can’t access any backend service.
- **Example:** A web app using one software load balancer for all requests; if it crashes, the whole site goes down.
- **Remedy:** Deploy redundant (multiple) load balancer instances with automatic failover to ensure high availability.

***

### 2. **Configuration Complexity**
- **Challenge:** Load balancers have many options—health checks, algorithms, timeouts. Poor configuration can cause unbalanced load or downtime.
- **Example:** Incorrect health check intervals might let failed servers keep getting traffic, causing errors for users.
- **Remedy:** Routinely review and optimize configurations; use automation or consult experts to prevent misconfiguration.

***

### 3. **Scalability Limitations**
- **Challenge:** The load balancer itself can become a bottleneck if traffic outgrows its capacity.
- **Example:** Sudden spike in hits for a viral news story overwhelms a single, unscalable load balancer instance.
- **Remedy:** Plan for horizontal or vertical scaling—add more instances or upgrade resources; use cloud-based scalable load balancers.

***

### 4. **Latency**
- **Challenge:** A load balancer adds an extra hop, introducing some delay (latency).
- **Example:** A global gaming service experiences visible lag if the load balancer is poorly optimized or far from major user groups.
- **Remedy:** Optimize routing algorithms and geographically distribute balancers closer to users to minimize added latency.

***

### 5. **Sticky Sessions (Session Persistence)**
- **Challenge:** Keeping user sessions “sticky” (assigning the same user to the same backend) is often needed, but can create unbalanced traffic.
- **Example:** In an e-commerce site, most premium users land on one backend (due to stickiness), overloading it while others are underused.
- **Remedy:** Use smart session balancing or redesign apps to minimize session dependence for better distribution.

***

### 6. **Cost**
- **Challenge:** Hardware, software licensing, or managed load balancing can be expensive, especially at scale.
- **Example:** A startup spends excessively on proprietary hardware balancers before realizing they could accomplish the same with affordable cloud or open-source options.
- **Remedy:** Choose cost-effective, scalable solutions such as open-source or pay-as-you-go cloud services.

***

### 7. **Health Checks and Monitoring**
- **Challenge:** If health checks are too lax or misconfigured, failing or unhealthy servers may still get traffic.
- **Example:** If a backend server is slow but not fully “down,” the load balancer might keep routing traffic to it, causing timeouts for users.
- **Remedy:** Set up thorough, regular health checks and real-time monitoring so only healthy servers receive requests.

***

**Summary:**  
Load balancers are essential for performance and reliability in modern apps, but they bring operational, configuration, and architectural challenges. With careful setup—including redundancy, proper configuration, scaling plans, optimized algorithms, budget awareness, and robust health checks—these challenges can be effectively managed.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/challenges-of-load-balancers)
