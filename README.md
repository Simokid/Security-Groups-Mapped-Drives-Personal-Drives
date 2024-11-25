<h1>Overview: Lab 7 Security Groups, Mapped Drives, Personal Drives</h1>

This section of my home lab documentation focuses on managing **Security Groups**, **Mapped Drives**, and **Personal Drives** in a domain environment. The project demonstrates how to create and configure security groups for managing permissions, set up mapped drives for network access, and configure personal drives for user-specific storage. 

<h2>Objectives</h2>

- Create and configure **Security Groups** in Active Directory to manage access to resources and network drives.
- Set up **Mapped Drives** to enable users to access shared resources across the network automatically.
- Configure **Personal Drives** for individual users to store data securely in the domain environment.
- Implement best practices for **permission management** using security groups and ensuring appropriate access control for mapped and personal drives.


<h2>Documentation</h2>

In this home lab, we will focus on implementing **Security Groups**, **Mapped Drives**, **Personal Drives**, and **Drive Letter Mapping**. Let’s start by opening **Server Manager** on our **Windows Server 2022**. Then, select **File and Storage Services** on the left-hand side, followed by **Shares**. Right-click and select **New Share**.




1. <p align="center">
   <img src="https://i.imgur.com/OXZLtA2.png" height="100%" width="100%" alt="Disk Sanitization Steps 1"/>
   <br />
   <br />
</p>

Click Next until you reach the Specify Share Name screen. Name the share HR, then continue selecting Next until you reach the Create button. Click Create to finish setting up the shared folder.

2. <p align="center">
   <img src="https://i.imgur.com/FpY54MH.png" height="100%" width="100%" alt="Disk Sanitization Steps 2"/>
   <br />
   <br />
</p>

Repeat the process, but this time name the share Personal. Select Next, then click Create to complete the setup for the second shared folder.

3. <p align="center">
   <img src="https://i.imgur.com/fkZJgVW.png" height="100%" width="100%" alt="Disk Sanitization Steps 3"/>
   <br />
   <br />
</p>

Now that we have our shared folders, open File Explorer → This PC → Local C Drive → Shares to access the shared folders.

4. <p align="center">
   <img src="https://i.imgur.com/KiHvsmG.png" height="100%" width="100%" alt="Disk Sanitization Steps 4"/>
   <br />
   <br />
</p>

Now, go to Active Directory Users and Computers → right-click on Users → select New → then click Group to create a new security group.

5. <p align="center">
   <img src="https://i.imgur.com/HePii5u.png" height="100%" width="100%" alt="Disk Sanitization Steps 5"/>
   <br />
   <br />
</p>

Name the group name “HR”.

6. <p align="center">
   <img src="https://i.imgur.com/8fJMHuA.png" height="100%" width="100%" alt="Disk Sanitization Steps 6"/>
   <br />
   <br />
</p>

Now lets double click on “HR” → select “Managed By” → “Change” then enter “Helpdesk”. 

7. <p align="center">
   <img src="https://i.imgur.com/yGRCS6Z.png" height="100%" width="100%" alt="Disk Sanitization Steps 7"/>
   <br />
   <br />
</p>

We will create another group the same way and call it “Personal” and have it managed by Helpdesk as well. 

8. <p align="center">
   <img src="https://i.imgur.com/Ks0PqDY.png" height="100%" width="100%" alt="Disk Sanitization Steps 8"/>
   <br />
   <br />
</p>

Now, go back to the shared folders. Right-click on Personal → select Properties, then navigate to the Sharing tab. Highlight the path \\SERVER2022\Personal, right-click, and select Copy. Then, paste this path into the Description field of the Personal properties in Active Directory Users and Computers.


9. <p align="center">
   <img src="https://i.imgur.com/9AF8KqY.png" height="100%" width="100%" alt="Disk Sanitization Steps 9"/>
   <br />
   <br />
</p>

s

10. <p align="center">
   <img src="https://i.imgur.com/OJoHw28.png" height="100%" width="100%" alt="Disk Sanitization Steps 10"/>
   <br />
   <br />
</p>

Repeat the process for the HR share folder. Once that’s done, open the HR group in Active Directory Users and Computers and click on the Members tab. Select Add, then search for and add Bob to the group.

11. <p align="center">
   <img src="https://i.imgur.com/ziWccE1.png" height="100%" width="100%" alt="Disk Sanitization Steps 11"/>
   <br />
   <br />
</p>

Repeat the process for the Personal share folder. Open the Personal group in Active Directory Users and Computers, click on the Members tab, select Add, and then add Bob to the group.

12. <p align="center">
   <img src="https://i.imgur.com/Qtvj8h1.png" height="100%" width="100%" alt="Disk Sanitization Steps 12"/>
   <br />
   <br />
</p>

To verify, select the HR organizational unit in the domain, then double-click on Bob. Next, go to the Member Of tab to confirm that Bob is a member of the HR group.

13. <p align="center">
   <img src="https://i.imgur.com/mRPy4c8.png" height="100%" width="100%" alt="Disk Sanitization Steps 13"/>
   <br />
   <br />
</p>

Now, we will focus on configuring the correct permissions. To do this, navigate to the Personal share folder, right-click on it, and select Properties. In the Security tab, click on Advanced, then select Disable Inheritance.

14. <p align="center">
   <img src="https://i.imgur.com/eVDaGjC.png" height="100%" width="100%" alt="Disk Sanitization Steps 14"/>
   <br />
   <br />
</p>

Select the first option “Covert inherited permissions…”

15. <p align="center">
   <img src="https://i.imgur.com/zy73RaK.png" height="100%" width="100%" alt="Disk Sanitization Steps 15"/>
   <br />
   <br />
</p>

Now remove both “Users”. This removes any users who do not have access to this personal folder. 

16. <p align="center">
   <img src="https://i.imgur.com/keMDWwm.png" height="100%" width="100%" alt="Disk Sanitization Steps 16"/>
   <br />
   <br />
</p>

Click Add, then select Select a principal. Add the Helpdesk group and assign the Modify permission under the basic permissions section.

17. <p align="center">
   <img src="https://i.imgur.com/TzRV84B.png" height="100%" width="100%" alt="Disk Sanitization Steps 17"/>
   <br />
   <br />
</p>

Repeat the process and add the Personal group, ensuring the Modify permission is enabled under the basic permissions section.

18. <p align="center">
   <img src="https://i.imgur.com/2vYLhuj.png" height="100%" width="100%" alt="Disk Sanitization Steps 18"/>
   <br />
   <br />
</p>

Now, in the Personal folder properties, navigate to the Sharing tab → select Share... → right-click on Personal → choose Read/Write, then click Share.

19. <p align="center">
   <img src="https://i.imgur.com/AMYnfmj.png" height="100%" width="100%" alt="Disk Sanitization Steps 19"/>
   <br />
   <br />
</p>

Now, repeat the process on the **HR** folder:

1. Right-click on **HR** → select the **Security** tab → click **Advanced**.
2. Select **Disable Inheritance** → choose **Convert inherited permissions...**.
3. Delete the two **Users** permissions.
4. Click **Add**, then **Select a Principal**, and add **Helpdesk**.
5. Enable **Modify** for basic permissions.
6. Click **OK**, then **Apply**.


20. <p align="center">
   <img src="https://i.imgur.com/5WafDvo.png" height="100%" width="100%" alt="Disk Sanitization Steps 20"/>
   <br />
   <br />
</p>

Now, let's repeat the same process for the **HR** folder:

1. Right-click on **HR** → select the **Security** tab → click **Advanced**.
2. Click **Add**, then **Select a Principal**, and add **HR**.
3. Enable **Modify** for basic permissions.
4. Click **OK**, then **Apply**.

This will allow **HR** group members to access the HR shared folder with the proper permissions.

21. <p align="center">
   <img src="https://i.imgur.com/Jjiz5LG.png" height="100%" width="100%" alt="Disk Sanitization Steps 21"/>
   <br />
   <br />
</p>

To ensure the **HR** group can "Read/Write" in the sharing properties, follow these steps:

1. Right-click on the **HR** folder.
2. Select **Properties** and go to the **Sharing** tab.
3. Click **Share…**.
4. In the **Network Access** window, ensure **HR** is listed.
5. Right-click on **HR** and select **Read/Write**.
6. Click **Share** to confirm the settings.

This ensures that members of the **HR** group have the correct permissions to both read and write to the HR shared folder.

22. <p align="center">
   <img src="https://i.imgur.com/fhedpHg.png" height="100%" width="100%" alt="Disk Sanitization Steps 22"/>
   <br />
   <br />
</p>

To check Bob's access to the **HR** folder on Desktop2:

1. Log in as **Bob** on the **Desktop2** account.
2. Open **File Explorer**.
3. In the **File Explorer** search bar, paste the following network path:`\\Server2022\HR`
4. Press **Enter** to navigate to the **HR** shared folder.

Since Bob is part of the **HR** group, he should have access to this folder. You should be able to see the contents of the **HR** folder. If you followed the permissions setup correctly, Bob should have **Read/Write** access to this folder.


23. <p align="center">
   <img src="https://i.imgur.com/r57qNEv.png" height="100%" width="100%" alt="Disk Sanitization Steps 23"/>
   <br />
   <br />
</p>

- **Copy the network path** for the HR folder: \Server2022\HR
- Right-click on **This PC** in **File Explorer** and select **Map this Network drive**.
- In the **Map Network Drive** window:
    - **Drive letter**: Choose a drive letter, such as **Z:**
    - **Folder**: Paste the network path \Server2022\HR into the folder field.
- Check the box for **Reconnect at sign-in** if you want the drive to be remapped automatically on login.
- Click **Finish**.

24. <p align="center">
   <img src="https://i.imgur.com/tc1f5hD.png" height="100%" width="100%" alt="Disk Sanitization Steps 24"/>
   <br />
   <br />
</p>

s

25. <p align="center">
   <img src="https://i.imgur.com/gr61oSK.png" height="100%" width="100%" alt="Disk Sanitization Steps 25"/>
   <br />
   <br />
</p>

Another method to map a personal drive is by accessing your Windows Server 2022 account, copying the network path from the "Personal Properties" section in the shared folders.

26. <p align="center">
   <img src="https://i.imgur.com/5ZRXcuV.png" height="100%" width="100%" alt="Disk Sanitization Steps 26"/>
   <br />
   <br />
</p>

Next, open Active Directory Users and Computers, search for "Bob," right-click on his name, and select "Properties." Then, go to the "Profile" tab and under "Home Folder," choose "Connect" and set the drive letter to P:. Paste the network path for the drive: \SERVER2022\Personal%username% (make sure to include "%username%"). Finally, click "Apply." This will create a personal folder within Bob's directory.

27. <p align="center">
   <img src="https://i.imgur.com/HB65kT2.png" height="100%" width="100%" alt="Disk Sanitization Steps 27"/>
   <br />
   <br />
</p>

Once we log into Desktop2 as Bob, we will see that both the Personal and HR drives are mapped.

28. <p align="center">
   <img src="https://i.imgur.com/7FnDcol.png" height="100%" width="100%" alt="Disk Sanitization Steps 28"/>
   <br />
   <br />
</p>

Congratulations we have successfully configured on how to implement Security Groups, Map Drives, Personal Drives and Map Letter.

Next Lab 8 : Windows 10 Remote Access: Remote Desktop, Remote Registry



