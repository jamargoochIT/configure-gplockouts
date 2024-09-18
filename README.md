<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Account Lockouts in Group Policy</h1>
This tutorial goes through configuring account lockouts in Group Policy within Azure Virtual Machines.<br /><br><br><br><br>


Configureing account lockouts helps prevent unauthorized access and reduces brute force attacks.<br> 
So, first up, we’ll go to the Windows Desktop search bar and type in Group Policy and open the app.




In Group Policy Management we’ll click on Forest:mydomain.com -> Domains -> mydomain.com -> Default Domain Policy.
The default Domain Policy is already attached to the domain, we’re going to edit it.
Right-click on Default Domain Policy and select Edit.

Image 46 


In the Group Policy Management Editor window, we’ll go to Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Polices -> Account Lockout Policy.
In the adjacent window titled Policy, here is where we’ll edit the settings. 

Image 47 


Here we can change the what we need by clicking on a setting and checking the box marked define this policy setting. 
The last setting: Reset Account Lockout Counter After, will reset the account lockout attempt counter if they wait a specific amount of time, for example if this setting is set to 5 minutes and they have a lockout threshold of 3 (how many failed attempts before the user gets locked out.) and they fail 2 lockouts, then they wait 5 minutes, the user will have 3 more failed attempts again instead of having only 1 left.

Image 48 

Image 49  

Click apply and then OK.

Image 50 


After we’ve adjusted each setting to our needs, we need to go to the Windows Search Bar and type in PowerShell.
Image 30 


In PowerShell, we’ll type gpupdate /force.
Image 51  

When it’s finished it will say the policy has been updated successfully.
The changes to the policy we’ve made will be applied automatically around every 90 minutes. But using this command will update the policy immediately.
And that’s it.

We can test if the policy we adjusted works by failing to log-in fail to log in as one of our users.
After six failed log-in attempts we’ll get this message.
Image 52 

To unlock the users account, we’ll need to be logged into DC-1. We’ll need to open Active Directory Users and Computers, and then go to the Employees OU in the mydomain forest.

Image 53 


We’ll right-click on the user whose account has been locked and select properties. We’ll click on the Account tab, then check the box next to where it says unlock account, then click Apply and then OK.

Image 54 


After that we can right-click on the users account and select reset password.

Image 55 


You can set the password to what we like, and choose whether or not it’s required for the user to change their password after their first log-in. 
After that click OK.

You can also right-click on the user and select disable or enable their account.

And that’s it, we’re all done.

