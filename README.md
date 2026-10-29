# NETWORKWALKS-POORV-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP

# Cybersecurity Lab Environment Setup - Week 1

## Project Overview
This project documents the setup of a virtual cybersecurity and penetration-testing laboratory using VirtualBox and Kali Linux. The purpose of this isolated lab is to create a controlled environment where network scanning, vulnerability assessment, and security testing can be performed safely.

## Network Architecture & Configuration
The lab utilizes a custom NAT Network in VirtualBox to allow virtual machines to communicate with each other locally while routing outside traffic through the host machine.

* **Hypervisor:** Oracle VM VirtualBox (v7+)
* **Main OS:** Kali Linux (Debian 64-bit)
* **Network Mode:** NAT Network
* **Network Name:** NatNetwork
* **Subnet:** `10.0.0.0/24`
* **Gateway:** `10.0.0.1`

### VirtualBox Settings Configuration
The Kali Linux machine was attached to the custom `NatNetwork` with Promiscuous Mode set to "Allow All". 

[Insert Screenshot (3).png here - showing the VirtualBox Network settings]

### Kali Linux IP Configuration
A static IP was manually configured inside the Kali Linux environment using the network manager:
* **IPv4 Address:** `10.0.0.2`
* **Netmask:** `24`
* **Gateway:** `10.0.0.1`
* **DNS Servers:** `8.8.8.8, 10.0.0.1`

[Insert Screenshot_2026-10-29_08_23_02.png here - showing the terminal ip configuration output]

### Host Integrations
To streamline workflows between the Windows host and the Kali Linux virtual machine, the following features were enabled:
* Bidirectional Shared Clipboard
* Bidirectional Drag'n'Drop
* Auto-mounted Shared Folder mapped to the host's `/downloads` directory.

## Troubleshooting Experience
**Issue:** During the lab setup, after successfully configuring the static IP (`10.0.0.2`) on Kali Linux, the machine lost all internet connectivity.
**Solution:** This is a known issue with VirtualBox v7 and newer versions of Kali Linux (2026.1+). To resolve it, I opened the Kali terminal and applied a workaround to the NetworkManager using `nmcli` to disable the DAD (Duplicate Address Detection) timeout. 

The exact commands used were:
`sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0`
`sudo nmcli connection down "Wired connection 1"`
`sudo nmcli connection up "Wired connection 1"`

After applying these commands and restarting the connection, full internet access was restored.

[Insert Screenshot_2026-10-29_07_59_29.jpg here - showing Kali connected to the internet]

## Next Steps
<img width="1920" height="1080" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/7780daf0-2035-469c-8ec7-17ba189b0077" />
<img width="1920" height="922" alt="Screenshot_2026-10-29_08_23_02" src="https://github.com/user-attachments/assets/1910fd77-7765-48f6-95f0-23be7433a796" />
<img width="1920" height="923" alt="Screenshot_2026-10-29_08_08_00" src="https://github.com/user-attachments/assets/39ef3d8b-ec60-4e2e-aba3-f1a8f8f3c141" />
<img width="1920" height="922" alt="Screenshot_2026-10-29_07_59_29" src="https://github.com/user-attachments/assets/b4859aa7-4387-410a-817f-d946370004dc" />

This completes Phase 1 of the lab setup. In upcoming phases, vulnerable target machines (such as Windows 10 at `10.0.0.10` and Android at `10.0.0.9`) will be added to this isolated `10.0.0.0/24` subnet for ethical hacking practice.
