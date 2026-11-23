# Sending Email Notifications Using the TrakSYS API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824503797011-Sending-Email-Notifications-Using-the-TrakSYS-API*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

In some scenarios, it may be desirable to automatically send Email Notifications or Alerts on a periodic basis or when certain conditions have been met. Some installations may have much more in depth requirements which involve more complex logic on when the emails should be sent and who should receive them. One possible way to satisfy this requirement is to use the [Notification API Service](https://portal.parsec-corp.com/hc/en-us/articles/360037580554-Using-the-API). This service can be used to programmatically send Email Notifications using custom scripting. While this service can be used in all areas of the TrakSYS application, the following example shows how to send an Email Notification using a Module. Note that the Data Management Service feature line must be present on the TrakSYS license in order to use Modules. This method assumes that [Notification Definitions](https://docs.parsec-corp.com/entity-reference/configuration-entities/notification-definition) and [Notification Targets](https://docs.parsec-corp.com/entity-reference/configuration-entities/notification-target) have been configured.

Within a Module Script Step, it is possible to access the Notification Service with custom scripting using the TrakSYS API. All available methods can be viewed in IntelliSense.

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/7052596123283)

Assuming that a Notification Definition has been configured, the `CreateNotificationForNotificationDefinition()` method can be used to send out notifications to a specific email address. As shown below, the code should reside in the `Execute()` method of the Module Script Step.
    
    
    public override bool Execute(IModuleContext ctx)
    {
      //Create args dictionary
      Dictionary<string, object> args = new Dictionary<string, object>();
      //Populate the dictionary as needed...
    
      //Send email notification
      ctx.Api.Notification.CreateNotificationForNotificationDefinition("NotifDefinitionKeyHere", "YourEmail@domain.com", args);
      return true;
    }
    
    

Depending on how the Module is configured, the email can now be sent out on a periodic interval. Optionally, the module can be programmatically triggered from different areas of the application. Information about programmatically triggering modules from Script Classes can be found **[here](https://portal.parsec-corp.com/hc/en-us/articles/360035503214-Using-a-Logic-Service-Script-Class-to-Trigger-a-DMS-Module)**. While the example is specifically for Script Classes, similar code can be used to send it from other locations as well (e.g. Page Definitions, Module Scripts, Script Tags, etc.).
