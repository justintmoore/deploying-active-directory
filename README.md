<p align="center">
    <img src="https://i.imgur.com/8EzPyDZ.png" alt=osTicket logo"/>  
    
    
## Tools, Utilities, Services Used
- Microsoft Azure <br>
- Remote Desktop <br>

## Environments Used
- Windows 10 <br>
- Windows Server 2022
  

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
  
</p>

