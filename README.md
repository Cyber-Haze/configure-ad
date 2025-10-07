<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2> High-Level Deployment and Configuration Steps</h2>  

<p> 

  - Install Active Directory & Promote DC-1 to Domain Controller
  - Create Domain Admin User & Normal User Accounts
  - 
  


</p>

 <h2>  Step 1: Install Active Directory </h2> 

<p> 
  
**Configure and install Active Directory services on the designated Domain Controller virtual machine.**

1. Install "Active Directory Domain Services" in DC-1  
   - In the Server Manager dashboard  
   - Click **Add roles and features**  
   - Select **Active Directory Domain Services**
   - Finish installation.

     
</p>

 <p>     
   
<img width="1287" height="613" alt="image" src="https://github.com/user-attachments/assets/891234aa-a0c4-4ecd-8bd7-72019c8f373c" />
<img width="752" height="258" alt="image" src="https://github.com/user-attachments/assets/9aa09135-90c5-45ac-9550-b79d43e9dbbb" />
   
</p> 

<p>

<h2></h2>

2. Click on the flag at the top right of the screen with the warning sign  
   - Select "Promote this server to Domain Controller"
   - Add a new forest: "mydomain.com"
   

<p> 

<img width="997" height="400" alt="image" src="https://github.com/user-attachments/assets/28053711-483e-468b-9b78-e80138bc5302" />
<img width="758" height="331" alt="image" src="https://github.com/user-attachments/assets/31e2ade8-4a4f-4a1a-973b-76b489a4f79e" />

</p>

In the Event you need to restore AD, Ensure you create a password for such a time 

</p>
<P> 
<img width="747" height="389" alt="image" src="https://github.com/user-attachments/assets/ecb59ed5-3509-443a-ba3a-2aad1ffa21e1" />

</P>

<p> 

- After installation you AD-VM will restart.
- Because of the New Domain Controller setup, the context of login has changed and must be specified.
- To log in you now login as mydomain.com\labuser


</p>
<p> 
<img width="400" height="246" alt="image" src="https://github.com/user-attachments/assets/c4e2ed53-a21c-4c82-9720-6237154821fb" />

</p>

<H2> Create Domain Admin User & Normal User Accounts </H2>

**Create Organizational Units (OU) named _EMPLOYEES, _CLIENTS, and _ADMINS **

 <p>  

   - Open AD Users and Computers from Start Menu
   - Right click Mydomain.com > Select New > Organizational Unit
   - Create OU's : _EMPLOYEES, _CLIENTS, and _ADMINS
 
 </p>
<br/> 
<P> 

<img width="751" height="526" alt="image" src="https://github.com/user-attachments/assets/2ef32c6b-2f91-4a0e-a6a6-2a881395554e" />
<img width="672" height="303" alt="image" src="https://github.com/user-attachments/assets/737a079d-5889-49ba-912d-27afbf598b17" />

</P>

<h2> </h2> 

**Create a Domain Admin user within the domain**

<p> 
  
   - Right click on the OU  _ADMINS and create a new user named Jane Doe.
   - Username jane_admin  
  
  </p>
  
<p> 

<img width="747" height="398" alt="image" src="https://github.com/user-attachments/assets/3a585330-ecba-43a3-aa8a-d48fb93e3320" />
<img width="435" height="371" alt="image" src="https://github.com/user-attachments/assets/45a266c2-5a70-414c-ae94-1f04993dfa20" />
<img width="425" height="363" alt="image" src="https://github.com/user-attachments/assets/88b1057b-973d-4f4d-b9ad-fce4f13661e6" />


</p>

<h2> </h2> 

<p>

**Add jane_admin to the "Domain Admins" Security Group** 

<p>
  
   - Turn Jane Doe into an admin by right clicking her name > properties
   - member of and adding her to the "Domain Admins" Security Group

</p>
  
<p> 
<img width="834" height="499" alt="image" src="https://github.com/user-attachments/assets/52d9411e-ca86-48cc-b967-cdcf9a1d45ae" />
<img width="408" height="219" alt="image" src="https://github.com/user-attachments/assets/0ad7d0b0-8c5d-48b3-ab0f-64f2aced76a4" />



</p>

<p>


## Step 6: Log out of DC-1 to log back in as Jane Doe


   - Log back in as "mydomain.com\jane_admin"
   - Use jane_admin as your admin account from now on

<img width="453" height="557" alt="Screenshot 2025-09-06 104858" src="https://github.com/user-attachments/assets/a2406d9b-e020-47ef-8727-cc6a44ddbd49" />


<p>



## Step 7: Login to Client-1 as the original local admin and join it to the domain  (Computer will restart)

   - Right click the start menu > click system > click rename this pc advanced
   - Under the computer name tab, click on "Change"
   - Join it to the domain "mydomain.com"
   

<img width="825" height="552" alt="Screenshot 2025-09-06 105051" src="https://github.com/user-attachments/assets/6bcc6533-ec89-4d80-b10c-b2568baeb5d4" />

 - Enter the name and password of an account with permission to join the domain.
 - Use the account: mydomain.com\jane_admin
 - Once Client-1 has been added, the VM will restart.

<img width="462" height="304" alt="Screenshot 2025-09-06 105113" src="https://github.com/user-attachments/assets/89e75f2c-7389-4d7e-ac81-93658bbd7a1f" />



<p>

## Step 8: Login to the Domain Controller and verify Client-1 shows up in ADUC

   - Expand mydomain.com then go to "computers" to verify

<img width="756" height="533" alt="Screenshot 2025-09-06 105129" src="https://github.com/user-attachments/assets/77b4a2eb-5c15-4ac3-877b-26ffce42a2a7" />



<p>

## Step 9: Create a new OU named "_CLIENTS" and drag Client-1 into there


<img width="759" height="531" alt="Screenshot 2025-09-06 105212" src="https://github.com/user-attachments/assets/cf818cfe-f34d-4453-a195-b95328514884" />




<p>


## Step 10: Setting up RDP & User Accounts via PowerShell

   - Setup RDP for non-administrative users on Client-1
   - We have to login to Client-1 as an admin (using mydomain.com\jane_admin) right click the start menu and open system.
   - Click on "Remote Desktop" on User Accounts and click "Select users that can remotely access this PC"
   - Allow "Domain Users" access to remote desktop.
   - After completing those steps you should be able to log into Client-1 as normal user (any user).

<img width="460" height="256" alt="Screenshot 2025-09-06 105242" src="https://github.com/user-attachments/assets/f443d0c3-1ad2-4d18-b2fe-8a48a3ea949d" />





<p>


## Step 11: Run Powershell script

   - Use a Powershell script to generate a number of users for our Active Directory Domain.
   - Login to DC-1 as mydomain.com\jane_admin
   - Open Powershell_ISE as an administrator and create a new file then save
   - [(https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)]
   - Paste the script to generate thousands of users into the domain.
   - Run Script

<img width="827" height="495" alt="Screenshot 2025-09-06 105259" src="https://github.com/user-attachments/assets/0aae0939-8ea6-4bd3-b001-537a460a9a14" />

- When finished, open ADUC and observe the accounts in the appropriate OU  "_EMPLOYEES"

<img width="828" height="495" alt="Screenshot 2025-09-06 105319" src="https://github.com/user-attachments/assets/31ee762b-8696-4dbd-85d9-873952f806b1" />






<p>


## Step 12: Login as any user
  
  - Now you can login as any of the users that was created by the script to further verify that the script has worked.
  - Take note of the default password in the script (Password1) for all users.

<img width="450" height="557" alt="Screenshot 2025-09-06 105619" src="https://github.com/user-attachments/assets/b5f52c67-bba4-4505-b9cc-848b73d31ff9" />



As you can see the Powershell script created a user with the username "bid.tuk". We were able to login to Client-1 with his credentials as a normal user.

<img width="824" height="429" alt="Screenshot 2025-09-06 105653" src="https://github.com/user-attachments/assets/e413e324-61f5-4834-bdb1-a2b102a918f0" />









<p>






