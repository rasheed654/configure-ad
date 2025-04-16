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
<img width="1203" alt="Screenshot 2025-04-16 at 4 11 27 PM" src="https://github.com/user-attachments/assets/45b2fef8-11ab-4003-a92d-f17f0d3b9a72" />






</p>
<p>
Log into Client-1 as mydomain.com\jane_admin
Open system properties
Click “Remote Desktop”
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now

</p>
<br />

<p>
<img width="2002" alt="Screenshot 2025-04-16 at 4 18 59 PM" src="https://github.com/user-attachments/assets/fb640d48-edd3-4df3-9a0d-6ad828e427eb" />
</p>
<p>
Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator
</p>
<br />

<p>
<img width="2000" alt="Screenshot 2025-04-16 at 4 27 09 PM" src="https://github.com/user-attachments/assets/ad9ea892-6d2a-4609-8eb6-502dfa52d15b" />

</p>
<p>
Create a new File and paste the contents of the script into it that creates new users.
Run the script and observe the accounts being created

</p>
<br />

<p>
<img width="752" alt="Screenshot 2025-04-16 at 4 35 45 PM" src="https://github.com/user-attachments/assets/ddb8503a-eb29-4680-a375-8b5749586ecc" />

</p>
<p>
When finished, open Active Directory Users and computers and observe the accounts in the appropriate OU　(_EMPLOYEES)

</p>
<br />

<p>
<img width="439" alt="Screenshot 2025-04-16 at 4 42 03 PM" src="https://github.com/user-attachments/assets/e2a8a104-6ea9-4ff4-8466-5ed8d422649b" />


</p>
<p>
Attempt to log into Client-1 with one of the accounts (take note of the password in the script)


</p>
<br />

<h2>Group Policy and Mangaing Accounts</h2>

<h3>Dealing with account lockout </h3>

<p>
<img width="439" alt="Screenshot 2025-04-16 at 4 42 03 PM" src="https://github.com/user-attachments/assets/e2a8a104-6ea9-4ff4-8466-5ed8d422649b" />


</p>
<p>
Get logged into dc-1
Pick a random user account you created previously
Attempt to log in with it 10 times with a bad password
</p>
<br />

<p>
<img width="788" alt="Screenshot 2025-04-16 at 5 25 47 PM" src="https://github.com/user-attachments/assets/84efaa3b-3926-46ac-a1ad-c61ab287ee99" />



</p>
<p>
Open the Group Policy Management Console (GPMC)
Log in to a machine with Group Policy Management Console installed (typically, a Domain Controller).
Click Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.
2. Create or Edit a Group Policy Object (GPO)
In the GPMC, navigate to the Group Policy Objects section.
Right-click Group Policy Objects and select New to create a new GPO, or right-click an existing GPO and select Edit to modify it.
Give the new GPO a descriptive name if you're creating a new one, like "Account Lockout Policy".
3. Navigate to the Account Lockout Policy Settings
In the Group Policy Management Editor, expand the following:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
4. Configure Account Lockout Policy Settings
You will see three primary settings that you need to configure:
Account Lockout Duration:
Definition: The time in minutes that an account remains locked before it is automatically unlocked.
Configuration: Double-click on this setting, select Define this policy setting, and then set the duration (e.g., 30 minutes).
Account Lockout Threshold:
Definition: The number of failed logon attempts that will trigger an account lockout.
Configuration: Double-click on this setting, select Define this policy setting, and then set the threshold (e.g., 3 invalid attempts).
Reset Account Lockout Counter After:
Definition: The time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts.
Configuration: Double-click on this setting, select Define this policy setting, and then set the time (e.g., 15 minutes).
5. Link the GPO to an Organizational Unit (OU)
Once the GPO is configured, you need to link it to the appropriate Organizational Unit (OU) or domain where you want the policy to apply.
In the GPMC, right-click the OU or domain where you want to apply the GPO and select Link an Existing GPO.
Choose the GPO you created or modified earlier and click OK.
6. Update Group Policy
You can wait for the Group Policy to propagate automatically, or you can force an update immediately.
On a client machine or server, open Command Prompt and type gpupdate /force, then press Enter.
<img width="975" alt="Screenshot 2025-04-16 at 5 28 39 PM" src="https://github.com/user-attachments/assets/3e81f409-3f3f-4256-ac8a-95026cee5051" />

</p>
<br />

<p>
<img width="259" alt="Screenshot 2025-04-16 at 5 41 46 PM" src="https://github.com/user-attachments/assets/b1de4e38-412d-4332-be26-9ae4936f3015" />



</p>
<p>
Observe that the account has been locked out within Active Directory
</p>
<br />

<p>
<img width="412" alt="Screenshot 2025-04-16 at 5 44 18 PM" src="https://github.com/user-attachments/assets/72c05212-021c-4b59-aa02-b59dad9540d1" />
</p>
<p>
Unlock the account
</p>
<br />

<p>
<img width="518" alt="Screenshot 2025-04-16 at 5 51 47 PM" src="https://github.com/user-attachments/assets/b13b60ad-1aa1-4fa2-8d72-6f015af808cc" />

</p>
<p>
Reset the password
then Atempt to log in with it.
</p>
<br />

<p>
<img width="518" alt="Screenshot 2025-04-16 at 5 51 47 PM" src="https://github.com/user-attachments/assets/b13b60ad-1aa1-4fa2-8d72-6f015af808cc" />

</p>
<p>
Reset the password
then Atempt to log in with it.
</p>
<br />

<h3>Enabling and Disabling Accounts </h3>

<p>
<img width="517" alt="Screenshot 2025-04-16 at 6 02 12 PM" src="https://github.com/user-attachments/assets/3d703aca-b821-4333-b9fe-c71e6258b0e2" />
</p>
<p>
Disable the same account in Active Directory
Attempt to login with it, observe the error message
</p>
<br />

<p>
<img width="513" alt="Screenshot 2025-04-16 at 6 08 22 PM" src="https://github.com/user-attachments/assets/6d35c077-2d8b-404c-afb6-7d3bfc28eb21" />

</p>
<p>
Re-enable the account and attempt to login with it.
</p>
<br />


