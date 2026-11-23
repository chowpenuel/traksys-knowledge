# Long Running Status Activity Example

*Source: https://portal.parsec-corp.com/hc/en-us/articles/1500012496401-Long-Running-Status-Activity-Example*
*Last updated: 2025-05-21T22:53:20Z*

---

Applies to | TrakSYS 10+

### **Summary**

In TrakSYS 10, the Long Running Status Activity Helper functionality was implemented. This is a new infrastructure that can be used for initiating and visualizing the status of long running operations. This process replicates an async status bar experience from the User Interface (UI). In TrakSYS 11, this functionality was improved so that custom JavaScript code was no longer required for it to function. It was also simplified to a C# helper class instead of a Part. This functionality is useful in scenarios where a long running action is required and real time status updates should be provided during the progress.

While the example in this article uses a Visual Page Definition, it can be used in other parts of the TrakSYS software (such as a Data Management Service Module). When the Long Running Status is initiated, a record is created in the tLongRunningStatus table. The UI can then display the results of the record by referencing the GUID field while the process is progressing. After the process is complete, the Maintenance Service will remove the record from the table. While the process is executing, the Wait For Status Activity page is used to display updates to the user. This is different from other built-in Wait For pages, which simply wait for a process to finish.

The following example was created using a Visual Page Definition with a Buttons Part. **Note** : The code uses `System.Threading.Thread.Sleep()` in several areas to simulate a delay. This is only for demonstration purposes and should **not** be used in real world installations.

### **Example**

To use the Long Running Status Activity, the following `using` statements need to be added.
    
    
    using ETS.Ts.Core.Services.Web.StatusActivities;
    using ETS.Core.Api.Services.StatusActivities;
    

The following parameters can then be declared. The `_activityHelper` variable shown below will contain the configuration options and properties for the Status Activity Helper. This allows users to set properties such as success URLs, failure URLs, timeout values, and more.
    
    
    private Dictionary<string,string> _params;
    private LongRunningActivityPageHelper _activityHelper;
    

The code below provides a simulated example of how the Long Running Status Activity feature can be used. The `ButtonClick()` method is passing values into the `UpdateIntervalCount()` method when the user clicks a button. From here, several updates are being logged as the process progresses. The `UpdateProgress()` method can be used to increment the overall progress on the Progress Bar. The `UpdateStatus()` method is then used to write status messages to the page while the process is running.
    
    
    protected override bool ContentPage_Init()
    {
      _params = new Dictionary<string,string>();
      _activityHelper = this.Ets.Api.Create.InstanceOf<LongRunningActivityPageHelper>();
      return true;
    }
    
    /// **********************************************************
    protected void ButtonClick(object sender, EventArgs e)
    {
      this.Ets.Form.UpdateModelValueByFormKey("Example.", _params);
      if (!this.Ets.Form.IsValid) return;
      // run the activity helper
      _activityHelper.RequestActivity(_params, this.UpdateIntervalCount, "Update is running...");
    }
    
    /// ***********************************************************
    private void UpdateIntervalCount (Dictionary<string,string> paramInfo, LongRunningActivityContext context)
    {
      try
      {     
        // method uses Thread.Sleep to mimic processing delays
        System.Threading.Thread.Sleep(1500);
    
        var status = context.Status;
        status.UpdateStatus("Update Started...");
        System.Threading.Thread.Sleep(1500);
    
        // Adds a new message to the top of the progress bar, updates the progress bar to 21.1%, and adds an icon to the message
        status.UpdateStatus("Running Step 1 of 3 – Updating DateTime...", 0.211, "fa-hourglass-start");
        System.Threading.Thread.Sleep(200);
        
        // Updates the progress bar to 33%
        status.UpdateProgress(0.33);
        System.Threading.Thread.Sleep(2000 + 2700);
    
        // Updates the progress bar to 66%
        status.UpdateStatus("Running Step 2 of 3 – Updating Count...", 0.66);
        System.Threading.Thread.Sleep(2000 + 3840);
    
        // Updates the progress bar to 99%
        status.UpdateStatus("Running Step 3 of 3 – Final Check...", 0.99);
    
        System.Threading.Thread.Sleep(2000 + 2950);
        status.UpdateStatusAsSuccess("Update finished!");
      }
    
      catch (Exception ex)
      {
        context.Status.UpdateStatus(ex.Message);
        context.Status.UpdateStatusAsFailure("Failed");
      }
    }
    
