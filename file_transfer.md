# Secure File Transfer Setup Between VMware Virtual Machines

This repository demonstrates the configuration and implementation of secure file transfer capabilities between VMware virtual machines using OpenSSH and Secure Copy Protocol (SCP).

## Overview

The implementation establishes encrypted file transfer channels between two VMware virtual machines through properly configured SSH services. The destination system operates Ubuntu Linux with OpenSSH server capabilities, while the source system initiates secure file transfer operations using standard SCP commands.

## Prerequisites

- Two VMware virtual machines with network connectivity
- Ubuntu Linux distribution on the destination system
- Administrative privileges on both systems
- Network access between systems on SSH port 22

## VMware Network Configuration

### Configure Bridged Network Connection

Before establishing file transfer capabilities, configure the virtual machine network settings to enable direct network communication between systems.

**Steps to Configure Bridged Connection:**

1. Access the VMware virtual machine settings
2. Navigate to Device → Network Adapter
3. Change network connection from NAT to Bridged
4. Select "Replicate physical network connection state"
5. Apply configuration changes and restart the virtual machine

This configuration enables the virtual machines to obtain IP addresses directly from the physical network, facilitating direct communication between systems without network address translation barriers.

## Destination System Configuration

### Step 1: Install OpenSSH Server

Install the OpenSSH server package to enable secure remote access capabilities:

```bash
sudo apt install openssh-server
```

The system will automatically handle dependency resolution and package configuration. Upon successful installation, the latest OpenSSH version will be available for service deployment.

### Step 2: Enable SSH Service

Configure the SSH service for automatic startup during system boot:

```bash
sudo systemctl enable ssh
```

This command ensures persistent service availability across system restart cycles.

### Step 3: Start SSH Service

Activate the SSH service immediately without requiring system restart:

```bash
sudo systemctl start ssh
```

The SSH daemon will begin accepting incoming secure connections following successful activation.

### Step 4: Verify Service Status

Confirm proper service deployment and operational status:

```bash
sudo systemctl status ssh
```

The status output provides comprehensive operational details including process identification, memory utilization, service state, and activity logs.

## Source System Operations

### Step 1: Directory Listing and File Verification

Before initiating file transfer operations, verify the presence and location of files within the source system directory structure:

```bash
ls
```

This command displays the current directory contents, enabling verification of file availability and proper file naming. The directory listing typically reveals system directories including Downloads, Templates, Videos, and various application installations such as Google Cloud SDK and Hadoop distributions.

**Example Output Structure:**
- System directories: Downloads, Templates, Videos
- Development tools: gae-hello-world, google-cloud-sdk, hadoop installations
- Target files: bk1.txt (designated for transfer)
- Configuration files: weather_data.txt, server configuration files

### Step 2: File Transfer Execution

Execute secure file transfer operations using the SCP protocol:

```bash
scp [local_file] [username]@[destination_ip]:[remote_path]
```

**Example Implementation:**

```bash
scp bk1.txt bikram@172.16.9.109:/home/bikram1
```

**Command Parameters:**
- `bk1.txt`: Local file designated for transfer
- `bikram`: Destination system username
- `172.16.9.109`: Target system IP address
- `/home/bikram1`: Remote directory path for file placement

## Network Configuration

The implementation utilizes the following network parameters:

- **Protocol**: SSH over TCP port 22
- **Authentication**: Username and password credentials
- **Encryption**: Standard SSH encryption protocols
- **Network Scope**: VMware virtual machine internal network

## Security Considerations

The configuration implements industry-standard security measures including encrypted data transmission, user authentication verification, and secure session management. All file transfers occur through encrypted channels, ensuring data confidentiality and integrity during transmission.

## Verification Results

Successful implementation demonstrates:
- Complete SSH service installation and configuration
- Stable service operation with efficient resource utilization
- Successful file transfer completion with progress reporting
- Proper authentication and network connectivity validation

## Troubleshooting

Common configuration issues and resolution approaches:

**Service Status Issues:**
Verify service status using `systemctl status ssh` and review system logs for error identification.

**Network Connectivity:**
Confirm network accessibility using `ping` commands and verify firewall configuration permits SSH traffic.

**Authentication Problems:**
Validate user credentials and verify account permissions on the destination system.

## Additional Resources

For comprehensive SSH configuration and security hardening procedures, consult the official OpenSSH documentation and Ubuntu system administration guides.

## License

This documentation is provided for educational and administrative purposes. Implementation should follow organizational security policies and network administration guidelines.
