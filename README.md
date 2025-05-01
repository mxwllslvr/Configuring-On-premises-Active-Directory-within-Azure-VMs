
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring On-premises Active Directory within Azure VMs</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com/watch?v=nLdh1Tb3jvc)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create and configure Azure Virtual Machines
- Install and configure Active Directory Domain Services
- Configure networking and join client to domain
- Test and validate the deployment

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Create Azure VMs"/>
</p>
<p>
<b>Step 1: Create and Configure Azure Virtual Machines</b><br />
1. Log in to the Azure Portal and navigate to "Virtual Machines".<br />
2. Create a new VM using Windows Server 2022 as the OS. Name it DC-1(e.g., "Domain Controller 1").<br />
3. Configure the VM size (e.g., Standard_D2s_v3) and set up a public IP address.<br />
4. Create another VM using Windows 10 (21H2) as the client machine (e.g., "Client-VM").<br />
5. Ensure both VMs are in the same Virtual Network (VNet) and subnet for communication.<br />
6. Use Remote Desktop to connect to the AD-Server VM and set a static IP address in the network adapter settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Install AD DS"/>
</p>
<p>
<b>Step 2: Install and Configure Active Directory Domain Services</b><br />
1. On the AD-Server VM, open Server Manager and select "Add roles and features".<br />
2. Install the "Active Directory Domain Services" role, including management tools.<br />
3. After installation, promote the server to a Domain Controller by configuring a new forest (e.g., "mydomain.local").<br />
4. Follow the wizard to complete the setup, rebooting the server as required.<br />
5. Verify AD DS is running by checking the Active Directory Users and Computers console.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Configure Client"/>
</p>
<p>
<b>Step 3: Configure Networking and Join Client to Domain</b><br />
1. On the AD-Server, configure DNS to point to its own static IP address.<br />
2. On the Client-VM, set the DNS server to the AD-Server’s static IP address.<br />
3. Join the Client-VM to the domain (e.g., "mydomain.local") via System Properties > Computer Name > Change.<br />
4. Log in to the Client-VM with a domain account to verify connectivity.<br />
5. Optionally, use PowerShell to create additional domain users (`New-ADUser`) or OUs (`New-ADOrganizationalUnit`).
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Test Deployment"/>
</p>
<p>
<b>Step 4: Test and Validate the Deployment</b><br />
1. On the Client-VM, verify domain login with a domain user account.<br />
2. Use PowerShell on the AD-Server to run `Get-ADDomain` and `Get-ADUser` to confirm domain functionality.<br />
3. Test Group Policy by creating a simple GPO (e.g., set desktop wallpaper) and applying it to an OU.<br />
4. Ensure the client receives the GPO by running `gpupdate /force` and logging in again.<br />
5. Monitor the Azure Portal for VM performance and connectivity issues.
</p>
<br />
