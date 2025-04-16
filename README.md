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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1912" alt="Screenshot 2025-04-16 at 12 55 53 PM" src="https://github.com/user-attachments/assets/48ca8929-b1c9-4e42-8586-67f77c94fccb" />
/>
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
