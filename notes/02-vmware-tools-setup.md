
---

### 02-vmware-tools-setup.md

```markdown
# VMware Tools Setup Guide

## Why VMware Tools?
VMware Tools improves the performance and usability of your VM by enabling:
- Copy/paste between host and VM
- Drag and drop files
- Better mouse movement (no need to click to capture/release)
- Time synchronization
- Screen resolution adjustment

## Installation Steps

### Step 1: Install Open VM Tools

```bash
sudo apt update
sudo apt install open-vm-tools open-vm-tools-desktop -y


#open-vm-tools	Core VMware integration (time sync, mouse, etc.)
#open-vm-tools-desktop	Desktop integration (copy/paste, drag/drop)