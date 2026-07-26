# AWS Site-to-Site VPN Lab Validation

## Overview

This document provides a validation checklist after deploying an AWS Site-to-Site VPN lab to ensure connectivity, routing, and tunnel health.

## Prerequisites

- AWS VPN Connection created
- Customer Gateway configured
- Virtual Private Gateway or Transit Gateway attached
- On-premises router configured
- BGP or static routing completed

## Validation Steps

### Tunnel Status

- Verify both VPN tunnels are UP.
- Confirm IKE negotiation is successful.
- Check IPsec Security Associations (SAs).

### Routing

- Verify learned routes.
- Confirm route propagation (if using BGP).
- Validate VPC route tables.

### Connectivity

- Ping EC2 instances from the on-premises network.
- Verify return traffic.
- Test application connectivity.

### Monitoring

- Review CloudWatch VPN metrics.
- Check tunnel status events.
- Monitor packet loss and latency.

## Common Issues

- Incorrect pre-shared key
- Phase 1 or Phase 2 mismatch
- Missing VPC routes
- Firewall blocking VPN traffic
- BGP ASN mismatch

## Best Practices

- Configure both tunnels for redundancy.
- Test failover regularly.
- Monitor tunnel health continuously.
- Document routing and VPN parameters.
- Save configuration backups after validation.
