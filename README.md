**Setting Up Resources in Azure**

1. **Create the Domain Controller VM (Windows Server 2022) named “DC-1”**
    - Note the Resource Group and Virtual Network (Vnet) created.
    - Set Domain Controller’s NIC Private IP address to be static.

2. **Create the Client VM (Windows 10) named “Client-1”**
    - Use the Resource Group and Vnet from Step 1.
    - Ensure both VMs are in the same Vnet (verify with Network Watcher).

3. **Ensure Connectivity between the Client and Domain Controller**
    - Login to Client-1 with Remote Desktop, and ping DC-1’s private IP address with `ping -t <ip address>` (perpetual ping).
    - Login to the Domain Controller, enable ICMPv4 in the local Windows Firewall, and check ping success on Client-1.

4. **Install Active Directory**
    - Login to DC-1 and install Active Directory Domain Services.
    - Promote as a DC, setting up a new forest (e.g., mydomain.com).
    - Restart and log back into DC-1 as user: mydomain.com\labuser.

5. **Create Admin and Normal User Account in AD**
    - In ADUC, create an OU called “_EMPLOYEES” and another named “_ADMINS.”
    - Create a new employee, “Jane Doe” (username: jane_admin), with the same password.
    - Add jane_admin to the “Domain Admins” Security Group.
    - Log in as “mydomain.com\jane_admin.”

6. **Join Client-1 to the Domain (mydomain.com)**
    - Set Client-1’s DNS settings to DC’s Private IP address.
    - Restart Client-1 from the Azure Portal.
    - Login to Client-1 as the local admin (labuser) and join it to the domain (computer will restart).
    - Verify Client-1 in ADUC under the “Computers” container.

7. **Organize Clients into an OU**
    - Create a new OU named “_CLIENTS” in ADUC and move Client-1 into it.

8. **Setup Remote Desktop for Non-Administrative Users on Client-1**
    - Log into Client-1 as mydomain.com\jane_admin, open system properties, and click “Remote Desktop.”
    - Allow “domain users” access to remote desktop.
    - Log into Client-1 as a normal, non-administrative user.

9. **Create Additional Users and Test Login on Client-1**
    - Log into DC-1 as jane_admin.
    - Open PowerShell_ise as an administrator.
    - Copy and run the script to create additional users.
    - Observe the accounts in ADUC.
    - Attempt to log into Client-1 with one of the newly created accounts.
