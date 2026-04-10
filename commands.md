# OpenStack Commands Reference

## Authentication
| Command | Purpose |
|---------|---------|
| `source /opt/stack/devstack/openrc admin admin` | Authenticate with OpenStack |

## View Available Resources
| Command | Purpose |
|---------|---------|
| `openstack image list` | List available OS images |
| `openstack flavor list` | List available VM sizes (CPU/RAM/Disk) |
| `openstack network list` | List available networks |
| `openstack security group list` | List firewall groups |
| `openstack keypair list` | List SSH key pairs |

## VM Operations
| Command | Purpose |
|---------|---------|
| `openstack server create --flavor <flavor> --image <image> --key-name <key> --network <network> --security-group <sg> <name>` | Create a VM |
| `openstack server list` | List all VMs |
| `openstack server show <VM_NAME>` | Show VM details |
| `openstack server stop <VM_NAME>` | Power off VM |
| `openstack server start <VM_NAME>` | Power on VM |
| `openstack server reboot <VM_NAME>` | Restart VM |
| `openstack server delete <VM_NAME>` | Remove VM permanently |
| `openstack console log show <VM_NAME>` | View boot console output |

## Key Pair Management
| Command | Purpose |
|---------|---------|
| `openstack keypair create my-key > ~/.ssh/my-key.pem` | Create new key pair |
| `chmod 600 ~/.ssh/my-key.pem` | Fix key permissions |
| `openstack keypair create --public-key ~/.ssh/my-key.pub my-key` | Upload existing public key |

## Security Groups
| Command | Purpose |
|---------|---------|
| `openstack security group rule create --proto tcp --dst-port 22 default` | Allow SSH access |
| `openstack security group rule create --proto icmp default` | Allow ping |
| `openstack security group rule list default` | List rules for default group |

## SSH Access
| Command | Purpose |
|---------|---------|
| `ssh -i ~/.ssh/my-key.pem cirros@<VM_IP>` | SSH into CirrOS VM |
| `ssh -i ~/.ssh/my-key.pem ubuntu@<VM_IP>` | SSH into Ubuntu VM |