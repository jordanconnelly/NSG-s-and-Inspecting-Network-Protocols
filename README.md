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
<h2>Observing ICMP Traffic</h2>

<p>
Open Microsoft Remote Desktop from the Start menu and type in VM1's public IP address. Use the username and password used to create VM1 to log in.
<p>
<img src="https://imgur.com/xHkVimc.png" height="40%" width="80%">
<p></p>
Inside VM1 we will now install Wireshark by searching "download Wireshark" on Google. Proceed through the setup instructions using the standard configurations. Open Wireshark from the Start menu.
<p>
<img src="https://imgur.com/eu8FolK.png" height="20%" width="40%"> <img src="https://imgur.com/drDIZlP.png" height="20%" width="40%">
<p></p>
Click the Run icon at the top left of the page (the shark fin icon) to observe all traffic occurring in VM1. At the top of the page type "icmp" in the search bar to filter the results to only see ICMP traffic. Currently, there is no ICMP traffic in VM1.
<p>
<img src="https://imgur.com/KW78nMM.png" height="20%" width="40%"> <img src="https://imgur.com/TNiPBmm.png" height="20%" width="40%">
<p></p>
Now we will attempt to Ping VM2 from VM1. Obtain VM2's private IP address(10.0.0.5) from Azure. Open PowerShell from the Start menu in VM1 and type in "ping 10.0.0.5". The pings are successful because VM1 and VM2 are in the same Virtual Network. Open Wireshark again and observe the ICMP traffic (ping and reply) between the Virtual Machines.
<p>
<img src="https://imgur.com/lKCOkiV.png" height="20%" width="40%"> <img src="https://imgur.com/hlbA0Yf.png" height="20%" width="40%">
<p></p>
Open Powershell again and attempt to ping Google by typing "ping www.google.com -4", the -4 in the command line forces Powershell to use Google's IPv4. Open Wireshark again to observe the ICMP traffic between VM1 and Google.
<p>
<img src="https://imgur.com/ioaaeAZ.png" height="20%" width="40%"> <img src="https://imgur.com/fNlPJYK.png" height="20%" width="40%">
<p></p>
Next we will initiate a perpetual ping between VM1 and VM2. In PowerShell type in "ping 10.0.0.5 -t", -t signifies a perpetual ping. We can also view this perpetual ping in Wireshark.
<p>
<img src="https://imgur.com/xGJ08HL.png" height="20%" width="40%"> <img src="https://imgur.com/iqlKUom.png" height="20%" width="40%">
<p></p>
In Azure we will open the Network Security Groups and disable inbound ICMP traffic for VM2. Type "Network Security Groups" in the search bar and select "VM2-nsg", select Settings>Inbound Security Rules on the left menu, click on Add Rule. Change the Protocol to ICMP, the Priority to any number smaller than 300 (to give this rule the highest priority), and rename the rule.
<p>
<img src="https://imgur.com/LXgJCyt.png" height="40%" width="80%">
<p></p>
Now all inbound ICMP traffic to VM2 is denied. In PowerShell this is denoted by "Request timed out" and in Wireshark by only seeing requests with no replies.
<p>
<img src="https://imgur.com/rTiCeaI.png" height="20%" width="40%">  <img src="https://imgur.com/owvcyqF.png" height="20%" width="40%">
<p></p>

<h2>Observing SSH Traffic</h2>

<p>
Delete the Inbound rule for ICMP in Azure. In VM1, open Wireshark and filter for SSH traffic only. Open PowerShell and SSH into VM2 using it's private IP address (ssh username@ip address). Answer 'yes" to the question asked and type in the password for VM2. You are now in VM2's SSH. Type in different Ubuntu commands are observe the traffic in WireShark.
<p>
<img src="https://imgur.com/MiV6trP.png" height="40%" width="80%">
