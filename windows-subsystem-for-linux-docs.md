# Installing and Configuring WSL 2 with Ubuntu and Custom Mount

## System Requirements

### Operating System

#### Windows 10:
Version 2004 or higher

Build 19041 or later

#### Windows 11:
Any version supports WSL 2 out of the box

You can check your Windows version by running: `winver`

### System Architecture
64-bit system with support for virtualization

Required: x64 or ARM64

Virtualization must be enabled in BIOS/UEFI

### Optional but Recommended
At least 8 GB of RAM (4 GB minimum, but performance suffers)

Solid-State Drive (SSD) for better file I/O performance

Windows Subsystem for Linux feature enabled (can be enabled via wsl --install)

Virtual Machine Platform feature must be enabled (WSL 2 uses a lightweight VM)

### Incompatible Systems
32-bit versions of Windows (not supported)

Windows 7 or 8 (WSL not available)

Older Windows 10 versions (pre-2004)

## Installing WSL 2 with Ubuntu

### 1. Install Ubuntu
```
wsl --install -d ubuntu
```
Wait for the installation to complete. You’ll be prompted to enter a new username and password.

Note: On Windows 10, you may need to run `wsl --update`

### 2. Launch Ubuntu
```
wsl -d ubuntu
```

### 3. Disable Auto-Mounting of Drives
Edit WSL configuration:
```
sudo nano /etc/wsl.conf
```

Add:
```
[automount]
enabled = false
```
Press `Ctrl+O` to save, then `Enter`, and `Ctrl+X` to exit.

### 4. Create a Custom Mount Script
Create the mount script:
```
sudo nano /etc/init.d/manual-mount.sh
```

Add:
```
#!/bin/bash

mountpoint="/home/user/location-where-the-directory-will-be-mounted"
winpath="location-of-the-directory-on-the-main-machine"

if ! mountpoint -q "$mountpoint"; then
  mkdir -p "$mountpoint"
  mount -t drvfs "$winpath" "$mountpoint"
fi
```

Press `Ctrl+O` to save, then `Enter`, and `Ctrl+X` to exit.

Make it executable with:
```
sudo chmod +x /etc/init.d/manual-mount.sh
```

### 5. Run Script Automatically on Shell Start

Edit .bashrc:
```
nano ~/.bashrc
```

Add:
```
sudo /etc/init.d/manual-mount.sh
```

### 6. Allow Passwordless Execution for the Mount Script
Run:
```
sudo visudo
```

Add:
```
USERNAME ALL=(ALL) NOPASSWD: /etc/init.d/manual-mount.sh
```

### 7. Restart WSL
```
wsl --shutdown
```

### 8. Final Check
Launch Ubuntu:
```
wsl -d Ubuntu
```
Check if your mount is present:
```
ls /home/user/location-where-the-directory-is-mounted
```
