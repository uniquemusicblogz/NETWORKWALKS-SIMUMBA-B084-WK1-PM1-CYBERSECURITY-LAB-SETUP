# Cybersecurity Lab Environment Setup

![Kali Linux](https://img.shields.io/badge/Kali%20Linux-2026.2-557C94?style=flat-square&logo=kalilinux&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VirtualBox-7.2-183A61?style=flat-square&logo=virtualbox&logoColor=white)
![Network](https://img.shields.io/badge/Network-10.0.0.0%2F24-0070C0?style=flat-square)
![Focus](https://img.shields.io/badge/Focus-Penetration%20Testing-C00000?style=flat-square)

A virtual cybersecurity and penetration-testing laboratory built with **VirtualBox** and **Kali Linux**, designed for controlled, repeatable security practice.

---

## Table of Contents

1. [Overview](#overview)
2. [Objectives](#objectives)
3. [Intended Use](#intended-use)
4. [Lab Configuration](#lab-configuration)
5. [Setup Procedure](#setup-procedure)
6. [Verification](#verification)
7. [Troubleshooting](#troubleshooting)
8. [Key Takeaways](#key-takeaways)
9. [Resources](#resources)
10. [Author](#author)

---

## Overview

This project establishes an isolated lab environment in which security tools, network scanning, reconnaissance, and vulnerability assessment can be performed safely and repeatedly. The lab runs on a **private virtual network**, allowing additional virtual machines to be added later as targets for authorised testing.

## Objectives

- Install and configure VirtualBox
- Install and import Kali Linux as a virtual machine
- Create a private **NAT Network** for the lab
- Configure network connectivity for Kali Linux
- Assign a consistent IP address to the Kali VM
- Verify network connectivity and DNS resolution
- Create a clean snapshot for recovery
- Document the complete setup process
- Prepare the environment for future cybersecurity projects

## Intended Use

The lab supports the following activities:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security tool experimentation

> **Warning:** This lab must only be used on systems you own or have explicit permission to test. Unauthorised scanning or exploitation is illegal and unethical.

---

## Lab Configuration

| Component | Configuration |
|---|---|
| Host OS | Windows 11 |
| Host RAM | 8 GB |
| Processor | Intel Core i5 |
| Hypervisor | VirtualBox 7.2 |
| Security OS | Kali Linux 2026.2 |
| Kali RAM | 2048 MB |
| Virtual Network | NAT Network |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |
| Reserved Range for Future VMs | 10.0.0.3 – 10.0.0.99 |

---

## Setup Procedure

### Step 1: Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual machine package, which may be distributed as a `.7z` archive.

### Step 2: Install VirtualBox

VirtualBox 7.2 was installed as the hypervisor for the lab.

### Step 3: Create the NAT Network

A dedicated NAT Network was created in VirtualBox with the following settings:

```
Network Name:  NatNetwork
IPv4 Prefix:   10.0.0.0/24
DHCP:          Enabled
IPv6:          Disabled
```

![NAT Network settings](network-settings.png)

A NAT Network was selected because virtual machines on the same network can communicate with one another while still reaching the internet. This allows attacker and target machines to interact within the lab.

### Step 4: Import Kali Linux

The official Kali Linux virtual machine was downloaded and imported into VirtualBox. The network adapter was configured as follows:

```
Adapter 1
  Attached to:   NAT Network
  Network:       NatNetwork
  Adapter Type:  Intel PRO/1000 MT Desktop
```

The VM was allocated **2048 MB** of RAM. A shared folder was also configured to transfer files between the Windows host and the Kali VM.

![Kali Linux home screen](Kali-Linux-Home.png)

### Step 5: Configure the Kali Linux Network

The network configuration was set to a consistent IPv4 address:

```
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0
Gateway:      10.0.0.1
DNS:          8.8.8.8
```

A fixed address makes the lab easier to document and simplifies referencing the Kali machine in future exercises.

![Kali network settings](network-settings-2.png)

### Step 6: Create a Clean Snapshot

Once the initial configuration was complete, a VirtualBox snapshot was taken:

```
Snapshot name: MY FRESH KALI
```

This snapshot serves as the clean baseline for the lab. If a future exercise alters or damages the VM configuration, the machine can be restored to this state.

---

## Verification

| Test | Command | Expected Result |
|---|---|---|
| Check IP address | `ip a` | Kali IP `10.0.0.2/24` displayed |
| Test gateway | `ping 10.0.0.1` | Successful replies |
| Test internet connectivity | `ping 8.8.8.8` | Successful replies |
| Test DNS resolution | `nslookup networkwalks.com` | Domain resolves |
| Verify Nmap | `nmap --version` | Nmap version displayed |
| Verify snapshot | Restore snapshot, then run `ip a` | Baseline configuration restored |

**Example results:**

```
IP Address:  10.0.0.2/24
Gateway:     10.0.0.1
DNS:         8.8.8.8
```

---

## Troubleshooting

### Internet connectivity fails after static IP configuration

After manually configuring IPv4 settings, internet connectivity may fail depending on the Kali/NetworkManager configuration.

**Workaround used in this lab:**

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

Restart the network connection or reboot the VM, then retest connectivity.

> **Note:** Connection names vary between systems. Run `nmcli connection show` first to identify yours.

---

## Key Takeaways

- **NAT vs. NAT Network:** A standard NAT isolates each VM behind the host, whereas a NAT Network allows multiple VMs to communicate with each other while still providing outbound connectivity.
- **Virtual networking:** VirtualBox virtual adapters connect VMs to different network types, and the chosen configuration determines how machines can interact.
- **Static IP configuration:** Setting and verifying IPv4 addressing, subnet masks, gateways, and DNS in Linux.
- **Snapshots:** A clean snapshot should be taken before any risky or experimental activity, providing a known-good recovery point.
- **Documentation:** Recording commands, configuration, screenshots, problems, and solutions is a core professional practice.

---

## Resources

- [7-Zip](https://7-zip.org/download.html)
- [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux Downloads](https://www.kali.org/get-kali/)

---

## Author

**Simumba AKAKULUBELWA** | B084
<br>
**Network Engineering Student | Cybersecurity Learner | Aspiring Network Security Professional**

This repository represents my practical learning journey as I develop my skills in networking, Linux, virtualisation, and cybersecurity.

[LinkedIn](https://www.linkedin.com/in/simumba-akakulubelwa/)

**Program:** Cybersecurity at Networkwalks · **Week:** 01 · **Project:** Cybersecurity & Pentesting Lab Setup
