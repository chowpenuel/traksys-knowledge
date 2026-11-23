# Creating a Custom Web Service

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115003923447-Creating-a-Custom-Web-Service*
*Last updated: 2025-08-05T21:45:44Z*

---

Applies To | TrakSYS 10+

### **Summary**

The following article describes how to create a web service endpoint. This is a way to expose web services through the TrakSYS Web by leveraging Microsoft's Web API 2.0. 

### **Web Service Overview**

In TrakSYS, a web service endpoint is exposed by means of a Web Script. **By convention, the name of the class must end with `Controller`**. The class inherits from the WebApi base class `ApiController`. The kind of functionality that is exposed and how it is accessed is controlled by decorating the class and its methods with certain attributes (`RoutePrefix`, `Route`, `HttpGet`, `HttpPost`, `HttpPut` and `HttpDelete`). 

#### **_System.Web.Http_**

This C# namespace contains many of the different features used by the Web API framework. By default, this namespace is not included in the TrakSYS script class templates. The following using directive should be added to the class to reduce repetitive code:
    
    
    using System.Web.Http;
    

####  **_RoutePrefix_**

A common prefix can be used for the entire controller by decorating the class with this attribute. This means all the web service URLs/endpoints in the class will start the same way. The `RoutePrefix` attribute should start with "**api/{sitekey}/custom** " (where {sitekey} is the actual string). This naming convention is important because it helps notify the TrakSYS framework under which site this particular function call is working. This is especially important if you want to call `api.Site.GetCurrentDateTime` since this and many other functions need an accurate value.

The use of the "custom" string in the attribute is also important to prevent errors resolving Web API URLs since TrakSYS web services use the same "api/{sitekey}/" prefix.

#### _**Route**_

Routing is how Web API matches an HTTP request to an action. By decorating the methods in the class with the `Route` attribute, the web service URL/endpoint is completed. To call a specific action, the URL/endpoint used will be the method's `Route` attribute appended to the class's `RoutePrefix` attribute. 

#### _**Http Methods**_

Instead of following the naming convention for HTTP methods, an action's HTTP method can be explicitly specified by decorating the action method with the corresponding attribute (e.g. `HttpGet`, `HttpPost`, etc.).

### **Sample Web Service**

The following is a simple example that illustrates how to use a web service to add two numbers and return the result. In this case, all parameters are integers. The Web API framework has many more features, including the ability to accept and return more complex types (e.g. custom classes), providing additional flexibility that can be further explored via Microsoft's documentation.

  1. In the TrakSYS Web, navigate to the **Developer** section and the **Scripts | Web** sub-section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18856185774995)  
  

  2. Create a new Script Group by clicking **New** under **Groups** in Slice 1.
  3. Give the Script Group a name and click **Save**.
  4. Click on the new Script Group in Slice 1.
  5. Create a new Script by clicking **New** under **Scripts** in Slice 2.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18856234401555)  
  

  6. Give the script the name **MathController** and click **Save**.
  7. Select the **MathController** script in Slice 2 and click on its **Script** action in Slice 3 to load the script editor.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18856260023059)  
  

  8. In the MathController script editor, enter the following code (note the use of attributes and inheritance as discussed above):  
  

         
         using System;
         using System.Collections.Generic;
         using System.Web.Http; // must be added
         using ETS.Core;
         using ETS.Core.Api;
         using ETS.Core.Api.Models.Data;
         using ETS.Core.Enums;
         using ETS.Core.Extensions;
         using ETS.Core.Scripting;
         using ETS.Ts.Core.ContentParts;
         using ETS.Ts.Core.Enums;
         
         namespace ETS.Ts.Core.Scripting
         {
           /// ******************************************************************
           [RoutePrefix("api/{sitekey}/custom/math")]
           public class MathController : ApiController
           {
             /// ******************************************************************
             /// example: //server/ts/api/home/custom/math/addnumbers?a=10&b=32
             /// ******************************************************************
             [HttpGet]
             [Route("AddNumbers")]
             public int AddNumbers(int a, int b)
             {
               return a + b;
             }
           }
         }
         

  9. Click **Save**.
  10. Click **Full Compile**.



The web service is now deployed. To call the web service, please refer to [this article](https://portal.parsec-corp.com/hc/en-us/articles/115004224848).

#### **Additional Resources**

  * [Calling a Custom Web Service](https://portal.parsec-corp.com/hc/en-us/articles/115004224848)
  * [Getting Started with ASP.NET Web API 2 (C#) : docs.microsoft.com](https://docs.microsoft.com/en-us/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)


