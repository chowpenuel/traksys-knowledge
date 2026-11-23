# Services Management Using the TrakSYS API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360048584354-Services-Management-Using-the-TrakSYS-API*
*Last updated: 2025-08-07T21:54:17Z*

---

### Summary

The TrakSYS services can now be started, stopped, and restarted within the TrakSYS Web using the API. This can be useful for controlling the TrakSYS services without having to access the application server or the TrakSYS Installation Manager.

### Example

The following example shows how to control the TrakSYS services using the API. This example assumes that a Visual Page Definition is being used to implement this functionality. The example uses a Buttons Part to demonstrate the functionality, however, other Parts can also be used (e.g. the Form Buttons Part, Tile Parts, etc.).

Within the Code tab of the Visual Page Definition, the following using statement must be added to control the services with the API:
    
    
    using ETS.Ts.Core.Services.Web.StatusActivities;
    

Then, declare an Activity Helper variable. This is used to display active progress of an activity through a standard webpage. More information about LongRunningActivity can be found [here](https://portal.parsec-corp.com/hc/en-us/articles/360038064413-Debugging-Best-Practices).
    
    
    // Declare a Long Running Activity Helper variable
    private LongRunningActivityPageHelper _activityHelper;
    

Next, place the following code within the `ContentPage_Init()` method of the page. 
    
    
    _activityHelper = this.Ets.Api.Create.InstanceOf<LongRunningActivityPageHelper>();
    _activityHelper.IsProgressBarVisible = false;
    // This property can be changed to redirect to a desired page on success
    // _activityHelper.DefaultWaitForSuccessUrl
    

From here, button handler methods can be added to control the Start, Stop, and Restart actions for each service. The example below will attempt to start the Logic Service with an ID of 1:
    
    
    private void Start_Click(object sender, EventArgs e)
    {
      //The ID of of the Logic Manager Service in tLogicManager
      int logicID = 1;
      _activityHelper.RequestActivity(logicID, this.ActualStartLs, "Starting Service...");
    }
    
    private void ActualStartLs(int logicID, LongRunningActivityContext context)
    {
      // Possible values are: "Logic Service", "Historian Service", "Workflow Service", "Data Management Service", "Maintenance Service"
      string serviceType = "Logic Service";
      var svc = context.Api.Create.InstanceOf<ETS.Core.Services.Security.ManagedTsServiceController>();
      // Start the Logic Service
      svc.StartService(serviceType, logicID, context.StatusUuid);
    
      // Stop the Logic Service
      // svc.StopService(serviceType, logicID, context.StatusUuid);
      // Restart the Logic Service
      // svc.RestartService(serviceType, logicID, context.StatusUuid);
    }
    

### Controlling Data Management Service Modules Using the API (TrakSYS 13+)

Starting with TrakSYS 13, individual Modules can now be started, stopped, and restarted using the TrakSYS API. This is in addition to the example above for the parent Data Management Service. This functionality is available within all scripting areas of the TrakSYS application (e.g. the TS Web, Logic Script Classes, Script Class Tags, Script Tags, Workflow Script Steps, Module Script Steps, Web Scripts, Shared Scripts, etc.). Slight syntax changes will be required depending on the area executing the code. This can be useful for controlling individual Modules without having to access the application server or the TrakSYS Installation Manager.

**Note** : The parent Data Management Service (DMS) must be running when the code is executed in order for this feature to function as intended.

### Example

The following example shows how to control individual Modules using the API. This example assumes that a Visual Page Definition is being used to implement this functionality. The example uses a Buttons Part to demonstrate the functionality, however, other Parts can also be used (e.g. the Form Buttons Part, Tile Parts, etc.).
    
    
    private void ModuleServiceControl(object sender, EventArgs e)
    {
      try
      {
        // Provide the Module Name
        string moduleName = "YourModuleNameHere";
        // Alternatively, the Module ID can be provided instead
        //int moduleID = 1; // Provide a valid ModuleID
    
        // Start Options
        // Start the Module with the provided Name
        this.Ets.Api.Data.DbModule.Do.StartModuleByName(moduleName).ThrowIfFailed();
        // Start the Module by Module ID
        //this.Ets.Api.Data.DbModule.Do.StartModule(moduleID).ThrowIfFailed();
    
        // Stop Options
        // Stop the Module with the provided Name
        //this.Ets.Api.Data.DbModule.Do.StopModuleByName(moduleName).ThrowIfFailed();
        // Stop the Module by Module ID
        //this.Ets.Api.Data.DbModule.Do.StopModule(moduleID).ThrowIfFailed();
    
        // Restart Options
        // Restart the Module with the provided Name
        //this.Ets.Api.Data.DbModule.Do.RestartModuleByName(moduleName).ThrowIfFailed();
        // Restart the Module by Module ID
        //this.Ets.Api.Data.DbModule.Do.RestartModule(moduleID).ThrowIfFailed();
      }
      catch (Exception ex)
      {
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

As mentioned in the code comments above, either a Module ID or the Module Name can be provided. Then the TrakSYS API can be used to Start, Stop, or Restart the individual Module based on the given ID or Name.
