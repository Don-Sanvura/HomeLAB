Domain Controller (DC): Runs Windows Server (e.g., Windows Server 2019 or 2022). It runs Active Directory Domain Services (AD DS), DNS, and DHCP.   Client Computer: Runs Windows 10/11 Pro. This machine will be joined to your newly created domain to test user logins, group policies, and permissions.   

<h1>Creating your first virtual machine using vitual box </h1>
<img width="1330" height="700" alt="image" src="https://github.com/user-attachments/assets/10d71113-b754-4731-9a2d-90f52a83e072" />

<h1>For our server we are going to be using  Windows Server 2022</h1>
<img width="1240" height="603" alt="image" src="https://github.com/user-attachments/assets/f866681b-8341-447e-9b9f-018cb78bf728" />

<h1>Running the the vitual machine </h1>
<img width="1362" height="688" alt="image" src="https://github.com/user-attachments/assets/f93eef4d-8d94-44cc-969d-ea62855291cd" />

<h1>Fixing error messsage</h1>
<img width="536" height="234" alt="image" src="https://github.com/user-attachments/assets/a3477dd6-3e94-48b1-8c55-db70a11ab889" />

<table>
<tr>
<td>

<h2>once successfull you should be able to install your operating system</h2>
<img width="402" height="276" alt="image" src="https://github.com/user-attachments/assets/07322e7f-5839-4edd-86b6-17c8e65810e6" />

<h4>1. Power Off the Virtual Machine</h4>

<p>Close the setup window and completely power off the VM in VirtualBox.</p>

<p><strong>Verification:</strong> Status changes from <code>Running</code> to <code>Powered Off</code>.</p>

</td>

<td>

<h4>2. Check Storage Controller Settings</h4>

<p>Go to <strong>Settings → Storage</strong> and check the optical drive containing the ISO. Use <strong>SATA</strong> or <strong>NVMe</strong> if appropriate.</p>

<p><strong>Verification:</strong> The Windows Server ISO is mounted correctly with no warning icons.</p>

</td>
</tr>
</table>
<img width="1146" height="312" alt="image" src="https://github.com/user-attachments/assets/60364c51-6b55-4195-874b-14b6c4f19454" />


# Active Directory Home Lab — Oracle VirtualBox

<p>
Building an <strong>Active Directory (AD) home lab</strong> in Oracle VirtualBox is a fantastic project for practicing enterprise administration, user management, and security.
</p>

<h2>Architecture Overview</h2>

<p>
To simulate a real enterprise environment, this lab requires two virtual machines (VMs):
</p>

<table>
<thead>
<tr>
<th>Virtual Machine</th>
<th>Operating System</th>
<th>Purpose</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Domain Controller (DC01)</strong></td>
<td>Windows Server 2019 / 2022</td>
<td>Runs Active Directory Domain Services (AD DS), DNS, and DHCP.</td>
</tr>
<tr>
<td><strong>Client Computer</strong></td>
<td>Windows 10 / 11 Pro</td>
<td>Joins the domain to test user logins, Group Policy, and permissions.</td>
</tr>
</tbody>
</table>

<h2>Step-by-Step Build Guide</h2>

<h3>1. Download Required ISOs &amp; Tools</h3>

<p>
<strong>Prerequisite:</strong> Download and install Oracle VirtualBox. Next, download evaluation ISO images for Windows Server 2019/2022 and Windows 10/11 Pro from the official Microsoft Evaluation Center or your educational portal.
</p>

<p>
<strong>Verification:</strong> VirtualBox opens successfully, and both operating system ISO files are saved locally on your host machine.
</p>

<h3>2. Configure the Windows Server VM</h3>

<p>
Create a new VM in VirtualBox named <code>DC01</code>. Allocate at least <strong>2 GB–4 GB of RAM</strong> and attach your Windows Server ISO.
</p>

<p>
For internet access and communication between your lab machines, configure two network adapters:
</p>

<ul>
<li><strong>Adapter 1:</strong> NAT — provides internet access.</li>
<li><strong>Adapter 2:</strong> Internal Network — use a network name such as <code>intnet</code> for communication between the lab machines.</li>
</ul>

<p>
<strong>Verification:</strong> The server boots successfully, Windows Server installs correctly, and you can log into the desktop.
</p>

<h3>3. Install Active Directory Domain Services (AD DS)</h3>

<p>
Inside your Windows Server VM, assign a <strong>static IP address</strong> to the internal network adapter.
</p>

<p>Then:</p>

<ol>
<li>Open <strong>Server Manager</strong>.</li>
<li>Select <strong>Add roles and features</strong>.</li>
<li>Select <strong>Active Directory Domain Services</strong>.</li>
<li>Complete the installation wizard.</li>
<li>Click the yellow warning flag at the top of Server Manager.</li>
<li>Select <strong>Promote this server to a domain controller</strong>.</li>
<li>Select <strong>Add a new forest</strong>.</li>
<li>Enter a domain such as <code>lab.local</code>.</li>
<li>Set the <strong>DSRM password</strong>.</li>
<li>Complete the configuration and allow the server to restart.</li>
</ol>

<p>
<strong>Verification:</strong> After rebooting, the login screen should display your domain before the username, for example:
</p>

<pre><code>LAB\Administrator</code></pre>

<h3>4. Manage Accounts, Groups, and Organizational Units (OUs)</h3>

<p>
On the Domain Controller, open:
</p>

<pre><code>Server Manager → Tools → Active Directory Users and Computers (ADUC)</code></pre>

<h4>Create Organizational Units</h4>

<p>
Right-click your domain and select <strong>New → Organizational Unit</strong>. Create logical departments such as:
</p>

<ul>
<li><code>IT_Dept</code></li>
<li><code>HR_Dept</code></li>
<li><code>Finance_Dept</code></li>
<li><code>Users</code></li>
</ul>

<h4>Create Users</h4>

<p>
Right-click an OU and select <strong>New → User</strong> to create individual user accounts and configure their credentials and password policies.
</p>

<h4>Create Groups &amp; Permissions</h4>

<p>
Right-click an OU and select <strong>New → Group</strong>. Groups can be configured as either <strong>Security</strong> or <strong>Distribution</strong> groups.
</p>

<p>
Double-click a group, open the <strong>Members</strong> tab, and add the appropriate users.
</p>

<p>
For file and folder permissions, right-click a directory and select:
</p>

<pre><code>Properties → Security</code></pre>

<p>
You can then assign access rights to the appropriate security groups.
</p>

<p>
<strong>Verification:</strong> Users are successfully organized into custom OUs, assigned to security groups, and given the appropriate permissions.
</p>

<h3>5. Deploy and Join the Client Machine</h3>

<p>
Create a second VM in VirtualBox using <strong>Windows 10/11 Pro</strong>.
</p>

<p>
Configure the client's network adapter to use the same Internal Network as the Domain Controller:
</p>

<pre><code>Internal Network → intnet</code></pre>

<p>Once Windows is installed:</p>

<ol>
<li>Open the system settings.</li>
<li>Change the computer name if required.</li>
<li>Select the option to join a <strong>Domain</strong>.</li>
<li>Enter your domain name, for example <code>lab.local</code>.</li>
<li>Enter the Domain Controller administrator credentials when prompted.</li>
<li>Restart the client computer.</li>
</ol>

<p>
<strong>Verification:</strong> The client successfully joins the domain and you can log into the Windows client using one of the user accounts created through ADUC on the Domain Controller.
</p>

<h2>Lab Architecture</h2>

<pre>
                 ┌───────────────────────────┐
                 │        Host Computer      │
                 │      Oracle VirtualBox    │
                 └─────────────┬─────────────┘
                               │
                    ┌──────────┴──────────┐
                    │    Internal Network  │
                    │       intnet         │
                    └──────────┬──────────┘
                               │
              ┌────────────────┴────────────────┐
              │                                 │
      ┌───────▼────────┐                ┌───────▼────────┐
      │      DC01      │                │  Client PC     │
      │ Windows Server │                │ Windows 10/11  │
      │                │                │      Pro       │
      │ • AD DS        │                │                │
      │ • DNS          │                │ • Domain User  │
      │ • DHCP         │                │ • GPO Testing  │
      └────────────────┘                └────────────────┘
</pre>

<h2>Skills Practiced</h2>

<ul>
<li>Active Directory Domain Services (AD DS)</li>
<li>Windows Server administration</li>
<li>DNS and DHCP configuration</li>
<li>Organizational Unit (OU) management</li>
<li>User and security group management</li>
<li>Windows domain joining</li>
<li>File and folder permissions</li>
<li>Virtual machine networking</li>
<li>Basic Group Policy management</li>
<li>Enterprise user administration</li>
</ul>

<h2>Lab Verification Checklist</h2>

<ul>
<li>☐ Windows Server VM successfully installed</li>
<li>☐ Static IP configured on the Domain Controller</li>
<li>☐ Active Directory Domain Services installed</li>
<li>☐ New AD forest created</li>
<li>☐ DNS configured</li>
<li>☐ OUs created</li>
<li>☐ Users created</li>
<li>☐ Security groups configured</li>
<li>☐ Windows client successfully joined to the domain</li>
<li>☐ Domain user successfully logged into the client</li>
<li>☐ Permissions successfully tested</li>
</ul>

<h2>Conclusion</h2>

<p>
This Active Directory home lab provides a practical environment for learning Windows Server administration and enterprise identity management. Using Oracle VirtualBox makes it possible to safely experiment with domains, users, groups, permissions, DNS, DHCP, and Group Policy without requiring physical enterprise hardware.
</p>           

      
    
