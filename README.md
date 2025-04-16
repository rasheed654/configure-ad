<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 Preparing AD Infrastructure in Azure
- Step 2 Deploying Active Directory
- Step 3 Creating Users With Powershell
- Step 4 Group Policy and Managing Accounts

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1912" alt="Screenshot 2025-04-16 at 12 55 53 PM" src="https://github.com/user-attachments/assets/48ca8929-b1c9-4e42-8586-67f77c94fccb" />

</p>
<p>
Create a resource group
</p>
<br />

<p>
<img width="1896" alt="Screenshot 2025-04-16 at 12 56 16 PM" src="https://github.com/user-attachments/assets/45a8caa0-23f2-4bfe-9146-bc7e190f79ba" />

</p>
<p>
Create a Active Directory
</p>
<br />

<p>
<img width="934" alt="Screenshot 2025-04-16 at 12 30 59 PM" src="https://github.com/user-attachments/assets/6b1a1251-6ed5-4a3f-b769-d13b139062b7" />
</p>
<p>
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
</p>
<br />

<p>
<img width="569" alt="Screenshot 2025-04-16 at 12 50 43 PM" src="https://github.com/user-attachments/assets/1e515a87-830c-4539-83d5-98df8a46dd24" />
</p>
<p>
After VM is created, set Domain Controller’s NIC Private IP address to be static
</p>
<br />

<p>
<<p>
<img width="945" alt="Screenshot 2025-04-16 at 12 38 36 PM" src="https://github.com/user-attachments/assets/23cb05ca-4c94-439c-82ea-56015527d830" />
</p>
<p>
Create the Client VM (Windows 10) named “Client-1”
</p>
<br />

<p>
<img width="901" alt="Screenshot 2025-04-16 at 1 59 06 PM" src="https://github.com/user-attachments/assets/878a6fce-81c3-461b-89bd-62e66f8c306e" />


</p>
<p>
Login To DC-1 and turn off Windows Firewall.
</p>
<br />

<p>

  <img width="1105" alt="Screenshot 2025-04-16 at 1 31 38 PM" src="https://github.com/user-attachments/assets/f4a38174-763b-482d-9dc3-1ab6b544ca88" />

</p>
<p>
Set Client-1 DNS settings to DC-1 Private IP Address
</p>
<br />


<p>
<img width="2227" alt="Screenshot 2025-04-16 at 1 37 52 PM" src="https://github.com/user-attachments/assets/57bda9c3-6fad-47e7-bd4a-bbc1622efc17" />
</p>
<p>
From the Azure portal, restart Client 1
</p>
<br />

<p>
<img width="1576" alt="Screenshot 2025-04-16 at 2 00 03 PM" src="https://github.com/user-attachments/assets/b25d59dd-5405-4a4c-981e-4d895b91025d" />



</p>
<p>
Login To Client-1 and ping DC-1 private IP address and make sure ping succeded.
</p>
<br />

<p>
<img width="1562" alt="Screenshot 2025-04-16 at 2 03 38 PM" src="https://github.com/user-attachments/assets/670142cd-4932-45da-b010-594f570a9a13" />

</p>
<p>
From Client-1, open PowerShell and run ipconfig /all
The output for the DNS settings should show DC-1’s private IP Address

</p>
<br />

<h2>Deploying Active Directory</h2>

<p>
<img width="1663" alt="Screenshot 2025-04-16 at 2 26 41 PM" src="https://github.com/user-attachments/assets/5d31e334-ca5c-414c-b5ca-8516f4b63c1c" />
</p>
<p>
Login to DC-1 and install Active Directory Domain Services
</p>
<br />

<p>
<img width="1666" alt="Screenshot 2025-04-16 at 2 33 56 PM" src="https://github.com/user-attachments/assets/ed5c9ce6-4c20-4bd6-be54-d70dc8445068" />

</p>
<p>
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
</p>
<br />

<p>
<img width="443" alt="Screenshot 2025-04-16 at 2 49 48 PM" src="https://github.com/user-attachments/assets/55098f2b-a02c-465d-b022-1e3b644bfbfb" />


</p>
<p>
Restart and then log back into DC-1 as user: mydomain.com\labuser

</p>
<br />

<p>
<img width="754" alt="Screenshot 2025-04-16 at 2 58 15 PM" src="https://github.com/user-attachments/assets/5c11cf17-9b8b-4302-9b5b-675ec502aa5e" />



</p>
<p>
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
Create another Organizational Unit (OU) called “_ADMINS”

</p>
<br />

<p>
<img width="753" alt="Screenshot 2025-04-16 at 3 08 04 PM" src="https://github.com/user-attachments/assets/1329f11e-5ec5-4bbd-a372-63a252404f89" />




</p>
<p>
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”


</p>
<br />

<p>
<img width="412" alt="Screenshot 2025-04-16 at 3 14 27 PM" src="https://github.com/user-attachments/assets/fa15606b-7935-4cd6-b28d-3a3c3bdab293" />





</p>
<p>
Add jane_admin to the “Domain Admins” Security Group


</p>
<br />

<p>
<img width="440" alt="Screenshot 2025-04-16 at 3 26 52 PM" src="https://github.com/user-attachments/assets/55f92b42-c58d-4f53-b2cd-c0705f8650d7" />


</p>
<p>
Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”
User jane_admin as your admin account from now on

</p>
<br />

<p>
<img width="1201" alt="Screenshot 2025-04-16 at 3 43 24 PM" src="https://github.com/user-attachments/assets/00e5fb8d-9017-45d6-99e5-a0797f30eb5f" />



</p>
<p>
Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)

</p>
<br />

<p>
<img width="753" alt="Screenshot 2025-04-16 at 3 54 29 PM" src="https://github.com/user-attachments/assets/9165bfde-9fcd-420b-a802-095a435522e9" />




</p>
<p>
Login to the Domain Controller and verify Client-1 shows up in ADUC
Create a new OU named “_CLIENTS” and drag Client-1 into there

</p>
<br />

<h2>Creating Users With Powershell</h2>

<p>
<img width="1201" alt="Screenshot 2025-04-16 at 4 06 40 PM" src="https://github.com/user-attachments/assets/710e561d-08f7-486e-ba4e-7da05bcc5041" />





</p>
<p>
Log into Client-1 as mydomain.com\jane_admin
Open system properties
Click “Remote Desktop”
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now

</p>
<br />
