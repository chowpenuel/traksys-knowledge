# Accessing the TrakSYS API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/43625704630035-Accessing-the-TrakSYS-API*
*Last updated: 2025-08-13T18:08:07Z*

---

### Summary

The TrakSYS API can be used in various areas of the application and in external applications while performing development work. However, accessing the API varies slightly depending on the TrakSYS context. This article describes the various ways of referencing existing instances of the API and how to create new ones as needed.

### Existing API Instances in TrakSYS

In the following areas of the application, an instance of the API is already available for use (the samples below show a local variable, `api`, being set to the instance for additional simplicity). 

#### Logic Service Script Classes

In all Logic Service Script Class types, the TrakSYS API is available through the `context` object passed in for each of the methods:
    
    
    /// ******************************************************************
    /// <summary>This method is called at the end of each Logic Service scan.</summary>
    /// ******************************************************************
    public override void PostScan(IPostScanContext context)
    {
      ETS.Core.Api.ApiService api = context.Api;
    }
    

#### TrakSYS Web

The TrakSYS API is part of the `Ets` object within the page Script tab:
    
    
    /// ***********************************************************
    /// <remarks>
    /// All Page level ContentProperties have been set from default
    /// values or Ets.Values. Content Parts are not yet loaded/initialized.
    ///
    /// Do things like:
    ///   Check Page Permissions
    ///   Set Resource Strings
    /// </remarks>
    /// ***********************************************************
    protected override bool ContentPage_Init()
    {
      ETS.Core.Api.ApiService api = this.Ets.Api;
      return true;
    }
    

#### Module Script Steps

When using Data Management Service Modules, the TrakSYS API is accessible through the use of Module Script Steps. It is made available through the `context` object provided for the `Execute()` method:
    
    
    /// ******************************************************************
    /// <summary>
    /// This method is called each time this Step is executed within the Module.
    /// This is where the main code for Step execution should be placed.
    /// </summary>
    /// ******************************************************************
    public override bool Execute(IModuleContext ctx)
    {
      ETS.Core.Api.ApiService api = ctx.Api;
      return true;
    }
    

#### Workflow Process Execute Script Steps

The TrakSYS API is part of the `Ets` object within the Execute Script Step:
    
    
    // Reference the API Service
    ETS.Core.Api.ApiService api = Ets.Api;
    

#### Production Scheduling Plugins (Discrete and Batching)

When using Production Scheduling Plugins, an instance of the TrakSYS API has been created and made available in a class level variable. The following code is automatically included in both Discrete and Batching Plugins:
    
    
    private readonly ApiService _api;
    
    public Another_Discrete_PS_Script(ApiService api)
    {
      _api = api;
      this.Settings = null;
    }
    

The `_api` variable can then be used to access the TrakSYS API in any of the other methods within the Plugin.

#### TrakSYS Connect Plugins

When using TrakSYS Connect Plugins, each method will have a `context` object that can be used to access the TrakSYS API. The type of `context` object can change depending on whether it is created for a Payload Definition or an Interface Definition. If it is created for a Payload Definition, the type of Payload can also have an impact on the type of `context` object (e.g., XML, JSON, CSV, Query String, String Only, Custom, etc.). The following code example was taken from a Payload Definition Connect Plugin with a JSON data type:
    
    
    public Result<bool> Init(IInterfacePluginContext context, InterfaceDefinitionFilePullSettings settings)
    {
      var r = new Result<bool>();
    
      **ETS.Core.Api.ApiService api = context;**
    
      return r.AsSuccess(true);
    }
    

#### Script Tags (Advanced Scripting)

The TrakSYS API is accessible through the global `Context` object that is available to all Script Tags:
    
    
    // Reference the API Service
    ETS.Core.Api.ApiService api = Context.Api;
    

#### Script Class Tags (Tag Script Class)

The TrakSYS API is accessible through the global `Context` object that is available to all Tag Script Classes:
    
    
    /// ******************************************************************
    /// <summary>
    /// This method is called to evaluate the value for the script tag.
    /// </summary>
    /// ******************************************************************
    public override object EvaluateValue()
    {
      ETS.Core.Api.ApiService api = this.Context.Api;
      return null;
    }
    

#### Database Transfer Scripts

When using Database Transfer Scripts, the TrakSYS API is accessible through the `context` object provided in each method. Note that the type of context object will vary depending on the method and type of Database Transfer Script (e.g., Export Plugin or Import Plugin). The example below was used in an Export Plugin:
    
    
    /// ***********************************************************
    /// <summary>
    /// This method is the first plugin method to be called and
    /// occurs before any data is exported into the Xml Document.
    /// </summary>
    /// ***********************************************************
    public override bool PreExport(XDocument doc, IDatabaseTransferExportContext context)
    {
      ETS.Core.Api.ApiService api = context.Api;
      return true;
    }
    

### Creating an Instance of the TrakSYS API

In the following areas of the application, the API must be instantiated prior to its use (the samples below show a local variable, `api`, being set to the instance for additional simplicity).

#### Custom Script Classes

The TrakSYS API can be used in custom scripts (e.g. Web Scripts, Shared Scripts, Module Shared Scripts, and Workflow Scripts) once it has been instantiated.
    
    
    // Get an instance of the API Service
    ETS.Core.Api.ApiService api = ETS.Core.Api.ApiService.GetInstance();
    

#### External Applications

The TrakSYS API can be used by referencing the `Core.Api.dll` file located in the root TrakSYS directory under **...\Program Files (x86)\Parsec\TrakSYS** for TrakSYS 11.2.5 and older or **...\Program Files\Parsec\TrakSYS** for TrakSYS 12+. Once this file has been referenced, the following code can be used to connect to the installation:
    
    
    // set the connection info (only required when the API code is NOT running on a machine with TrakSYS components installed)
    var ci = new ETS.Core.Api.Models.ConnectionInfo();
    ci.ApplicationName = "APPNAME";
    ci.Server = "SERVERNAME";
    ci.Name = "DATABASENAME";
    ci.Login = "edbApp";
    ci.Password = "Sqlapp!23";
    ci.UsesWindowsAuthentication = false;
    
    var api = ETS.Core.Api.ApiService.StartupNewApplicationWithConnectionSettings(ci);
    
    // the api object can now be used
    
    

**Note** : The [StartupNewApplicationWithConnectionSettings()](https://docs.parsec-corp.com/api-reference/accessing-api/external-application) method should only be used on startup within external applications. Attempting to use it inside of the TrakSYS application can cause serious issues in the TrakSYS Web.
