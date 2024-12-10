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


**1) Create Windows 10 VM**

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

**2) Create Liux VM**

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




  
**3) Observe ICMP Traffic**


   **Attain the windows-vm public IP address from Azure.**


![windows ip](https://github.com/user-attachments/assets/6d9b989c-d016-488f-a629-6c78de6f3d2f)


   **Use Remote Desktop Connection to connect to virtual machine.**


   ![rdp](https://github.com/user-attachments/assets/de72703b-0c90-494c-89c5-e9e75eb6eb0e)



   **Within your Windows 10 Virtual Machine, Install Wireshark
   
This will allow us to view all the network traffic that is occurring.
   https://www.wireshark.org
   

  ![open wireshark](https://github.com/user-attachments/assets/22abebf8-1be8-435b-849a-154883e13c52)

![wireshark](https://github.com/user-attachments/assets/a51ae46a-797b-439d-ba79-dc34bdfde539)



  **Choose Windows 64 Installer**        **Run and Finish Wireshark install**


![64 windows](https://github.com/user-attachments/assets/9639f355-56ee-4bc1-8734-61c83d4db5ee)







**Open Wireshark and start packet capture**

A packet is a small unit of data transmitted over a network.

A packet capture is a networking technique that involves intercepting and recording data packets that are traveling across a network.


![image](https://github.com/user-attachments/assets/f863744f-244a-46de-9e30-71fb684ec237)




You will see a flow of traffic in wireshark


![capture](https://github.com/user-attachments/assets/9fc4b300-6b78-4e17-9980-3c7f432d56cb)





**Within Wireshark, filter for ICMP traffic only**

ICMP is a network-level protocol that sends error messages b/t devices on the internet, using command line "ping".



![icmp no traffic](https://github.com/user-attachments/assets/b22d9367-9af1-4d3c-af66-a3aab96346dc)






**Retrieve the private IP address of the linux-vm.** 

![linux private ip](https://github.com/user-attachments/assets/9226d4e5-87ed-414f-b198-3c29ff0b4460)



**Attempt to ping the linux-vm from within the Windows 10 VM in Powershell**

Ping allows us to know if two different devices on a network can communicate with each other.





**Observe ping requests and replies within WireShark**

You will see a "request" from the windows-vm private ip address and a reply from the linux-vm private ip address.

ping 10.0.0.5






**From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.youtube.com)**

ping youtube.com




**observe the traffic in WireShark**





























  


  
  


  
  

  
   
   

   
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
