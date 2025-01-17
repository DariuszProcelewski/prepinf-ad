<p align="center">
   
![image](https://github.com/user-attachments/assets/ed0136be-67fc-4a03-9e83-f354841dc4c1)
</p>

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory Infrastructure in Azure</h1>
This tutorial outlines preparing AD Infrastructure in Azure.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Configuration Steps</h2>

Steps to Set Up  Domain Controller and VM's in Azure

1) Create a Resource Group

![Screenshot 2025-01-16 055658](https://github.com/user-attachments/assets/f158ca8e-5359-483c-bd46-1313dfebb8af)
![Screenshot 2025-01-16 060000](https://github.com/user-attachments/assets/6980a569-46b7-4a2a-ac05-8150f5bf45c0)

Begin by creating a dedicated resource group to organize and manage related resources.

Create a Virtual Network and Subnet
![Screenshot 2025-01-16 060300](https://github.com/user-attachments/assets/7335a377-c2b9-4869-ac26-784c8184bdca)
![Screenshot 2025-01-16 060457](https://github.com/user-attachments/assets/7895b55a-5449-4b82-a88b-290e4c9b8cbc)

Configure a virtual network and a subnet to establish the necessary infrastructure for the domain controller.

Deploy the Domain Controller VM

2) Create a Virtual Machine using Windows Server 2022 and name it "DC-1".

![Screenshot 2025-01-16 060741](https://github.com/user-attachments/assets/6e24c5c8-3e17-40a7-b6e9-378a4c5a4732)
![Screenshot 2025-01-16 061258](https://github.com/user-attachments/assets/abb23de1-a7f3-4228-b846-6c5fdfc275be)
![Screenshot 2025-01-16 061408](https://github.com/user-attachments/assets/eed0ddba-be41-426b-a266-108478558320)
![image](https://github.com/user-attachments/assets/957fea81-cc2b-4916-832f-a7129efed024)
![Screenshot 2025-01-16 061921](https://github.com/user-attachments/assets/31d9841e-74bf-4116-9b1e-1f42c9bf9e02)

3) Set a Static Private IP for the Domain Controller. Once the VM is created, configure the NIC (Network Interface Card) to use a static private IP address for consistent network connectivity.
Disable Windows Firewall (Testing Purposes)

![Screenshot 2025-01-16 065711](https://github.com/user-attachments/assets/046d9b9f-9887-4eec-9e70-0cbde65ce9a8)
![Screenshot 2025-01-16 065934](https://github.com/user-attachments/assets/968b3f8a-289d-4228-8558-d72f37806700)
![Screenshot 2025-01-16 070059](https://github.com/user-attachments/assets/3fc5b36e-0a33-4716-bedf-5c356752d9cc)


4) Log in to the VM (dc-1) and temporarily disable the Windows Firewall to test connectivity during setup.

![image](https://github.com/user-attachments/assets/b6c4e46c-7120-4c31-8278-f7f8f5d93f37)

This process establishes the foundation for a domain controller within a virtualized environment.

Run "wf.msc" and disable Firewall.

![image](https://github.com/user-attachments/assets/9bd3f8d8-5c1d-4cfb-a6b9-095417f00b4c)
![Screenshot 2025-01-17 053616](https://github.com/user-attachments/assets/397dfd32-f58e-47bb-9ce0-82c521fa46a0)
![Screenshot 2025-01-17 053840](https://github.com/user-attachments/assets/fa9ad88d-f724-45bd-a7a4-c06401efeced)
![Screenshot 2025-01-17 053931](https://github.com/user-attachments/assets/3d1c5459-0a75-451a-a35d-651c5d14328e)
![image](https://github.com/user-attachments/assets/c9d09076-2022-4a33-a47c-185520538156)

5) Setup Client-1 in Azure

Create the Client VM (Windows 10) named “Client-1”

![Screenshot 2025-01-16 064727](https://github.com/user-attachments/assets/20a678fc-9087-4d7a-8099-b6be66825b0d)
![Screenshot 2025-01-16 064928](https://github.com/user-attachments/assets/2e8de1d0-e26d-4fc9-963c-757667211cd1)
![Screenshot 2025-01-16 065037](https://github.com/user-attachments/assets/3468f51f-afb4-4c8b-9cfb-bf33d0bf3964)

6) After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address

Copy dc-1 private adress (IF YOU HAVE ISSUE WITH SAVING NETWORK INTERFACE SCROLL TO THE BOTTOM FOR SOLUTION)

![Screenshot 2025-01-17 054416](https://github.com/user-attachments/assets/31e9783c-e34e-490a-aaa5-46af4d37f5fd)
![Screenshot 2025-01-17 054542](https://github.com/user-attachments/assets/4eb8ffbc-7ccd-4198-b7a2-198facc08921)
![Screenshot 2025-01-17 054835](https://github.com/user-attachments/assets/cb2924ba-97ef-4c3f-a095-224fd1f8a5fc)

From the Azure Portal, restart Client-1

![Screenshot 2025-01-17 061008](https://github.com/user-attachments/assets/0b0ac706-140d-4990-b281-ed3cd1f1112e)


- Log in to **Client-1**.
   
![Screenshot 2025-01-17 061206](https://github.com/user-attachments/assets/4d6afd85-4994-456b-a890-68cb7bbfc915)
![image](https://github.com/user-attachments/assets/119cc862-2e21-4685-8f3d-56e8e9ffbf1d)
![image](https://github.com/user-attachments/assets/9a3dae41-85da-4597-bc5b-b4ea6e36524b)

- Test connectivity to **DC-1** by pinging its private IP address.
   
- Confirm that the ping is successful.
   
   ![Screenshot 2025-01-17 062007](https://github.com/user-attachments/assets/e823d4c6-6218-491e-a940-d1ce1e2f0bc3)
   
- On **Client-1**, open PowerShell and execute `ipconfig /all`.  
- Verify that the DNS settings in the output display **DC-1**’s private IP address.
  
   ![Screenshot 2025-01-17 062617](https://github.com/user-attachments/assets/e393832d-dcfc-4e89-84f0-8cc23bb98e78)






_____________________________________________________________________________________________________________________________________________________________________________


*IF YOU HAVE FAILED TO SAVE NETWORK INTERFACE FOLLOW STEPS TO FIX IT*
![image](https://github.com/user-attachments/assets/a9bf2e83-ac88-469d-8988-ea1df86ce4ac)

 Check Network Security Group (NSG) Rules: Make sure any Network Security Group (NSG) rules allow traffic on port 53 (DNS) from Client-1 to DC-1. If traffic is restricted, Client-1 won’t be able to resolve the domain through DC-1.


To do this, I did the following:

#1 Search for "Network security groups" in Azure and click into "Network security groups" when it comes up. Not the classic version.

#2 Click into "client-1-nsg" (or whatever you have it named) and do the following steps:

- Click the "Settings" dropdown menu

- Click "Inbound security rules"

- Click "Add"

- Leave everything alone except in the "Destination port ranges" field; change the number to 53 and in the "Priority" field change it to 290

- Click the "Save" button

- Then click "Outbound security rules" and complete the same process again

#3  Then click into "dc-1-nsg" and do the same process again.

#4  Go to "Virtual machines"

#5  Click the checkbox next to "client-1" and "dc-1" and click "Restart" in the top bar
