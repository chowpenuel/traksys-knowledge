# Scripting Best Practices and Anti-Patterns

*Source: https://portal.parsec-corp.com/hc/en-us/articles/22461914877587-Scripting-Best-Practices-and-Anti-Patterns*
*Last updated: 2025-08-07T21:52:32Z*

---

### Summary

This document provides a set of scripting best practice guidelines showing how to most efficiently use the TrakSYS platform. It also highlights various Anti-Patterns, which are commonly used practices that go against best practices.

### Terminology

A scripting **Best Practice** is defined as a set of informal rules that the software development community has learned over time, which can help improve the quality of software. In other words, these are guidelines for code that are most optimal for maintainability, quality, dependability, efficiency, and usability.

A scripting **Anti-Pattern** is defined as a common response to a recurring problem that is usually ineffective and risks being highly counterproductive. In other words, these are common practices that should **not** be used as they can be highly inefficient, not maintainable, or can potentially introduce additional issues to the solution.

**Note** : Not all Best Practices listed below will have an Anti-Pattern and not all Anti-Patterns will have an associated Best Practice.

### Scripting Best Practices and Anti-Patterns

#### Best Practice : Check the Result object for Success  
Anti-Pattern : Ignore the Result object

When using the TrakSYS API, many of the methods return the `Result<T>` object. One key property of this object is the `Success` property which returns a value based on whether or not the operation was successful. If the operation is not successful, the method will populate the `Messages` list with reasons that explain root cause of the failure. If the process is successful, then the `Return` property will contain the desired content instead.

#### Anti-Pattern Example
    
    
    var dt = this.Ets.Api.Util.Db.GetDataTable(sql).Return;
    

This can work most of the time, but can occasionally fail. When it does fail, the end result will be the unhelpful "Object referenced not set to an instance of an object" error message.

#### Best Practice Example : Option 1 - ThrowIf Extension Methods
    
    
    var dt = this.Ets.Api.Util.Db.GetDataTable(sql).ThrowIfFailed();
    

The code required for this Best Practice is slightly longer than the Anti-Pattern example. However, instead of returning a `NULL` on failure, it will instead throw an Exception. The behavior will be similar to the above example, except that the failure message will provide more useful information about the root cause of the failure.

#### Best Practice Example : Option 2 - Using the Form Validation Summary Part
    
    
    var resultDt = this.Ets.Api.Util.Db.GetDataTable(sql);
    if (!this.Ets.Form.AddResultMessagesWithPrefixIfFailed(resultDt, "")) return false;
    

The code example above requires a "Form Validation Summary Part" (`ETS.Forms.TsValidationSummary`) on the page. If the process fails, the code will exit the current function and display error messages based on how the Form Validation Summary part is configured. This is useful for giving information to end users explaining why a failure happened without failing the entire page.

#### Best Practice Example : Option 3 - Using Debug.Fail
    
    
    this.Ets.Debug.FailFromResultMessages(resultDt.Messages);
    

This approach is very similar to the first option. It is particularly useful when executing code inside of Server Click handlers if they do not have Try Catch logic. With this method, if any Exceptions are raised, the entire page will error and the user will be redirected to an error page. With this approach, the failure of the page will be determined by the `PageMode` setting (values of either `DebugMode` or `RedirectOnError`). This setting can be found under the Webs section of the TrakSYS Settings dialog window through the TrakSYS Installation Manager.

#### Best Practice Example : Option 4 - Custom Error Handling
    
    
    var resultDt = this.Ets.Api.Util.Db.GetDataTable(sql);
    if (!resultDt.Success)
    {
      // custom code to handle failure
    }
    

This example acknowledges the fact that the method could fail and includes custom logic to handle these scenarios. This is preferable as it does not assume that the call will always be successful.

#### Best Practice : Add values to a Dictionary using the Accessor  
Anti-Pattern : Add values to a Dictionary using the `Add()` method

When adding key-value pairs to a Dictionary, it is usually to add or overwrite a value. This is especially true with `IEtsValuesDictionary` as new data can be added to the Values Dictionary from a variety of locations. If the `Add()` method is used, it can cause the page to produce an error of "An item with the same key has already been added" if the key already exists in the Dictionary.

#### Anti-Pattern Example
    
    
    this.Ets.Values.Add("SubSystemID", -1);
    

This example will fail if the URL for the page is similar to `mypage?SubSystemID=1` or if the key has been added from any other possible area that is able to add Values Dictionary values.

#### Best Practice Example
    
    
    this.Ets.Values["SubSystemID"] = -1;
    

This example will either add the new key of "SubSystemID" to the dictionary, or overwrite the existing value with -1 if it already exists. It will perform this process without generating an error message. However, there might be times where displaying an error message may be desirable. In these scenarios, it is recommended to use `ContainsKey("SubSystemID")` and provide a more useful error message.

#### Best Practice : Retrieve values from a Dictionary using the GetAs Extension methods  
Anti-Pattern : Retrieve values from a Dictionary using the Accessor

When retrieving values from a Dictionary, it is recommended to use one of the available [GetAs() extension methods](https://docs.parsec-corp.com/tsweb/scripting/page-definition-scripting/properties/values). Many data structures in TrakSYS are stored in a Dictionary. Therefore, enabling access to a consistent data retrieval is considered a scripting Best Practice.

#### Anti-Pattern Example
    
    
    int subSystemID = (int)this.Ets.Values["SubSystemID"];
    

The code in the example above will produce an error message if the "SubSystemID" key does not exist in the Dictionary. It will also produce an error if the value inside the Dictionary is not a valid type that can be directly cast as an integer (e.g., if the value for the key "SubSystemID" is a string value of "1", an error will still be produced).

#### Best Practice Example
    
    
    int subSystemID = this.Ets.Values.GetAsInt("SubSystemID");
    

The code in the example above will not produce an error message. If the key does not exist, it will return the `defaultValue` instead (for integer values in TrakSYS, this is typically a value of -1). If the value stored in the "SubSystemID" key is a string, it will attempt to cast the string to an integer and return that value (e.g., if the value is "1" it will return the integer value of 1). If the value in the dictionary contains a data type that cannot be cast to an integer (e.g., a string with a value of "this is not a number"), then the value of the subSystemID key will be -1.

#### Best Practice : Using the Post Redirect Get (PRG) pattern of web development  
Anti-Pattern : Not redirecting after success when a server click event is raised

#### Anti-Pattern Example
    
    
    uow.Execute();
    return;
    

The example shown above will execute the unit of work and push the changes to the database. However, if the user is not redirected, the page will not be updated with new information. This can cause confusion for users viewing the page and they may try to click the button or link again thinking that the first execution did not register or succeed.

#### Best Practice Example
    
    
    var result = uow.ExecuteReturnsResultObject();
    if(!result.Success)
    {
      this.Ets.Debug.FailFromResultMessages(result);
      return false;
    }
    this.Ets.Pages.RedirectToPageUrl();
    return true;
    

This approach not only adds additional error handling, but redirects the user on success. This redirection will automatically refresh the content on the page (if the page is redirected to itself) or to a different page giving the user a visual cue that the operation succeeded. More information about the PRG method of web development can be found in the last section of **[this article](https://portal.parsec-corp.com/hc/en-us/articles/360009094974-User-Interface-Design)**.

#### Best Practice : Retrieve values from a DataRow using the Get Extension methods  
Anti-Pattern : Retrieve values from a DataRow using the Accessor

#### Anti-Pattern Example
    
    
    DataRow dr = dt.Rows[0];
    int sysID = dr["SystemID"].AsInt();
    

Using the code above will fail the entire page and can produce obscure error messages. Additionally, the process will fail any time a provided value cannot be converted into the desired data type (e.g., an Integer in this case). Finally, this method does not allow a default value if the process does fail.

#### Best Practice Example
    
    
    DataRow dr = dt.Rows[0];
    int sysID = dr.GetInteger("SystemID");
    

This approach provides more descriptive error messages if the process fails. Additionally, if the value cannot be converted into the specified data type, a default value can be provided for the field instead. This allows the developer to output any failure messages to the page or log file without failing the entire page.

#### Best Practice : Using `ToSql()` or `ToSqlNullable()` extension methods to insert parameters into custom SQL  
Anti-Pattern : Inserting raw parameters into custom SQL

#### Anti-Pattern Example
    
    
    string sysKey = "PL1";
    string sql = "SELECT * FROM tSystem WHERE [Key] = '{0}'".FormatWith(sysKey);
    

The code example above will attempt to use the raw value provided for the query. While this can work in most cases, issues can arise if the value contains special characters that need to be escaped. Additionally, depending on how the query is written, this method is susceptible to SQL injection attacks.

#### Best Practice Example
    
    
    string sysKey = "PL1";
    string sql = "SELECT * FROM tSystem WHERE [Key] = {0}".FormatWith(sysKey.ToSql());
    

This approach uses the `ToSql()` extension method, which provides automatic encoding for values that contain special characters. It also has some built-in safeguards to help prevent SQL injection attacks.

#### Best Practice : Using `GetStartDateTimeOffset()` to retrieve DateTimeOffset values  
Anti-Pattern : Using `GetAsDateTimeOffset("SDT")` to retrieve DateTimeOffset values

#### Anti-Pattern Example
    
    
    DateTimeOffset startDateTime = this.Ets.Values.GetAsDateTimeOffset("sdt", this.Ets.SiteNow);
    DateTimeOffset endDateTime = this.Ets.Values.GetAsDateTimeOffset("edt", this.Ets.SiteNow);
    

This method will return the actual value for the SDT and EDT keys. While this may work, it can return drastically different results depending on how it's used in queries. Additionally, it only factors in the values specifically for the SDT or EDT Keys. It does not account for the built-in SD or ED keys if the data suddenly relies on date instead of a full date time offset value.

#### Best Practice Example
    
    
    DateTimeOffset startDateTime = this.Ets.Values.GetStartDateTimeOffset();
    DateTimeOffset endDateTime = this.Ets.Values.GetEndDateTimeOffset();
    

The calls used above are mainly used for the built-in Filter Parts (or code that also uses the built-in Filter structure that these Parts use). Additionally, these methods have extra checks that are included which can reference the SD or ED Values Dictionary keys if a value is not provided for the standard SDT or EDT keys. Furthermore, the value is optimized to display data from queries using a BETWEEN statement when retrieving data. If multiple pages use this call, these optimizations will be uniform across each page to ensure that the data is consistent.

#### Best Practice : Using `ToVariantString()` or `AsIntFromVariant()` to load variant values  
Anti-Pattern : Using the raw strings of variant values or static Parse methods

#### Anti-Pattern Example : Option 1 - Using the raw strings of variant values
    
    
    DbOeeInterval interval = this.Ets.Api.Data.DbOeeInterval.Load.ByID(123);
    string customMetric = interval.Capture01;
    

The issue with the method above revolves around value conversions. This is more prevalent for values that can change based on different languages and cultures. For example, different cultures can use different types of number separators. If the value switches from using a period to a comma to distinguish a decimal value based on a change in the user's culture (e.g., language code), it can cause issues if the solution is programmed to look specifically for the period character.

#### Anti-Pattern Example : Option 2 - Using static Parse methods on raw variant values
    
    
    DbOeeInterval interval = this.Ets.Api.Data.DbOeeInterval.Load.ByID(123);
    double customMetric = double.Parse(interval.Capture01);
    

While the code above may work for a current solution, it does not account for any changes that may occur in the future. The values stored in the Capture Fields are strings. Therefore, it can be possible to store multiple types of values that can be parsed into different data types. If the data type of the value stored in the Capture Field changes, then any static Parse methods looking for the previous data type may no longer work. Additionally, the error messages thrown by these methods are usually unhelpful.

#### Best Practice Example
    
    
    DbOeeInterval interval = this.Ets.Api.Data.DbOeeInterval.Load.ByID(123);
    // do null check on interval
    int customMetric = interval.Capture01.AsDoubleFromVariant(0.00);
    

This method is preferred as it has several built-in checks that account for the issues mentioned in the first two options. It can help resolve differences in number separators across different cultures to maintain uniform results. Additionally, it helps verify the data type of the provided value. If the value cannot be casted to the specific data type, a default value can be provided instead of failing the entire page.

#### Best Practice : Using `AsInt()` or `ConvertUtil()` to retrieve and convert values  
Anti-Pattern : Using `int.Parse` to retrieve and convert values

#### Anti-Pattern Example
    
    
    DbEvent ev = this.Ets.Api.Data.DbEvent.Load.ByID(123);
    int vendorID = int.Parse(ev.Capture01);
    

The code example above can produce obscure error messages when the process fails and it will fail the entire page.

#### Best Practice Example
    
    
    DbEvent ev = this.Ets.Api.Data.DbEvent.Load.ByID(123);
    int vendorID = ev.Capture01.AsInt(-1);
    

Using the TrakSYS extension method shown above can provide more informative error messages if the conversion fails. Additionally, it provides the option to specify a default value. This way, if the conversion fails, the default value will be provided and any error messages can be logged to the page or the TrakSYS log file. This way, it will not fail the entire page.

#### Best Practice : Using `Ets.Values.CopyFromModel()` or `Ets.Form.UpdateModelWithKeyPrefix()` for to retrieve or save data with Forms Parts

#### Best Practice Example
    
    
    DbEvent ev = this.Ets.Api.Data.DbEvent.Load.ByID(123);
    bool result = this.Ets.Values.CopyFromModel(ev, "Event.");
    
    
    bool updateResult = this.Ets.Form.UpdateModelWithKeyPrefix(ev, "Event.");
    

Using the TrakSYS API provides a consistent and sustainable way to map properties between a TrakSYS object and a User Interface. This is typically achieved by using the built-in Model Object structure. The best practice pattern is sustainable throughout version upgrades and works with Trace Logging to assist with troubleshooting. Without using the TrakSYS API calls, a developer would need to manually map each individual property of the model, which provides numerous opportunities for errors, requires more significant maintenance during version upgrades, and would require additional development time to implement supporting troubleshooting methods.

#### Best Practice : Using the built-in responsive CSS to adjust elements  
Anti-Pattern : Using style attribute inline with set sizes

#### Anti-Pattern Example
    
    
    <div style="padding-left: 20px;">indented</div>
    

The example above uses a hard-coded size, which can be problematic when viewing the page on different types of devices. For example, if a user views the element on a very large screen, the rendering may not line up with other elements on the page. Inversely, if the element is viewed on devices with smaller screens (such as smartphones), the sizing may be too large and push other elements down which can create an undesirable experience.

#### Best Practice Example
    
    
    <div class="tsmargin-sm-left-small">indented</div>
    

This solution uses built-in responsive classes that will automatically adjust with the size of the screen. This eliminates any rendering issues for more extreme scenarios.

#### Best Practice: Using Model Objects to get the next ID or using `GetNextSequenceByKey()`  
Anti-Pattern : Using `SELECT MAX(ID)` to get the next ID

#### Anti-Pattern Example
    
    
    DbEvent ev = this.Ets.Api.Data.DbEvent.Create.FromParentEventDefinition(parent);
    string sql = @"SELECT MAX(ID) FROM tEvent";
    int maxID = this.Ets.Api.Util.Db.ExecuteScalar<int>(sql, -1).ThrowIfFailed();
    ev.ID = maxID + 1;
    

The primary issue with the code above is that it does not increment the associated record in the `tSequence` table. The TrakSYS services rely on the `tSequence` table to retrieve ID values every time an entry is written to a table. If a user manually inserts a record with a hard-coded ID value, a TrakSYS service (such as the Logic Service) will get the next value in `tSequence` and attempt to use it for the newest record. This process disregards the current highest ID in the table. Therefore, when the record insertion is attempted, the process will fail and produce a "FOREIGN KEY constraint" error message.

Additionally, this does not account for ID values that have been used and deleted, which can result in compromised auditing data.

#### Best Practice Example : Option 1 - Use Model Objects to get the next ID

If Model Objects are being used for built-in TrakSYS tables, it is not necessary to specify a value for the ID field of any entity. When the changes are pushed to the database, the API will automatically retrieve the next value for that entity in the `tSequence` table on record creation. This eliminates the potential for a "FOREIGN KEY constraint" error message while slightly reducing the amount of code required to create the entity.

#### Best Practice Example : Option 2 - Use the `GetNextSequenceByKey()` method to get the next ID
    
    
    int nextEventID = this.Ets.Api.Util.Db.GetNextSequenceByKey("EventID");
    

For scenarios where Model Objects cannot be used or if retrieving the next ID in sequence for a specific entity is required, something similar to the code shown above should be used. This will help ensure that there are no ID conflicts when the record is created.

#### Best Practice : Use `<%:` or `<%#:` to reference values using ASP.NET  
Anti-Pattern : Use `<%=` or `<%#` to reference values using ASP.NET

#### Anti-Pattern Example
    
    
    <%= this.OutputName %>
    

This method uses an older .NET style syntax that was mainly used to inject ASP.NET objects. This can be used in View Fragment parts to render values. While this method can work, there can be issues if the value contains special characters (e.g., /, \, *, <, >, #, &, %, ^, and more).

#### Best Practice Example
    
    
    <%: this.OutputName %>
    

This example is preferred as it addresses the issues outlined in the Anti-Pattern Example. Not only will it automatically handle the encoding for special characters, but it also renders characters if the encoded value is included within the expression. For example, if the the value contains "&amp;", it will render the escaped ampersand character.

#### Best Practice : Use the Validation Summary Part in combination with `Ets.Form.AddResultMessagesWithPrefixIfFailed()` or `AddValidationError()`

#### Best Practice Example
    
    
    string notes = this.Ets.Form.GetValueAsStringByKey("Model.Notes", "");
    if(notes.IsNullOrWhiteSpace())
    {
      this.Ets.Form.AddValidationError("Notes are required.", "Model.Notes");
      return;
    }
    

The Validation Summary Part provides a great way to display warnings and error messages on a page to allow users to either confirm an action or to provide more information if a failure has occurred. This works well when checking the result object of an operation or providing custom validation. The example above is checking a specific control on a page and will provide an error message if the value is not provided for the field. This method can be used to enforce required fields on forms.

#### Best Practice : Use `this.Ets.Js` functions to add custom JavaScript

#### Best Practice Examples

While there are several ways to add JavaScript to a page through C# code, the TrakSYS API provides several methods that can be used for different scenarios depending on the project requirements. Information about each of these methods is listed below:
    
    
    this.Ets.Js.Add()
    

This method adds plain JavaScript to the page.  

    
    
    this.Ets.Js.AddBackBoneReadyAllJavascript()
    

This is similar to `this.Ets.Js.Add`, but it automatically wraps the JavaScript code inside “`ets.bb.page.listenTo('readyAll', function(page) { /* your code here */ })`”.
    
    
    this.Ets.Js.AddBackBoneReadyJavascript()
    

This is similar to `this.Ets.Js.Add`, but it automatically wraps the JavaScript code inside “`ets.bb.page.listenTo('ready', function(page) { /* your code here */ })`”.
    
    
    this.Ets.Js.AddDocReadyJavascript()
    

This is similar to `this.Ets.Js.Add`, but it automatically wraps the JavaScript code inside “`$(function() { /* your code here */ })`”
    
    
    this.Ets.Js.AddForUnqiueKey()
    

This API method allows users to add a unique key to the JavaScript code. If this call is used multiple times and the same key is used for each call, only the first call using the same key will be added to the page. The other calls with the same key will not be added to the page during the page render process.

#### Best Practice : Use `Ets.Debug.Trace` and `Ets.Debug.TraceObject` to troubleshoot Pages

#### Best Practice Example
    
    
    DbEvent ev = this.Ets.Api.Data.DbEvent.Load.WithSql(sql);
    if(ev == null)
    {
      this.Ets.Debug.Trace(sql);
    }
    else
    {
      this.Ets.Debug.TraceObject(ev);
    }
    

The methods shown above allow users to add values, entire SQL statements, and full objects to the page trace. These methods can even be used to trace the value or object multiple times throughout the code execution. This can be very useful for tracking value and state changes as the page code is being executed. After the troubleshooting process is complete, these methods can be removed from the page code.

#### Best Practice: Use the Values Dictionary to modify Part properties.  
Anti-Pattern : Modify Part properties during the a Content Page's Initialization process

#### Anti-Pattern Example
    
    
    var imageLogo = (ETS.Ts.Core.ContentParts.TsImage)this.ImageLogo;
    imageLogo.Height = 300;
    imageLogo.Width = 200;
    

The issue with the method above is that these values can be overwritten at multiple stages of the page's code execution. This can make troubleshooting the issue more difficult as the issue now becomes a matter of execution timing instead of code logic or syntax. This is especially true if conditional logic is used to directly modify the part properties at different points in the code execution process.

#### Best Practice Example
    
    
    this.Ets.Values["ImageLogo.IsVisible"] = 1;
    

Many Parts and Pages have properties that allow Values Dictionary Keys to be specified. It is recommended to control these properties through the Values Dictionary as TrakSYS automatically maintains these values through the execution order. If a property needs to be updated multiple times during page execution, the values can simply be passed to the Values Dictionary Key. This method also provides a more uniform way of updating properties across multiple pages.

#### Best-Practice: Pass Values Dictionary value changes on page redirect  
Anti-Pattern : Modify Values Dictionary in server (e.g., Click) events

#### Anti-Pattern Example
    
    
    private void Start_Click(object sender, EventArgs e)
    {
      this.Ets.Values["SystemID"] = 123;
      return true;
    }
    

The example above will change the Values Dictionary value for that key, but only for the button click event. Once the event is finished executing and a page post back occurs, the updated value will not persist. This is also true if the button click event redirects the user to a different page and the Values Dictionary value is not included within the query string.

#### Best Practice Example
    
    
    private void Start_Click(object sender, EventArgs e)
    {
      try
      {
        string rawUrl = "~/pages/home/Packaging/Line1?SystemID=123";
        string url = this.Ets.ProcessExpressionUrl(rawUrl);
        this.Ets.Pages.RedirectToUrl(url);
      }
      catch(Exception ex)
      {
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

This method allows new Values Dictionary values to persist as it is included within the query string of the page redirect. Note that this method does allow new and existing Values Dictionary values to to passed into another page. Furthermore, it can be used to redirect to self (along with other pages) while passing in these values through the query string.

#### Anti-Pattern : Use ETS prefixes in the Values Dictionary

#### Anti-Pattern Example
    
    
    this.Ets.Values["ETS.Culture"] = "es";
    

The example above uses a built-in Values Dictionary Key that is automatically populated by the TrakSYS software. These keys are reserved for the software and can be overwritten or changed at any time. It is recommended to define a different, custom naming structure if maintaining a uniform Values Dictionary naming style is required. This can include defining a custom prefix, suffix, or both for each key (as long as it does not match any of the built-in Values Dictionary Keys).

#### Best Practice : Use Logic Service context object to retrieve or change Tag Values (within the Logic Service)  
Anti-Pattern : Use the TrakSYS API to retrieve or change Tag Values

#### Anti-Pattern Example
    
    
    public override void PostScan(IPostScanContext context)
    {
      var api = ETS.Core.Api.ApiService.GetInstance();
      var tag = api.Data.DbTag.Load.ByID(123);
      tag.Value = (int.Parse(tag.Value) + 1).ToString();
      api.Data.DbTag.Save.UpdateExisting(tag);
    }
    

While the example above does work, the issue is with code efficiency. Generally, it can be very inefficient to load an entire tag object simply to change the tag value. While the impact may be minor for a single instance, the performance impact can compound quickly if a large number of tag objects are loaded. This is especially true if the code is placed within a method or Script Class that executes on every Logic Service scan. 

#### Best Practice Example
    
    
    public override void PostScan(IPostScanContext context)
    {
      var tag = context.Tags[tagName];
      var newValue = tag.ValueInteger + 1;
      context.QueueTagNameEqualsForAssignment(tag.Name, newValue);
    }
    

The method above uses the context object, which has access to several objects and properties stored within memory of the Logic Service. This allows the code to reference an existing in-memory object to make the value change instead of having to create and load an entirely new tag object.

#### Best Practice : Use UpdateTagValueList to update multiple virtual tags (from outside Logic Service)  
Anti-Pattern : Update the Tag Values one at a time

#### Anti-Pattern Example : Option 1 - Using `UpdateVirtualTagByName()` or `UpdateVirtualTagByID()` for each individual tag
    
    
    this.Ets.Api.Tags.UpdateVirtualTagByName("LINE1.JOB.PRODUCT.CODE", "P.1234").ThrowIfFailed();
    this.Ets.Api.Tags.UpdateVirtualTagByName("LINE1.JOB.QUANTITY", 5000).ThrowIfFailed();
    

The issue with the code example above is scripting practices and execution efficiency. If a large number of tags need to be changed (e.g., 20, 50, or more tags), a line of code will have to be written for each individual tag. When the code is executed, the tag changes will be processed one-by-one as opposed to a batch process.

#### Anti-Pattern Example : Option 2 - Using the Unit Of Work object to update multiple tag values
    
    
    this.Ets.Api.Tags.UpdateVirtualTagByName("LINE1.JOB.PRODUCT.CODE", "P.1234", uow).ThrowIfFailed();
    this.Ets.Api.Tags.UpdateVirtualTagByName("LINE1.JOB.QUANTITY", 5000, uow).ThrowIfFailed();
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
    

This example is better since it does include the Unit of Work object, which adds additional error handling. It will also not create any bugs or invalid data. However, it still contains similar performance inefficiencies as the first option. A line of code will have to be created for every tag and the tag changes will have to be processed one-by-one. Additionally, the code will have to wait for the Unit of Work object to attempt the changes before they are pushed to the TrakSYS database. 

#### Best Practice Example
    
    
    var tagsToUpdate = new List<ETS.Core.Api.Models.Tags.Tag>();
    tagsToUpdate.Add(new ETS.Core.Api.Models.Tags.Tag
    {
      Name = "LINE1.JOB.PRODUCT.CODE",
      Value = "P.1234"
    });
    tagsToUpdate.Add(new ETS.Core.Api.Models.Tags.Tag
    {
      Name = "LINE1.JOB.QUANTITY",
      Value = 5000.ToVariantString()
    });
    this.Ets.Api.Tags.UpdateTagValueList(tagsToUpdate).ThrowIfFailed();
    

This method is preferred as it contains all of the tag names and values within a single list object. Although the code example above is manually providing tag value changes, it is possible to query a list of tags instead and insert the results into a list. This allows users to have a dynamic list of tag value changes depending on the rest of the logic and functionality. Additionally, the value changes are processed as a batch rather than individual, one-by-one updates.

#### Best Practice : Use `Api.Tags` to update a single Virtual Tag Value (from outside Logic Service)  
Anti-Pattern : Use the DbTag object to update Virtual Tag Values

#### Anti-Pattern Example
    
    
    var tag = this.Ets.Api.Data.DbTag.Load.ByID(123);
    tag.Value = "P.1234";
    this.Ets.Api.Data.DbTag.Save.UpdateExisting(tag);
    

With the code example above, the primary issue is code efficiency. The example is creating and loading an entire tag object simply to change the tag value. The performance impacts can compound very quickly if there are a large number of operations doing this.

#### Best Practice Example
    
    
    this.Ets.Api.Tags.UpdateVirtualTagByID(123, "P.1234").ThrowIfFailed();
    

This method provides the tag value change based on a tag ID. Optionally, if only the tag name is provided, `this.Ets.Api.Tags.UpdateVirtualTagByName()` can be used instead. This is much more efficient as it is not necessary to create and load entire objects.

#### Best Practice : Use Tags GetList to retrieve multiple tag values (from outside Logic Service)  
Anti-Pattern : Load the tags individually

#### Anti-Pattern Example
    
    
    var faultTag = this.Ets.Api.Tags.Load.ByName("LINE1.OPC.FAULT1").ThrowIfLoadFailed("Tag.Name", "LINE1.OPC.FAULT1");
    var productTag = this.Ets.Api.Tags.Load.ByName("LINE1.JOB.PRODUCT.CODE").ThrowIfLoadFailed("Tag.Name", "LINE1.JOB.PRODUCT.CODE");
    

The example above is inefficient as it loads tag object one-by-one. This concept does not scale well if a large number of tag objects are needed.

#### Best Practice Example
    
    
    var tagsToRetrieve = new List<string>();
    tagsToRetrieve.Add("LINE1.OPC.FAULT1");
    tagsToRetrieve.Add("LINE1.JOB.PRODUCT.CODE");
    var dictTagsByName = this.Ets.Api.Tags.GetList.ForTagNames(tagsToRetrieve).ThrowIfNull("Error loading tags");
    

This example is preferred as as all tag objects are retrieved in a single list. This can make it much easier (and more efficient) to modify large numbers of tags by simply iterating through the list. While the example above is adding tags one-by-one, it is possible to query a list of tags and store the results in the list object.

#### Best Practice : Use `Api.Tags` to retrieve a single Tag Value (from outside Logic Service)  
Anti-Pattern : Use the DbTag object to retrieve Tag Values

#### Anti-Pattern Example
    
    
    DbTag jobTag = this.Ets.Api.DbTag.Load.ByID(123);
    

While this method does work, it is inefficient as an entire DbTag object has to be created and loaded. This will load every field for the tag record to simply retrieve the tag value. 

#### Best Practice Example
    
    
    Tag jobTag = this.Ets.Api.Tags.Load.ByID(123).ThrowIfFailed();
    

This method uses the Tags service to retrieve the tag value instead. This method is more efficient as it only loads a few commonly used fields (like tag value) for a given tag. Reducing the number of fields loaded per entry can significantly speed up loading times.

#### Best Practice : Use `Ets.SiteNow` or `context.Now` to get the current DateTimeOffset  
Anti-Pattern : Use `SELECT SYSDATETIMEOFFSET()`, `DateTimeOffset.Now` or `DateTime.Now`

#### Anti-Pattern Example
    
    
    task.CreatedDateTime = DateTimeOffset.Now;
    

While the above example does work to assign a DateTimeOffset value, the value may be inconsistent. If `DateTimeOffset.Now` is called multiple times during a method, the timestamp may be different each time, which can cause issues when multiple records should have their timestamps aligned. This is typically more prevalent for distributed installations where slight timing discrepancies can occur between machines.

#### Best Practice Example
    
    
    task.CreatedDateTime = this.Ets.SiteNow;
    

The above example will provide consistent DateTimeOffset values throughout the entire execution of a script. Even for scripts with longer execution times, the value at the start of the execution will be the same as the value at the end. This can help ensure consistent timestamps when working with multiple entities in a single logical execution. 

#### Best Practice : Retrieve data from database or external systems in Data Management Service (DMS) Script Scripts or Logic Service Script Classes  
Anti-Pattern : Retrieve data from database or external systems within a Script Tag.

#### Anti-Pattern Example
    
    
    DataTable dt = this.Context.Api.Util.Db.GetDataTable(sql, externalConnectionString).ThrowIfFailed();
    foreach(DataRow dr in dt.Rows)
    {
      //loop and parse data
    }
    

Never use SQL queries within script tags. Since some script tags can run on every scan (depending on the scripting inside of the script tag), having SQL queries execute on every scan can significantly impact the scan times and cause constant overscans. This can cause widespread effects within multiple areas of the application and may impact the accuracy of OEE metrics.

#### Best Practice Example
    
    
    public override bool Execute(IModuleContext ctx)
    {
      DataTable dt = ctx.Api.Util.Db.GetDataTable(sql, externalConnectionString);
      foreach(DataRow dr in dt.Rows)
      {
        // loop and parse data
      }
      return true;
    }
    

If SQL queries are needed for the tags in the implementation or if there are script tags with a large amount of scripting, it's recommended to use Modules for these types of operations. Since Modules are executed using the Data Management Service, this reduces the stress on the Logic Service and can help reduce scan times. If Modules are not available, Logic Service script classes can also be used. However, the recommendation is to ensure that the code is only executed when it is necessary. Having the code execute on every scan can cause performance issues within the Logic Service.
