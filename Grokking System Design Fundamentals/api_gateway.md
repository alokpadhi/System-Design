# Introduction to API Gateway

Here’s a detailed summary of the "Introduction to API Gateway" page, with an example:

***

### **What is an API Gateway?**
- An **API Gateway** is a server-side architectural component that acts as an intermediary between clients (such as browsers, mobile apps, or third-party services) and backend systems, microservices, or APIs.
- **Main purpose:**  
  - Provides a single entry point for all client requests to access backend system services and functionalities.
  - Receives each client’s request, determines the correct backend service/microservice, forwards the request, gathers the response from the backend, and finally sends this response back to the client.
- The API gateway **offloads common cross-service tasks** (like authentication, request routing, and rate limiting), allowing microservices to focus only on their business logic, thereby improving the overall scalability and performance of the system.

***

### **API Gateway vs. Load Balancer**
- **API Gateway:**  
  - Primary responsibility is **routing**—it intelligently sends API requests to the correct microservice based on the specific URL or API route.
  - Frequently handles API-specific tasks like security (authentication, authorization), rate limiting, and API composability (combining multiple service calls into one).
  - **Example:** If a user requests `/orders/123`, the API gateway analyzes the path and forwards the request to the Order Service. For `/users/1/cart`, it forwards it to the Cart Service.
- **Load Balancer:**  
  - Focused strictly on **distribution**—it takes incoming network requests and evenly spreads them across a pool of backend servers.
  - Typically operates at network or transport layer (IP, HTTP) and does not care about application-specific routes.
  - **Example:** Incoming traffic for an e-commerce website (regardless of content) is distributed among 10 backend servers so that no single server is overloaded.

***

### **Difference in Usage**
- **API Gateway:**  
  - Designed to handle structured API requests—where every request has a specific endpoint or resource.
  - Common in microservices/decomposition architectures where each resource or function is managed by a separate service.
  - Often enforces policies, aggregates responses, and simplifies client interaction with a system of many backends.
- **Load Balancer:**  
  - Best for distributing generic traffic across identical or stateless servers (e.g., scaling a monolithic app, CDN edge distribution).

***

**Summary Example:**  
A fintech company builds its backend from multiple microservices (user, accounts, transactions, notifications). The **API gateway** acts as the entry, handling security and routing for end users—the user never knows the backend structure. The system also uses a **load balancer** to spread traffic among multiple replicas of each microservice to ensure reliability and performance.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/introduction-to-api-gateway)

# Usage of API gateway

Here is a detailed summary of the "Usage of API Gateway" page, complete with real-world examples:

***

### **Key Usages of API Gateways**

1. **Request Routing**  
   - **What it does:** Directs client requests to the correct backend service.  
   - **Example:** For an e-commerce site, all cart-related requests go automatically to the cart service, product requests to product catalog, and so on.

2. **Aggregation of Multiple Services**  
   - **What it does:** Combines data from several services into a single client response.  
   - **Example:** A mobile app shows user profile, order history, and recommendations in one view. The API Gateway fetches from user, order, and recommendation services, aggregates, and returns one payload.

3. **Security Enforcement**  
   - **What it does:** Manages authentication, authorization, and rate limiting to protect backends.  
   - **Example:** Checks a user’s JWT token before forwarding requests; imposes request rate limits per user.

4. **Load Balancing**  
   - **What it does:** Evenly distributes traffic across all backend service instances.  
   - **Example:** During high demand, directs requests for the product catalog to multiple server replicas, preventing overload.

5. **Caching Responses**  
   - **What it does:** Stores frequently accessed data for fast retrieval.  
   - **Example:** Product info is cached at the API Gateway, so repeated requests don’t reach the backend every time.

6. **Protocol Translation**  
   - **What it does:** Converts between different networking protocols.  
   - **Example:** Gateway receives HTTP from clients, communicates with an internal gRPC backend.

7. **Monitoring and Logging**  
   - **What it does:** Tracks and records requests for analysis and debugging.  
   - **Example:** Logs response times, errors, and request paths to monitor health and diagnose problems.

8. **Transformation of Requests/Responses**  
   - **What it does:** Modifies data format or structure as needed.  
   - **Example:** Converts backend XML responses into JSON for a client expecting JSON.

9. **API Versioning**  
   - **What it does:** Handles multiple versions of APIs for backward compatibility.  
   - **Example:** Routes requests from old mobile app versions to v1 endpoints, new apps to v2.

10. **Rate Limiting and Throttling**  
    - **What it does:** Restricts maximum requests per user/timeframe.  
    - **Example:** Allows only 100 calls per minute per user to prevent abuse of free tier.

11. **API Monetization**  
    - **What it does:** Manages subscription tiers and billing for API usage.  
    - **Example:** Paid users get higher limits, tracked and enforced by the gateway.

12. **Service Discovery Integration**  
    - **What it does:** Automatically finds and routes to healthy, available service instances.  
    - **Example:** In Kubernetes, as pods scale up/down, gateway always routes to available pods.

13. **Circuit Breaker Pattern Implementation**  
    - **What it does:** Temporarily blocks requests to failing services to prevent cascading failures.  
    - **Example:** Stops sending orders to a crashing order service, returns fallback response.

14. **Content-Based Routing**  
    - **What it does:** Routes based on content, headers, or query parameters.  
    - **Example:** Image uploads go to an image service, videos to a video service.

15. **SSL Termination**  
    - **What it does:** API gateway centrally handles HTTPS encryption/decryption.  
    - **Example:** Clients use HTTPS to the gateway; the gateway may use HTTP for internal calls.

16. **Policy Enforcement**  
    - **What it does:** Applies organization-wide rules and validations.  
    - **Example:** Rejects requests missing required headers.

17. **Multi-Tenancy Support**  
    - **What it does:** Maintains isolation and custom config for different clients/tenants.  
    - **Example:** SaaS with tenant-specific databases and rate limits.

18. **A/B Testing and Canary Releases**  
    - **What it does:** Simultaneously directs some traffic to new or experimental services.  
    - **Example:** Sends 10% of users to new recommendation engine and collects feedback.

19. **Localization and Internationalization**  
    - **What it does:** Adapts responses to different regional formats or languages.  
    - **Example:** Gateway formats prices/currencies based on user’s locale.

20. **Reducing Client Complexity**  
    - **What it does:** Offers composite endpoints so the client makes fewer, simpler requests.  
    - **Example:** Single registration API endpoint triggers account creation, welcome email, event logging—all handled by gateway orchestration.

***

**Real-World Example: Netflix**  
Netflix uses an API Gateway to handle millions of concurrent requests from TVs, phones, and browsers. The gateway routes, aggregates, secures, and optimizes interactions with thousands of backend microservices, enabling efficient, fail-safe, and responsive global streaming.

***

**Conclusion:**  
API Gateways in modern microservices simplify client-server interaction, boost security and performance, and centralize management of cross-service concerns, making them essential to scalable distributed applications.

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/usage-of-api-gateway)

# Advantages and disadvantages of using API gateway

Here is a detailed summary of the "Advantages and Disadvantages of Using API Gateway" page, with examples:

***

### **Advantages of Using an API Gateway**

1. **Improved Performance**
   - Gateways can cache responses, limit excessive requests, and optimize communication between clients and backends, reducing latency.
   - *Example:* Repeated requests for common product data are quickly served from the cache at the gateway, minimizing backend load and speeding up user experience.

2. **Simplified System Design**
   - By acting as a single entry point, the API Gateway centralizes API management, monitoring, and deployment, reducing overall system complexity.
   - *Example:* Developers update endpoints in one place rather than in every client app.

3. **Enhanced Security**
   - Enforces authentication and authorization policies centrally, shielding backend services and letting developers focus on business logic.
   - *Example:* All traffic is authenticated and rate-limited at the gateway; only authorized calls reach core services.

4. **Improved Scalability**
   - Distributes requests among multiple service instances for better scaling.
   - *Example:* During flash sales, incoming requests for order processing are spread across many microservices for smooth handling.

5. **Better Monitoring & Visibility**
   - Collects and reports metrics about API calls for operations, debugging, and reliability improvement.
   - *Example:* Engineers use gateway logs to identify and resolve API performance bottlenecks.

6. **Simplified Client Integration**
   - Provides a unified interface for accessing multiple services, easing client-side development.
   - *Example:* A mobile app integrates with a single endpoint despite many backend microservices.

7. **Protocol and Data Format Transformation**
   - Converts between protocols (e.g., HTTP to gRPC) or formats (e.g., JSON to XML), flexibly connecting diverse clients and services.
   - *Example:* Clients using JSON can talk to a backend returning XML, handled transparently by the gateway.

8. **API Versioning and Backward Compatibility**
   - Manages multiple API versions to avoid breaking existing clients.
   - *Example:* Legacy apps call v1 routes; new apps use v2—all managed by the gateway.

9. **Enhanced Error Handling**
   - Offers standardized error responses, making debugging and user experience better.
   - *Example:* All errors are formatted the same way for all client requests, regardless of the failing backend.

10. **Load Balancing and Fault Tolerance**
    - Distributes traffic evenly and reroutes during failures to maintain system uptime.
    - *Example:* If a payments microservice instance fails, the gateway redirects new requests to healthy ones.

***

### **Disadvantages of Using an API Gateway**

1. **Additional Complexity**
   - Adds another layer to your system, requiring extra management.
   - *Example:* Developers must learn gateway-specific configs and tools.

2. **Single Point of Failure**
   - If not replicated across multiple instances/zones, the gateway can take down the whole system if it fails.
   - *Example:* A misconfigured gateway crashing leaves all clients unable to access backend services.

3. **Latency**
   - Adds an extra hop, especially if doing heavy processing.
   - *Example:* Slow custom request/response transformations introduce user-visible lag.

4. **Vendor Lock-in**
   - Using a managed service can make future migration or customization difficult.
   - *Example:* A team using AWS API Gateway must rewrite logic if moving to another cloud.

5. **Cost**
   - Extra infrastructure, licensing, or cloud costs—especially for high-traffic applications.
   - *Example:* API Gateway usage costs become significant as traffic scales up.

6. **Maintenance Overhead**
   - Requires updates, monitoring, and troubleshooting.
   - *Example:* Engineers spend time managing updates and scaling the gateway itself.

7. **Configuration Complexity**
   - Full-featured gateways have complex configs, which can be hard to manage or synchronize.
   - *Example:* Dealing with large YAML config files and ensuring changes are deployed correctly across environments.

***

**Summary:**  
API Gateways aggregate, secure, and optimize APIs, offering major benefits (performance, security, management, client simplicity). They can also bring downsides: more complexity, potential bottlenecks, costs, and maintenance needs. Teams must weigh these factors for their system’s needs and scale.Here’s a detailed summary of the "Advantages and Disadvantages of Using API Gateway" page with examples:

[Ref](https://www.designgurus.io/course-play/grokking-system-design-fundamentals/doc/advantages-and-disadvantages-of-using-api-gateway)
