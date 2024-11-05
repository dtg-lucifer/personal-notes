### 1. **Load Balancing**
   - **Definition**: Distributes incoming network traffic across multiple servers to ensure no single server is overwhelmed.
   - **Types**:
     - **DNS-based Load Balancing**: Uses DNS to distribute traffic to different servers.
     - **Reverse Proxy**: Like **Nginx** or **HAProxy** for distributing HTTP requests.
     - **Hardware vs. Software Load Balancers**.
   - **Techniques**: Round-robin, Least Connections, IP Hashing, Weighted Load Balancing.
   - **Considerations**: **Sticky Sessions** (ensuring a client keeps connecting to the same server), **Global Load Balancing** for geographic distribution, **failover**.

### 2. **Caching**
   - **Definition**: Temporarily stores data in memory to reduce database load and improve response times.
   - **Types**:
     - **In-memory Caching**: Tools like **Redis** or **Memcached** for fast, volatile storage.
     - **Database Query Caching**: Caching frequent queries to reduce database hits.
     - **Content Delivery Network (CDN)**: Caching static assets like images, CSS, and JavaScript on servers closer to the user.
   - **Cache Invalidation Strategies**: Least Recently Used (LRU), TTL (Time to Live), Write-through, Write-back, and Write-around caches.
   - **Trade-offs**: Cache consistency, cache misses, and cache size limitations.

### 3. **Database Sharding and Partitioning**
   - **Definition**: Splitting a large dataset into smaller, more manageable pieces (shards or partitions) distributed across multiple servers.
   - **Horizontal vs. Vertical Partitioning**:
     - **Horizontal Partitioning** (Sharding): Distribute rows across databases.
     - **Vertical Partitioning**: Distribute columns across databases.
   - **Shard Keys**: Choosing an optimal shard key to distribute load evenly (e.g., user ID).
   - **Challenges**: Data consistency, cross-shard queries, and rebalancing shards when adding/removing nodes.
   - **Tools**: Databases like **Cassandra**, **MongoDB**, or **MySQL** with sharding.

### 4. **Replication**
   - **Definition**: Copying data across multiple machines to improve availability and fault tolerance.
   - **Types of Replication**:
     - **Master-Slave** (Primary-Replica): Writes go to the master, and reads are offloaded to replicas.
     - **Master-Master**: Both nodes can handle reads and writes, with synchronization between them.
   - **Challenges**:
     - **Replication Lag**: Time delay between writing to the master and propagating to the replicas.
     - **Consistency**: Ensuring data is the same across all replicas.
     - **Leader Election**: Mechanism for electing a new leader in case of a failure.
   - **Tools**: **Cassandra**, **MySQL**, **PostgreSQL** replication, and **ZooKeeper** for coordination.

### 5. **Distributed Systems and Consistency Models**
   - **CAP Theorem**: In distributed systems, you can choose only two out of three: **Consistency**, **Availability**, and **Partition Tolerance**.
     - **Consistency**: Every read receives the most recent write.
     - **Availability**: Every request receives a response (without guarantee of the latest data).
     - **Partition Tolerance**: The system continues to operate despite network partitioning.
   - **Consistency Models**:
     - **Strong Consistency**: Guarantees that all nodes see the same data at the same time.
     - **Eventual Consistency**: Updates propagate asynchronously, and the system eventually becomes consistent.
     - **Causal Consistency**, **Read Your Writes**, and other consistency levels.

### 6. **Rate Limiting and Throttling**
   - **Definition**: Controlling the rate of incoming requests to prevent system overload.
   - **Rate Limiting Techniques**:
     - **Token Bucket Algorithm**: Tokens are generated at a fixed rate and requests consume them.
     - **Leaky Bucket Algorithm**: Processes requests at a constant rate regardless of bursty traffic.
   - **Use Cases**: Preventing **DDoS attacks**, protecting APIs, and ensuring fair resource allocation.

### 7. **Content Delivery Networks (CDNs)**
   - **Definition**: Geographically distributed servers that cache content (especially static assets like images, videos) closer to the user.
   - **Benefits**: Reduces latency, improves loading times, and offloads traffic from the origin server.
   - **Popular CDNs**: **Cloudflare**, **Akamai**, **Amazon CloudFront**, **Google Cloud CDN**.

### 8. **Event-Driven Architecture**
   - **Definition**: Systems that communicate via events, typically using pub/sub or event sourcing.
   - **Pub/Sub Pattern**: A system where publishers send messages that are consumed by multiple subscribers asynchronously.
   - **Event Sourcing**: Storing the state of the system as a series of events, rather than as a direct result of actions.
   - **Use Cases**: Real-time applications, microservices, IoT.

### 9. **Service Discovery**
   - **Definition**: Mechanism by which microservices or distributed systems automatically locate and connect to each other.
   - **Approaches**:
     - **Client-Side Discovery**: Clients know how to find the service (using a service registry like **Consul**, **Eureka**).
     - **Server-Side Discovery**: A load balancer routes requests to services.
   - **Tools**: **Consul**, **Eureka**, **Zookeeper**, **Kubernetes DNS**.

### 10. **API Gateway**
   - **Definition**: A single entry point for external clients to interact with various backend services.
   - **Features**: Request routing, rate limiting, user authentication, logging, and monitoring.
   - **Benefits**: Decouples clients from services, simplifies service discovery, and enhances security.
   - **Tools**: **Kong**, **NGINX**, **AWS API Gateway**.

### 11. **Data Consistency and Availability (ACID vs. BASE)**
   - **ACID**: Stands for **Atomicity**, **Consistency**, **Isolation**, and **Durability**; traditional databases follow this.
   - **BASE**: Stands for **Basically Available**, **Soft State**, **Eventual Consistency**; often followed in distributed systems.
   - **Trade-offs**: ACID provides strict consistency at the cost of scalability, while BASE focuses on availability and scalability at the expense of consistency.

### 12. **Monolithic vs. Microservices Architecture**
   - **Monolithic**: Single, unified codebase for the entire application.
   - **Microservices**: An application is divided into smaller, independent services that communicate via APIs or message queues.
   - **Challenges in Microservices**: Communication between services, service discovery, consistency, and monitoring.

### 13. **Logging and Monitoring**
   - **Definition**: Collecting and analyzing logs and metrics from a system to ensure its health and detect issues.
   - **Tools**:
     - **Log Aggregation**: **ELK Stack (Elasticsearch, Logstash, Kibana)**, **Splunk**.
     - **Monitoring and Alerting**: **Prometheus**, **Grafana**, **Datadog**.
     - **Distributed Tracing**: **Jaeger**, **Zipkin** for understanding request flows in distributed systems.

### 14. **Security in System Design**
   - **Authentication & Authorization**: How users are authenticated and what permissions they have.
   - **Data Encryption**: Encrypting data at rest (stored in databases) and in transit (e.g., using HTTPS, TLS).
   - **OAuth & JWT**: Token-based authentication systems used in APIs.
   - **Mitigating DDoS Attacks**: Using firewalls, rate limiting, and load balancers.
   
---

### Things to Focus on for Interviews:
- **Trade-offs**: Understand the **pros and cons** of different approaches (e.g., sharding vs. replication, ACID vs. BASE).
- **Scalability**: Know how to scale services and handle large-scale traffic.
- **Consistency vs. Availability**: Understand when to prioritize one over the other based on business needs.
- **Fault Tolerance**: Learn how systems can recover from failures (e.g., leader election, failover).
- **Latency Optimization**: Techniques like caching, using CDNs, and choosing the right database models for low-latency applications.

Mastering these topics will make you well-prepared for system design interviews and give you a strong understanding of distributed systems architecture.