<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>



Create two Virtual Machines:

1. DC-1 (Windows Server 2022)

2. Client-1 (Windows 10 Pro)

(Note-Both of the Virtual Machines should be in the same resourse group)



<p>

![AD part 1](https://i.imgur.com/BHn4nAd.gif)

</p>
<p>

</p>
<br />



<p>

![AD part 2](https://i.imgur.com/Uefi9Nf.gif)

</p>
<p>



Set the DC-1 Private IP address to static

Go to Virtual Machines --> DC-1 | Networking --> Network Interface | IP Configurations





</p>
<br />

<p>

![AD part 3](https://i.imgur.com/DK5eW9d.gif)

</p>
<p>

  
  
  

Login to Client-1 with remote desktop (Copy the public IP Address from the azure portal and paste it on the remote desktop connection)

Once you are logged in the Client-1 Virtual Machine, open the Command line and enter the following command

"ping -t 10.3.0.4 (DC-1 private IP Address)"

The ping request will be timed out 

In order to succeed the ping we will need to open DC-1 VM and enable some inbound rules

Login to DC-1 with remote desktop using its public IP address
  

  
Go to wf.msc -> Inbound rules -> Enable the following inbound rules

1. Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In) - Private (Profile)

2. Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In) - Domain (Profile)

Once you enable the inbound rules go back to Client-1 Virtual Machine and check the ping request

The ping request is now succeed
  
Stop the ping using ctrl+c
</p>
<br />

<p>

![AD part 4](https://i.imgur.com/C7oDVXM.gif)

<IMG SRC="https://i.imgur.com/C7oDVXM.gif">
</p>




  
  
  
