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
    ![image](https://github.com/Zues4366/Active-Directory/assets/33434045/1c81ca30-b544-4408-bd4f-61d58b3f7685)
  - Set DC's Private IP from Dynamic to Static
  - Log into DC to enable Inbound Rules for "Core Networking Diagnostics" ICMPv4 on the local windows Firewall
    - This allows CVM to have connectivity to the DC

<h2>Step Process</h2>

1. After configuration, log in to the CVM and ensure there is connectivity with the DC
2. Go back to the DC virtual machine to set up the active directory
3. Back in the Server Manager, in the top-right area find a flag icon with a caution symbol and click on it
4. Click "Promote this server to a domain controller"
5. In the Deployment Configuration window, pick "Add a new forest"
   - Put down any domain name _eg. thisdomain.com_ and click "Next"
