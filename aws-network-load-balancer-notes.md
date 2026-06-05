# AWS Network Load Balancer (NLB)

## What is an NLB?

AWS Network Load Balancer operates at Layer 4 (Transport Layer) and is designed to handle millions of requests per second with ultra-low latency.

## Key Features

- Layer 4 load balancing
- High performance and low latency
- Static IP support
- Preserves source IP address
- Supports TCP, UDP, and TLS traffic

## Common Use Cases

- High-performance applications
- Real-time communication services
- Gaming platforms
- Financial applications
- Hybrid cloud deployments

## Benefits

- Scales automatically
- Highly available across Availability Zones
- Handles sudden traffic spikes
- Integrates with Auto Scaling

## NLB vs ALB

| Feature | NLB | ALB |
|----------|----------|----------|
| Layer | Layer 4 | Layer 7 |
| Protocols | TCP, UDP, TLS | HTTP, HTTPS |
| Source IP Preservation | Yes | No |
| Static IP | Yes | No |

## Best Practices

- Enable health checks
- Deploy across multiple Availability Zones
- Monitor with CloudWatch
- Use TLS listeners when required
- Review target group health regularly
