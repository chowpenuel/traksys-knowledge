# Using Security Assertion Markup Language (SAML) Authentication

*Source: https://portal.parsec-corp.com/hc/en-us/articles/25277193493779-Using-Security-Assertion-Markup-Language-SAML-Authentication*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 12.0.2+

### Summary

Starting in version 12.0.2, TrakSYS includes the ability to authenticate users with the Security Assertion Markup Language (SAML) protocol. This feature can be used in scenarios where a third-party identity provider (e.g. Azure Active Directory, Okta, etc.) is preferred.

TrakSYS can be used with any SAML identity provider. For this article, Okta and Azure Active Directory is used as an example. Authentication settings may vary depending on the Identity Provider used. 

**Note** : All settings should be lower-case as they are case sensitive. Additionally, when using SAML authentication, HTTPS must be enabled for the TrakSYS Web.

### Using Okta with SAML Authentication

This section demonstrates how to register the TrakSYS web application in an App hosted by Okta to allow SAML authentication through Okta as an external identity provider. In many cases, an organization will have an existing App. Depending on a variety of implementation-specific factors, it may be desirable to create a separate App strictly for SAML authentication purposes. However, this is not required. The app registration can be done in an existing App. (**Note:** the settings and screenshots shown in this document are accurate as of January 31st, 2024 and are subject to change at Okta's discretion. For the latest revision of the configuration, please consult Okta's documentation).

#### Configuring the Okta Identity Provider

  1. In Okta, select **Applications | Applications**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423127571)  
  

  2. Click the Create App Integration button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423144211)  
  

  3. Within the "Create App Integration" options, select "**SAML 2.0** " and click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423169299)  
  

  4. Within the "General Settings" section, provide an App name. For the purpose of this example, "Ts12SamlTest" will be used. In real-world installations, the provided name should make sense for the site and application. Afterwards, click Next.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423179411)  
  

  5. The following values should be provided for each of the properties below (where <YourServerNameHere> is the name of the server hosting IIS. In a majority of cases, this is the machine name of the TrakSYS application server. The exact value should match what is stored on the SSL certificate within IIS).   
  
**Note** : Uncheck the "Use this for Recipient URL and Destination URL" checkbox to reveal the Recipient URL and Destination URL settings.  
  
**Setting** | **Value**  
---|---  
Single sign-on URL | https://<YourServerName>/ts/account/saml/logonsaml.aspx  
Recipient URL | https://<YourServerName>/ts/account/logon.aspx  
Destination URL | https://<YourServerName>/ts/account/saml/logonsaml.aspx  
Audience URI (SP Entity ID) | https://<YourServerName>/ts/account/logon.aspx  
Single Logout URL* | https://<YourServerName>/ts/account/saml/logoffsaml.aspx  
  
*The Single logout URL can be found within the '**Show Advanced Settings** ' section and is only available if you upload a Signing Certificate from the Identity Provider (e.g., an Active Directory). Single logout URL is not required for the SAML functionality.  
  

  6. The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841396588179)  
  

  7. Next, scroll down to the 'Group Attribute Statements (optional)' section. On the existing row, type "Groups" into the "Name" field. Leave the Name format set to "Unspecified" and set the Filter dropdown to "Matches regex." Finally, enter ".*" (without quotes) into the filter textbox field. The final result is shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841396612499)  
  

  8. Click the Next button to continue.
  9. On the Feedback screen, select the "I'm an Okta customer adding an internal app" option and click Finish.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423246739)  
  

  10. On the resulting page, copy the Metadata URL. It is recommended to temporarily store this value in an easily accessible location (such as a text document on the desktop). This value will be needed in a later step when configuring TrakSYS to use SAML authentication.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423276691)  
  

  11. At this point, users can be added to the application. Users can be imported from an Active Directory or they can be manually created within Okta. For instructions and information about Active Directory integration, see the Okta Docs **[here](https://help.okta.com/en-us/content/topics/directory/ad-agent-main.htm?cshid=ext_Directory_AD_agent)**. For the purpose of this example, a user will be manually added to the application in Okta.  
  
To manually add users, navigate to **Directory | People** and click the Add Person button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423288723)  
  
To manually add groups, navigate to **Directory | Groups** and click the Add group button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841396694931)  
  

  12. Once Users and Groups have been created, they will need to be assigned to the application. To do this, navigate to **Applications | Applications**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423127571)  
  

  13. Select the application on the resulting page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841423329939)  
  

  14. Under the Assignment section, click **Assign | Assign to People** or **Assign to Groups** (depending on whether a user or group is being assigned).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25841396741267)  
  

  15. Once the assignments have been made, the users or groups should appear within the list.



#### Configuring SAML Authentication with Okta in TrakSYS

The following steps describe the required configuration for using SAML authentication with Okta in TrakSYS. The values are based on the configuration settings shown in the previous section and may be slightly different depending on your Okta settings.

  1. Open the TrakSYS Installation Manager and navigate to the Overview tab. Then, click the TrakSYS Settings link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25796255960339)  
  

  2. In the Settings dialog, scroll down to the WebAuthSaml section at the bottom.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25796241357459)  
  

  3. The following values should be provided for each of the properties below  
  
**Setting** | **Value**  
---|---  
SamlClaimsKeyGroup | groups  
SamlCalimsKeyName | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name  
SamlClaimsKeyUsername | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier  
SamlMetadataAddress | This is the value copied in step 10 in the previous section  
SamlServerPath | https://<YourServerName>/ts  
SamlLogonIsEnabled | True  
SamlSingleSignoutEnabled | False*  
  
*The default value is True, however, since this was not enabled in Okta for this example, this should be False. If the Single logout is configured in Okta, then this needs to be True.  
  

  4. The final result should look similar to what's shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25845837374739)  
  

  5. Click OK to save the changes.
  6. Next, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application).
  7. To finish the configuration, see the "Configuring and Using SAML Users in TrakSYS" section at the bottom of this article.



### Using Azure with SAML Authentication

This section demonstrates how to register the TrakSYS web application in a Microsoft Entra ID tenant in order to allow SAML authentication using Azure as the Identity Provider for TrakSYS. (**Note:** the Azure settings and screenshots shown in this document are accurate as of January 31st, 2024 and are subject to change at Microsoft's discretion. For the latest revision on the Microsoft Entra ID configuration, please consult Microsoft's documentation).

**Note** : a subscription to Microsoft Entra ID is required to use SAML authentication.

#### Configuring the Azure Identity Provider

In many cases, an organization will have an existing Microsoft Entra ID tenant. Depending on a variety of implementation-specific factors, such as the organization's policies, it may be desirable to create a separate tenant strictly for SAML authentication. However, this is not required. The app registration can be done in the existing tenant.

  1. Log into Azure and select the Microsoft Entra ID option under Azure services.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792970240275)  
  

  2. On the resulting page, click the Enterprise applications link under the Manage section of the first slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792970257683)  
  

  3. On the top navigation bar, click the New application button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921012755)  
  

  4. On the top navigation bar, click the Create your own application link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921047955)  
  

  5. A new options menu should appear on the right side of the screen. Provide a name for the application. For this example, "Ts12SamlTest" is being used. In actual implementations, it is recommended to choose a name that makes sense for the Site and installation. Ensure that the **Integrate any other application you don't find in the gallery (Non-gallery)** radio button option is selected.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921059731)  
  

  6. Click the create button.
  7. On the app's Overview page, click the 2. Set up single sign on option under the Getting Started section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921069843)  
  

  8. Choose SAML as the single sign-on method.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792970335891)  
  

  9. Click the Edit button on the Basic SAML Configuration section. This will bring up the Basic SAML Configuration menu options.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921109779)  
  

  10. Under **Identifier (Entity ID)** , click the Add identifier button. When the identifier text box appears, enter the following URL (where <YourServerNameHere> is the name of the server hosting IIS. In a majority of cases, this is the machine name of the TrakSYS application server. The exact value should match what is stored on the SSL certificate within IIS):  
  

         
         https://<YourServerNameHere>/ts/account/logon.aspx

  
![](https://portal.parsec-corp.com/hc/article_attachments/25792970382227)  
  

  11. Under **Reply URL (Assertion Consumer Service URL)** , click the Add reply URL button. When the reply URL text box appears, enter the following URL (where <YourServerNameHere> is the name of the server hosting IIS):  
  

         
         https://<YourServerNameHere>/ts/account/saml/logonsaml.aspx

  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921144851)  
  

  12. Under **Sign on URL (Optional)** , enter the following URL (where <YourServerNameHere> is the name of the server hosting IIS):  
  

         
         https://<YourServerNameHere>/ts/account/logon.aspx

  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921172755)  
  

  13. Under **Logout Url (Optional)** , enter the following URL (where <YourServerNameHere> is the name of the server hosting IIS):  
  

         
         https://<YourServerNameHere>/ts/account/saml/logoffsaml.aspx

  
![](https://portal.parsec-corp.com/hc/article_attachments/25792921197331)  
  

  14. The final result should look similar to the following:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25792970512403)  
  

  15. Click the Save button to save the changes.
  16. Next, click the Edit button for the Attributes & Claims section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25794973890451)  
  

  17. On the top navigation, click the Add a group claim link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25794989433235)  
  

  18. Select the appropriate groups for the application. For this example, the "All groups" radio button option and the "Group ID" Source Attribute were selected for configuration.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25794973915667)  
  

  19. Click the Save button to save the changes.
  20. Exit the Attributes & Claims section. This should redirect the user back to the Set up Single Sign-On with SAML page.
  21. Under SAML Certificates, copy the value from the App Federation Metadata URL field. It is recommended to temporarily store this value in an easily accessible location (such as a text document on the desktop). This value will be needed in a later step when configuring TrakSYS to use SAML authentication.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25794973929107)  
  

  22. Then, navigate to Users and groups.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25794973936915)  
  

  23. On the top navigation, click the Add user/group link to add users and groups as needed. **Note** : adding groups is a feature only available for paid subscriptions in Azure.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/25796241344019)  
  

  24. Once the Users and Groups have been selected, click the Assign button.
  25. The selected Users and Groups show now be displayed.



#### Configuring SAML Authentication with Azure in TrakSYS

The following steps describe the required configuration for using SAML authentication with Azure in TrakSYS. The values are based on the configuration settings shown in the previous section and may be slightly different depending on your Entra ID settings.

  1. Open the TrakSYS Installation Manager and navigate to the Overview tab. Then, click the TrakSYS Settings link.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25796255960339)  
  

  2. In the Settings dialog, scroll down to the WebAuthSaml section at the bottom.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25796241357459)  
  

  3. The following values should be provided for each of the properties below:  
  
**Setting** | **Value**  
---|---  
SamlClaimsKeyGroup | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups  
SamlCalimsKeyName | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name  
SamlClaimsKeyUsername | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier  
SamlMetadataAddress | This is the value copied in step 21 in the previous section  
SamlServerPath | https://<YourServerName>/ts  
SamlLogonIsEnabled | True  
SamlSingleSignoutEnabled | False*  
  
*The default value is True, but it has been set to False for testing purposes.  
  

  4. The final result should look similar to what's shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25798890816915)  
  

  5. Click OK to save the changes.
  6. Next, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-Reloading-the-TrakSYS-Application).



### Configuring and Using SAML Users in TrakSYS

  1. Open the TrakSYS Web and navigate to **Administration | Users**.
  2. Click the New button on the second slice to create a new user.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25797989196947)  
  

  3. Select the SAML User option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25798010470803)  
  

  4. Provide a Name and Login for the user. The Login should match the login used in the Azure Entra ID configuration (e.g., typically the user's email address).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25798010485779)  
  

  5. The new user should now appear under the Users list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25797989254675)  
  

  6. Now, when logging into the TrakSYS Web, a new "Sign in with SAML" option will appear.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25799318046227)  
  

  7. Clicking the link will redirect the user to the external Identity Provider. After providing the correct credentials, the user should be successfully authenticated and will be logged into the TrakSYS Web.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/25799318057235)



### Configuring and Using SAML Groups

If configuring individual SAML Users within TrakSYS is not desirable or feasible, it is possible to use SAML Groups instead (similar to using Windows Groups). While this process is specific to Okta, a similar process can be used for other identity providers. Depending on the identity provider used, there may be extra configuration that is required for successful authentication. If this is the case, it is recommended to refer to the identity provider's documentation. The following steps show how to configure a SAML Group in Okta and associate it with the configured SAML Group in TrakSYS. **Note** : At a minimum, these steps assume that all steps under the "Using Okta with SAML Authentication" and "Configuring SAML Authentication with Okta in TrakSYS" sections listed above have been successfully performed.

  1. To manually add a SAML Group in Okta, navigate to **Directory | Groups**. Then, click the Add group button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777604010899)  
  

  2. Provide a Name for the group and save the changes. For the purpose of this example, the group was named "Workers." The newly created group should now appear within the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777604012563)  
  

  3. Click the newly created group. On the resulting page, click the Assign people button under the People tab.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777609287955)  
  

  4. Assign users as needed. Then, click the Done button. The user should now appear within the list.
  5. Next, navigate to the Applications tab and click the Assign applications button.   
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777609290131)  
  

  6. Assign the existing SAML application and click Done. The application should now be associated with the Group and User.
  7. To create SAML Groups in TrakSYS, open the TrakSYS Web and navigate to **Administration | Users**.
  8. Click the New button on the second slice to create a new Group User.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777604016787)  
  

  9. On the resulting page, select the SAML Group option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777609293715)  
  

  10. In the Login field, enter the Name of the SAML Group (provided in Step 2).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777609296275)  
  

  11. After saving the changes, the SAML Group should now appear within the Users list. To create additional Groups, repeat Steps 8 through 10 as needed.
  12. Once all SAML Groups have been added, logout of the TrakSYS Web. Then, login with the SAML User associated with the SAML Group. The User should now be authenticated through the Group and should inherit any Roles and Page Permissions that are assigned to the Group.
  13. To verify that the user is correctly affiliated with the Group in TrakSYS, click the user name in the top right corner of the TrakSYS Web and click Settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777604022931)  
  

  14. On the resulting page, click the SAML Groups link under the Related section of the first slice. This will show a list of all detected SAML Groups affiliated with the currently logged in SAML User. If all settings are configured correctly, the SAML Group should appear within the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/34777609301011)


