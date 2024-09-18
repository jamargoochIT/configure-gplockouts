<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Account Lockouts in Group Policy</h1>
This tutorial goes through configuring account lockouts in Group Policy within Azure Virtual Machines.<br /><br><br><br><br>


Configureing account lockouts helps prevent unauthorized access and reduces brute force attacks.<br> 
So, first up, we’ll go to the Windows Desktop search bar and type in Group Policy and open the app.
![30](https://github.com/user-attachments/assets/cee79cfa-ea3b-4f67-b255-afa86be487ce)<br><br><br><br>





In Group Policy Management we’ll click on Forest:mydomain.com -> Domains -> mydomain.com -> Default Domain Policy.
The default Domain Policy is already attached to the domain, we’re going to edit it.
Right-click on Default Domain Policy and select Edit.

![46](https://github.com/user-attachments/assets/01c7237e-f5d5-4869-ade3-cfeb247def29)<br><br><br><br>




In the Group Policy Management Editor window, we’ll go to Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Polices -> Account Lockout Policy.
In the adjacent window titled Policy, here is where we’ll edit the settings. 

![47](https://github.com/user-attachments/assets/7c386727-a4b0-4f6f-b531-f328a506b248)<br><br><br><br>




Here we can change the what we need by clicking on a setting and checking the box marked define this policy setting. 
The last setting: Reset Account Lockout Counter After, will reset the account lockout attempt counter if they wait a specific amount of time, for example if this setting is set to 5 minutes and they have a lockout threshold of 3 (how many failed attempts before the user gets locked out.) and they fail 2 lockouts, then they wait 5 minutes, the user will have 3 more failed attempts again instead of having only 1 left.<br>

![48](https://github.com/user-attachments/assets/389cd282-22ec-42e4-b40a-397ba0996c86)

![49](https://github.com/user-attachments/assets/931bc540-ffdc-4504-b592-6b481838e687)<br><br><br><br>



Click apply and then OK.

![50](https://github.com/user-attachments/assets/5f4e3f52-d8c2-4fea-b772-d8ed13f4ea42)<br><br><br><br>



After we’ve adjusted each setting to our needs, we need to go to the Windows Search Bar and type in PowerShell.
![30](https://github.com/user-attachments/assets/da937aed-35a6-4187-b1a0-2be54df6def6)<br><br><br><br>



In PowerShell, we’ll type gpupdate /force.
![51](https://github.com/user-attachments/assets/a937b0a1-b8cc-484a-91f9-1d49fa34e368)<br>


When it’s finished it will say the policy has been updated successfully.
The changes to the policy we’ve made will be applied automatically around every 90 minutes. But using this command will update the policy immediately.
<br><br><br><br>

We can test if the policy we adjusted works by failing to log-in fail to log in as one of our users.
After six failed log-in attempts we’ll get this message.<br>
![52](https://github.com/user-attachments/assets/b37b8385-3da4-4195-8aec-b4d037657888)<br><br><br><br>



To unlock the users account, we’ll need to be logged into DC-1. We’ll need to open Active Directory Users and Computers, and then go to the Employees OU in the mydomain forest.

![53](https://github.com/user-attachments/assets/3a191a56-ea21-4f59-9b84-378a66f5b554)<br><br><br><br>




We’ll right-click on the user whose account has been locked and select properties. We’ll click on the Account tab, then check the box next to where it says unlock account, then click Apply and then OK.

![54](https://github.com/user-attachments/assets/ad81a4aa-f5b1-4b3e-95d7-48e290c91481)<br><br><br><br>




After that we can right-click on the users account and select reset password.

![55](https://github.com/user-attachments/assets/4bf5df08-baf1-4e8b-9a0e-4ea1c300fe0c)<br><br><br><br>




You can set the password to what we like, and choose whether or not it’s required for the user to change their password after their first log-in. 
After that click OK.<br><br>

You can also right-click on the user and select disable or enable their account.<br><br>

And that’s it, we’re all done.

