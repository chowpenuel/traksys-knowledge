# Starting a Workflow Process Using Custom Code

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824885158675-Starting-a-Workflow-Process-Using-Custom-Code*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 11.1.0+

In [TrakSYS 11.1.0](https://portal.parsec-corp.com/hc/en-us/articles/360043699394-What-s-New-in-TrakSYS-11-1), Visual Workflow functionality was added to the TrakSYS software. This feature allows users to create Workflow diagrams representing different processes. These diagrams can the be updated in real time as steps are executed and completed. While Workflow Processes can be started manually though the built-in TrakSYS pages, they can also be executed programmatically. More specifically, a Process can be executed with the TrakSYS API using the WorkflowService (`Api.Workflow`).

Assuming that a Process Definition has been configured, the following is a simple example of how to programmatically start a Workflow Process. The example was created within a button click method on a Visual Page Definition. Similar code can be used in other areas of the application (e.g. Module Script Steps, Script Classes, etc.).
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Provide a Process Key from an existing Process Definition
        string ProcessKey = "ProcessDefinitionKeyHere";
        
        // Create Process Definition Sink Object
        var sinkObject = this.Ets.Api.Workflow.CreateProcessSinkStart(ProcessKey)  
                                                                .ThrowIfFailed();
    
        // Insert the Sink object into the Database
        this.Ets.Api.Data.DbProcessSinkStart.Save.InsertAsNew(sinkObject)  
                                                        .ThrowIfFailed();
      }
      catch (Exception ex)
      {
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

As the example demonstrates, a Process Definition Sink Object is created and takes in the Process Definition Key as a parameter. The object is then inserted into the tProcessSinkStart table. From here, the record will be processed, the Workflow Process will start, and the tProcessSinkStart record will be removed from the table.
