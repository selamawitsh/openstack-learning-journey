# DevStack Installation Guide

## What is DevStack?
DevStack is a one-machine installation of OpenStack designed for development and learning. It runs entirely on a single VM or physical server.

## Prerequisites

| Requirement | Minimum | My Setup |
|-------------|---------|----------|
| RAM | 8GB | 8GB |
| CPU Cores | 4 | 4 vCPUs |
| Disk Space | 100GB | 100GB |
| Operating System | Ubuntu 22.04 | Ubuntu 22.04 |

## Step-by-Step Installation

### Step 1: Create a Stack User

OpenStack services should run under a dedicated `stack` user, not your regular user.

```bash
# Create the stack user with home directory /opt/stack
sudo useradd -s /bin/bash -d /opt/stack -m stack

# Allow stack user to run sudo without password
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack

# Create the stack user with home directory /opt/stack
sudo useradd -s /bin/bash -d /opt/stack -m stack

# Allow stack user to run sudo without password
echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack

# Why? Running OpenStack services as a non-root user is a security best practice.

# Switch to stack user
sudo -u stack -i

# Clone DevStack repository
git clone https://opendev.org/openstack/devstack
cd devstack

# Create local.conf configuration file
cat > local.conf <<EOF
[[local|localrc]]
ADMIN_PASSWORD=secret
DATABASE_PASSWORD=\$ADMIN_PASSWORD
RABBIT_PASSWORD=\$ADMIN_PASSWORD
SERVICE_PASSWORD=\$ADMIN_PASSWORD
HOST_IP=192.168.45.128
EOF

# Run installation
./stack.sh

# Verify Installation
#This is your host IP: 192.168.45.128
#Horizon is now available at http://192.168.45.128/dashboard
#Keystone is serving at http://192.168.45.128/identity/