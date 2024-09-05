<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Resources (Create Resource Group w/ Windows 10 and Ubuntu Virtual Machines) with Microsoft Azure
- Connect to Windows 10 VM and Download/Install Wireshark
- Observe ICMP Traffic with Wireshark
- Connect to Ubuntu VM on Windows VM Through SSH
- Observe SSH Traffic with Wireshark
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h3>Part 1: Create Resource Group and Resources</h3>

1. Create Resource Group


2. Create Windows 10 Virtual Machine


