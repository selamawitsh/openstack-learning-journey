
---

### 06-security-groups.md

```markdown
# OpenStack Security Groups Guide

## What are Security Groups?
Security groups act as virtual firewalls for your VMs. They control which incoming and outgoing traffic is allowed.

**Key concept:** By default, ALL incoming traffic is BLOCKED, and ALL outgoing traffic is ALLOWED.

## Security Group Rules

Each rule consists of:

| Component | Example | Description |
|-----------|---------|-------------|
| Direction | Ingress/Egress | Incoming or outgoing traffic |
| Protocol | TCP, UDP, ICMP | Type of traffic |
| Port Range | 22, 80, 443 | Which port number |
| Remote IP | 0.0.0.0/0, 192.168.1.0/24 | Who can connect |

## Viewing Security Groups

```bash
# List all security groups
openstack security group list

# Show details of default group
openstack security group show default

# List rules in default group
openstack security group rule list default