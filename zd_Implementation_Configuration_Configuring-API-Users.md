# Configuring API Users

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360058636833-Configuring-API-Users*
*Last updated: 2026-03-03T01:10:56Z*

---

Applies To | TrakSYS 11.1.1+

### Summary

API User is a new user type that allows external applications to access TrakSYS Web APIs securely. This is done through the use of authentication tokens, which can be generated within the User properties. This article explains how the API User is used to securely connect to TrakSYS.

It is important to note that while the API User can enforce authentication for Web API requests, it does not secure the connection. It is highly recommended to use a secure SSL/TLS connection when accessing TrakSYS over the internet.

For the purpose of this example, the [Postman application](https://www.postman.com/downloads/) will be used. This application provides thick client and web client options. The thick client version is used to demonstrate the functionality. This example makes the following assumptions:

  * TrakSYS is installed and can be accessed directly on the server using the following URL: **http://localhost/ts**.
  * The Site Page Definition Key contains a value of **Home**.
  * A Logic Service Instance has been created under **Configuration | Services | Logic Services**.



### Creating the API User

  1. Open the TrakSYS Web and navigate to **Administration | Users**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702191528979)  
  

  2. Click New on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702255841043)  
  

  3. Select the API User option on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702267125779)  
  

  4. Enter a Name and click the Save button to create the user. Note that the Login field is automatically populated when the user editor is opened.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702453376403)  
  

  5. The user should now appear within the list.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702448506643)



### Procedure

The following examples address three different scenarios with different security settings.

#### **Example 1: No security**

For the first scenario, the Logic Service information will be retrieved using no security. To do this, the `WebApiSecurityMode` setting, under the Web section of TrakSYS Settings, should be set to `None`.

![](https://portal.parsec-corp.com/hc/article_attachments/18702584049043)

The following URL is used to retrieve Logic Service information: `http://localhost/ts/api/home/services/LogicServiceStatusForCurrentSite/`. In the Postman application, the request was a success and Logic Service configuration information is displayed.

![](https://portal.parsec-corp.com/hc/article_attachments/18702751803283)

#### **Example 2: Adding Security**

For the next scenario, security will be added to the installation. Set `WebApiSecurityMode` to either `OriginOnly` or `OriginOnlyAuthenticated`.

![](https://portal.parsec-corp.com/hc/article_attachments/18702633091347)

After saving the changes, [Reload the TrakSYS Application](https://portal.parsec-corp.com/hc/en-us/articles/360006969353-How-to-Reload-the-TrakSYS-Application). Now when the same request is made, a 401 error message appears saying that the request was denied.

![](https://portal.parsec-corp.com/hc/article_attachments/18702843511827)

#### **Example 3: Including the API User**

For the next example, the API User will be included in the authentication process so the call can succeed. Once again, `WebApiSecurityMode` should be set to `OriginOnly` or `OriginOnlyAuthenticated`. To give access to the client, a token must be generated from the API User as follows:

  1. Open the TrakSYS Web and navigate to **Administration | Users**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702880384531)  
  

  2. Select the API User on the first slice and click the Generate API Token button on the third slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702860755603)  
  

  3. On the resulting page, enter the number of days for which the token will be valid. For the purpose of this test, 10 days is being used. A value of 0 can be used if the token should not expire.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18702906968979)  
  

  4. Clicking the Generate Token button will redirect the user to a page displaying the authentication token.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18703049261843)  




The fully generated token should appear as a large, randomized string of letters, numbers, and characters. Note that tokens will only be displayed on this page, it should be copied and saved elsewhere. Once the user leaves the page, there is no way to retrieve it. In that scenario, a new token will have to be generated.

Now that a token has been generated, it can be added in the Postman App for authorization purposes. 

![](https://portal.parsec-corp.com/hc/article_attachments/18703143549971)

After adding the token, the application is successfully able to make the call and retrieve the Logic Service information.

![](https://portal.parsec-corp.com/hc/article_attachments/18703168816659)

#### **Example 4: API User with Roles (TrakSYS 11.2.0+)**

In TrakSYS 11.2.0, the `SecuredByPermission` option was introduced to allow API Users to be used with Roles. This is useful in scenarios where more granular control over permissions is required when making API calls. To use this option, set `WebApiSecurityMode` to `SecuredByPermission`. 

![](https://portal.parsec-corp.com/hc/article_attachments/18702644291859)

A [Role](https://portal.parsec-corp.com/hc/en-us/articles/115001575094-How-to-Configure-Page-Permissions-for-Roles) can then be created within the TrakSYS Web under **Administration | Roles**. Within the Role properties, the Web API tab contains various options to allow API calls for specific actions and to certain entities.

![](https://portal.parsec-corp.com/hc/article_attachments/18703652460947)

After saving the Role, the API User can be assigned to it by selecting the newly created Role and clicking the Assign button in the second slice.

![](https://portal.parsec-corp.com/hc/article_attachments/18703657403795)

Once the API User has been assigned, only API calls explicitly allowed by the Role should succeed.

### Configuring the Logic Service to use API Users

If Web API security is enabled, the Logic Service must also be associated with an API User to allow specific functionality (such as Refresh Key broadcasts, Fast Tag updates, Notification Alerts, and more) to work as intended. The recommended minimum permissions for a secured API can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/4409084922131-Minimum-Permissions-for-a-Secured-Web-API)**. The following steps describe how to assign an API User to the Logic Service. Note that the configuration changes shown below will require a Logic Service restart.

  1. In the TrakSYS Web, navigate to **Configuration | Services | Logic Services**.
  2. On the first slice, select the desired Logic Service Instance. Then, click the Set API User Token link on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40216857104147)  
  

  3. On the resulting page, specify a value (in days) for the token lifetime. Then, select the desired API User. In the example below, the API User created in the first section of this article is assigned. Additionally, the Token is set to never expire.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40216857106579)  
  

  4. Click the Assign button to apply the changes.
  5. Start or restart the Logic Service.



The Logic Service should now use the permissions of the assigned API User for internal operations and when making web calls.
