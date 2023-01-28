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

![ezgif com-gif-maker (5)](https://user-images.githubusercontent.com/121186222/215218260-9825b9a7-f1aa-488c-9560-b74c794b4d0c.gif)

  
![ezgif com-gif-maker (6)](https://user-images.githubusercontent.com/121186222/215218444-ce25fe29-2d7f-4888-8a87-4088fd0f01d8.gif)

  

<h3>Installing Active Directory</h3>

Go back to DC-1 and open Server Manager

In Server Manager click on "Add roles and features"

Add a new forest and name the domain as mydomain.com

Proceed to install Active Directory

After the installation of Active Directory, the DC-1 VM will be logged off and you will need to restart the VM







Log back in to the DC-1 with the context of the domain 

Enter the username as mydomain.com\labuser and use the password as before you used to login to DC-1 VM

Once logged in, go to Server Manager --> Tools --> Active Directory Users and Computers --> mydomain.com 

In the Active Directory Users and Computers create two Organizational Units

1. _EMPLOYEES
2. _ADMINS

In the _ADMINS section create a new user named as "Jessica Doe" and create new credentials for the user

-Username- Jessica_admin

-Password- ********

Make Jessica Doe an administrator by going to properties and making her a member of Domain Admin group

We can now login to DC-1 Virtual Machine in the context of Jessica Doe








Make Client-1 a member of mydomain.com, to do so we will need to set the Client-1 DNS settings to DC-1 private IP Address

Set the Client-1 DNS settings to DC-1 private IP address

In Azure Portal go to DC-1 --> Networking --> Copy the NIC Private IP Address

Next go to Client-1 --> Networking --> Network Interface --> DNS Servers --> Click on Custom --> Paste the NIC Private IP address --> Save the changes

Restart the Client-1 Virtual Machine in Azure Portal 






Login to Client-1 Virtual Machine and then go to start --> system --> Rename this Pc (Advnaced)

Click on change and make Client-1 a member of mydomain.com



















  
  
  
