# AWS VPC Flow Logs Troubleshooting Lab

## Objective

Use AWS VPC Flow Logs to investigate network connectivity problems between resources inside an AWS VPC.

## Architecture

```text
Client
   |
   v
Public/Private Subnet
   |
   v
EC2 Instance
   |
   v
Security Group
   |
   v
Network ACL
   |
   v
VPC Routing
```

## What VPC Flow Logs Capture

VPC Flow Logs provide information about IP traffic associated with:

* VPCs
* Subnets
* Elastic Network Interfaces
* EC2 instances
* Network interfaces used by AWS services

## Important Flow Log Fields

Common fields include:

```text
srcaddr
dstaddr
srcport
dstport
protocol
packets
bytes
action
start
end
```

The `action` field is especially useful:

```text
ACCEPT
REJECT
```

`ACCEPT` indicates that the recorded traffic was permitted.

`REJECT` indicates that the recorded traffic was rejected, for example because of a security group or network ACL rule.

## Troubleshooting Scenario

Assume an application server cannot communicate with another workload on TCP port 443.

```text
Application Server
10.10.1.10
      |
      | TCP/443
      v
Destination Server
10.20.1.20
```

Start by checking the relevant VPC Flow Logs.

## Investigation Workflow

### 1. Identify Source and Destination

Document:

```text
Source IP
Destination IP
Protocol
Source Port
Destination Port
```

### 2. Review Flow Logs

Search for traffic matching the source and destination addresses.

Example:

```text
10.10.1.10 → 10.20.1.20 TCP/443
```

### 3. Check the Action

If the record shows:

```text
ACCEPT
```

continue investigating routing, return traffic, application availability, and other relevant components.

If it shows:

```text
REJECT
```

investigate applicable security controls.

### 4. Verify Security Groups

Check:

* Inbound rules
* Outbound rules
* Protocol
* Port
* Source/destination configuration

Remember that security groups are stateful.

### 5. Verify Network ACLs

Check both:

```text
Inbound NACL Rules
Outbound NACL Rules
```

Network ACLs are stateless, so both directions must be permitted.

### 6. Verify Routing

Review the subnet route tables.

Confirm that the required destination has an appropriate route and next hop.

Depending on the architecture, this could involve:

* Local VPC routing
* Transit Gateway
* VPC Peering
* VPN
* Direct Connect
* NAT Gateway

### 7. Check Return Traffic

A successful forward path does not automatically prove that the complete application path is functioning.

Validate the return path from destination to source.

## Example Troubleshooting Logic

```text
Application Failure
        |
        v
Identify Source/Destination
        |
        v
Review VPC Flow Logs
        |
        v
ACCEPT or REJECT?
     /        \
 REJECT      ACCEPT
   |            |
   v            v
SG/NACL      Routing
Review       Return Path
             Application
```

## Useful AWS CLI Examples

Describe VPC Flow Logs:

```bash
aws ec2 describe-flow-logs
```

Review route tables:

```bash
aws ec2 describe-route-tables
```

Review security groups:

```bash
aws ec2 describe-security-groups
```

Review network ACLs:

```bash
aws ec2 describe-network-acls
```

## Production Validation Checklist

* Source IP identified
* Destination IP identified
* Required protocol and port confirmed
* Relevant Flow Log records located
* ACCEPT/REJECT action reviewed
* Security groups validated
* Network ACLs validated
* Route tables validated
* Return path validated
* Application listening state verified
* Connectivity retested

## Best Practices

* Enable Flow Logs for critical environments.
* Centralize logs where appropriate.
* Define suitable log retention.
* Use descriptive resource tags.
* Monitor recurring rejected traffic.
* Correlate Flow Logs with firewall and application logs.
* Document common connectivity troubleshooting procedures.
* Avoid assuming that every REJECT record represents an incident.

## Key Takeaway

VPC Flow Logs provide visibility into network traffic metadata and are valuable when troubleshooting AWS connectivity. Combine them with security-group, NACL, routing, return-path, and application validation rather than using Flow Logs as the only troubleshooting source.
