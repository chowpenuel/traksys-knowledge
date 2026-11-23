# Debugging

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360038064413-Debugging*
*Last updated: 2025-02-06T23:47:42Z*

---

### Summary

Scripting in TrakSYS is different than scripting in Visual Studio or other scripting software. Some familiar capabilities do not exist in a web-based development tool. However, there are various tools available to help fill these gaps. This article is an introduction to some of the troubleshooting and debugging tools used in TrakSYS. The listed examples and information are for demonstration purposes and do not represent all available options.

### Result Objects

When using the API to write to the TrakSYS database, the methods typically return a [Result<T>](https://docs.parsec-corp.com/api-reference/api-models-reference/api-models/result-t) object. The Result objects include the following properties and methods:

  * [ Method ] `ThrowIfFailed()`
  * [ Property ] `Messages`
  * [ Property ] `Return`
  * [ Property ] `Success`



These Result objects are essential to troubleshooting errors in script in a controlled manner. They provide an updated model and additional context when writing and _should never be ignored_. The `ThrowIfFailed` method can be used as a quick way to enforce validation before continuing. The three listed properties can be used to create more extensive troubleshooting. More information on this extension method can be found [here](https://docs.parsec-corp.com/tsweb/scripting/extension-methods).

### Ets.Debug

In the TS Web, there are special debug tools that are designed to interact with the Trace Log and display error messages. These are accessible through `this.Ets.Debug`.

The following methods are useful for custom error-handling:

  * [ Method ] `this.Ets.Debug.FailContentPage()`
  * [ Method ] `this.Ets.Debug.FailFromException()`
  * [ Method ] `this.Ets.Debug.FailFromResultMessages()`



`FailContentPage` will allow for the input of a custom error message that can be displayed. `FailFromException` works easily with try-catch blocks. `FailFromResultMessages` works with the Result object mentioned above.

The following methods are useful when troubleshooting during Page execution:

  * [ Method ] `this.Ets.Debug.Trace()`
  * [ Method ] `this.Ets.Debug.TraceObject()`



These methods provide a way to write to the Trace Log. `Trace` allows for a custom message to be inserted into the Trace Log at that time in the Page’s execution. It is useful to track specific points of time in the execution and to output the information at that point. `TraceObject` is similar, but it allows for an entire object to be inserted into the Trace Log, with the object’s properties being written out for extensive troubleshooting. More information on these debug methods can be found [here](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/scripting/page-definition-scripting/properties/debug.html).

### Logs and Custom Logs

Outside of the TS Web, there is no Trace Log. Instead, errors and troubleshooting are completed through the two Log tables, `tLog` and `tLogCustom`. `tLog` is the default table used by the standard components of TrakSYS. It may include many other records that are automatically generated. `tLogCustom` is not natively used by TrakSYS. It contains fewer columns but can be utilized by custom scripts for more isolated and extensive record keeping. The `tLog` and `tLogCustom` can be accessed and written to using the following calls:

  * `Ets.Api.Util.Log.WriteError()`
  * `Ets.Api.Util.Log.WriteErrorsFromResultObject()`
  * `Ets.Api.Util.Log.WriteException()`
  * `Ets.Api.Util.Log.WriteInformation()`
  * `Ets.Api.Util.LogCustom.Write()`
  * `Ets.Api.Util.LogCustom.WriteError()`
  * `Ets.Api.Util.LogCustom.WriteErrorsFromResultObject()`
  * `Ets.Api.Util.LogCustom.WriteException()`
  * `Ets.Api.Util.LogCustom.WriteInformation()`



Each call has a different set of parameters and will write to the log with different categories and information. Using the appropriate call will make filtering information as easy as possible. More information on these methods can be found starting [here](https://docs.parsec-corp.com/api-reference/api-services-reference/api.util/api.util.log/writeerror).

### Debug Unit of Work

When interacting with the database through the API, no SQL is needed to complete reads or writes. For more complex interactions, this can involve saving many objects at once. To ensure that the entire transaction is completed successfully, a [Unit of Work](https://docs.parsec-corp.com/api-reference/api-models-reference/unitofwork) is used to treat it all as a single batch transaction. This, however, does not always provide a lot of visibility into what is occurring. To view the transactions that the API attempts, the Unit of Work can be replaced with a Debug Unit of Work.

To create one, the following can be used:
    
    
    this.Ets.Api.Create.InstanceOf<DebugUnitOfWork>();
    

It will create a `DebugUnitOfWork` object that can be used interchangeably with the normal `UnitOfWork` object in the various API calls. However, this `DebugUnitOfWork` will not actually commit records to the database when executed. It will instead output the full transaction’s query to the Trace Log for debugging purposes. The result may look something like this:
    
    
    DECLARE @pID int = 112
    DECLARE @pIsTemplate bit = 0
    DECLARE @pTemplateParentID int = NULL
    
    [… all other properties …]
    
    UPDATE dbo.tSystem SET 
    [IsTemplate] = @pIsTemplate, [TemplateParentID] = @pTemplateParentID
    
    [… all other properties … ]
    
    WHERE [ID] = @pID
    

This provides a useful SQL-based view into the transactions that are being run through the API.

### Long Running Activity

In web pages that run a lot of scripts or logic, the user can be left on a Page for an extended period waiting for an update without any visual cues while the logic is processed. To make it more interactive, `LongRunningActivity` can be used to display active progress of an activity through a standard webpage. This can be accomplished through the use of `LongRunningActivityPageHelper`.

First, the helper is created:
    
    
    _activityHelper = this.Ets.Api.Create.InstanceOf<LongRunningActivityPageHelper>();
    

Then in a given method, the helper calls an activity using the following pattern:
    
    
    _activityHelper.RequestActivity(_params, this.Long_Running_Method, "Some Description...");
    

The method that is run will be whatever “Long_Running_Method” is replaced with, and the params will be passed in as well.

The called method will need a signature that has the first parameter for the params, and a second parameter for `LongRunningActivityContext`. It will look something like this:
    
    
    private void My_Long_Running_Method(ExampleParamObject paramInfo, LongRunningActivityContext context)
    

When the activity helper is used, it will redirect the user to a `LongRunningActivity` Page. In the method identified in the activity helper request, the `context` object can be used to update the status and progress bar during the logic processing. It will look something like this:
    
    
    var status = context.Status;
    status.UpdateStatus("Starting Long Running Process...", 0);
    

The status can be updated as many times as needed. There are also various other status-updating extension methods available.
