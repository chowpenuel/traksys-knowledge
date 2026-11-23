# Microsoft Office 365 Email Registration

*Source: https://portal.parsec-corp.com/hc/en-us/articles/4408446482707-Microsoft-Office-365-Email-Registration*
*Last updated: 2026-06-01T21:41:44Z*

---

Applies To | TrakSYS 11.2.2+

### Summary

Starting in version 11.2.2 of TrakSYS, a new method of connecting to and sending email is available. This new method utilizes OAuth 2.0 and App Registrations in the Azure Active Directory. Using this new method, credentials are exchanged only once and a secure token is registered. This is more secure than alternative configurations where a users credentials are being passed every time a message is sent.

The following article describes the process of setting up TrakSYS with Microsoft Office 365 OAuth Email. Note that the screenshots and details here are based on the Azure Portal at the time of this articles publishing/updating. The Azure Portal changes frequently and the exact positioning and labeling may be slightly different.

#### **General Process**

The general process of setting up the Office 365 email connection is broken down into the following steps...

  * Establishing an Office 365 User / Email Account for Message Broadcast
  * Creating an App Registration in Azure Active Directory
  * Authorizing TrakSYS to send Email via the App Registration
  * TrakSYS Email Settings
  * Apply the TrakSYS 11.2.4 Hotfix for Notifications.
  * Testing the Email Connection



The remaining sections in this article cover these steps in more detail.

### Establishing an Office 365 User / Email Account for Message Broadcast

An Office 365 user with a mailbox must be allocated as the "sender" for all messages that will originate from TrakSYS. It is recommended that an actual human user's account not be used for this, but rather a new dedicated account be established. Emails that originate from this account will be sent from this new account/email address, so name it appropriately. Keep track of this sender account's password, as it will be required to complete the setup process.

The remainder of this article will use **traksys@company.com** as the placeholder for the sender account.

### Creating an App Registration in Azure Active Directory

An Azure Active Directory administrator must create an App Registration with specific settings to be used to connect to and relay mail through. The following steps describe how this should be configured...

  * Select App Registrations from the Azure Active Directory menu.



![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/4408446673811)

  * Select New Registration from the top menu.



![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/4408446738323)

  * Provide a Name for the App Registration. This name can be anything and is not programmatically referenced later, it is just for human organizational reference.
  * The Redirect URI must be provided and can be obtained from the target TrakSYS implementation. The URL to be used is listed in the Instructions portion of the **Administration | Settings | Microsoft 365 Email** page.



![](https://portal.parsec-corp.com/hc/article_attachments/20737223293843)

  * Once these values are entered, click the Register button at the bottom of the form.



![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/4408452642323)

  * Navigate to the API Permissions tab and add the SMTP.Send Permission.
  * Click Add a Permission.



![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/4408492655123)

  * Select Microsoft Graph and then Delegated Permissions.



![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/4408492667923)

![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/4408492702739)

  * Find and select the SMTP.Send Permission.



![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/4408485088659)

  * Navigate to the Certificates & Secrets tab and generate a new Secret..
  * Click New Client Secret.



![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/4408485135891)

  * Enter a value for Description. This value is not used programmatically and is just used as a descriptor.
  * Enter an Expiration time. This value can be set to any duration, however, when the Secret expires, TrakSYS email sending access will not function, and a new Secret will have to be re-generated and the authorization process repeated.



![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/4408492952211)

  * Save the Secret's Value for use later in this procedure as it is not possible to view the value again after closing this page.



![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/4408493501843)

At this point, the App Registration is complete and TrakSYS can be authorized to send email.

### Authorizing TrakSYS to send Email via the App Registration

Once the App Registration is complete, the steps below describe how to authorize TrakSYS to send email via Office 365. Completing these steps will require the following important aspects...

  * Administrator access to the TrakSYS Web.
  * Use of Edge or Chrome browser (this does not work via Internet Explorer).
  * Browsing in a logged in session from inside the actual TrakSYS Web server using localhost URL (this cannot be done from a remote web client).



To authorize TrakSYS to send email...

  * Navigate to **Administration | Settings**.
  * Click on OAuth settings.



![](https://portal.parsec-corp.com/hc/article_attachments/20737282175251)  
  


Configure the Microsoft 365 Email fields with the following information.  
  


![](https://portal.parsec-corp.com/hc/article_attachments/20737335751187)

  * Provide the Application (client) ID from the **Azure App Registration | Overview**.



![mceclip10.png](https://portal.parsec-corp.com/hc/article_attachments/4408493543827)

  * Provide the Client Secret from the **Azure App Registration | Certificates & Secrets**.



![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/4408493501843)

  * Provide the Authorization Endpoint and Token Endpoint from the **Azure App Registration | Overview | Endpoints**. Use the v2 values.



![mceclip11.png](https://portal.parsec-corp.com/hc/article_attachments/4408493639443)

Click the Authorize button.

![](https://portal.parsec-corp.com/hc/article_attachments/20737414665363)

  * The UI will be redirected to a Microsoft Office 365 login. Provide the login and password for the sender account. Accept any delegation.
  * CONDITIONAL: Depending on the account configuration, additional approval may be required from an administrator. If this is the case, something similar to the following prompt will appear:



![](https://portal.parsec-corp.com/hc/article_attachments/52221072061971)

  * A splash/wait screen will be displayed for a few seconds. If successful, the UI will be redirected to a Microsoft 365 Email Settings page.



### TrakSYS Email Settings

Once all of the Azure and Microsoft 365 settings have been configured, the Email Settings must be configured within the TrakSYS software. To reach these settings, do the following:

  * Open the TrakSYS Installation Manager and navigate to the Overview tab.
  * Click the TrakSYS Settings button to open the Settings dialog window.



![](https://portal.parsec-corp.com/hc/article_attachments/20734607153939)

  * Scroll down to the Notification section and fill in the appropriate information. According to [Microsoft Documentation](https://learn.microsoft.com/en-us/exchange/mail-flow-best-practices/how-to-set-up-a-multifunction-device-or-application-to-send-email-using-microsoft-365-or-office-365), the settings shown below are recommended for the most secure setup.

![](https://portal.parsec-corp.com/hc/article_attachments/52220901584787)

  * Click OK to save the changes.
  * Navigate to the Services tab of the TrakSYS Installation Manager and Start or Restart the Maintenance Service.



![](https://portal.parsec-corp.com/hc/article_attachments/20737520210067)

  * Finally, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application). At this point, all settings should be properly configured.



### TrakSYS Hotfix for Office 365 Notifications (TrakSYS 11.2.3 and 11.2.4 only)

Due to changes implemented by Microsoft in Windows Updates, this functionality no longer works as intended in TrakSYS 11.2.3 and 11.2.4. Therefore, a hotfix was created to help restore this functionality.

**Note** : The hotfix is only applicable to TrakSYS 11.2.4. There is no hotfix available for TrakSYS 11.2.3. If this version is being used, it is recommended to apply the [TrakSYS 11.2.5 update](https://portal.parsec-corp.com/hc/en-us/articles/1500011645841-TrakSYS-11-2-Updates) to restore this functionality. If applying the update is currently not feasible, it is possible to create a [Mail Relay](https://portal.parsec-corp.com/hc/en-us/articles/360000981133-Configuring-Notifications-with-Microsoft-Office365) as a workaround instead.

The hotfix files have been attached to the bottom of this article. The folder and file extensions have been renamed. To apply the hotfix, please do the following:

  1. Download the attached file.
  2. Extract the contents of the .zip folder.
  3. On the TrakSYS application server, stop the Maintenance Service and close the TrakSYS Installation Manager if it is open.
  4. In the root TrakSYS Installation folder (**…\Program Files (x86)\Parsec\TrakSYS**), make a backup of the **InstallationManager.exe** and **MaintenanceService.exe** files by copying them to a different location (such as the desktop).
  5. Copy the hotfix executable files into the root TrakSYS installation folder. This should override the existing executable files.
  6. Open the TrakSYS Installation Manager and start the Maintenance Service.



### Sending a Test Email to Verify Configuration Settings.

With the Microsoft Office 365 email settings configured, it is recommended to send out a test email notification to verify if the configuration of the Email Notification.

There are 3 Tests that can be carried out to verify the Email notification functionality using Microsoft Office 365.

  1. Use the "**Test** " function for a notification definition.
  2. Use the "**Send Test E-Mail** " functionality from the TrakSYS Installation Manager.
  3. Send a Test E-Mail using the TrakSYS API.



**Note** : If TrakSYS 11.2.4 is being used, the first two options will not work. In this version, the email functionality can only be tested programmatically using the TrakSYS API.

#### **Using the "Test" function for a Notification Definition (TrakSYS 11.2.5 and 12.0.1+)**

This first option using the built-in "Test" functionality for a configured Notification Definition. The steps below assume that a [Notification Definition has been configured](https://portal.parsec-corp.com/hc/en-us/articles/360004903154-Configuring-Notifications-and-Alerts).

  * Open the TrakSYS Web and navigate to **Configuration | Notifications**.
  * Select a Notification Group on the first slice. Then, select the desired Notification Definition on the second slice. 
  * On the third slice, click the Test button.



![](https://portal.parsec-corp.com/hc/article_attachments/20738567453459)

  * On the resulting page, enter an email address and click Send.



![](https://portal.parsec-corp.com/hc/article_attachments/20738744210963)

  * If all settings are correctly configured, a Success status should appear on the result page.



![](https://portal.parsec-corp.com/hc/article_attachments/20740162500371)

#### **Using the "Send Test E-Mail" Functionality**

This second option involves the Send Test E-Mail functionality available within the TrakSYS Installation Manager. The following steps describe how to access and use this feature.

  * Open the TrakSYS Installation Manager and navigate to the Diagnostics tab.
  * Then, click the Send Test E-Mail button on the top right corner of the application.



![](https://portal.parsec-corp.com/hc/article_attachments/41184383907091)

  * On the resulting dialog window, enter the desired email address. Then, click OK to send the email.



![](https://portal.parsec-corp.com/hc/article_attachments/20740292974995)

  * If all settings are correctly configured, the result should be a success.



![](https://portal.parsec-corp.com/hc/article_attachments/20740721759507)

#### **Send a Test E-Mail using the TrakSYS API (TrakSYS 11.2.2+)**

This final method involves using the TrakSYS API within a Button Click method on a Visual Page Definition. The following C# code creates an E-mail Notification object and sends the message to the specified Notification Target. Once the notification has been sent, a record containing details of the message will appear within the tNotification table.
    
    
    protected void Button_Click(object sender, EventArgs e)
    {
       //Create a notification entity.
       //Create unit of work. 
       var uow = this.Ets.Api.CreateUnitOfWork();
    
       //Create notification object
       var notificationObj = this.Ets.Api.Notification.CreateNotificationForEmail("inbox@domain.com", " Email Notification Title", "Email Notification Message.", uow);
       uow.ExecuteReturnsResultObject().ThrowIfFailed();
    }
    

####    
**Attachments:**
