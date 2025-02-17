# Lab 4 – Troubleshoot Messaging Security

## Lab scenario

In the labs for this course, you're taking on the role of Adatum Corporations Messaging Administrator. You've deployed Microsoft 365 in a virtualized lab environment, and you've been tasked with completing a pilot that tests various M365 & Exchange functionalities as they relate to Adatum's business requirements.

In this lab, you'll be focusing on the features that can help you protect sensitive information in your organization and to troubleshoot any issues that may arise.

First, we'll review encrypting messages utilizing Sensitivity labels. This is an important feature that allows you to mark certain messages as containing sensitive information and then encrypt them to protect that information from unauthorized access. You'll walk through the process of creating and applying sensitivity labels, and ensure that the encryption is working properly.

Next, you'll dive into Applying sensitivity label (via RMS template) to a Mail flow Rule. This feature allows you to automatically encrypt messages that contain sensitive information by setting up a rule that applies a specific sensitivity label to messages that meet certain criteria.

Finally, you'll test the behavior of the above mail flow rule to ensure that its working as expected and that messages are being properly encrypted.

By the end of this lab, you'll have a thorough understanding of how to test and troubleshoot these features in your organization and how to protect sensitive information. These skills will be useful for any administrator or IT professional responsible for maintaining and securing a Microsoft 365 environment.

## Lab Setup

The labs in this course have been prepared for a Microsoft Exchange deployment at Adatum Corporation. Adatum is running a Microsoft 365 cloud-only deployment. The lab environments have been specifically designed in this manner to give you experience managing Microsoft Exchange in a Microsoft 365 deployment. You'll be provided with one virtual machines and a Microsoft 365 tenant to complete the lab steps.

### Sign in to the lab virtual machines

The labs in this course will use one virtual machine:

- **LON-CL1:** A stand-alone Windows 11 client virtual machine with Microsoft 365 suite of apps pre-installed.

**Note:** Lab virtual machine sign-in instructions will be provided to you by your instructor.

**Important:** The exercises in the MS-220 labs are cloud-only deployments. A local administrator account has been created on the client VMs. You'll sign-into the VMs as a local administrator instead of a domain account. Following your sign-in, the desktop will indicate that you're logged in on **LON-CL1**

### Review installed applications

Once you signed in to the VM, observe the start menu, and verify following applications have been installed:

- Microsoft Outlook

### Review Microsoft 365 tenant

Besides the single VM, you'll also be provided with a Microsoft 365 tenant with the following highlights:

- Office 365 E5 with Enterprise Mobility + Security E5.

- 15 licenses in total with 5 available of 15 (10 used).

- One Global Administrator (MOD Administrator) and 9 standard users have been pre-created.

- **Note:** Microsoft 365 sign-in instructions will be provided to you by your instructor.

- The username of the Global Administrator (MOD Administrator) is **admin@xxxxxZZZZZZ.onmicrosoft.com**.

- **xxxxxZZZZZZ.onmicrosoft.com** - This is the domain associated with the Microsoft 365 tenant that was provided by the lab hosting provider. The first part of this domain name (xxxxxZZZZZZ) is the unique tenant ID provided by the lab hosting provider. The **xxxxxZZZZZZ** portion of the tenant ID, which is the tenant suffix ID, will be unique for each student.

    **IMPORTANT:** The instructions that are provided in the lab exercise for this course are based on the new Microsoft 365 admin center UI and not the classic UI.

### Personal Email Account Setup

In this lab, you'll be partnering with another student to exchange emails with. However, If you don't have a partner, or are following the self-paced version of this course, you can exchange emails from a personal Microsoft Outlook email account (@outlook.com, @Hotmail.com, @live.com, etc.) with your tenant admin account, **admin@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the unique tenant prefix provided by your lab hosting provider).

If you don't have a Personal Microsoft Outlook email account, you can follow the steps below to configure one:

1. On **LON-CL1**, right-click the **Microsoft Edge** icon from your taskbar and select **New InPrivate Window**
2. To create a new account, navigate to the following URL: **<https://signup.live.com>**
3. On the **Create account** account window, type in a unique name followed by either **@Outlook.com** or **@Hotmail.com**( For example, **User1@Outlook.com**) and then select **Next**.
4. Once a unique email address has been accepted, you'll be prompted to **Create a password**. Enter a unique password that has at least 8 characters and contains at least two of the following: uppercase letters, lowercase letters, numbers, and symbols, and then select **Next**.

    **Important**: Before selecting **Next**, please be sure to review both the [Microsoft Services Agreement](https://www.microsoft.com/servicesagreement/default.aspx?azure-portal=true) and [Privacy and cookies statement](https://go.microsoft.com/fwlink/?LinkID=521839). By selecting **Next**, you choose to agree to Microsoft's service agreement.

5. On the **What's your name?** window, enter your full name (or if you'd prefer, fictitious information), and then select **Next**.
6. On the **What's your birthdate?** window, choose your **Country/region** and enter a **Birthdate**, then select **Next**.
7. On the **Create account** window, select **Next** and solve the generated puzzle.
8. On the **Stay signed in?** page, select **Yes**.
9. In a new **Microsoft Edge** tab, navigate to the URL: **<https://outlook.live.com/mail/>**.
10. Confirm you're able to sign-in to your new email account. Make note of your sign-in details for future lab tasks.

## Instructions

### Task 1 - Create a Sensitivity Label

In this lab task, you'll create a Sensitivity label named "Highly Confidential - Project Falcon" using the Microsoft Purview compliance portal on LON-CL1. The purpose of this label will be to encrypt emails that contain sensitive information (as part of Project Falcon) and to ensure that they're only visible to the authorized users we choose.

1. On **LON-CL1**, select **Ctrl+Alt+Delete** to sign-in. Sign-into **LON-CL1** as the local administrator account that was created by your lab hosting provider (**Administrator**) with the password **Pa55w.rd**.

2. You'll begin by accessing the **Microsoft Purview** compliance portal on **LON-CL1**. Select the **Microsoft Edge** icon from your taskbar and enter the following URL in the address bar: **<https://compliance.microsoft.com/mail/>**.

3. On the **Sign in** page, enter **admin@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider), and then enter the tenant email password provided by your lab hosting provider on the **Enter password** page. Select **Sign in**.

4. On the **Stay signed in?** window, select the **Don’t show this again** check box and then select **Yes**.

5. In the **Microsoft Purview** compliance portal, on the left-hand navigation pane, select **Information Protection**.

6. On the **Information protection** page that is displayed, select the **Labels** tab from the menu.

7. On the **Labels** page, select **+ Create a label**.

8. A **New Sensitivity Label** page should be displayed. Under **Name and create a tooltip for your label** enter the following information:

    - Name: enter **Highly Confidential - Project Falcon**

    - Display Name: enter **Highly Confidential - Project Falcon**

    - Description for users: enter **Confidential - Data is classified and protected**

    - Description for admins: leave blank

    Select **Next**.

9. On the **Define the scope for this label** page, leave the default settings enabled and select **Next**.

10. On the **Choose protection settings for labeled items** page, enable **Apply or remove encryption** and then select **Next**.

11. On the **Encryption** Page, with **Configure encryption settings** enabled, select the following options:

    - Assign permissions now or let users decide? - select **Assign permissions now**

    - User access to content expires? - select **A number of days after label is applied**

    - Access expires this many days after the label is applied - enter **30**

    - Allow offline access - select **Never**

12. While still on the **Encryption page**, Under the **Assign permissions to a specific user or groups** select the **Assign permissions** link. A new window displaying **Assign permissions** Should now be displayed on the right-hand side of the screen. Configure the following options:

    - Select **+ Add users or groups**. From the list of users that is displayed, select **MOD Administrator** & **Allan Deyoung** and then select **Add**.

    When finished, select **Save** and then select **Next**.

13. On the **Auto-labeling for filed and emails**, leave the default setting (disabled) and select **Next**.

14. On the **Define protection settings for groups and sites** page, leave the options disabled (Unchecked) and select **Next**.

15. On the **Auto-labeling for schematized data assets (preview)** page, leave the default setting (disabled) and select **Next**.

16. On the **Review your settings and finish** page, review all the configured settings. If needed, you can modify the settings by clicking the **Edit** link under the setting name. When finished reviewing the settings, select **Create label**.

    When prompted **Your sensitivity label was created**, select **Don't create a policy yet** and then select **Done**.

17. You should now be back on the **Information protection** page with the **Labels** tab selected. To assign the label we created to a policy, select the **Label policies** tab from the menu.

18. Under the **Label policies** tab, select **Global sensitivity label policy**.

19. On the new **Global sensitivity label policy** page that appears on the right-hand side of the window, select **Edit policy**.

20. A **Choose sensitivity labels to publish** page should be displayed. Under **Sensitivity labels to publish**, select the **Edit** link.

21. on the **Sensitivity labels to publish** page that appears, scroll down to the bottom and enable (Check) **Project Falcon** and then select **Add**.

22. Select **Next** on all proceeding pages until you reach **Review and finish** and then select **Submit**.

    **Note:** If you receive a **Client Error** warning stating **AddExchangeLocation and RemoveExchangeLocation parameters have same Location(s)**, select **OK** and follow the below steps.

    - On the **Review and finish** under **Publish to users and groups*, select **Edit**.

    - On the **Publish to users and groups** page, select the **Choose user or group** link.

    - Hover to the left of the **Name** heading and a check-box should appear. Select this check-box to select all users and then select **Done**

    - select **Next** on all proceeding pages until you reach **Review and finish** and then select **Submit**.

23. Once you see **Policy updated**, select **Done**.

24. Leave the **Information protection - Microsoft Purview** tab open in **Microsoft Edge** and proceed to the next task.

### Task 2 - Configure a Mail Flow Rule to Apply Office Message Encryption

In this task, you'll be implementing a new Mail flow rule to encrypt emails when "Project Falcon" is written in the subject field or body of a email. Using Mail Flow rules to automatically apply Encryption can help keep your organization secure in the event a user forgets to stamp their email correctly.

1. You should still be logged into **LON-CL1** as the **Administrator** with a password of **Pa55w.rd**; however, if the Windows sign-in page appears, then sign-in now.

2. The **Microsoft Edge** browser should still have the **Information protection - Microsoft Purview** tab open in **Microsoft Edge**. We'll now navigate to the **Exchange Admin Center** by opening a new tab in **Microsoft Edge** and navigating to the following URL: **<https://admin.exchange.microsoft.com/>**.

3. In the **Exchange Admin Center** (EAC), in the left-hand navigation pane select **Mail flow**. In the expanded menu that appears, select **Rules**.

4. On the **Rules** page, Select the **+ Add a rule** icon in the menu bar and in the drop-down menu that appears, select **Apply Office 365 Message Encryption and rights protection to messages**.

5. In the **New Transport rule** wizard that appears, under **Set rule conditions** enter **Project Falcon** in the **Name** field.

6. In the **Apply this rule if** drop-down menu, select **The subject or body**.

     A new drop-down menu will be displayed on the right. From this drop-down, select **Subject or body includes any of these words.**

7. In the **specify words or phrases** window that appears, enter **Project Falcon** in the text field and then select **Add**.

8. The word **Project Falcon** should be displayed below the text field. Once completed, select **Save**.

9. This brings you back to the **Set rule conditions** page. Under **Do the following**, next to **Rights protect message with** select the **Select one** link.

10. In the **Select RMS template** window that appears, select **Project Falcon** From the drop-down menu and then select **Save**.

11. Back on the **Set rule conditions** page, leave the **Except if** condition as the default setting, and then select **Next.**

12. In the **Set rule settings** window that appears, ensure **Rule mode** is set to **enforce**.

    Leave all other settings as default and then select **Next**.

13. In the **Review and finish** page, Verify the rule conditions and settings are correct. If corrections are needed, select **Edit rule conditions,** or **Edit rule settings** and make the necessary corrections. Once you've verified the conditions and rules are correct, select **Finish**.

    It may take up to a minute to create the rule. Once **Transport rule created successfully** is displayed, select **Done**.

14. You'll now be brought back to the **Rules** page. Notice the rule **Sensitive material** shows a status of **Disabled**.

    Select the word **Disabled** which will open up a new window for the **Sensitive material** rule settings. Under **Enable or disable rule** select the slider button so that it shows **Enabled** and then close the window by selecting **X** in the upper right-hand corner.

    **Note:** After enabling the rule, it may take up to a minute for the rule to refresh and display as enabled.

15. Leave the **Exchange Admin Center** open to the **rules** tab on the **mail flow** page and proceed to the next task.

### Task 3 - Test Office Message Encryption Behavior

In the previous task you created a new Mail flow rule to add Office Message encryption (OME) to emails with **Project Falcon** in the subject or body. You'll now test mail flow to ensure that our external partners will be able to open and view these encrypted emails as expected.

1. You should still be logged into **LON-CL1** as the **Administrator** with a password of **Pa55w.rd**; however, if the Windows sign-in page appears, then sign-in now.

2. The **Microsoft Edge** browser should still be open on the **Exchange Admin Center** tabs. We now want to open **Outlook for the Web** by opening a new tab in **Microsoft Edge** and navigating to the following URL: **<https://outlook.office.com/mail/>**.

    If prompted, Sign-in with the tenant email account provided (**admin@xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is your unique tenant prefix provided by your lab hosting provider) and the tenant password provided (Found under the resources tab in the VMs instruction pane).

3. In **Outlook on the Web** select **New mail**.

4. In the message pane that appears on the right-side of the screen, enter the following information:

    - To: Type in your partners admin email address. This email address will be similar to your admin email address (**admin@xxxxxZZZZZZ.onmicrosoft.com**) but differ slightly.  

    - Subject: enter **Project Falcon**

    - Message Body: Enter **Project Falcon Update**

    **Note:** If don't have a partner, in the "To:" line, enter your personal Microsoft Outlook email account (@Outlook.com, @live.com, @hotmail.com, etc.).

5. Select **Send**.

    **Note:** If the email doesn't arrive inside of your partners / personal inbox, open a new **Microsoft Edge** tab and enter the following URL: **<https://security.microsoft.com/quarantine?viewid=Email>**. On the **Quarantine** page find and select the check box next to your email. In the options at top of the pane that opens, select **release email**. This issue may happen as some tenants may have pre-configured quarantine rules in place.

6. You should receive an email in your inbox with the subject: **Project Falcon** from your partners admin account.

    Alternatively, if you're using a personal Microsoft Outlook email account follow the steps below before continuing:

    - Minimize your open **Microsoft Edge** browser.

    - In the Task bar, right-click **Microsoft Edge** and select **New InPrivate Window**.

    - Navigate to the following URL: **<https://outlook.office.com/mail/>**

    - Sign in using your personal Microsoft Outlook email account details.

    - Navigate to your inbox and confirm you see the email with the subject: **Project Falcon**.

7. In the message preview, double-click the email to open it in a new window. You should notice one of two possible messages displayed:

    **Message 1** - You'll see the OME wrapper container:

    ![Screenshot of Office Message Encryption wrapper email](/Images/OME_Message1.png)

    If you select **Read the message** > **Sign in with work or school account** > sign in if prompted, The message body will open and display:

    ![Screenshot of Office Message Encryption body](/Images/OME_Message1_body.png)

    **Message 2** - You'll bypass the OME wrapper container (no prompt to **read the message**) and be displayed with an insufficient permission error:

    ![Screenshot of Office Message Encryption preview](/Images/OME_Message2.png)

    **Note:** In some other scenarios there's a third possible message outcome that displays the message: **The message you tried to open is protected with Information Rights Management. The sender didn't give you the rights necessary to view the message. To open this message on behalf of another user, use Outlook. Download a free trial of Microsoft Outlook.**

    No matter how the message is displayed to you / how you open the message, if you don't have the correct permissions you'll be unable to view the message body. This is because your organization / personal Microsoft Outlook email account wasn't granted the correct permissions to view these internal encrypted emails. In the real world, if you receive one of these permission-related errors when opening up an encrypted message, it likely means that the sender will need to resend with the appropriate Label (sensitivity label) applied.

8. Keep the **Outlook** tab open in **Microsoft Edge** and proceed to the next task.

    If you're using a personal Microsoft Outlook email account, leave the **InPrivate** Microsoft Edge Browser open.

### Task 4 - Resolve an Office Message Encryption Permission Issue

In the previous task, we identified an issue where our external partners were receiving permission-related issues when attempting to open Project Falcon encrypted emails. In this lab task, you'll review the configuration settings in the "Project Falcon" Sensitivity label and modify the settings in order to allow these partners to view the emails.

1. You should still be logged into **LON-CL1** as the **Administrator** with a password of **Pa55w.rd**; however, if the Windows sign-in page appears, then sign-in now.

2. The **Microsoft Edge** browser should still have the **Information protection - Microsoft Purview** tab open in **Microsoft Edge**. If not, in a new **Microsoft Edge** tab, enter following URL in the address bar: **<https://compliance.microsoft.com/mail/>**.

     If prompted, Sign-in with the tenant email account provided (**admin@xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is your unique tenant prefix provided by your lab hosting provider) and the tenant password provided (Found under the resources tab in the VMs instruction pane).

3. In the **Microsoft Purview** compliance portal, on the left-hand navigation pane, select **Information Protection**.

4. On the **Information protection** page that is displayed, select the **Labels** tab from the menu.

5. In the List of Labels that appear, select **Project Falcon**.

6. In the **Project Falcon** details pane that appears on the right, select **Edit label**.

7. The **Edit Sensitivity Label** page should be displayed.

    With a partner, or on your own, take a few minutes review the sensitivity labels configuration and attempt to identify the configuration change needed to allow external partners to view encrypted emails sent with the **Project Falcon** label added.

    Once finished reviewing the configuration, proceed to the next steps to see if your solution is correct.

8. In the **Edit Sensitivity label** pane, select **Next** until you reach **Encryption** page.

9. On the **Encryption** page, scroll down to **Assign permissions to specific users and groups** and then select the **Assign permissions** link.

10. On the **Assign permissions** pane that open on the right, we see four options:

    - **Add all users and groups in your organization**

    - **Add any authenticated users**

    - **Add users or groups**

    - **Add specific email addresses or domains**

    because we want to add specific partner email accounts, we would choose the last option, **Add specific email addresses or domains**.

11. After selecting **Add specific email addresses or domains** a text box should appear displaying **Enter email address or domain**.

    Enter your partners admin account email address (Your partners admin email tenant prefix should look similar to yours **@xxxxxZZZZZZ.onmicrosoft.com**) then select **Add**.

    **Note:** If you don't have a partner, instead type in your personal Microsoft Outlook email account (@Outlook.com, @live.com, @hotmail.com, etc.) that you used earlier in Task 3.

12. Once finished adding the correct email address, you should see it displayed under the **Enter email address or domain** text box. Once finished select **Save**.

13. Back on the **Edit sensitivity label** window, select **Next** until you get to **Review your settings and finish**.

14. On the **Review your settings and finish** page, review all the configured settings. If needed, you can modify the settings by clicking the **Edit** link under the setting name. When finished reviewing the settings, select **Save label**.

    When prompted **Label updates**, select **Done**.

15. A new window displaying **Choose sensitivity labels to publish** will appear. As we've already published this label to the default label policy, select **Cancel**.

16. To test the modified label behavior, repeat steps 2 through 8 in Task 3 of this lab.

17. Select the email you just received to review the message body.

    **Note:** the email may be in your **Junk Email** Folder.

    You should now be able to view the full message body and its contents:

    ![Screenshot of Office Message Encryption Message](/Images/OME_Working.png)

## End of lab 4
