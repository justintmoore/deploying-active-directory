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
    <img src="" height="60%" width="60%" alt="placeholder"/>
</p>
<br> 


