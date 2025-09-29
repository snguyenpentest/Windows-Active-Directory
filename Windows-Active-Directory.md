# Windows Active Directory

Documented my experience of setting up Windows Active Directory on a Windows Server 2016 VM in Oracle VM VirtualBox 6.1X.

### My host PC has the following specs:<br>
> •	Windows 10 Home<br>
•	Intel i5-4670k CPU @3.4GHz<br>
•	32 GB RAM<br>
•	1 TB SSD<br>

Note: We've previously installed Oracle VM VirtualBox 6.1X for this project<br>

### Overview: <br>
1.	Create and set up a Windows Server 2016 VM with Windows Active Directory<br>
2.	Set up Windows 10 Enterprise machines in a VM environment<br>
3.	Set up DNS and Make the Active Directory a Domain Controller<br>
4.	Set up a new Windows10 Enterprise account<br>
5.	Create and Add a New User into the Domain<br>
6.	Set up the user account with standard permissions and successfully logged into the local Domain


After we installed Oracle VM VirtualBox 6.1X, let's set up Windows Server 2016 on a new VM.
## 1. Set up Windows Server 2016 and Windows Active Directory: 
![image](https://github.com/user-attachments/assets/1dd4c523-8434-46e4-9438-f54edbb32e45)

> Username: AD0admin<br>
Password: admin<br>
Hostname: WindowServer2016<br>
Domain Name: myguest.virtualbox.org<br>

## 2. After installing Oracle > Windows Server 2016, begin the same installation process for Windows 10 workstation(s). 
![image](https://github.com/user-attachments/assets/636e94fc-56e7-4024-a2d5-626c24955fab)

When Server 2016 is finished installing on the vm, you should see the desktop, then do the following:

1) Change the PC name in Server 2016 to your desired name, so we can easily identify the servers and workstations.
> In this example, we named it "Hokage".  
2) Add an administrator account password; otherwise, we cannot create the DNS server. 

### 3. Set up DNS and Make the Active Directory a Domain Controller
> (2) Add roles and features -> this server will have role-based Active Directory Domain Services.
![image](https://github.com/user-attachments/assets/4fa94044-fd80-4fb2-809a-65921628b453)
> Once completed, you’ll see the flag icon have a notification.

Click on the flag icon and “Promote this server to a domain controller”
![image](https://github.com/user-attachments/assets/27751c62-375b-4306-9f84-074c57914761)
![image](https://github.com/user-attachments/assets/59431a09-508f-4906-bdc8-54ba82670ed2)

#### Active Directory Domain Services Configuration Wizard:
1.	Deployment Configuration: Add a New Forest -> Root Domain Name: leafvillage.local<br>
2.	Domain Controller Options -> Password: *******<br>
3.	DNS Options (press next)<br>
4.	Additional Options: NetBIOS domain name: LEAFVILLAGE (autofilled)<br>
5.	Paths (press next)<br>
6.	Review Options (press next)<br>
7.	Prerequisites Check -> Install<br>
8.	It should restart once completed<br>
![image](https://github.com/user-attachments/assets/92ad704b-201c-4e48-b3b7-f6e8ae3cce9b)

### 4. Set up a new Windows10 Enterprise account
During this time, finish the setup for the Windows 10 (enterprise) User1<br>
> local Name: Naruto<br>
> Password: *********<br>
> •	Join Domain<br>
> •	Complete account setup <br>
> •	No Cortana or additional services for Windows collecting data<br>
> •	Rename PC (we chose 9Tails)<br>

Once the Server 2016 instance restarts, go to the Server Manager Dashboard > top right > “Tools” > “Active Directory Users and Computers”<br>
![image](https://github.com/user-attachments/assets/59564e9e-bc78-4072-9cec-f1531a522932)

Under leafvillage.local tree > Domain Controllers, confirm that the PC (Workstation1) is the Domain Controller.

### 5. Create and Add a New User into the Domain
Select “Users”, right click an empty space User group > New > User. <br>
![image](https://github.com/user-attachments/assets/5eb18002-dc53-473d-a66e-57315c3d853f)

Create new user of desired name and password 
> Note: we can choose to set the password to not expire because it’s a test environment<br>
![image](https://github.com/user-attachments/assets/5580e898-a239-4b81-9bc6-83278cfc8201)

Now we go on the Windows10 user account and join the Domain.
1.	Navigate to the search bar and type “Domain” 
2.	Select “Access work or school”
3.	Select “Connect”

![image](https://github.com/user-attachments/assets/f20e559b-437e-48d8-9bbc-6be07c2e667b)

Select “Join this device to a local / Active Directory Domain”
> It should say unable to join
- In order to fix this, we first find the IPv4 address of the Server 2016 local machine, and then use it as the DNS IPv4 on the Windows2010 user.

We can do in 3 different ways:
> 1. Command line: go to the Server2016 window > go to command line (cmd) > type in the command “ipconfig” > locate IPv4 address
> or 
> 2. Right click “Network” icon on bottom right > “Open Network and sharing options > click on local machine name (leafvillage.local) > IPv4 is listed
> 3. Go to Windows10 User > Network and Sharing Center > Ethernet > properties > double-click on TCP/IPv4 

![image](https://github.com/user-attachments/assets/7ae93486-3c71-4f74-9ddf-d5b81ccf5220)

Use the IPv4 address found and input it under “Use the following DNS server address. Alternate DNS server: 8.8.8.8 > press okay on all window prompts
![image](https://github.com/user-attachments/assets/48e52a82-8ec4-4586-891e-bef7c79c6d94)

1.	Now still on Windows10 user, navigate back to the “Access work or school” page and input the name of the local machine (in this case leafvillage.local).
2.	It should now give you permission to access the DNS
3.	Login was Nuzumaki, password: ********
![image](https://github.com/user-attachments/assets/68b9b261-3ec9-4e83-aa5d-51df9725f272)
![image](https://github.com/user-attachments/assets/3724dcf1-0d8f-4759-b08e-de3ea8552193)
> Standard user > Next > Restart

If successful, you’ll see the account is now under the Domain Name! 
![image](https://github.com/user-attachments/assets/a97dbbba-d015-4e7f-8994-5c47b4e03d8c)

Following all these steps, we’ve successfully:
1. Set up Windows Server 2016 in a VM environment
2. Set up Windows 10 Enterprise in a VM environment
3. Created and set up Windows Active Directory on Windows Server 2016
4. Set up DNS and made the Active Directory a Domain Controller
5. Set up a new Windows10 Enterprise account
6. Added a new User into the Domain
8. Set the account up with standard permissions and successfully logged into the local Domain
