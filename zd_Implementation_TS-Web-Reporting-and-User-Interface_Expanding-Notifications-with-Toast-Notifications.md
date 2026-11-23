# Expanding Notifications with Toast Notifications

*Source: https://portal.parsec-corp.com/hc/en-us/articles/34888853144723-Expanding-Notifications-with-Toast-Notifications*
*Last updated: 2025-05-21T22:42:51Z*

---

Applies To | TrakSYS 12.0.2+

### Summary

Toast Notifications were introduced in TrakSYS 12.0.2. These notifications can be used to send on-screen messages to provide alerts or informational status updates to users. A step-by-step general configuration guide for Toast Notifications can be referenced in the following article: [Configuring Toast Notifications](https://portal.parsec-corp.com/hc/en-us/articles/28480693428115-Configuring-Toast-Notifications)

A Key difference of Toast Notifications compared to Notification Definitions is that they are executed through JavaScript. As a result, the management of and approach to Toast Notifications is quite different from Notification Definitions. This article will provide an example of how Toast Notifications can be managed and deployed, including how to relay information from incoming Email and Alert Notifications in real time.

The following features and concepts will be used in this example:

  * Custom Properties
  * Custom Content Part
  * Web Service



Below is additional information on these topics:

  * [Configuring Custom Properties](https://portal.parsec-corp.com/hc/en-us/articles/360006058054-Configuring-Custom-Properties)
  * [Creating a Custom Web Service](https://portal.parsec-corp.com/hc/en-us/articles/115003923447-Creating-a-Custom-Web-Service)
  * [Calling a Custom Web Service](https://portal.parsec-corp.com/hc/en-us/articles/115004224848-Calling-a-Custom-Web-Service)
  * [Creating Custom Content Pages and Parts](https://portal.parsec-corp.com/hc/en-us/articles/115004572994-Creating-Custom-Content-Pages-and-Parts)



### Configuring Custom Properties

From within the TS Web interface, navigate to **Configuration** | **Custom Properties** , create a Scheme as well as Group:

![](https://portal.parsec-corp.com/hc/article_attachments/34898067471891)

Then create a Custom Property for the Group with a String data type:

![](https://portal.parsec-corp.com/hc/article_attachments/34898081514003)

Notification Target IDs will serve to filter which Notifications will be returned. One option for setting the IDs is through this Custom Property, which will determine what Notifications specific Users and User Groups should receive.

### Configuring a Custom Content Part

Next, create a Custom Content Part, select the C# Script editor and paste the following:
    
    
    using System;
    using System.Collections.Generic;
    using System.Data;
    using System.Linq;
    using System.Web;
    using System.Web.ModelBinding;
    using System.Web.UI.DataVisualization.Charting;
    using ETS.Core.Api;
    using ETS.Core.Api.Models;
    using ETS.Core.Api.Models.Data;
    using ETS.Core.Enums;
    using ETS.Core.Extensions;
    using ETS.Core.Scripting;
    using ETS.Core.Services.Resource;
    using ETS.Ts.Core.ContentParts;
    using ETS.Ts.Core.Enums;
    using ETS.Ts.Core.Scripting;
    
    namespace ETS.Ts.Content
    {
      /// ***********************************************************  
      
      // class name MUST match Custom Part Key
      public partial class ToastPart : ContentPartBase
      {
        //// Declare properties with ContentProperty Attribute so they are exposed for editing from the Part Editor
        [ContentProperty(
          Label="Use Current User", 
          DefaultValuesKey="UserCheck", 
          GroupKey=nameof(ContentPropertyGroup._GENERAL), 
          DisplayOrder=1,
          ShouldRenderKeyInput=true)]
        public bool UserCheck { get; set; } = true;
    
        [ContentProperty(Label="Manual Target IDs (CSV)", 
          DefaultValuesKey="ToastTargetIDs", 
          GroupKey=nameof(ContentPropertyGroup._GENERAL), 
          DisplayOrder=2)]
        public string ToastTargetIDs { get; set; } = "-1";
    
        /// ***********************************************************
        protected override bool ContentPart_Init()
        {
          int userID = -1;
    
          // Return current user ID if property is true
          if(UserCheck)
          {
            userID = this.Ets.User.UserID;
          }
    
          // js that will execute Toast Notifications on Page
          string js = @"
          let url = ets.rootPath + '/api/home/toastnotif/ToastSub?targetIDs={0}&userID={1}';".FormatWith(ToastTargetIDs, userID);
    
          js+= @"
          ets.ready((page) => {
            toastSub();
          });
    
          function toastSub() {
    
            var p = $.get(url).done(function(data){
    
              // Do not continue if no new notifications  
              // Optionally implement !document.hidden to execute only when tab is active
              if (data.length === 0) {return;};
              
                const item = data[0];
                
                const options = {
                caption: 'New Notification',
                body: item.Title,
                theme: 1 /*  0 - none | 1 - primary | 2 - success | 3 - danger */,
                autoHideSeconds: 10,
                iconCss: 'fa-triangle-exclamation',
                isBodyRawHtml: true,
                extraCss: ''
                };
    
                ets.ui.showAdvancedToast(options);
    
                const remainingNotifs = data.length - 1;
    
                const options2 = {
                caption: remainingNotifs + ' More Notifications',
                body: 'Please review remaining Notifications <br/>that have been sent',
                theme: 1 /*  0 - none | 1 - primary | 2 - success | 3 - danger */,
                autoHideSeconds: 20,
                iconCss: 'fa-triangle-exclamation',
                isBodyRawHtml: true,
                extraCss: ''
                };
    
                ets.ui.showAdvancedToast(options2);
            });
    
            // produce alert notifying user there was an error while attempting to retrive new notifications
            p.fail(function(data) {
              ets.ui.alert('An error occured while retrieving new notifications', 'ERROR');
            });
    
    
          };
    
          // Start a repeating interval to check notifications every 5 seconds
          const interval = setInterval(toastSub, 5000);";
    
          // Add js to Page Definition
          this.Ets.Js.Add(js);
    
          return true;
        }
    
        /// ***********************************************************
        protected override bool DataBindProcessExpressionToChildControls()
        {
          if (!base.DataBindProcessExpressionToChildControls()) return false;
          return true;
        }
      }
    }

This Custom Content Part serves multiple purposes. First, it allows easy deployment of Toast Notifications across Page Definitions. When this part is added to a page, the Toast Notification functionality will automatically be available, eliminating the need to place the JavaScript on each individual page.

Second, the part will expose three properties that can be set with unique values per page that dictate how the Notifications will behave. These properties include:

  * Use Current User



This property determines if the TargetIDs for filtering the Notifications should come from the Custom Property of the current User.

  * Manual Target IDs (CSV)



This property is the second option for setting TargetIDs on a page basis. This allows all Users to receive the same Notifications on this page. Note that the Use Current User property will override this property if set to yes.

### Configuring a Web Service

This Web Service is called in the JavaScript code and acts as the mechanism for checking and returning any recent Notifications produced from Notification Definitions. Here is the example script that will be used for this example:
    
    
    using System;
    using System.Collections.Generic;
    using ETS.Core;
    using ETS.Core.Api;
    using ETS.Core.Api.Models.Data;
    using ETS.Core.Enums;
    using ETS.Core.Extensions;
    using ETS.Core.Scripting;
    using ETS.Ts.Core.ContentParts;
    using ETS.Ts.Core.Enums;
    
    using System.Web.Http;
    
    namespace ETS.Ts.Core.Scripting
    {
      /// ******************************************************************
      [RoutePrefix("api/home/toastnotif")]
      public class ToastNotificationController : ApiController
      {
        private ApiService _api;
    
        public ToastNotificationController(ApiService api)
        {       _api = api;
        }
    
        // Put in ID from content property part
        [HttpGet]
        [Route("ToastSub")]
        public List<DbNotification> ToastNotifs(string targetIDs, int userID)
        {
          // If userID is not -1, override manual targetIDs with CP targetIDs
          if (userID != -1)
          {
            var userObj = _api.Data.DbUser.Load.ByID(userID).ThrowIfLoadFailed("ID", userID);
            targetIDs = userObj.CustomProperties["UserToastCPS.ToastIDs"].Value;
          }
    
          // Return notifications only from last 5 seconds, and by TargetIDs
          string sql = @"
            SELECT *
            FROM tNotification
            WHERE NotificationDateTime > '{0}'
            AND NotificationTargetID IN ({1})
            ORDER BY ID DESC"          
          .FormatWith(_api.Site.GetCurrentDateTime().AddSeconds(-5), targetIDs);
    
          var newNotifs = _api.Data.DbNotification.GetList.WithSql(sql).ThrowIfLoadFailed("SQL", sql);
    
          return newNotifs;
        }
    
      }
    }

This Web Service will return a list of Notifications based on the TargetIDs supplied from the Custom Content Part. This list will be added to the JS in the Custom Content Part to produce Toast Notifications based on the tNotification records returned.

Perform a Full Compile once the script above has been saved.

### Configuring a Page Definition

We will now create a Visual Page and place the Custom Content part on it. We will be setting the Use Current User property to true, and leaving the Manual Target IDs property default:

![](https://portal.parsec-corp.com/hc/article_attachments/34933635322515)

The User in this example has valid Target ID values in the Custom Properties:

![](https://portal.parsec-corp.com/hc/article_attachments/34933635323795)

Another Visual Page has also been created to send 3 Notifications using the [CreateNotification](https://docs.parsec-corp.com/api-reference/api-services-reference/api.notification/createnotification) API method on button click.

Here is a demonstration of the end result, showcasing Notifications being sent on One Visual Page, followed by the Toasts being generated in real-time on the Custom Content Part Visual Page:

![](https://portal.parsec-corp.com/hc/article_attachments/34933635325203)

This example serves to demonstrate how Toasts can be used to generate and display critical or important information to operators in real-time. Given that the Web Service can leverage model objects, other data entities such as Events, Tasks, and more can also be displayed.

Note that the Web Service call will consume resources on the server hosting the TrakSYS Web. In addition, the JavaScript code will consume resources on the client machines. Therefore, thorough testing is recommended to ensure acceptable performance and making adjustments to the JavaScript code as needed.
