## **Introduction to Load Balancing**
*  The main goal of load balancing is to ensure high availability, reliability, and performance by avoiding overloading a single server and avoiding downtime.
*  To utilize full scalability and redundancy, we can try to balance the load at each layer of the system. We can add LBs at three places:
    * Between the user and the web server
    * Between web servers and an internal platform layer, like application servers or cache servers
    * Between internal platform layer and database
* **How load balancer works?**
    * The client sends the request -> pass on to load balancer -> load balancer decides which server to send the request -> server sends back the response to LB -> LB sends the response back to client

## **Load Balancing Algorithms**

### **Purpose**

Distribute traffic across multiple servers to:

* Avoid overloading any one server
* Optimize performance (latency, throughput)
* Ensure high availability & reliability

---

### **1. Round Robin**

**Mechanism**: Sends requests in a fixed, cyclic order among servers.

**Pros**:

* Simple, fair, easy to implement
* Good for stateless, equal-capacity environments

**Cons**:

* Ignores current server load
* No session affinity
* Not ideal for varying server capacities

**Use Cases**:

* Stateless applications
* Homogeneous server environments

---

### **2. Least Connections**

**Mechanism**: Sends request to server with fewest **active connections**.

**Pros**:

* Load-aware and dynamic
* Adapts to variable workloads

**Cons**:

* Requires real-time state tracking
* Can struggle with short-lived connections

**Use Cases**:

* Stateful apps
* Heterogeneous environments with variable traffic

---

### **3. Weighted Round Robin (WRR)**

**Mechanism**: Like Round Robin but with **server weights**.

**Pros**:

* Respects server capacity differences
* Adjustable and scalable

**Cons**:

* Requires accurate weight settings
* Doesn’t adapt to real-time load changes

**Use Cases**:

* Servers with different processing capabilities
* Scalable web/database clusters

---

### **4. Weighted Least Connections**

**Mechanism**: Combines **Least Connections** + **Weights** for capacity.

**Pros**:

* Dynamic & capacity-aware
* Efficient for heterogeneous setups

**Cons**:

* Higher complexity
* Requires both weight and connection state tracking

**Use Cases**:

* High-traffic apps, stateful services
* Mixed-capacity servers

---

### **5. IP Hash**

**Mechanism**: Uses client IP hash to pick server (consistent client-server mapping).

**Pros**:

* Ensures **session persistence**
* Simple and deterministic

**Cons**:

* Can lead to uneven distribution
* Not load-aware
* Server pool changes disrupt mapping

**Use Cases**:

* Stateful apps (e.g., shopping carts)
* Geo-distributed client bases

---

### **6. Least Response Time**

**Mechanism**: Chooses server with lowest average **response time**.

**Pros**:

* Optimizes performance dynamically
* Good resource utilization

**Cons**:

* Requires continuous monitoring
* May be affected by short-term latency spikes

**Use Cases**:

* Real-time apps (gaming, trading)
* Fast-response web services/APIs

---

### **7. Random**

**Mechanism**: Randomly assigns each request to any server.

**Pros**:

* Extremely simple
* No state tracking required

**Cons**:

* No awareness of server load or sessions
* Can lead to short-term imbalance

**Use Cases**:

* Stateless apps
* Equal-capacity servers
* Simple deployments

---

### **8. Least Bandwidth**

**Mechanism**: Sends request to server using **least bandwidth** currently.

**Pros**:

* Good for managing network traffic
* Prevents network bottlenecks

**Cons**:

* Requires bandwidth monitoring
* Variability may cause rebalancing overhead

**Use Cases**:

* High-bandwidth apps (video, file transfer)
* CDNs and real-time services

---

### **9. Custom Load**

**Mechanism**: Uses **custom-defined metrics** (CPU, memory, etc.) to route traffic.

**Pros**:

* Highly flexible and tailored
* Optimized for complex systems

**Cons**:

* High complexity
* Monitoring overhead and risk of misconfiguration

**Use Cases**:

* Complex, dynamic systems
* Apps needing multi-metric load control

---

## ✅ **Quick Comparison Table**

| Algorithm                  | Load-Aware | Session Affinity | Use Case                          |
| -------------------------- | ---------- | ---------------- | --------------------------------- |
| Round Robin                | ❌          | ❌                | Stateless, equal-capacity servers |
| Least Connections          | ✅          | Partial          | Variable traffic, stateful apps   |
| Weighted Round Robin       | ❌          | ❌                | Mixed-capacity servers            |
| Weighted Least Connections | ✅          | Partial          | Heterogeneous, high-traffic apps  |
| IP Hash                    | ❌          | ✅                | Stateful apps needing persistence |
| Least Response Time        | ✅          | ❌                | Low-latency, real-time apps       |
| Random                     | ❌          | ❌                | Stateless, simple deployments     |
| Least Bandwidth            | ✅          | ❌                | Bandwidth-sensitive apps          |
| Custom Load                | ✅ (custom) | Optional         | Complex/dynamic environments      |

---
### **Uses of Load Balancing**

1. **Improves Website Performance**
   Distributes traffic across multiple servers to ensure fast response times and avoid overloading any single server.
   *E.g., E-commerce site during peak sales.*

2. **Ensures High Availability & Reliability**
   Redirects traffic to healthy servers if one fails, avoiding downtime.
   *E.g., Banking app maintains service during server outages.*

3. **Enables Scalability**
   Easily accommodates growing demand by adding more servers to the pool.
   *E.g., Streaming platform handles user growth smoothly.*

4. **Provides Redundancy**
   Maintains multiple copies of data/services to prevent loss from hardware failure.
   *E.g., File storage services keep data available even if one server fails.*

5. **Optimizes Network Traffic**
   Distributes data across multiple links or paths to reduce congestion.
   *E.g., Corporate networks use multiple internet connections efficiently.*

6. **Supports Geographic Distribution**
   Routes users to the nearest or best-performing data center to reduce latency.
   *E.g., Global companies improve UX by region-based routing.*

7. **Boosts Application Performance**
   Assigns dedicated resources per application to maintain optimal service levels.
   *E.g., Enterprises ensure email, file sharing, etc., run smoothly.*

8. **Enhances Security**
   Mitigates DDoS attacks by spreading traffic across multiple servers.
   *E.g., News websites stay online during attack attempts.*

9. **Reduces Costs**
   Improves resource utilization, lowering hardware and energy expenses.
   *E.g., SMBs minimize server usage with efficient distribution.*

10. **Enables Content Caching**
    Serves static content from the load balancer directly for faster delivery.
    *E.g., Popular streaming content cached at the edge to reduce server load.*

---

### **Types of Load Balancers**

1. **Hardware Load Balancer**

* **What**: Physical device using ASICs/FPGAs for traffic distribution.
* **Pros**: High performance, built-in features, handles large volumes.
* **Cons**: Expensive, less scalable, needs expertise.
* **Use Case**: Large e-commerce platforms for web traffic distribution.

2. **Software Load Balancer**

* **What**: Runs on general-purpose servers or VMs using software algorithms.
* **Pros**: Cost-effective, scalable, flexible deployment.
* **Cons**: Lower performance under heavy load, resource-intensive.
* **Use Case**: Startups using cloud VMs for app traffic management.

3. **Cloud-based Load Balancer**

* **What**: Managed service from cloud providers.
* **Pros**: Scalable, low maintenance, pay-as-you-go pricing.
* **Cons**: Less control, vendor lock-in risks.
* **Use Case**: Mobile apps distributing API requests across cloud servers.

4. **DNS Load Balancer**

* **What**: Uses DNS to resolve a domain to multiple IPs.
* **Pros**: Simple, geographic distribution possible.
* **Cons**: No real-time health checks, slow updates.
* **Use Case**: CDNs routing users to nearest edge servers.

5. **Global Server Load Balancing (GSLB)**

* **What**: Combines DNS load balancing with health checks and routing logic.
* **Pros**: Intelligent distribution across global data centers.
* **Cons**: Complex setup, DNS limitations.
* **Use Case**: Multinational companies optimizing latency and uptime.

6. **Hybrid Load Balancer**

* **What**: Mix of hardware, software, and cloud load balancing techniques.
* **Pros**: Highly flexible, best performance and reliability mix.
* **Cons**: Complex, costly, requires deep expertise.
* **Use Case**: Streaming platforms managing global scale and varied traffic types.

7. **Layer 4 Load Balancer (Transport Layer)**

* **What**: Uses TCP/UDP headers (IP and port) to route traffic.
* **Pros**: Fast, protocol-agnostic, simple.
* **Cons**: No app-level awareness or session handling.
* **Use Case**: Online gaming platforms distributing player traffic.

8. **Layer 7 Load Balancer (Application Layer)**

* **What**: Uses HTTP headers, cookies, and URLs for routing.
* **Pros**: Smart, supports session persistence, SSL offloading.
* **Cons**: Slower, complex, needs more resources.
* **Use Case**: Web apps routing API requests to appropriate microservices.

---

### **Stateless vs. Stateful Load Balancing**

#### **Stateless Load Balancing**

* **Definition**: Does **not store session information**; routes each request independently.
* **Routing Basis**: Uses request data like IP address, URL, or headers.
* **Pros**: Fast, simple, and scalable.
* **Use Case**: Apps where each request is independent (e.g., product search by location).

#### **Stateful Load Balancing**

* **Definition**: **Maintains session information**; ensures client requests go to the same server.
* **Use Case**: Apps needing session persistence (e.g., user login and personal data access).

**Types of Stateful Load Balancing**:

1. **Source IP Affinity**:

   * Routes based on client’s IP.
   * **Limitation**: Unreliable if IP changes (e.g., mobile users).
2. **Session Affinity**:

   * Uses session ID (e.g., cookie or URL param) for consistent routing.
   * **More robust** than IP-based affinity.

---

### **When to Use**

* **Stateless**: For scalable, stateless services (e.g., APIs, search).
* **Stateful**: For apps requiring session tracking (e.g., e-commerce login).

