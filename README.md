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

  ![image](https://github.com/user-attachments/assets/0b938d33-1c31-41a1-8b18-55cfa34d4c26)

2. Create Windows 10 Virtual Machine (VM1)
  - Select the previously created Resource Group and Region
  - Choose Windows 10 for the Operating System

  ![image](https://github.com/user-attachments/assets/6f39604a-0e83-4823-9c1b-91359e51f4d7)

  - Select a size for virtual cpu cores and amount of RAM (I'm selecting 2 cores and 16 GB or RAM)
  - Create a username and password
  - Check box under Licensing and then click Next until you get to Networking

  ![image](https://github.com/user-attachments/assets/5d37f63b-93d4-454b-bb2e-094b675009dc)

  - Let Azure create a virtual network and public IP address for you and click Review and Create

  ![image](https://github.com/user-attachments/assets/f496c973-e33c-416b-b45d-61d5eb5e0c7f)

  - After validation passes click Create

  ![image](https://github.com/user-attachments/assets/89ce06cf-5ca4-4bbb-a988-12171bc21f3e)

3. Create Linux Virtual Machine (VM2)
  - Select the previously created Resource Group and Region
  - Choose Ubuntu Server 24.04

  ![image](https://github.com/user-attachments/assets/29021a84-a10d-4de6-92db-280187973771)

  - Select size for vcpus and memory again
  - Under Administrator Account/Authentication type check Password
  - Create a username and password

  ![image](https://github.com/user-attachments/assets/6d21c12b-bde7-42d3-948c-f1962e2df4ce)

  - Click Next until getting to Networking tab
  - Select the same virtual network that was created for VM1

  ![image](https://github.com/user-attachments/assets/47d205a9-3d00-4c8a-9326-9c715d78792b)

  - Click Review and Create
  - After validation passes click Create

4. Check under Resource Groups to see your resources after creating both Virtual Machines
  - You can now see you have created two of every resource except for just one virtual network that both VMs now share

  ![image](https://github.com/user-attachments/assets/23d1b495-9f45-4576-a62a-f5743cc085cb)


  <h3>Part 2: Observe ICMP Traffic</h3>

  <h3>Part 3: Observe SSH Traffic</h3>

  <h3>Part 4: Observe DHCP Traffic</h3>

  <h3>Part 5: Observe DNS Traffic</h3>

  <h3>Part 6: Observe RDP Traffic</h3>


