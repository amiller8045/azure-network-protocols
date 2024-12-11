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

1) Create a Windows 10 VM
2) Create a Linux VM
3) Observe ICMP Traffic
4) Configure a Firewall (Network Security Group)
5) Observe SSH Traffic
6) Observe DHCP Traffic
7) Observe DNS Traffic
8) Observe RDP Traffic
   

<h2>Actions and Observations</h2>


**1) Create Windows 10 VM**

   - Sign in to Azure and create a Resource Group.**


   
![Create](https://github.com/user-attachments/assets/aef9f6f7-b496-458c-927f-6b6f1925b0cc)


- Create a Windows 10 Virtual Machine.**

![RG](https://github.com/user-attachments/assets/fe02cd99-d76d-4f81-8411-9859c59a8531)

   
<p>

   - Name: windows-vm / Image: Windows 10 Pro / Region: Same as Resource Group**

![windows spec 1](https://github.com/user-attachments/assets/62b79e26-d3aa-4a98-9a15-1c07a4c5d2a8)

<p>

   
   - Size: 2 VCPUs with 8 GB of memory / Create a username and password / Check Licensing field / Click Next twice.**

   
![Windows spec 2](https://github.com/user-attachments/assets/48282fec-aeb3-47f2-a6aa-8796b3078ce6)


   <p>

  - "Create New"  Virtual Network, if it doesn't automatically. Click OK and Review then Review and Create.**

![create new](https://github.com/user-attachments/assets/86d7e77d-29db-4272-bbdf-560c59120e92)

  <p>

  
  - The next screen should say "validation passed". Notice hourly subscription cost. Then click Create.**


![validation](https://github.com/user-attachments/assets/a4b691fa-d3c1-49f7-bd24-f6a736cdde46)

<p>

<p>

**2) Create Linux VM**

  - Must have the same Resource Group and Region / Name: linux-vm / Image: Ubuntu Server 22 or 24**
<p>


![linux 1](https://github.com/user-attachments/assets/4317cf89-aa9d-4896-88bb-0d3b735d4d59)

   <p>

  - Same size and username/password as windows-vm, Click Next twice.**

![linux 2](https://github.com/user-attachments/assets/3071a14e-d501-472b-a64e-49050d9d083d)

<p>

  - Same Virtual Network as windows-vm. Review + Create**

  

  **Once it passes validation, click Create.**

  
![create linux](https://github.com/user-attachments/assets/f45d7321-e7f7-4022-a9c6-f0b495bac45e)




  
**3) Observe ICMP Traffic**

Internet Control Message Protocol (ICMP) traffic is a network-level protocol that sends error messages and operational information between devices on the Internet,

   - Attain the windows-vm public IP address from Azure.**


![windows ip](https://github.com/user-attachments/assets/6d9b989c-d016-488f-a629-6c78de6f3d2f)


   - Use Remote Desktop Connection to connect to the virtual machine.**


   ![rdp](https://github.com/user-attachments/assets/de72703b-0c90-494c-89c5-e9e75eb6eb0e)



   - Within your Windows 10 Virtual Machine, Install Wireshark
   
This will allow us to view all the network traffic that is occurring.
   https://www.wireshark.org
   

  ![open wireshark](https://github.com/user-attachments/assets/22abebf8-1be8-435b-849a-154883e13c52)




  - Choose Windows 64 Installer**        - Run and Finish Wireshark install**


![64 windows](https://github.com/user-attachments/assets/f7f49c0f-1c8b-4241-ae17-76ff250261e4)







- Open Wireshark and start packet capture**

A packet is a small unit of data transmitted over a network.

Packet capture is a networking technique that intercepts and records data packets traveling across a network.


![image](https://github.com/user-attachments/assets/f863744f-244a-46de-9e30-71fb684ec237)




- You will see a flow of traffic in Wireshark.


![capture](https://github.com/user-attachments/assets/9fc4b300-6b78-4e17-9980-3c7f432d56cb)





- Within Wireshark, filter for ICMP traffic only**

ICMP is a network-level protocol that sends error messages b/t devices on the internet, using command line "ping".



![icmp no traffic](https://github.com/user-attachments/assets/b22d9367-9af1-4d3c-af66-a3aab96346dc)






- Retrieve the private IP address of the linux-vm.** 

![linux private ip](https://github.com/user-attachments/assets/9226d4e5-87ed-414f-b198-3c29ff0b4460)



- Attempt to ping the linux-vm from within the Windows 10 VM in Powershell**

Ping allows us to know if two different devices on a network can communicate with each other.

- Open Powershell

![powershell](https://github.com/user-attachments/assets/706f6ca2-c0df-4d1e-8a54-a6b20f90fea2)


- ping 10.0.0.5

- Type "ping 10.0.0.5" and press Enter.

Hopefully, there will be a 0% loss

![ping 10 0 0 5](https://github.com/user-attachments/assets/3b6a5e6f-fb30-4bfe-9bb9-dd7c47d068b3)


   



- Observe ping requests and replies within WireShark**

You will see a "request" from the windows-vm private ip address and a reply from the linux-vm private ip address.


![ping convo](https://github.com/user-attachments/assets/d5017dcf-eb2b-4d35-a91c-85d9b4f017b4)


- Let's start a non-stop ping to the linux-vm using "ping 10.0.0.5 -t" and press Enter.**

-t means ping forever

You will notice the non-stop ping on Wireshark in the background.

![image](https://github.com/user-attachments/assets/cd7fb729-ae43-4c48-b454-4cbe04464150)



**4) Configure linux-vm Firewall (Network Security Group)**

A firewall is a network security system that monitors and controls incoming and outgoing network traffic.

- Disable incoming ICMP Traffic

**Networking -> Network Settings -> Network Security Group: linux-vm-nsg -> Settings -> Inbound Security Rules -> Add** 

![linux secur](https://github.com/user-attachments/assets/f98b32e2-b6c8-48a2-801e-089c20845b68)

![add rule](https://github.com/user-attachments/assets/a40cd3ac-0b00-460b-9c8b-6dae202d29be)



- Source and Destination should be Any. Destination means linux-vm, and source means any other device.

- Port will just be the star symbol (*) because IMCP doesn't use a port.

- The Protocol will be ICMPv4 since it doesn't use UDP or TCP.

- The Action is to "Deny" pings from coming in.

- Set the priority at a lower number than other rules so this will take precedence. Then Save.

![add rule](https://github.com/user-attachments/assets/104d55a6-0bea-4d97-825e-5a9ab7215c26)


![5 rule](https://github.com/user-attachments/assets/ff63a9d0-81fb-4f82-b4d1-f5238675eca9)


![1 rule](https://github.com/user-attachments/assets/bfb20be2-67c3-469c-a5a8-ac2f2324610e)


- New Rule**

![image](https://github.com/user-attachments/assets/419577d2-c2bf-4370-8e90-4dbd1f641433)



- Back in Powershell press enter and look for "Request Timed Out".**

- Back in Wireshark now you will only see requests from the windows-vm.**

Since we stopped all incoming ICMP traffic for the linux-vm, our windows-vm can't ping it.


![ping stop](https://github.com/user-attachments/assets/37b12538-2268-49a9-ab50-99c66ffc3cb5)


- Re-enable ICMP Traffic for linux-vm.**

- Simply delete the new rule we create for ICMP**

![image](https://github.com/user-attachments/assets/ee7b6882-8769-4eea-9cc9-0dccd34c72b3)

- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)**

Once the Azure resource manager recognizes the rule has been deleted, the traffic will resume.

![ping return](https://github.com/user-attachments/assets/396892e1-007d-4b59-b380-6acec49831a2)


- Stop Ping**

**Control + C**

Powershell will return to an empty command line.

![Control C](https://github.com/user-attachments/assets/7465cfce-75a6-4f0d-bcba-db08a57f3575)



**5) Observe SSH Traffic)**

SSH, or Secure Shell, is a network protocol that allows two computers to communicate securely over an unsecured network.**

- Log back into the windows-vm

- Back in Wireshark, start a packet capture up

- Filter for SSH traffic only, As you can see there is nothing since we have not initiated as SSH command.




![ssh](https://github.com/user-attachments/assets/f039d14d-26f9-401e-ab48-a20dd6b34224)




- From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)

- Open PowerShell, and type: ssh labuser@<private IP address> and press Enter.

![labuser@10 0 0 5](https://github.com/user-attachments/assets/4399a72c-152b-4f7c-9d01-ccde2d08527f)

- Type "yes" to continue connecting and press Enter.

  ![yes](https://github.com/user-attachments/assets/3da50e8b-114c-4f8c-95b4-9d4536efdabc)




- Type the linux-vm password and press Enter. The password will not appear, so type carefully.



  ![password](https://github.com/user-attachments/assets/53374c51-a581-440c-9949-c9fd19fc3899)


- Observe SSH traffic spam in WireShark

![image](https://github.com/user-attachments/assets/09253818-f321-4f19-8006-4d5034498224)


- Notice the prompt has changed to the linux-vm. We are now connected to that virtual machine via SSH.


Now you can Enter commands for that computer such as:

"hostname": name of that virtual machine

"uname -a": info about the operating system


![linux labuser](https://github.com/user-attachments/assets/b96fb214-c2d2-4051-b177-cbb8d68878d9)



![hostname](https://github.com/user-attachments/assets/544e76e0-9f4d-46ef-95cd-f7c228066441)


- Remember, SSH is encrypted. Any keystroke made in Powershell will generate traffic in Wireshark b/t the two virtual machines but is not discernible by others.

  ![encrypted](https://github.com/user-attachments/assets/c96c41bf-9e3e-4f85-8729-3802aadc100e)


- Another way to filter SSH traffic is typing "tcp.port==22". That's because SSH using TCP Port 22. 

![tcp](https://github.com/user-attachments/assets/95c7be7c-175b-4c6e-af21-4ab8231a3dc0)


 
-  Now Exit the SSH connection by typing ‘exit’ and pressing Enter.

-  You will see the connection is closed.



![exit](https://github.com/user-attachments/assets/84db98b6-3d5e-493d-948a-29c8d5732d08)


-  Type "hostname" to see that you are now back in the windows-vm

![windows-vm](https://github.com/user-attachments/assets/58f26dfc-1f2b-414d-afd2-2654375daa5b)



**6) Observe DHCP Traffic**

Dynamic Host Configuration Protocol (DHCP) is a network management protocol that automatically assigns IP addresses and other communication parameters to devices on a network using UDP ports 67 and 68.

UDP port 67 is used by DHCP servers to listen for messages from DHCP clients

UDP port 68 is used by DHCP clients to send messages to DHCP servers.


- In Wireshark, filter for DHCP traffic only. Type "DHCP"

- Open Powershell as admin and run "ipconfig /renew"

![powershell admin](https://github.com/user-attachments/assets/47617c4e-da30-42d9-9e8e-cd458566df00)


- Observe the DHCP traffic in Wireshark and take note of new ip address. In our case it will be the same as it was before but in Wireshark you will see a request from our windows-vm and an acknowledgement from the DHCP server.

  
![image](https://github.com/user-attachments/assets/c715dbdf-d787-46b4-b4be-db5ee7e7378d)

  

**7) Observe DNS Traffic**

DNS, or the Domain Name System, translates human-readable domain names  to machine-readable IP addresses.

- Restart capture

  ![restart](https://github.com/user-attachments/assets/4ed8c5be-a974-4259-a84b-40dc5ddbf386)


- Filter for DNS traffic

- In Powershell, issue the command "nslookup disney.com".


  Notice the ip address it gives you.

  Take note of the DNS traffic in Wireshark



![nslookup](https://github.com/user-attachments/assets/d2f34463-960b-4ad2-a084-67bbb9f15a8f)



- Type the ip address in a web browser and see where it leads you.

Looks like it is associated with Disney

![disney](https://github.com/user-attachments/assets/7d915a49-2f2f-4dc0-bff7-3b615b211a98)




<br />
