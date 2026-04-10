
---

### 05-networking-basics.md

```markdown
# OpenStack Networking Basics (Neutron)

## What is Neutron?
Neutron is OpenStack's networking service. It manages all networking resources: networks, subnets, routers, and IP addresses.

## Types of Networks

| Network Type | Description | Use Case |
|--------------|-------------|----------|
| **Public** | Accessible from outside OpenStack | SSH, web servers, external access |
| **Private** | Isolated within OpenStack | Internal communication between VMs |
| **Shared** | Accessible by multiple projects | Shared services like DNS |

## My Available Networks

From `openstack network list`:

| Network Name | Type | Purpose |
|--------------|------|---------|
| `public` | Public | External access (SSH, web) |
| `private` | Private | Internal VM communication |
| `shared` | Shared | Multi-project access |

## Viewing Networks

```bash
# List all networks
openstack network list

# Show network details
openstack network show public

# List subnets
openstack subnet list

# Show subnet details
openstack subnet show <SUBNET_ID>