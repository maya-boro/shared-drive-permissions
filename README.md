<p align="center">
<img src="https://i.imgur.com/ISCHHkF.png" height="20%" width="20%" alt="Shared Files Photo"/>
</p>

<h1>Shared Drive Permissions and the New Technology File System (NTFS)</h1>
This tutorial explains how to set up Shared Drive Permissions with the New Technology File System (NTFS).<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used</h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Steps</h2>

- Configure resources in Azure 
- Install Active Directory
- Connect the client to the domain controller 
- In Server Manager, create a shared drive folder.
- Create three department folders within the shared drive folder.
- In Active Directory, create three user accounts and add department titles.
- Setup file permissions for each department folder.
- Confirm that permissions have been set and map a drive under each user account. 

<h2>Setting Up Permissions</h2>

<p>
For this tutorial, there will be two virtual machines utilized. The first virtual machine (DC-1) will run Windows Server 2022 as its base operating system. The second virtual machine (Client-1) will run Windows 10 as its base operating system. Both virtual machines will be under the same resource group and virtual network (Vnet). This can be confirmed by viewing the topology available under Network Watcher in Azure. On the first virtual machine, a domain controller will be set up under the name "mydomain.com," and then the second virtual machine (Client-1) will be added to the domain "mydomain.com." The set-up for this is shown here:<h3><a href="https://github.com/maya-boro/configure-ad">Configuring Active Directory within Azure VMs</a></h3>
</p>

<p>
Once the two virtual machines are set up, we will create a shared drive folder by going to the server manager dashboard and selecting "Files and Storage Services" from the menu on the left-hand side. Then select "Shares," and under the shares option, right-click and select "New Share." The "New Share Wizard" will launch, and you will be prompted to select the profile for the new shared drive folder from the pop-up window. Choose "SMB-Share Quick." Click through the next prompt, and once you are prompted to enter a name for the new shared drive folder, enter "mydomain," and then continue to click "next" until you reach the confirmation section, where you will need to click "create" to allow the shared drive folder to be created.
</p>
<p>
<img src="https://i.imgur.com/FL1cQzY.png" height="70%" width="70%" alt="Create New Shared Drive Folder"/>
</p>
<br />

<p>
To confirm that the shared drive folder has been created, go to File Explorer, and select "This PC" from the left-hand side menu, and then select the C: drive. In the C: drive, click on the "Shares" folder, where you will find the shared drive folder "my domain." Right click on the "my domain" folder and select "Properties." Go to the "Sharing" tab and you will find the Network Folder Path, which is \\DC-1\mydomain.
</p>
<p>
<img src="https://i.imgur.com/bLw4N5h.png" height="70%" width="70%" alt="Confirm New Shared Drive Folder Created"/>
</p>
<br />

<p>
Now we will need to create three new folders within the "my domain" shared drive folder by clicking on the "mydomain" folder, then right-clicking and selecting "New Folder," and entering the folder name "Sales" for the first folder. After the "Sales" folder is created, create two additional folders, one named "HR" and another named "Finance."
</p>
<p>
<img src="https://i.imgur.com/tpuz5uN.png" height="70%" width="70%" alt="Creating Department Folders"/>
</p>
<br />

<p>
After that, we will create three new users by opening the server manager, going to "Tools" in the upper right-hand corner, and selecting "Active Directory Users and Computers." From the pop-up window, under mydomain.com on the left-hand side, right-click the "Users" folder and select "New" and then select "User." A new pop-up window will open where you will need to enter the first user account’s information for the user "Bob Smith" with a user login name of "bsmith." After the first user is created, create two other users, one named "Billy Barnes" with a user logon name of "bbarnes" and another named "Holly Cross" with a user logon name of "hcross."
</p>
<p>
<img src="https://i.imgur.com/y99Qg89.png" height="70%" width="70%" alt="Creating New Users"/>
</p>
<br />

<p>
Now we will add the department titles for each of the new user accounts by double clicking on each of the users and selecting the "Organization" tab from the pop-up window and adding the department title under the proper section of the form. Bob Smith’s department title is "Sales." Billy Barnes' department title is "HR," and Holly Cross' department title is "Finance."
</p>
<p>
<img src="https://i.imgur.com/nkenJdJ.png" height="70%" width="70%" alt="Adding User Department Titles"/>
</p>
<br />

<p>
Now we will set file permissions for the three folders created within the "mydomain" shared drive folder. Starting with the "Sales" folder, right-click the folder and select "Properties," and then from the pop-up window, select the "Security" tab followed by the "Advanced" button. Once in the advanced settings, select the "Add" button.
</p>
<p>
<img src="https://i.imgur.com/kvqpzxO.png" height="70%" width="70%" alt="Setting File Permissions Part One"/>
</p>
<br />

<p>
After selecting the "Add" button, within the advanced settings, the "Permission Entry" window will open. Within this window, click on "Select a principal" and enter the name "Bob Smith" within the "Enter the object name to select" box, and then click the "OK" button. Once this is complete, select "Modify" from the "Basic Permissions" list and click the "OK" button.
</p>
<p>
<img src="https://i.imgur.com/wmqbUTt.png" height="70%" width="70%" alt="Setting File Permissions Part Two"/>
</p>
<br />

<p>
Now within the advanced settings, click on "Disable inheritance" and from the pop-up window, select "Convert inherited permissions into explicit permissions on this object." Then under "Permission entries" in the advanced settings, select "Users" from the list and click "Remove." You will also need to remove "Authenticated Users" from the permissions entries list. Complete the same steps to set up permissions for the "HR" and "Finance" folders. The user account under "Billy Barnes" will need permission for the "HR" folder, and the user account under "Holly Cross" will need permission for the "Finance" folder.
</p>
<p>
<img src="https://i.imgur.com/mBOsJlw.png" height="70%" width="70%" alt="Setting File Permissions Part Part Three"/>
</p>
<br />

<p>
Now we will check to confirm that the permissions were set and map a drive under each user account for the assigned department folder. Log into the user account under Bob Smith. Go to File Explorer, enter \\dc-1 in the top bar, and then select the shared drive folder "my domain." You will not be able to access the "HR" or "Finance" folders. You will only be able to access the "Sales" folder. Click on the "Sales" folder, then right-click and select "New," then click on "Text Document" and name the document "bobsmith."
</p>
<p>
<img src="https://i.imgur.com/t3qaoDm.png" height="70%" width="70%" alt="Bob Smith Account"/>
</p>
<br />

<p>
Copy the network path from the top bar, right-click on "This PC," and select "Map network drive." Within the pop-up window, enter the network path for the "Sales" folder and click the "Finish" button. Close and re-open File Explorer, then click on "This PC," and you will find the Z: drive for the "Sales" folder.
</p>
<p>
<img src="https://i.imgur.com/WL6rjXv.png" height="70%" width="70%" alt="Map Sales Drive"/>
</p>
<br />

<p>
Now log into the user account under Billy Barnes. Go to File Explorer, enter \\dc-1 in the top bar, and then select the shared drive folder "my domain." You will not be able to access the "Sales" or "Finance" folders. You will only be able to access the "HR" folder. Click on the "HR" folder, then right-click and select "New," then click on "Text Document" and name the document "billybarnes."
</p>
<p>
<img src="https://i.imgur.com/P7zmFhS.png" height="70%" width="70%" alt="Billy Barnes Account"/>
</p>
<br />

<p>
Copy the network path from the top bar, right-click on "This PC," and select "Map network drive." Within the pop-up window, enter the network path for the "HR" folder and click the "Finish" button. Close and re-open File Explorer, then click on "This PC," and you will find the Z: drive for the "HR" folder.
</p>
<p>
<img src="https://i.imgur.com/nKv7wLT.png" height="70%" width="70%" alt="Map HR Drive"/>
</p>
<br />

<p>
Now log into the user account under Holly Cross. Go to File Explorer, enter \\dc-1 in the top bar, and then select the shared drive folder "my domain." You will not be able to access the "HR" or "Sales" folders. You will only be able to access the "Finance" folder. Click on the "Finance" folder, then right-click and select "New," then click on "Text Document" and name the document "hollycross."
</p>
<p>
<img src="https://i.imgur.com/famWhxo.png" height="70%" width="70%" alt="Holly Cross Account"/>
</p>
<br />

<p>
Lastly, copy the network path from the top bar, right-click on "This PC," and select "Map network drive." Within the pop-up window, enter the network path for the "Finance" folder and click the "Finish" button. Close and re-open File Explorer, then click on "This PC," and you will find the Z: drive for the "Finance" folder.
</p>
<p>
<img src="https://i.imgur.com/mTApKLP.png" height="70%" width="70%" alt="Map Finance Drive"/>
</p>
<br />
