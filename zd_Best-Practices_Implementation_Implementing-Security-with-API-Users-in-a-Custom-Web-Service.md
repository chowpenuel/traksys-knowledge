# Implementing Security with API Users in a Custom Web Service

*Source: https://portal.parsec-corp.com/hc/en-us/articles/12953691137043-Implementing-Security-with-API-Users-in-a-Custom-Web-Service*
*Last updated: 2025-05-21T23:04:35Z*

---

Applies To | TrakSYS 11.2.0+

TrakSYS provides the ability to [create](https://portal.parsec-corp.com/hc/en-us/articles/115003923447) and [call](https://portal.parsec-corp.com/hc/en-us/articles/115004224848) custom web services. To handle web service calls, [API Users](https://portal.parsec-corp.com/hc/en-us/articles/360058636833) can be created to help enforce basic authentication. For more complex requirements and scenarios, security can be programmatically implemented within the custom web service. The TrakSYS API can be used to check the Permission Set and Item to ensure that the API User has permissions to access the entity included in the call. The following code provides an example and starting point for implementing security in a custom web service.
    
    
    namespace ETS.Ts.Core.Scripting
    {
      /// ******************************************************************
      /// <summary>Class Description</summary>
      /// ******************************************************************
      [RoutePrefix("api/{siteKey}/testapi")]
      [ETS.Ts.Core.Services.Web.TsWebApiAuthorize]
      public class TestApiController : ApiController
      {
        private readonly IWebApiContext _ets;
    
        ///***********************************************************
        public TestApiController(IWebApiContext ets)
        {
          _ets = ets;
        }
    
        ///***********************************************************    
        [HttpGet]
        [Route("Permission")]
        public string Permission()
        {
          // if "OriginOnly" or "OriginOnlyAuthenticated" is used
          var isAllowed = _ets.HasPermission(PermissionKeys.WebApiSet, PermissionKeys.WebApiItemUpdateTagValue);
    
          // If "SecuredByPermission" is used it is recommended to use the below code.   
          // Otherwise, the code won't throw a "access denied" message.
          _ets.HasWebApiPermissionThrowIfDenied(PermissionKeys.WebApiSet, PermissionKeys.WebApiItemUpdateTagValue);
    
          if(isAllowed) 
          {
            return "You have permission";
          }
    
          return  "Goodbye";
        }
    
        ///***********************************************************    
        [HttpGet]
        [Route("Hi")]
        public string Hi()
        {
          if (!_ets.User.IsAnonymous)
          {
            return "Hello. I'm '" + _ets.User.DisplayName + "'";
          }
    
          return "Goodbye";
        }
      }
    }
    

If the SecuredByPermission option is being used and Roles have been assigned to the API Users, it is also possible to further extend the granularity of permissions using [Permission Sets](https://portal.parsec-corp.com/hc/en-us/articles/360006892954). The TrakSYS API can be used to check these permissions along with the standard permissions that are included in the Role configuration.

**Note** : While API Users do help enforce authentication, it is highly recommended to use HTTPS (SSL/TLS) to properly secure Web APIs. 
