# Using OpenID Connect (OIDC) Authentication

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500005733481-Using-OpenID-Connect-OIDC-Authentication*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.1.1+

### Summary

Starting in version 11.1.1, TrakSYS includes the ability to authenticate users with the OpenID Connect (OIDC) protocol. This feature can be used in scenarios where a third-party identity provider (e.g. Azure Active Directory, Okta, etc.) is preferred.

OpenID Connect allows Clients to verify the identity of the end-user based on the authentication performed by an Authentication Server. It also obtains basic profile information about the user in an interoperable and REST-like manner.

TrakSYS can be used with any OIDC identity provider. For this article, Azure Active Directory is used as an example. Authentication settings may vary depending on the Identity Provider used. 

**Note** : When using OIDC authentication, HTTPS must be enabled for the TrakSYS Web.

### Configuring the Azure AD Identity Provider

This section demonstrates how to register the TrakSYS web application in an Azure Active Directory tenant in order to allow OIDC authentication using Azure Active Directory as the Identity Provider for TrakSYS. (**Note:** the Azure settings and screenshots shown in this document are accurate as of May 14th, 2021 and are subject to change at Microsoft's discretion. For the latest revision on Azure AD Identity Provider configuration, please consult Microsoft's [documentation](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/auth-oidc)).

In many cases, an organization will have an existing Azure Active Directory tenant. Depending on a variety of implementation-specific factors, such as the organization's policies, it may be desirable to create a separate tenant strictly for OIDC authentication purposes. However, this is not required. The app registration can be done in the existing tenant. **In these scenarios, steps 3-12 below should be omitted.**

  1. Log into the Azure portal (<https://portal.azure.com/>) with an administrative account.
  2. Click on the Azure Active Directory icon under the Azure services section.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/1500007837021)  
  

  3. Click the "Create a tenant" button to create a new Active Directory tenant.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/1500007837341)  
  

  4. Choose the applicable Tenant type. For the purposes of this example, the Azure Active Directory option is being selected.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/1500007837581)  
  

  5. Click Next : Configuration >.  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/1500007667282)  
  

  6. Specify an Organization name and Initial domain name. For this example, the organization will be called Umbrella and the domain name is set to qtuumboidc.  
  
![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/1500007837961)  
  

  7. Click Next : Review + create >.  
  
![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/1500007667902)  
  

  8. On the following page, a validation will be performed to ensure that the name can be used. If it is available, a message will display indicating that the validation has passed.  
  
![mceclip6.png](https://portal.parsec-corp.com/hc/article_attachments/1500007838881)  
  

  9. After verifying the settings, click the Create button to create the tenant. Note that the creation process can take a few minutes to complete.  
  
![mceclip7.png](https://portal.parsec-corp.com/hc/article_attachments/1500007838961)  
  

  10. Once the tenant has been created, click the user profile in the top right corner and click the Switch directory link.  
  
![mceclip8.png](https://portal.parsec-corp.com/hc/article_attachments/1500007840041)  
  

  11. Select the newly created tenant within the list.  
  
![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/1500007840061)  
  

  12. Click the Azure Active Directory icon under the Azure services section.  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/1500007837021)  
  

  13. On the side navigation bar, click the App registrations option  
  
![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/1500016283321)  
  

  14. Click the New registration button to register a new application.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/1500016020402)  
  

  15. Enter a display name for the application, then select the account type. For the purposes of this example, the "Account in this organizational directory only" option has been selected. Other options may be more suitable depending on the implementation.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/1500016020462)  
  

  16. Next, specify a Redirect URI. In general, the URL should use the following format:  

         
         https://[(](https://\()ServerName)/ts/account/oidc/logonoidc.aspx

**Note:** HTTPS must be used in the URL as this feature has to be enabled for the TrakSYS Web in IIS. Additionally, the OIDC servers are case sensitive. Therefore, when the URL is entered, it should be in all lower case letters.  
  
![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/1500016283441)
  17. After verifying the settings, click the Register button to register the application.  
  
![mceclip13.png](https://portal.parsec-corp.com/hc/article_attachments/1500007843241)  
  

  18. Then, click the App registrations button mentioned in step 13. Under the Owned Applications tab, the newly registered application should appear in the list.  
  
![mceclip16.png](https://portal.parsec-corp.com/hc/article_attachments/1500007674302)
  19. Click the application link, then click the Certificates & secrets tab on the side navigation bar.  
  
![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/1500016020582)  
  

  20. Next, click the New client secret button under the Client secrets section.  
  
![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/1500016020622)  
  

  21. Add a description for the client secret, choose an expiration duration, then click Add.  
  
![mceclip19.png](https://portal.parsec-corp.com/hc/article_attachments/1500007674642)  
  

  22. A new entry should now appear in the list under the Client secrets section. Copy the text under the **Value** field and save it in a separate location. This value will be needed later on to use TrakSYS with OIDC authentication.  
  
![mceclip7.png](https://portal.parsec-corp.com/hc/article_attachments/1500016020762)  
  

  23. Click the Overview tab on the side navigation bar, copy the value for the Application (client) ID and save it in a separate location. This is the second piece of information needed for OIDC authentication.  
  
![mceclip8.png](https://portal.parsec-corp.com/hc/article_attachments/1500016020942)  
  

  24. Click on the Endpoints button to reveal the list of possible authentication endpoints.  
  
![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/1500016283841)  
  

  25. Copy the value for the "OpenID Connect metadata document" field and save it in a different location. This is the third required piece of information for the authentication process.  
  
![mceclip10.png](https://portal.parsec-corp.com/hc/article_attachments/1500016021002)



### Configuring OIDC Authentication in TrakSYS

  1. Open Installation Manager and click the TrakSYS Settings button within the Overview tab.  
  
![mceclip24.png](https://portal.parsec-corp.com/hc/article_attachments/1500007675342)  
  

  2. In the resulting dialog window, scroll down to the Web section at the bottom to view the OIDC settings.  
  
![mceclip25.png](https://portal.parsec-corp.com/hc/article_attachments/1500007675422)  
  
**Note** : depending on the OIDC provider, it may not be required to populate every OIDC setting. The minimum required fields are as follows:  
  
`OidcClaimsKeyUsername`  
`OidcClientID`  
`OidcClientSecret`  
`OidcMetadataAddress`  
  

  3. **Optional:** For the `OidcClaimsKeyName` field, enter a display name. This can be any user-specified value.
  4. For the `OidcClaimsKeyUsername` field, specify the key used to retrieve the user's username from the OIDC provider (e.g. preferred_username).
  5. For the `OidcClientID` field, enter the client ID value obtained from step 23 of the previous section.
  6. For the `OidcClientSecret` field, enter the client secret value obtained from step 22 of the previous section.
  7. For the `OidcMetadataAddress` field, enter the URL obtained from step 25 of the previous section.
  8. Set `OidcLogonIsEnabled` to True.
  9. Set a URL for the `OidcServerPath` field. This is where the OIDC provider will redirect after authenticating the user. To redirect back to the TrakSYS Web after authentication, the following URL can be used: https://ServerName/ts/ (note that the fully qualified domain name is used).
  10. The final result should look similar to the following:  
  
![mceclip11.png](https://portal.parsec-corp.com/hc/article_attachments/1500016284181)  
  

  11. Click OK to save the changes.
  12. [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353) to apply the changes.



### Inviting Users to the Azure Active Directory 

The following steps explain how to invite guest users to the Azure Active Directory tenant where the TrakSYS application is registered so they can be authenticated via OIDC.

**Note:** In many cases, the relevant users will already be members of the tenant. In these scenarios, this section is not applicable and should be omitted.

  1. Navigate the the tenant created in the first section of this article.
  2. Click the Users option on the side navigation bar.  
  
![mceclip12.png](https://portal.parsec-corp.com/hc/article_attachments/1500016021802)  
  

  3. Click the New guest user button to create a new guest user.  
  
![mceclip13.png](https://portal.parsec-corp.com/hc/article_attachments/1500016021942)  
  

  4. Enter the required fields for the user profile. Then click the Invite button to invite the user to the Active Directory.  
  
![mceclip14.png](https://portal.parsec-corp.com/hc/article_attachments/1500016284501)  
  

  5. The new user profile should now appear under the list of users.
  6. This will send an email to the specified address inviting the user to the tenant. The user needs to click the link contained in this email in order to redeem the invitation.



### Configuring and Using OIDC Users in TrakSYS

  1. Open the TrakSYS Web and navigate to **Administration | Users**.
  2. Click the New button on the second slice to create a new user.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18701614202899)  
  

  3. Select the OIDC User option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18701604558739)  
  

  4. On the resulting page, enter the Name and Login for the user. The login should match the login used in the Active Directory configuration (i.e. the user's email address). Then click Save.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18701646164243)  
  

  5. The new ODIC user should now appear within the Users list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18701701058323)  
  

  6. When logging into the TrakSYS Web, a new OpenID Connect option should now appear on the default login page. Click this option to login with an OIDC user.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18701833301651)  
  
**Note** : Depending on the provider, there may be an additional confirmation message that appears when an OIDC user logs in for the first time, such as the one below for Azure Active Directory.  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/1500007739242)  
  

  7. After accepting, the user is taken to the login page.  
  
![mceclip8.png](https://portal.parsec-corp.com/hc/article_attachments/1500007917541)  
  
![mceclip9.png](https://portal.parsec-corp.com/hc/article_attachments/1500007741822)  
  

  8. Once the user is successfully authenticated, they will be logged into the TrakSYS Web.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18701879407635)



### Configuring and Using OIDC Groups

If configuring individual OIDC Users within TrakSYS is not desirable or feasible, it is possible to use OIDC Groups instead (similar to using Windows Groups). However, there is extra configuration that may be required to allow individual Users to authenticate through the Group. For Microsoft Azure specifically, an Optional Claim must be configured for this process. Other identity providers may have similar requirements and may differ between providers. The following steps show how to create an Option Claim and configure an OIDC Group in TrakSYS. **Note** : these steps assume that the desired Groups already exist within Azure Active Directory.

  1. Access Azure Active Directory and navigate to **Manage | App Registrations**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975179539)  
  

  2. Choose the App Registration that has been created for this instance. Then, navigate to **Manage | Token Configuration**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33027024198547)  
  

  3. On the resulting page, click the “Add Groups Claim” button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33027024201107)  
  

  4. In the options, select the “All Groups” option. Depending on the use case, it may be desirable to check the “Groups assigned to the application” option as well. For this example, this option was left unchecked.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975188755)  
  

  5. Click "Add" to save the changes. At this point, the new Claim should be created. It is recommended to note the value specified for the Claim column. This is the exact value that should be placed within the OidcClaimsKeyGroup setting within the TrakSYS Settings (explained in further steps).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33027024206099)  
  

  6. After saving the changes, the ObjectID for each Group should be verified. This value is needed when configuring OIDC Groups in TrakSYS (also explained in further steps). To do so, access Azure Active Directory and navigate to **Manage | Groups**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33027024209043)  

  7. Under the All groups section, locate the Object ID of the desired Group. In the example below, only 1 group exists within the configuration. Depending on the configuration of the directory, there may be several more Groups present.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975195667)  
  

  8. Repeat Step 7 and document all desired ObjectIDs for the applicable Groups.
  9. Once this information has been recorded, open the TrakSYS Installation Manager and click the TrakSYS Settings button within the Overview tab.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975198611)  
  

  10. Scroll down to the WebAuthOidc section. Enter the Optional Claims Key provided in Step 5 into the OidcClaimsKeyGroup field. In this example, that value is "groups."  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975210643)  
  

  11. Click OK to save the changes.
  12. [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353) to apply the changes.
  13. To create OIDC Groups within TrakSYS, open the TrakSYS Web and navigate to **Administration | Users**.
  14. Click the New button on the second slice to create a new user.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975215123)  
  

  15. On the resulting page, select the OIDC Group option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33027024236691)  
  

  16. In the Login field, enter the ObjectID of the desired group (provided in Step 7).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/33026975232147)  
  

  17. After saving the changes, the OIDC Group should now appear within the Users list. To create additional Groups, repeat Steps 14 through 16 as needed.
  18. Once all OIDC Groups have been added, logout of the TrakSYS Web. Then, login with the OIDC User associated with the OIDC Group. The User should now be authenticated through the Group and should inherit any Roles and Page Permissions that are assigned to the Group.


