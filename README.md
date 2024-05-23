# NSG-s-and-Inspecting-Network-Protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)
- Windows Powershell

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create VMs and Install Wireshark
- Observe ICMP Traffic 
- Observe SSH Traffic  
- Observe RDP Traffic

<h2>Setting Up Resources</h2>

<p>
To start we will create a Resource Group in Microsoft Azure (RG1). Once created we will start building our first Virtual Machine (VM1). Place VM1 in RG1 and take note of the Region it is created in, we will need our second Virtual Machine (VM2) in the same Region. VM1 will be running Windows 10. Proceed to the "Networking" tab and allow VM1 to create a new Virtual Network and Subnet, I renamed the Virtual Network to "RG1-vnet". Click on "Review + create" to complete the VM1 setup.
<p>
<img src="https://imgur.com/3e1sKAg.png" height="20%" width="40%"> <img src="https://imgur.com/U3JrHy9.png" height="20%" width="40%">
<p></p>
Next, we will follow the same steps to create VM2 in the same Resource Group (RG1). This Virtual Machine will be running Ubuntu. Once on the "Networking" tab, place VM2 in the same Vnet (RG1-Vnet) and subnet as VM1.
<p>
<img src="https://imgur.com/OSiGDY3.png" height="20%" width="40%"> <img src="https://imgur.com/ZlMXuTg.png" height="20%" width="40%">
<img src=".png">
</p>
<p>
