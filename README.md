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

1. Use Remote Desktop to connect to Windows 10 VM and use credentials to login

![image](https://github.com/user-attachments/assets/77778be9-bf05-4aef-a4c3-5ee9de982682)


![image](https://github.com/user-attachments/assets/8fdf63f0-3ec2-48f3-a04c-f2715a5f0cdd)


2. Within Windows 10 VM, Install Wireshark
  - Go to www.google.com and type in wireshark download to go to their website
  - Click the version that matches your OS and download Wireshark

   ![image](https://github.com/user-attachments/assets/7db27453-3ee3-4f83-88f3-9aa2cd5ccd3e)
     
  - Open file explorer and navigate to downloads to install Wireshark
  
   ![image](https://github.com/user-attachments/assets/4941be4b-a9f4-4bc6-8752-d8dac62f7f73)

3. Open Wireshark and filter for ICMP traffic only

![image](https://github.com/user-attachments/assets/45a635ad-f41a-4b03-8fed-b0a06cfc90c9)

4. Retrieve the private IP address of Ubuntu VM and attempt to ping from Windows VM from command line

  ![image](https://github.com/user-attachments/assets/66478f8b-9f3a-4990-885b-059db7912c84)

  - Observe the ping requests and replies within Wireshark

  ![image](https://github.com/user-attachments/assets/56522d6f-6ae5-4097-888c-325e6253566c)

<h3>Part 3: Configuring a Firewall (Network Security Group)</h3>

1. Initiate a perpetual ping from Windows 10 VM to Ubuntu VM
  - Type 'ping 10.0.0.5 -t' (whatever your private IP address is for Ubuntu VM) in command line

  ![image](https://github.com/user-attachments/assets/dcec0b73-1dd3-4cd4-b453-23dd7220502a)

2. Open Network Security Groups on Ubuntu VM and disable incoming ICMP traffic by adding an Inbound Security Rule

   ![image](https://github.com/user-attachments/assets/3c5581e1-8c47-4894-a399-c83ef7568f70)

  - Back in Windows VM, observe the ICMP in Wireshark and the command line Ping activity
    
    ![image](https://github.com/user-attachments/assets/1ecf6b4d-0ae5-4844-86c5-ee525e6e62ab)

  - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using by deleting the security rule

    ![image](https://github.com/user-attachments/assets/cdea96a9-1eae-47b1-b9e5-622f01156214)

  - Back in Windows VM, observe the ICMP traffic in Wireshark and the command line Ping activity (should start working)

    ![image](https://github.com/user-attachments/assets/9dd7d4d0-0943-4b3f-86fc-ae27658c7d84)

  - Stop the ping activity with CTRL C in the command line

<h3>Part 4: Observe SSH Traffic</h3>

1. Back in Wireshark, filter for SSH traffic
2. From Windows 10 VM, "SSH into" your Ubuntu VM through either its private IP address or hostname(in my case VM2)

  ![image](https://github.com/user-attachments/assets/b79810ee-b006-4824-97b8-9c5addd99398)

  - Enter password that was created back in Azure
  - Observe SSH traffic back in Wireshard

  ![image](https://github.com/user-attachments/assets/52ce27bb-61e1-4681-a31f-447ce52c8b91)

  - Exit SSH by typing "exit" and pressing Enter

<h3>Part 5: Observe DHCP Traffic</h3>

1. Back in Wireshark, filter for DHCP traffic only
2. From Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)

   ![image](https://github.com/user-attachments/assets/bb505c80-c7e4-4924-a2ae-eacb8ba74fc0)

   - Observe the DCHP traffic appearing in Wireshark
  
   ![image](https://github.com/user-attachments/assets/37e4ceda-5fb2-41e9-94c4-6409a97ef887)

<h3>Part 6: Observe DNS Traffic</h3>

1. Back in Wireshark, filter for DNS traffic only
2. From Windows 10 VM within the command line, use nslookup to see whtat google.com and disney.com IP addresses are

   ![image](https://github.com/user-attachments/assets/7cd98ad2-c214-455d-b1c6-4d73c157eab6)

  ![image](https://github.com/user-attachments/assets/47db1f84-cf44-4196-8e7a-b499c073c435)

<h3>Part 7: Observe RDP Traffic</h3>

1.Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)

  ![image](https://github.com/user-attachments/assets/9f5f0f97-7f11-4f72-9593-9e0bef5bdb60)

  - Here we can see that there is non-stop spam of traffic because the RDP protocol is constantly showing you a live stream from one computer to another because traffic is always being         
transmitted


