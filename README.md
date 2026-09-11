<h1 align="center">🔐 Cybersecurity Lab Environment Setup</h1>

<p align="center">
  <b>Building an isolated virtual lab for penetration testing and ethical hacking practice</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Ver-VirtualBox%20v7.2-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-black?style=flat-square&logo=kalilinux" />
  <img src="https://img.shields.io/badge/Skill-Linux-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-teal?style=flat-square" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-gray?style=flat-square" />
  <img src="https://img.shields.io/badge/GitHub-black?style=flat-square&logo=github" />
  <br>
  <img src="https://img.shields.io/badge/Kali%20Linux-red?style=flat-square&logo=kalilinux" />
  <img src="https://img.shields.io/badge/NetworkWalks-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-orange?style=flat-square" />
  <img src="https://img.shields.io/badge/Priya Kishore%20Gehani%20CCIE-red?style=flat-square" />
</p>

---

## 📌 Project Overview

This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

---

## 🎯 Objectives

The main objectives of this project are to:
- Install and configure VirtualBox.
- Install/import Kali Linux as a virtual machine.
- Create a private NAT Network for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:
- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

> ⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## 🏗️ Lab Architecture

Additional target machines can be added to the same virtual network in future projects.

---

## ⚙️ Lab Configuration

| 🧩 Component | ⚙️ Configuration |
| :--- | :--- |
| **🖥️ Host OS** | Windows 10 |
| **🧠 Host RAM** | 8 GB |
| **⚡ Processor** | Intel Core i7 |
| **🧰 Hypervisor** | VirtualBox 7.2 |
| **🐉 Security OS** | Kali Linux 2026.2 |
| **🧠 Kali RAM** | 2048 MB |
| **🌐 Virtual Network** | NAT Network |
| **📡 Network Address** | 10.0.0.0/24 |
| **🐧 Kali IP Address** | 10.0.0.2/24 |
| **🚪 Default Gateway** | 10.0.0.1 |
| **🌍 DNS Server** | 8.8.8.8 |
| **🔮 Future VM Range** | 10.0.0.3–10.0.0.99 |

---

## 🪜 Lab Setup Procedure

### Step 1. Install 7-Zip
7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a .7z archive.
- **Tool:** 7-Zip

### Step 2. Install VirtualBox
VirtualBox was installed as the hypervisor.

### Step 3. Create the NAT Network
A dedicated NAT Network was created in VirtualBox.
- **Configuration:** 
  - Network Name: `NatNetwork`
  - IPv4 Prefix: `10.0.0.0/24`
  - DHCP: Enabled
  - IPv6: Disabled

A NAT Network was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity. This will allow future attacker and target VMs to communicate within the lab.

### Step 4. Import Kali Linux
The Kali Linux virtual machine was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM network adapter was configured as follows:
- **Adapter 1**
  - Attached to: NAT Network
  - Network: NatNetwork
  - Adapter Type: Intel PRO/1000 MT Desktop

The VM was allocated:
- **RAM:** 2048 MB

A shared folder was also configured for transferring required files between the host operating system and the Kali VM.

### Step 5. Configure the Kali Linux Network
The Kali Linux network configuration was checked and configured with a consistent IPv4 address.

Example configuration:
- **IP Address:** 10.0.0.2
- **Subnet Mask:** 255.255.255.0
- **Gateway:** 10.0.0.1
- **DNS:** 8.8.8.8

A consistent IP address makes it easier to document the lab and reference the Kali machine in future exercises.

### Step 6. Create a Clean VM Snapshot
After completing the initial configuration, a VirtualBox snapshot was created.

Example snapshot name:
`Clean Kali - Network Setup`

The snapshot represents the clean baseline of the laboratory. If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

---

## 🔎 Lab Verification

| ✅ Test | 🧾 Command | 🎯 Expected Result |
| :--- | :--- | :--- |
| **🌐 Check IP address** | `ip a` | Correct Kali IP displayed |
| **📡 Test gateway** | `ping 10.0.0.1` | Successful replies |
| **🌍 Test Internet connectivity** | `ping 8.8.8.8` | Successful replies |
| **🔎 Test DNS resolution** | `nslookup networkwalks.com` | Domain resolves |
| **🧰 Verify Nmap** | `nmap --version` | Nmap version displayed |
| **🔄 Verify snapshot** | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Results

- **IP Address:** `10.0.0.2/24`
- **Gateway:** `10.0.0.1`
- **DNS:** `8.8.8.8`

---

## 🐞 Problems Encountered & Solutions

Documenting problems is an important part of the project.

### Problem 1. Internet Connectivity After Static IP Configuration
After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali/NetworkManager configuration.

One workaround used during this lab was:
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
