# My OpenStack Learning Journey 

## About This Repository
This repository documents my complete journey learning OpenStack using DevStack. I'm recording every command, configuration, and troubleshooting step so I can refer back to it in the future.

## Environment
| Component | Details |
|-----------|---------|
| Host OS | [Your host OS - Windows/Mac/Linux] |
| Virtualization | VMware Workstation Player |
| Guest OS | Ubuntu 22.04 (Jammy) |
| OpenStack | DevStack (latest) |
| VM Resources | 8GB RAM, 4 vCPUs, 100GB disk |

## What I've Learned

### 1. Setting Up DevStack
- Created a `stack` user for OpenStack installation
- Cloned DevStack repository
- Configured `local.conf` with passwords and IP settings
- Ran `./stack.sh` to install

### 2. VMware Tools Configuration
- Installed `open-vm-tools` and `open-vm-tools-desktop`
- Switched from Wayland to Xorg for clipboard sharing
- Edited VM configuration parameters

### 3. Creating VMs in OpenStack

#### Via Horizon (Web Dashboard)
- Accessed dashboard at `http://192.168.45.128/dashboard`
- Created key pairs
- Launched instances with CirrOS image
- Used `m1.tiny` flavor

#### Via CLI
- Sourced OpenStack credentials: `source /opt/stack/devstack/openrc admin admin`
- Listed available resources: `openstack image list`, `openstack flavor list`
- Created VMs using: `openstack server create --flavor m1.tiny --image cirros-0.6.3-x86_64-disk --key-name my-key --network public --security-group default <VM_NAME>`

### 4. Troubleshooting Common Issues
| Issue | Solution |
|-------|----------|
| Copy/paste not working | Switched to Xorg, ran `vmware-user-suid-wrapper` |
| "More than one SecurityGroup exists" | Used security group ID instead of name |
| Key pair not downloading | Manually copied from Horizon dialog |

## Useful Commands Reference

```bash
# Authentication
source /opt/stack/devstack/openrc admin admin

# Resource listing
openstack image list
openstack flavor list
openstack network list
openstack security group list
openstack keypair list

# VM Management
openstack server create --flavor m1.tiny --image cirros-0.6.3-x86_64-disk --key-name my-key --network public --security-group default <VM_NAME>
openstack server list
openstack server show <VM_NAME>
openstack server stop <VM_NAME>
openstack server start <VM_NAME>
openstack server delete <VM_NAME>

