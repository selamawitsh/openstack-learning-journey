# Creating VMs via OpenStack CLI (Command Line)

## Why Use CLI Over Horizon?

| Horizon (GUI) | CLI (Command Line) |
|---------------|---------------------|
| Visual, beginner-friendly | Scriptable and automatable |
| Good for exploration | Faster for repeated tasks |
| Cannot automate | Can create 100 VMs with one command |
| Slower for power users | Works over SSH connections |

---

## Prerequisites: Authentication

### Step 1: Switch to Stack User

```bash
sudo -u stack -i
```

### Step 2: Source OpenRC Credentials

```bash
source /opt/stack/devstack/openrc admin admin
# Enter password: secret
```

**What this does:**  
Loads environment variables that tell the CLI where your OpenStack is and who you are.

---

### Step 3: Verify Authentication

```bash
openstack token issue
```

---

## Exploring Available Resources

Before creating a VM, see what's available:

```bash
# List operating system images
openstack image list

# List available VM sizes
openstack flavor list

# List networks
openstack network list

# List security groups
openstack security group list

# List SSH key pairs
openstack keypair list
```

---

## Setting Up SSH Key Pair (CLI Method)

### Option A: Create a New Key Pair

```bash
# Create and save key in one command
openstack keypair create my-cli-key > ~/.ssh/my-cli-key.pem

# Fix permissions
chmod 600 ~/.ssh/my-cli-key.pem

# Generate public key from private key
ssh-keygen -y -f ~/.ssh/my-cli-key.pem > ~/.ssh/my-cli-key.pub
```

---

### Option B: Upload an Existing Key

```bash
openstack keypair create --public-key ~/.ssh/my-key.pub my-key
```

---

## Configuring Security Groups (Allow SSH)

By default, the security group blocks all incoming traffic.

```bash
# Allow SSH (port 22)
openstack security group rule create --proto tcp --dst-port 22 default

# Allow ICMP (ping)
openstack security group rule create --proto icmp default

# Verify rules were added
openstack security group rule list default
```

---

## Creating a VM (The Main Command)

### Basic VM Creation Command

```bash
openstack server create \
    --flavor m1.tiny \
    --image cirros-0.6.3-x86_64-disk \
    --key-name my-key \
    --network public \
    --security-group default \
    First_VM_CLI
```

---

## Checking VM Status

### List all VMs

```bash
openstack server list
```

---

## Accessing Your VM

```bash
ssh -i ~/.ssh/my-key.pem cirros@172.24.4.79
```