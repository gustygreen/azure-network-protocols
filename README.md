<p align="center">
<img src="https://github.com/user-attachments/assets/dfdce942-53ba-4e94-bdc7-d2a3d95e6147" height="30%" width="30%"/>
</p>

<h1>Create Network Security Groups</h1>
In this tutorial, we explore the functionality of Network Security Groups and their effect on traffic between VMs.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows and Linux Command Line Tools
- Various Network Protocols (ICMP, SSH, DNS, DHCP, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro (22H2)
- Ubuntu Server 22.04

<h2>Actions and Observations</h2>
<p>
  
<p>
<img src="https://github.com/user-attachments/assets/1feffac1-bcc7-40e8-bd70-7fe4d38baaae" height="80%" width="80%"/>

</p>
<p>
Create two VMs in the Azure portal: one using a Windows 10 Pro image and the other using a Linux image, each with 2 vCPUs. Ensure both VMs are attached to the same virtual network during setup. Use RDP to access the Windows machine. 
We are using the same setup that was used for the [Observe ICMP Traffice and other Network Protocols using WireShark](https://github.com/gustygreen/ICMP).
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/b085d662-8495-4a6d-a4bc-70a5f8c10fc0" height="80%" width="80%"/>
</p>
<p>
With Wireshark open, on the Windows VM, use the ping -t command to continuously ping the Linux machine. Then, go to the Linux VM in Azure, navigate to Network Settings, and create an inbound port rule to deny ICMP traffic, effectively blocking it on the firewall.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/8498d156-65ab-4989-9aee-cfe53d5d6583" height="80%" width="80%"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/4afe93e8-3699-4875-922a-101cec258fd2" height="80%" width="80%"/>
</p>

<p>
Go to the Linux VM in Azure, navigate to Network Settings, and create an inbound port rule to deny ICMP traffic, effectively blocking it on the firewall.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/f737f7c8-502f-4538-959b-297da6a1f792" height="80%" width="80%"/>
</p>
<p>
After blocking ICMP traffic on the Linux machine’s firewall, check Wireshark on the Windows VM to see that the pings no longer receive replies. In PowerShell, you’ll see a message saying "Request Timed Out."
Wireshark will show (no response found!).
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/343dcb23-d9da-4496-a3cb-5c240e8d8458" height="80%" width="80%"/>
</p>
<p>
<img src="https://github.com/user-attachments/assets/5057b846-bfe8-456f-aba1-5f72005a4749" height="80%" width="80%"/>

<p>
Afterward, delete the inbound port rule to allow ICMP traffic again. To stop the continuous pinging, press Ctrl + C in PowerShell. 
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/50b2cc9d-2605-489a-b490-01c72edc63ac" height="80%" width="80%"/>
</p>
<p>
Next, we will filter SSH traffic using Wireshark. By now, you should have a basic understanding of how to navigate Wireshark. To proceed, open the command prompt on your Windows machine and establish an SSH connection to the Linux machine using the command: ssh labuser2@10.0.0.5. Once this command is executed, Wireshark will display the SSH traffic, allowing you to observe and analyze it in real time.You can type "exit" to end the linux SSH connection when you're done.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/09ffe3a3-223f-4e38-bfa1-d29ccb9e2485" height="80%" width="80%"/>
</p>
<p>
Next, we'll filter DNS traffic in Wireshark. Start by setting Wireshark to display only DNS traffic. To generate DNS activity, use the command nslookup www.google.com, which queries the DNS server for Google's IP address.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/ff25c848-3246-4976-8be9-f3d7bb927b7b" height="80%" width="80%"/>
</p>
<p>
Now, we'll use Wireshark to filter DHCP traffic. DHCP, or Dynamic Host Configuration Protocol, assigns IP addresses to devices. To generate DHCP traffic, enter the command ipconfig /renew in PowerShell, which requests a new IP address. Wireshark will capture this DHCP activity for analysis.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/23058fee-cc26-47bc-b880-dd144b023bb3" height="80%" width="80%"/>
</p>
<p>
Lastly, we'll filter for RDP traffic in Wireshark. Since we're using Remote Desktop Protocol to connect to our virtual machine, RDP traffic will appear continuously, providing ample data for analysis.
</p>
<br />
