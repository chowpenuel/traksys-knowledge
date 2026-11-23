# Programmatically Increasing Page Timeout

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824879411731-Programmatically-Increasing-Page-Timeout*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | TrakSYS 10+

In some scenarios it may be required to query a large amount of data or perform operations that may take several minutes to complete on a page. By default, TrakSYS uses the default SQL Server timeout of 30 seconds for most operations. Depending on the implementation requirements, there are several ways to extend the timeout or properly handle the longer executions. Some of these methods include:

  * Using Wait For pages.
  * Using the optional `commandTimeout` parameter if the [GetDataTable()](https://docs.parsec-corp.com/api-reference/api-services-reference/api.util/api.util.db/getdatatable) method is used to query data.
  * Using the [Long Running Activity](https://portal.parsec-corp.com/hc/en-us/articles/360038064413-Debugging-Best-Practices) helper.
  * Specifying a value on the Command Timeout setting for Data Table Parts that contain this option (e.g. the Custom SQL Data Table Part (`ETS.DataTables.TsDataTableCustomSql`))
  * Specifying a value for the Command Timeout setting under the Database tab of the TrakSYS Installation Manager.



However, if these options are not desirable or possible, it is possible to extend the timeout of a single Page Definition using the `ScriptTimeout` property. The following code example increases the page execution timeout to 1 hour (3600 seconds) but can be adjusted as needed. 
    
    
    protected override bool ContentPage_Init()
    {
       this.Page.Server.ScriptTimeout = 3600;
       return true;
    }
    
