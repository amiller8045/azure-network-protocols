<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we will observe various network traffic to and from Azure Virtual Machines with Wireshark and experiment with Network Security Groups. <br />




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

1) Create Windows 10 VM
2) Create Linux VM
3) Observe ICMP Traffic
4) Configure a Firewall (Network Security Group)
5) Observe SSH Traffic
6) Observe DHCP Traffic
7) Observe DNS Traffic
8) Observe RDP Traffic
   

<h2>Actions and Observations</h2>


1) Create Windows 10 VM

   **Sign in to Azure and create a Resource Group.**


   
![Create](https://github.com/user-attachments/assets/aef9f6f7-b496-458c-927f-6b6f1925b0cc)


  **Create a Windows 10 Virtual Machine.**

![RG](https://github.com/user-attachments/assets/fe02cd99-d76d-4f81-8411-9859c59a8531)

   
<p>

   **Name: windows-vm / Image: Windows 10 Pro / Region: Same as Resource Group**

![windows spec 1](https://github.com/user-attachments/assets/62b79e26-d3aa-4a98-9a15-1c07a4c5d2a8)

<p>

   
   **Size: 2 vcpus with 8 gb of memory / Create a username and password / Check Licensing field / Click Next twice.**

   
![Windows spec 2](https://github.com/user-attachments/assets/48282fec-aeb3-47f2-a6aa-8796b3078ce6)


   <p>

  **"Create new"  Virtual Network, if it doesn't automatically. Click OK and Review then Review and Create.**

![create new](https://github.com/user-attachments/assets/86d7e77d-29db-4272-bbdf-560c59120e92)

  <p>

  
  **The next screen should say "validation passed". Notice hourly subscription cost. Then click Create.**


![validation](https://github.com/user-attachments/assets/a4b691fa-d3c1-49f7-bd24-f6a736cdde46)

<p>

<p>

2) Create Liux VM

  **Must have the same Resource Group and Region / Name: linux-vm / Image: Ubunutu Server 22 or 24**
<p>


![linux 1](https://github.com/user-attachments/assets/4317cf89-aa9d-4896-88bb-0d3b735d4d59)

   <p>

  **Same size and username/password as windows-vm, Click Next twice.**

![linux 2](https://github.com/user-attachments/assets/3071a14e-d501-472b-a64e-49050d9d083d)

<p>

  **Same Virtual Network as windows-vm. Review + Create**

  

  **Once it passes validation, click Create.**

  
![create linux](https://github.com/user-attachments/assets/f45d7321-e7f7-4022-a9c6-f0b495bac45e)




  


  

  
  


  
  

  
   
   

   
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
