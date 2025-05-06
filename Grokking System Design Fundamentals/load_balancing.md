## **Introduction to Load Balancing**
*  The main goal of load balancing is to ensure high availability, reliability, and performance by avoiding overloading a single server and avoiding downtime.
*  To utilize full scalability and redundancy, we can try to balance the load at each layer of the system. We can add LBs at three places:
    * Between the user and the web server
    * Between web servers and an internal platform layer, like application servers or cache servers
    * Between internal platform layer and database
* **How load balancer works?**
    * The client sends the request -> pass on to load balancer -> load balancer decides which server to send the request -> server sends back the response to LB -> LB sends the response back to client
## **Load Balancing Algorithms**
1. **Round Robin**
   * This algorithm distributes incoming requests to servers in a cyclic order.
   * **Pros**
     * Equal distributions of requests among servers
     * easy
     * works well when servers have similar capacity
   * **Cons**
     * No load awareness
     * No session affinity
     * Performance issues with servers having different capacities
     * Predictable distribution pattern
   * **Usecases**
     * Homogeneous Environments
     * Stateless applications
2. **Round Robin**
   * This algorithm distributes incoming requests to servers in a cyclic order.
   * **Pros**
     * Equal distributions of requests among servers
     * easy
     * works well when servers have similar capacity
   * **Cons**
     * No load awareness
     * No session affinity
     * Performance issues with servers having different capacities
     * Predictable distribution pattern
   * **Usecases**
     * Homogeneous Environments
     * Stateless applications
