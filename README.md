
<p align="center">
<img src="https://i.imgur.com/jdR6rnG.png" alt="osTicket logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Resource Group)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10</b> (Version 22H2)


<h2> Deployment and Configuration Steps </h2>

- Step 1: Setup 2 Virtual machines (VM)
- Step 2: Test the Network between the Client- and Domain Controller (DC-1)
- Step 3: Setup your Domain
- Step 4: Setup a new User in Active Directory
- Step 5: Join Client-1 to Domain
- Step 6: In Client-1 set up Remote Desktop for Non-Admin Users




<h2>Step 1: Set up Resources in Azure </h2>

<p>
<img src="https://i.imgur.com/KUEDPON.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/aLUoxmK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/d1CM2Km.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/3zgPeBB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  

- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
- Set Domain Controller’s NIC Private IP address from dynamic to static
- Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created 
- Ensure that both VMs are in the same Vnet (you can check the topology with Network Watcher). Must be on the same Virtual Network (Vnet) in order to communicate with each other.
  
</p>

<h2>Step 2: Ensure Connectivity between the client and Domain Controller</h2>

<p>
<img src="https://i.imgur.com/YAKasef.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  
  
</p>
<p>
<img src="https://i.imgur.com/ktQ4pqG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
<img src="https://i.imgur.com/7sZ2NbF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


</p>

- Log in to the Domain Controller (DC-1) and enable ICMPv4 in on the local windows Firewall
- Login to the Domain Controller in the Remote Desktop
- Open Windows Defender Firewall Advanced Settings
- Select "Inbound Rules"
- Sort by "Protocol"
- Enable ICMPv4 rules
- Log in to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t (perpetual ping) to verify connectivity
 
</p>


<br />
<h2>Step 3: Install Active Directory </h2>
<p>
<img src="https://i.imgur.com/by5H0Xf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/PJNSVJe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


</p>

- Login to DC-1 through Remote Desktop
- Install Active Directory Domain Services:
- In the Server Manager, Select "Add Roles and Features"
- Continue- Select Next, Next, Next,
- Select "Active Directory Domain Services"
- "Add Features"; "Next"; "Next"; "Next"; "Install"; "Close"

   
</p>

<br />


<br />
<h2>Step 4: Set Up Active Directory</h2>
<p>
<img src="https://i.imgur.com/auNFgik.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/D8FLw1S.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

<p>
<img src="https://i.imgur.com/gVp03LC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

</p>


- Click "notification" to Select: "Promote this server to a Domain Controller"
- Select: "Add a new forest" (mydomain.com or your choice)
- Choose a Password and make note of this
- Complete Installation ("Next"; "Next"; "Next"; "Next" and "Install")
- Allow the server to close, which will disconnect the Remote Desktop.
- Restart and then log back into DC-1 as user: mydomain.com\ajefferson24

</p>





<br />
<h2>Step 5: Create Admin and Create a New Employee in AD</h2>




<p>
<img src="https://i.imgur.com/GrifNLo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>



<p>
<img src="https://i.imgur.com/6X8R5r6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/qdXrn9C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
<img src="https://i.imgur.com/1o4g97x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/1F0D6Hc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/FzsiC6a.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>




<p>
  
- Click “Active Directory Users and Computers”
- Righ click mydomain.com
- Select “new”
- Click Organizational Unit _OU) and create one called “_EMPLOYEES”
- Then a new OU named “_ADMINS”
  
</p>  
Create a new employee

</p> 

- right click(inside the empty space) inside the Admin OU
- new user-next-set password(uncheck box)(For practice purposes, check "password never expires" box)-next-finish

</p>  

I named after myself “Amanda Jefferson” with the user logon name “aj_admin” 

</p>  

- next
- set password(check password never expires)
- next
- finish

</p>  


<br />
<h2>Step 6: Add aj_admin to the “Domain Admins” Security Group</h2>



<p>
<img src="https://i.imgur.com/D4lFeAQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
 

<p>
<img src="https://i.imgur.com/FQkQG8C.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
<img src="https://i.imgur.com/TwSAPoD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>




- Select _ADMIN (OU) Jane Doe and right click to Select Properties
- Select "Member Of"
- Add Domain Users: "Domain"
- Select "Check Names" to open name options
- Select "Domain Admins"
- Complete by Selecting "Ok"; "Ok"; "Apply"; "Ok"
- Log out and close the Remote Desktop connection to DC-1
- Log back in as mydomain\jane_admin
click-properties-member of-add- type:domain-check name-click domain admin-ok-apply-ok)


<br />
<h2>Step 7: From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address </h2>



<p>
<img src="https://i.imgur.com/DjH0O3q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


- In Azure, Locate DC's Private IP address in the VM DC's Overview
- Open the VM Client-1
- Select "Networking"
- Select the "Network Interface" link
- Select "DNS Servers" in the Left Column
- Choose "Custom" DNS Servers
- Enter the DC's Private IP address as the DNS Server
- Click 'Save"
- Restart Client-1, From the Azure Portal



<br />
<h2>Step 8: Login to Client-1 (Remote Desktop) as the original local admin (ajefferson24) and join it to the domain (computer will restart)</h2>



<p>
<img src="https://i.imgur.com/qjUi7Ue.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

  
- Right Click Start menu
- Select "System"
- Select "Rename this PC (advanced)"
- Select "Change"
  
<p> 
  
In "Domain" box type: mydomain.com
  
<p> 
  
- Select "OK"
- In Computer Name/Domain Changes box: -"mydomain.com\jane_admin" and password
- Select "OK" and restart when prompted
  
<p> 
  
Login to the Domain Controller (Remote Desktop)
Navigate to Active Directory Users and Computers (ADUC)
Verify Client-1 shows up inside “Computers” container on the root of the domain
 
  
<h2>Step 9: Setup Remote Desktop for non-administrative users on Client-1 </h2>  
   
  
<p>
<img src="https://i.imgur.com/vknMGRj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>   
 
- Log into Client-1 as mydomain.com\aj_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user 

<p>   
   
Instead of adding an individual user we can add a specical Built-in group called domain users which all users in the domain are automatically in the security.
  
  
<h2>Step 10: Create random additional users </h2>  
  

<p>
<img src="https://i.imgur.com/wO0jAtU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>  

<p>
<img src="https://i.imgur.com/8fQt8ij.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>    
   

</p>

Within DC-1 Remote Desktop

</p>

- Open PowerShell ISE by right clicking to "Run as Administrator"
- Open new file
- Paste the contents of this (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) script file into it (randomly creating new users with "Password1" as their passwords for testing purposes)
- Open Active Directory and _EMPLOYEES to see the list of random users being added

</p>

<h2>Step 11: Test by choosing random name and accounts </h2>  




<p>
<img src="https://i.imgur.com/MFCll6v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>  
  
<p>
<img src="https://i.imgur.com/KLaXhWJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>      
  
   
 Within DC-1 Remote Desktop 
  
</p>  

- Navigate to: _EMPLOYEES
- Choose Name and Right Click to find properties
- Select Account
- Unlock Account when user is locked out
- Check box to Unlock Account 


 </p>   
  
  
  
  
  

Choose a random name, take note of account info
  
 </p> 
  

</p>  
  
  
  
<br />
  
<h2>Step 12: Fixing Common Password Issues </h2>  


<p>
<img src="https://i.imgur.com/4weWEzm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<img src="https://i.imgur.com/7NSvzNm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>



Reset Passwords

- Right Click Name
- Find Drop Down Menu to "Reset Password"
- Select Properties to copy logon name 
- Log into Client-1, using new account name to test access
<p>
