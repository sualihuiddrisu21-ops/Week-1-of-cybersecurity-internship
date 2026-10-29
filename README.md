<div align="center">

# 🔐🛡️ Cybersecurity Lab: Kali Linux & Isolated NAT Network Setup

*Building an isolated virtual lab for penetration testing and ethical hacking practice*
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Waqas%20Karim%20CCIE-C00000?style=flat-square" />
</p>

![Kali Linux Desktop](./Screenshot%202026-Kali%20UF.png)
A clean, reproducible, and isolated penetration testing lab built on Oracle VM VirtualBox and Kali Linux. Designed to practice cybersecurity tools safely without exposing the host machine or home network.

📌 Project Overview & Objectives

Core Goal: Set up an isolated offensive security lab using VirtualBox.

Architecture: Attacker workstation (Kali Linux) contained within a private virtual subnet.

Reliability: Baseline clean snapshot created for instant recovery.

Safety: Safe practice area for scans and exploits away from production LANs.

🏗️ Lab Architecture

Network Name: NatNetwork

Subnet: 10.0.0.0/24

Default Gateway: 10.0.0.1

Attacker VM IP: 10.0.0.2 (Static)

[ Host Machine (Windows) ]
        │
  [ VirtualBox NAT Network: 10.0.0.0/24 ]
        │
  [ Kali Linux (10.0.0.2) ] ──> (Future Target VMs)


⚡ Quick Setup Procedure

Step 1. Install 7-Zip

Installed 7-Zip to extract Kali .7z virtual disk archives.

Step 2. Install VirtualBox

Deployed Oracle VM VirtualBox along with the Extension Pack to enable enhanced virtualization drivers.

Step 3. Create the NAT Network
![VirtualBox NAT Network](./Screenshot%202026-10-28%20%20Natwork.png)
Created NatNetwork with IPv4 Prefix 10.0.0.0/24 and enabled DHCP for automatic lease management.

Step 4. Import Kali Linux

Imported the official pre-built Kali Linux VirtualBox image and configured system memory and vCPU allocations.

Step 5. Configure Network & Static IP
![Static IP Settings](./Screenshot%202026-ip%20settings.png)
Attached Kali's virtual network adapter to NAT Network (NatNetwork). Within Kali, configured a static IPv4 connection (10.0.0.2/24, Gateway: 10.0.0.1, DNS: 10.0.0.1).

Step 6. Create a Clean VM Snapshot
![Clean Snapshot](./Screenshot%202026-snapshot.png)
Created a baseline snapshot named My new kali linux with the description: "i have set up my ip adress and the internet works perfectly." This guarantees instant recovery if future tests or scripts corrupt the OS.

🛠️ Real Problem Encountered & Solution

The Issue: Disappearing Internet Connection After Reboot

Everything worked during initial setup. However, after exiting VirtualBox and reopening it later, internet access failed completely inside Kali (browsers could not resolve web pages). Following troubleshooting guides (including Mr. Waqas Karim's walkthrough) did not immediately resolve it.

How I Solved It (Adapter State Toggle):

Switched the Kali VM network adapter from NAT Network to Internal Network and booted up to verify interface connectivity.

Gracefully shut down, then switched the adapter back to NAT Network.

Rebooted Kali—this forced VirtualBox to rebind the virtual network adapter, instantly restoring full internet connectivity.
![Internet Connection Verified](./Screenshot%202026-network%20testing.png)
💡 Key Takeaways

NAT vs. NAT Network: Standard NAT isolates each machine by itself. NAT Network acts like a virtual switch so attacker and target VMs can communicate with one another.

Virtual Machine Networking: Different modes (Internal, Host-Only, Bridged, NAT Network) serve distinct isolation and routing needs.

Static IP Configuration: Critical targets and attacker boxes need predictable IPs so security scripts and listeners don't break when leases expire.

VM Snapshots: An essential safety net. Reverting to My new kali linux takes seconds, preventing full OS reinstalls.

Documentation: Capturing real troubleshooting steps and network configs saves hours of debugging down the road.

⚖️ Security & Ethical Use

All scanning, sniffing, and payload testing are strictly confined to this isolated local lab (10.0.0.0/24). Never run offensive tools against unauthorized devices or public networks.

👤 Author & Info

Author: Iddrisu Sualihu

Role: Cybersecurity & Systems Practitioner

Environment: VirtualBox 7.x | Kali Linux | 10.0.0.0/24 NAT Network

Snapshot Baseline: My new kali linux

Status: Complete & Verified ✅
