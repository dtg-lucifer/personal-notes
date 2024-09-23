### What is a Load Balancer?

A **load balancer** is a device that distributes network or application traffic across multiple servers to ensure no single server becomes overwhelmed. This helps improve the availability and reliability of your application by spreading the load evenly.

### How Load Balancers Work on AWS

AWS offers several types of load balancers under the Elastic Load Balancing (ELB) service:

1. **Application Load Balancer (ALB)**: Operates at the application layer (Layer 7) and is best suited for HTTP and HTTPS traffic.
2. **Network Load Balancer (NLB)**: Operates at the transport layer (Layer 4) and is designed for high-performance, low-latency traffic.
3. **Gateway Load Balancer (GLB)**: Integrates with third-party virtual appliances for traffic inspection and security.
4. **Classic Load Balancer (CLB)**: Operates at both the application and transport layers but is being phased out in favor of ALB and NLB.

***EXAMPLE LOAD BALANCER SETUP WITH TERRAFORM - [[003_aws_load_balancer]]***