<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Microsoft Azure Cloud </h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Setting up resources in Microsoft Azure
- Step 2: Ensure connectivity between a Client and a Domain Controller.
- Step 3: Install Active Directory
- Step 4: Create Users in Active Directory
- Step 5: Join the client machine to the Domain.
- Step 6: Setup Remote Desktop for users on the Client Machine.
- Step 7: Create users in the Domain Controller and Use them to log into the domain from the client machine.

 

<p>
<h2>Deployment and Configuration Steps</h2>

<h2>Step 1: Setting up resources in Microsoft Azure.</h2>
For this exercise,I begin by setting up the following resources in Microsoft Azure:

1. A domain controller running Windows (Windows Server 2022 Datacenter Azure Edition) in a virtual machine.

2. A client computer ( Named Client - 1) running Windows (Windows 10 Pro) in a virtual machine and will also be using the Domain Controller (DC-1) as its DNS server.


</p>
<p>
  
I then go to the Domain Controller’s IP configurations in order to change its private IP address settings from Dynamic to Static, ensuring that other devices and services relying on the Domain Controller server can always find it at the same address, which is crucial for maintaining consistent connectivity.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/1075a22e-6a1b-48cc-b0da-601e872dbceb)


</p>

<h2>Step 2: Ensure connectivity between the Client and the Domain Controller.</h2>
<p>
  
I then check for connectivity between the client and Domain Controller by sending a perpetual  ping to the domain controller’s private IP address. Then I login to the Domain controller and allow ICMPv4 traffic on its firewall to allow the ping to succeed and confirm connectivity.
I log into the client computer and send a perpetual ping to the Domain Controller. As expected, the ping timed out from the firewall blocking ICMPv4 traffic.


</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/fde0fd06-79c4-41be-bf75-1913e04c7f75)


</p>
<p>
  
 I then access the Domain Controller’s firewall and allow ICMP echo request traffic.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/36433346-c01e-4f35-abf4-16b5c3b9c1d8)


</p>
<p>
  
Now the ping is receiving requests as ICMPv4 traffic is flowing and shows connectivity between the client and the domain controller

</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/0b825a5f-601f-4549-baeb-565bd25c306f)


</p>

<h2> Step 3: Install Active Directory.</h2>

<p>
  
Next, install Active Directory in the Domain Controller ( DC-1).

</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/6a1efec5-dce4-4269-9c84-3de09ba02021)


</p>

<h2>Step 4: Create Users in Active Directory.</h2>

<p>
  
Next, I create two organizational units called Admins and Employees.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/f8ef0d1b-3d63-44c5-a023-ceda5b444468)


</p>
<p>
  
Next, I create an Admin employee called Charity Helen and also add her to the Domain Admins member group.
</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/25b4d64f-8275-4897-a4fb-4494a4b33c97)

</p>
<p>
  
I then log into the domain controller with the new user, Charity Hellen ( Charity_Admin)
</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/7a829ab6-9c73-4441-ae32-641ebfc1075f)

</p>
<p>
  
Next, I change the client virtual machine’s ( Client-1’s) DNS server to the Domain Controller’s private IP address. This is important as to have a single point of authority for both user authentication and name resolution, making it easier to manage and troubleshoot DNS-related issues.
</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/008d80ca-7011-4c45-bbe9-564001b130ca)

</p>

<h2>Step 5: Join the client machine to the Domain.</h2>

<p>
  
I then join the client ( Client-1 )  to the domain controller domain ( tiudydomain.com ) on the DC-1 virtual machine.

</p>
<br />

<p>

 ![image](https://github.com/teeckay/configure-ad/assets/64244011/bccbc7c4-5313-45af-a023-50dbd7d9c559)

![image](https://github.com/teeckay/configure-ad/assets/64244011/a7bfe430-d03c-4399-b49b-bd5b339a5913)


</p>

<h2>Step 6: Setup Remote Desktop for users on the Client Machine.</h2>

<p>
  
Next, I allow all domain users to be able to connect remotely to the client machine.

</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/f8476bdc-2c02-4b72-930e-9f385b33c7bd)

</p>

<h2>Step 7: Create users in the Domain Controller and Use them to log into the domain from the client machine.</h2>

<p>
Finally, I add an employee to the employee folder in the tiudydomain.com domain in the domain controller virtual machine. I then sign out of the client machine and use the new user,  Deon Cool to sign in to the domain from the client machine.
</p>
<br />

<p>
  
![image](https://github.com/teeckay/configure-ad/assets/64244011/8abf10e9-f1db-48a2-8ab9-d79579615ff5)

![image](https://github.com/teeckay/configure-ad/assets/64244011/ee541499-3aa0-4cef-894c-0ee346ecf0d1)

