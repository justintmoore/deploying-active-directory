<p align="center">
    <img src="https://i.imgur.com/8EzPyDZ.png" alt=osTicket logo"/>  
    
    
## Tools, Utilities, Services Used
- Microsoft Azure <br>
- Remote Desktop <br>

## Environments Used
- Windows 10 <br>
- Windows Server 2022
- Active Directory  
  

## Program Walkthrough
<p align="center">
    Objective: This lab is working on the premise that we have already created our client and domain controller as instructed in the previous lab. In this lab we will go in and install Active Directory. We will also be creating an Administrator account and a normal User account within AD. After we will join our client VM, to our domain, as well as setup RDP for non-administrative users on on client VM. Lastly we will create a bunch of additional users using a powershell script and attempt to log into our client VM with one of the users. We may even reset a random users password and attempt to login with them.
</p>
<br>

<p align="center">
   First we will remote desktop into our domain controller, click the windows icon at the bottom and open up Server Manager. 
</p>

<p align="center">
    <img src="https://i.imgur.com/F2NCTYy.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br> 

<p align="center">
  Select Add roles and features. Click next, then next. For Server Selection, there should be only one option from the server pool, select that and click next.
</p>

<p align="center">
    <img src="https://i.imgur.com/RNL89Ks.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br> 

<p align="center">
  For Server Roles, select Active Directory Domain Services. 
</p>

<p align="center">
    <img src="https://i.imgur.com/TTyh3I1.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br> 

<p align="center">
  A window will pop up, say yes to adding management tools. Click next until you reach Confirmation. Select Restart if Required and then Install
</p>

<p align="center">
    <img src="https://i.imgur.com/GJCi6Qo.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br> 

<p align="center">
  Next step is promoting our Domain Controller server to become the Root Server within Active Directory. By becoming the Root Server we can officially call this the Domain Controller of AD. 
</p>
<br>

<p align="center">
  This action of promoting our server to Domain Controller, creates something called a "forest". A forest is a container of sort, that all other domains live in. The domains within the forest inherit rules and schema from the Root Server(DC).
</p>
<br>

<p align="center">
  ** I should also mention for future knowledge that the Domain Controller essentially controls everything in the forest. We can have multiple Domain Controllers, for redundancy that mirror our Root Server Domain Controller. But ultimately our first Domain Controller runs the show.
</p>

<p align="center">
  If we go to our Domain Controller VM that I will call "DC", open up Server Manager, you can see a flag in the right hand corner. Click it, and select the link, Promote this server to a domain controller.
</p>

<p align="center">
    <img src="https://i.imgur.com/DFf0FOP.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  In Deployment Configuration, select Add a new forest. In Domain Controller Options create the domain name MYDOMAIN.com. Select Next until you get to installation, and install! (This could take a while!) After AD installs, it will automatically restart.
</p>
<br>

<p align="center">
  After it restarts we will log back in to our DC VM. There is a difference in the way we log on. Since it's been turned into a DC with a domain, we must specify the domain. Username should  <domainname>\<username>, and the password will be as it always was.
</p>

<p align="center">
    <img src="https://i.imgur.com/OzPNLpi.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  Now that we are logged back on, next on the agenda is to create a Domain Administrator within the domain on our Domain Controller "dc-1". Go to your taksk search bar at the bottom and type "active directory". There should be a application called Active Directory Users and Computers, click that.
</p>

<p align="center">
    <img src="https://i.imgur.com/uyPqwXO.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  Maximize the screen. on the left side of the screen you will see a direcory names "mydomain.com". Right click "mydomain.com", expand "new", and select Organizational Unit. Make sure for these next steps you don't mess them up.
</p>

<p align="center">
    <img src="https://i.imgur.com/wdisepq.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  After Selecting Organizational Unit, in the box provided type "_EMPLOYEES", don't forget the underscore. After that, we will create another one called "_ADMINS". We are creating these folders for accessibility, and ease of use later on in this lab.
</p>

<p align="center">
    <img src="https://i.imgur.com/ufYVmrb.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  Under mydomains.com right click the _ADMIN, go to new, and click User. We will create the Admin user as Jane Doe. Uncheck all boxes, leaving "password never expires" before submitting, and then press next then finish. Just because we added this user to a folder named _ADMIN doesn't make it an Admin account. We must add this user to the Domain Admins Security group.
</p>

<p align="center">
    <img src="https://i.imgur.com/xnsnBUX.png" height="60%" width="60%" alt="placeholder"/>
</p>
<p align="center">
    <img src="https://i.imgur.com/HTfCWPS.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  To add our Jane Doe user to our Domain Admins Security group we can right click Jane Doe, and select properties. Once inside of properties, we will choose the "Member of" domain -> Add.. ->
</p>

<p align="center">
    <img src="https://i.imgur.com/x5gLRjs.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  Inside of Select Groups, we will enter the object name: "Domain Admins", and click Check names. Now that we've completed that, apply changes and click ok. We will now log out/ close connection to dc-1 VM, and log back in as "mydomain.com\jane_admin".
</p>

<p align="center">
    <img src="https://i.imgur.com/uCEbZQ4.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
  Again when we loging our username will now be: <domainname>\<username>, in this case it will be mydomain\jane_admin. The password is whatever you set it to prior. Once logged in we can open up powershell and you'll see the username jane_admin in the prompt. You can also run the command "whoami" to see which user you are currently logged in as.
</p>

<p align="center">
    <img src="https://i.imgur.com/C43UwJt.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    Now that we are logged on, we are going to join client-1 VM, to the domain. Lets start by logging into our client-1 VM. In the task search bar below type "about" and open up about "About your PC". On the right side, you will see a link "Rename this PC (Advanced)".
</p>

<p align="center">
    <img src="https://i.imgur.com/bUSHN3V.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    Under the "Computer Name" tab -> click "Change" -> Go to Member -> Switch from Workgroup to Domain -> Enter your Domain Name. In our case it is mydomain.com. After click ok. 
</p>
<br>
<p>
    The only way this works is by having our Domain Controller configured as our DNS server for our client-1 VM.mydomain
</p>

<p align="center">
    <img src="https://i.imgur.com/J09kq6c.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    You will now be prompted to enter your admin credentials. You should receive a popup welcoming you to the domain! Client-1 VM will restart automatically. After it restarts you will have to Remote back in using RDP.
</p>

<p align="center">
    <img src="https://i.imgur.com/WtvBrvm.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    After you log back on, go to active directory users and computers -> click mydomain.com -> Computers -> You should see client-1. If you right click and select properties we can see a number of things. One of these if LAPS or Local Administration Password Solution. This allows you receive a unique randomized password, that you can use to login locally as the administrator.
</p>

<p align="center">
    <img src="https://i.imgur.com/oKz9GpR.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
   We have 2 more things to do before we end this lab. First we are going to configure RDP for non admin users on client-1 VM. Second, we will creat a bunch of additional users and attempt to log into client-1 with one of the users. Currently we should sign out of our current labuser on client-1 and sign in as jane_admin.
</p>
<br>
<p align="center">
 Once logged on we will...Right click Windows Icon -> System -> Remote Desktop -> User Accounts: Select users that can remotely access this pc -> Add -> Enter Object name "Domain Users", click Check Names -> Click Ok. In this instance, Domain Users represents everyone on the domain, so everyone on the domain will have access to Remote Desktop.
</p>

<p align="center">
    <img src="https://i.imgur.com/GKYXSVK.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
 Lastly, utilizing PowerShell ISE, we will be write a script that will create additional users on AD. To start we will log into dc-1, and open up PoerShell ISE as a administrator. 
</p>

<p align="center">
    <img src="https://i.imgur.com/dzZbgYs.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    Now that we have that open, Click this link, copy the raw file, and paste into PowerShell ISE. 
</p>
<br>
<p align="center">
     <b><a href="https://github.com/justintmoore/deploying-active-directory/blob/main/create-names-ps1">PowerShell: Name-Generator</a>.<b/>
    <br>
    Disclaimer: I take no credit for the script written.
</p>
<br>
         
<p align="center">
    Once we past the script into PowerShell, click the Run button on the top.
</p>

<p align="center">
    <img src="https://i.imgur.com/Cw0ZGgt.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    Once we past the script into PowerShell, click the Run button on the top. These names will just be a combination of random letters, but they will consist of a first name, and a last name. In the script you will notice that all passwords are "Password1". After Users are created, take note of any username, and we will attempt to login using that user.
</p>

<p align="center">
    <img src="https://i.imgur.com/5elLyUj.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    To test out one of these users, we will go back to Active Directory Users and Computers on our dc-1 VM. Under mydomain.com, click _EMPLOYEES. If you don't see any users, right click mydomain.com and select refresh. Choose a user at random, under general you will see their Display Name, which will be there username. 
</p>

<p align="center">
    <img src="https://i.imgur.com/GxSpcve.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    We will log out of our client-1 VM, and login as our user. Remember because we are part of the domain "mydomain.com", we must express that in our username.
</p>

<p align="center">
    <img src="https://i.imgur.com/MU3Hu2a.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

<p align="center">
    We have successfully logged in as another user. That ends this portion of the lab. 
</p>

<p align="center">
    <img src="https://i.imgur.com/p28Obeu.png" height="60%" width="60%" alt="placeholder"/>
</p>
<br>

## Lessons Learned
<p align="center">
    I learned a ton of great knoowledge here. Information Technology is a broad field, and for those of us interested in cybersecurity must understand that this is just a subfield of Information Technology. The basics of IT, lay the foundation for our career. How can we secure something, we don't understand, even at a theory level. In this lab I learned about Windows Server 22 and how how to install Active Directory. I got hands on experience on promoting a regular sever into a Root Server, creating a forest. I learned that a forest acts as a conrainer for sublevel domains, and how the Root Server acts as Top Level domain within that forest. I also learned about Organization Unites, and see them as folders within our domain that holds users, devices, and other rescources. I was able to get some practical exerience on AD onfigurations, and learned that PowerShell is a powerful tool that I need to learn!
</p>
<br>
<p align="center">
    <strong>The Marathon Continues!</strong>
</p>
