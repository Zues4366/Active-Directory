<h1 align="center">Active Directory</h1>

With Azure Virtual Machines, this demo illustrates the implementation of on-premises Active Directory with a Domain Controller and a Client VM.

<h2 align="center">Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2 align="center">Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)


<b>Configuration:</b>
  - Create 2 Virtual Environments:
    - Domain Controller (DC)
    - Client Virtual machine (CVM) (_Important_: Make sure it is using the vnet of the DC that was just created for this to work)
    ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/4b2287d9-247a-40c2-bf09-5a59574fedc9)
  - Set DC's Private IP from Dynamic to Static
    ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/dc6d314e-939a-4097-ac61-f58c9258eacd)
  - Log into DC to enable Inbound Rules for "Core Networking Diagnostics" ICMPv4 on the local windows Firewall
    ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/e87cd4b3-f89c-4056-889d-8550b696c259)
    - This allows CVM to have connectivity to the DC
     ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/9d92b86b-9280-49e6-9ffb-72d0e2504ed2)

<h2>Step Process</h2>

1. After configuration, log in to the CVM and ensure there is connectivity with the DC
2. Go back to the DC virtual machine to set up the active directory
    - "Active Directory Domain Services"
    ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/bb17a4f8-5728-4daf-8e1f-4bac6b8b2557)
3. Back in the Server Manager, in the top-right area find a flag icon with a caution symbol and click on it
4. Click "Promote this server to a domain controller"
5. In the Deployment Configuration window, pick "Add a new forest"
   - Put down any domain name _eg. thisdomain.com_ and click "Next"
   - Click "Install" and the virtual machine should restart
     ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/353f6ff2-d12b-490f-95e3-d7b2a4d3f808)
6. Log back into the DC but this time using the domain\user
   - ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/cb1f3404-d61a-48fb-828e-0f61b2a93542)
7. Head over to "Active Directory Users and Computers"
8. Under your domain site create two folders for Admins and Employees
9. In the admin folder add a user and set up their password as well as give the user domain admin for access to the DC
    ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/04177cf6-5073-4f31-a5ec-96437ba0f27f)

10. Go back to the Azure portal and access the network settings for the client machine
11. In "DNS Servers" change the settings to Custom and set the IP to the Private IP of the DC
    - Save and Restart the machine
    - Go back to Client's virtual machine and go into CMD to ipconfig /all to check the DNS Server is set to the DC's Private IP
      ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/1051ab52-842e-46bf-b505-517eff9b1636)

12. Get Back into the client's virtual machine and head over to "System" settings to rename the PC to be a member of your domain of the DC
![image](https://github.com/Zues4366/Active-Directory/assets/33434045/84a73c37-b00f-43d9-96e8-3d1e20897c08)

13. The client's machine should now allow any user under the domain\user to be able to log into it
