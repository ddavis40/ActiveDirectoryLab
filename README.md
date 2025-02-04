# Active Directory Home Lab

### [YouTube Demonstration](https://youtu.be/oGFOc58obVE)

## Description

In this Lab I went through an online tutorial done alongside [Josh Madakor](https://www.youtube.com/watch?v=MHsI8hJmggI) and set up what could be a corporate VMWare Network of virtual machines, with a user base of 1000+ users. I Used PowerShell, DHCP, and windows server 2019 with AD to create a DC for our 1000+ user base to use authorized clients to connect to their user accounts and to the internet using our client1-2 machines.
## Languages and Utilities Used

- **PowerShell**
- **Active Directory**
- **Windows Server 2019**


## Environments Used

- **Oracle VirtualBox**
- **Windows 10**
- **Windows Server 2019**

## Program walk-through


### Our Networking Diagram for the Lab:

![Network Diagram](https://i.imgur.com/yHy2Uq7.png)

### Our PowerShell Script:

![PowerShell Script](https://i.imgur.com/44qNBKC.png)

# Active Directory Home Lab Setup  

## 1. Install Virtualization Software
- Download and install **Oracle VirtualBox**  
- Download and install the **VirtualBox Extension Pack**  

## 2. Download Required Operating System ISOs
- Download **Windows 10 ISO**  
- Download **Windows Server 2019 ISO**  

## 3. Create the Domain Controller (DC) Virtual Machine
- Create a new VM in VirtualBox, named **DC (Domain Controller)**  
- Assign **2 GB RAM** and **virtual hard disk**  
- Configure **two network adapters**:  
  - **Adapter 1:** NAT (for internet access)  
  - **Adapter 2:** Internal Network (for communication with clients)  
- Attach **Windows Server 2019 ISO** and install the OS  
- Set up a **local administrator account**  

## 4. Configure the Domain Controller
- Install **VirtualBox Guest Additions** for better performance  
- Rename network adapters for clarity:  
  - **Internet** (External Network - NAT)  
  - **Internal** (Private Virtual Network)  
- Assign **Static IP Address** to the internal network adapter  
- Rename the server to **DC**  

## 5. Install Active Directory & Create Domain
- Install **Active Directory Domain Services (AD DS)** role  
- Promote the server to a **Domain Controller**  
- Create a new **domain** (e.g., `mydomain.com`)  

## 6. Create an Administrative Domain Account
- Create a new **Organizational Unit (OU)** called **Admins**  
- Add a **domain administrator account**  
- Assign **Domain Admin** privileges to the new account
![Admins](https://i.imgur.com/sybgQDs.png)

## 7. Configure NAT & Enable Internet Access for Clients
- Install **Remote Access (RAS) & Network Address Translation (NAT)**  
- Configure NAT on the **Internet Network Adapter** </br>
![NAT and remote access](https://i.imgur.com/KoF8uOS.png)

## 8. Set Up DHCP Server
- Install the **DHCP Server role**  
- Create a **DHCP scope** for client IP assignments  
- Configure **default gateway and DNS settings**
![DHCP screenshot](https://i.imgur.com/eM25pMJ.png)

Above you can see our scope we set and CLIENT1's lease.

## 9. Bulk Create Active Directory Users
- Download and extract a **PowerShell script** to generate users
- Run the script to **create 1000+ Active Directory user accounts**  
- Verify user creation in **Active Directory Users and Computers (ADUC)**
![User Account list](https://i.imgur.com/c2ETyBs.png)

Above is a screenshot of the list of users that we created with our PowerShell script and can use mydomain.com to connect to the internet.

## 10. Create & Configure a Windows 10 Client VM
- Create a new Virtual Machine in VirtualBox named **Client1**  
- Assign **4 GB RAM**  
- Configure **one network adapter** (Internal Network)  
- Attach **Windows 10 ISO** and install the OS  
- Configure a **local user account**  

## 11. Join Windows 10 Client to the Domain
- Verify **IP addressing** (ensure DHCP assigns a correct IP)
![ipconfig](https://i.imgur.com/ODjGuQu.png)

- Join the **Windows 10 VM** to the **Active Directory domain (`mydomain.com`)**
![IP address lease](https://i.imgur.com/eM25pMJ.png)

- Restart the VM and log in with an **Active Directory user account**  

## 12. Validate Domain Functionality
- Verify **internet access from the client VM**
![Google.com test](https://i.imgur.com/HwWLNef.png)
- Test **DNS resolution** (ping `mydomain.com`)  
- Check **Active Directory user authentication** (log in with a domain users)  
- Confirm **DHCP leases and domain-joined computers in ADUC**
![Leases](https://i.imgur.com/eM25pMJ.png)

