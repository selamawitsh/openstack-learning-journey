
---

### 03-horizon-vm-creation.md

```markdown
# Creating VMs via Horizon (OpenStack Web Dashboard)

## What is Horizon?
Horizon is the web-based graphical interface for OpenStack. It's the easiest way to get started with OpenStack before learning CLI commands.

## Accessing Horizon

1. Open web browser
2. Navigate to: `http://192.168.45.128/dashboard`
3. Login:
   - Username: `admin`
   - Password: `secret`

## The Four Essential Resources

Before creating a VM, understand these concepts:

| Resource | What It Is |
|----------|------------|
| **Image** | Operating system template |
| **Flavor** | CPU/RAM/Disk size |
| **Network** | Connectivity |
| **Key Pair** | SSH authentication |
| **Security Group** | Firewall rules |

## Step-by-Step VM Creation

### Step 1: Navigate to Launch Instance

### Step 2: Details Tab

| Field | My Value | Why |
|-------|----------|-----|
| Instance Name | `First_VM` | Unique identifier |
| Description | `My first OpenStack VM` | Optional notes |
| Availability Zone | `nova` | Default compute service |

### Step 3: Source Tab (Choose OS)

| Field | My Value | Why |
|-------|----------|-----|
| Select Boot Source | `Image` | Boot from OS template |
| Available Images | `cirros-0.6.3-x86_64-disk` | Tiny Linux (15MB) for learning |

**Why CirrOS?** 
- Boots in seconds (Ubuntu takes minutes)
- Uses only 192MB RAM
- Perfect for testing and learning

### Step 4: Flavor Tab (Choose VM Size)

| Flavor | vCPUs | RAM | Disk | Use Case |
|--------|-------|-----|------|----------|
| `m1.tiny` | 1 | 512MB | 1GB | **Best for learning** |
| `m1.nano` | 1 | 192MB | 1GB | For CirrOS only |
| `m1.small` | 1 | 2GB | 20GB | For Ubuntu VMs |

**My choice:** `m1.tiny`

### Step 5: Networks Tab

1. Find `public` network in "Available" list
2. Click the **(up arrow)** to move it to "Allocated"
3. The network should now appear under "Allocated"

**Why public network?** It provides external connectivity so you can SSH into your VM.

### Step 6: Security Groups Tab

1. Find `default` security group
2. Click the **(up arrow)** to allocate it

**Note:** The `default` security group blocks ALL incoming traffic by default. You'll need to add rules for SSH later.

### Step 7: Key Pair Tab (Most Important!)

**Option A: Create a new key pair**
1. Click **+ Create Key Pair**
2. Enter name: `my-key`
3. Click **Create Key Pair**


**Option B: Import existing key pair**
1. Click **Import Key Pair**
2. Name it (e.g., `my-existing-key`)
3. Paste your **public key** content
4. Click **Import Key Pair**

### Step 8: Save Your Key Pair (After Horizon)

```bash
# Move key to correct location
mv ~/Downloads/my-key.pem ~/.ssh/

# Set correct permissions (SSH requires this!)
chmod 600 ~/.ssh/my-key.pem

# Generate public key from private key
ssh-keygen -y -f ~/.ssh/my-key.pem > ~/.ssh/my-key.pub

### After Launch

Check VM Status
In Horizon: Project → Compute → Instances

| Status | Meaning |
|--------|---------|
| BUILD | VM is being created (wait 30-60 seconds) |
| ACTIVE | VM is running and ready |
| SHUTOFF | VM is powered off |
| ERROR | Something went wrong |

### What I Learned

- Horizon is user-friendly but requires clicking through multiple tabs

- Every VM needs: Image + Flavor + Network + Key Pair + Security Group

- The default security group blocks SSH by default - you must add the rule

- CirrOS is perfect for learning (fast boot, minimal resources)

- Save your private key immediately - you can't download it again!