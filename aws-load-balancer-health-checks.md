# AWS Load Balancer Health Checks

## Purpose

Health checks determine whether targets are available to receive traffic.

## Types of Health Checks

### Application Load Balancer (ALB)

- HTTP
- HTTPS

### Network Load Balancer (NLB)

- TCP
- HTTP
- HTTPS

## Health Check Components

- Protocol
- Port
- Path
- Interval
- Timeout
- Healthy Threshold
- Unhealthy Threshold

## Example

Protocol: HTTPS
Port: 443
Path: /health

## Benefits

- Removes unhealthy targets automatically
- Improves application availability
- Supports automatic recovery
- Reduces downtime

## Best Practices

- Use a dedicated health-check endpoint
- Monitor target group status
- Configure realistic thresholds
- Test health checks regularly
- Review CloudWatch metrics
