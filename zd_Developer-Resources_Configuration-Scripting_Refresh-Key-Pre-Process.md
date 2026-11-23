# Refresh Key Pre-Process

*Source: https://portal.parsec-corp.com/hc/en-us/articles/14802103974547-Refresh-Key-Pre-Process*
*Last updated: 2025-05-21T23:10:59Z*

---

Applies To | 11.1.0+

### Summary

In [TrakSYS 11.1.0](https://portal.parsec-corp.com/hc/en-us/articles/360043699394-What-s-New-in-TrakSYS-11-1), the Refresh Key Pre-Process feature was added. This feature helps optimize page refreshes when using Refresh Keys especially with a large number of screens. This feature was further improved in TrakSYS 11.2.0. The example provided in this article shows how to use this feature for TrakSYS 11.1.0 and 11.2.0+.

The following diagram represents the general flow of Refresh Keys if the Refresh Key Pre-Process feature is not used.

![](https://portal.parsec-corp.com/hc/article_attachments/14802506592403)

In this scenario, there are only three clients. However, the concept is the same regardless of the number of clients involved. As shown, the Logic Service will send a request to the TrakSYS Web notifying any connected clients that they need to perform a refresh. As a result, the 3 clients will make separate requests to the database. In this case, the same query will be executed 3 times within milliseconds of each other. This is typically fine in scenarios where there are a small number of clients and the queries are relatively simple. However, this can become an issue if larger numbers of clients with more intensive queries are involved.

To address these scenarios, the Refresh Key Pre-Process feature can be used to call the query only once. This method leverages the TrakSYS Web Cache using the `[GetCachedDataTable()](https://support.parsec-corp.com/refdocs/11/traksys/api-reference/api-services-reference/api.util/api.util.db/getcacheddatatable.html)` method to preload the query. The following diagram represents the flow when using the Refresh Key Pre-Process functionality.

![](https://portal.parsec-corp.com/hc/article_attachments/14802971482387)

Once the query is executed and cached, the Refresh Key is broadcasted to the active clients. These clients can then take advantage of the cached query. The cache duration can be set to a relatively low duration (e.g., a few seconds) as the intended purpose is to help prevent the query from executing more than once.

One factor to consider when determining whether to use Refresh Key Pre-Processing is that the query will be executed every time the Refresh Key is broadcasted. Without the Prefetch, if there are no active clients for a particular Refresh Key, then the query will not be executed. Therefore, this functionality may not be suitable for all scenarios.

Another factor to consider is that this functionality cannot be used at the Page Definition level due to timing concerns. Each client can potentially execute the same query and notice that the query is not cached. From here, they will simply execute the query normally and attempt to save it in the TrakSYS Web Cache. In this scenario, all clients will execute the same query, which defaults to the original Refresh Key functionality.

When using this functionality, the query executed by the Prefetch code (in the example below) needs to contain the exact same string. Therefore, the recommended best practice is to use a Web Script Class to retrieve the cached data and ensure that the cache is used by the clients. Additionally, a configuration record is required in order to use Refresh Key Pre-Processing. In TrakSYS 11.1.0 to 11.1.2, this will include an entry in the `tCustomSetting` table. In TrakSYS 11.2.0 and newer, this entry should be created in the `tWebconfiguration` table. This example will provide methods for both scenarios.

### Example

The following is an example of the Prefetch class by TrakSYS version. This code should be placed within a Web Script Group (under **Developer | Scripts | Web**).

#### **For TrakSYS 11.1.0 to 11.1.2**
    
    
    /// ******************************************************************
    /// <summary>Plugin Class for prefetching data</summary>
    /// ******************************************************************
    public class OeePreFetch : IRefreshKeyPlugin
    {
      public static void CreateConfigSetting(ApiService api)
      {
        // NOTE in 11.2.0+ DbCustomSetting is not used and will need to be adjusted when performing an eventual upgrade.
        var setting = new DbCustomSetting();
        setting.Name = "OeePreFetch"; // This can be any value.
        setting.Key = "OeePreFetch"; // This can be any value, but must be unique in the table.
        setting.AltName = "ts.config"; // This can only be ts.config. Do not use any other value.
        // DataText is a JSON payload that configures this class "OeePreFetch" to hook into the Refresh Key broadcast call stack.
        setting.DataText = @"{
        ""refreshKeys"": {
        ""hookTypes"": [ ""ETS.Ts.Core.Scripting.OeePreFetch"" ]
    }
    }";
        api.Data.DbCustomSetting.Save.InsertAsNew(setting).ThrowIfFailed();
      }
      
      /// ******************************************************************
      public bool IsForRefreshKey(string key)
      { 
        if (key.StartsWith("Oee.", StringComparison.InvariantCultureIgnoreCase)) return true;
        return false;
      }
    
      /// ******************************************************************
      public void PrefetchData(ApiService api, string key)
      {
        var dataSvc = api.Create.InstanceOf<OptimizedDataService>();
        
        // If the Key is "Oee.42" then it should return 42;
        int oeeCalcID = key.StringAfterIndex(4).AsInt(-1);
        if (oeeCalcID.IsNull()) return;
        
        dataSvc.GetOeeData(oeeCalcID);
      }
    }
    

#### **For TrakSYS 11.2.0 and Newer**
    
    
    /// ******************************************************************
    /// <summary>Plugin Class for prefetching data</summary>
    /// ******************************************************************
    public class OeePreFetch : IRefreshKeyPlugin
    {
      public static void CreateConfigSetting(ApiService api)
      {
        // NOTE that dbWebConfiguration is only available in TrakSYS 11.2.0 and newer.
        var webSetting = new DbWebConfiguration();
        webSetting.Name = "OeePreFetch"; // This can be any value.
        webSetting.Key = "OeePreFetch"; // This can be any value, but must be unique in the table.
        webSetting.Settings = @"{
        ""refreshKeys"": {
        ""hookTypes"": [ ""ETS.Ts.Core.Scripting.OeePreFetch, Ts.Scripting"" ]
    }
    }";
        webSetting.IsTransferEnabled = true;
        api.Data.DbWebConfiguration.Save.InsertAsNew(webSetting).ThrowIfFailed();
      }
    
      /// ******************************************************************
      public bool IsForRefreshKey(string key)
      {
        if (key.StartsWith("Oee.", StringComparison.InvariantCultureIgnoreCase)) return true;
        return false;
      }
    
      /// ******************************************************************
      public void PrefetchData(ApiService api, string key)
      {
        var dataSvc = api.Create.InstanceOf<OptimizedDataService>();
    
        // If the Key is "Oee.42" then it should return 42;
        int oeeCalcID = key.StringAfterIndex(4).AsInt(-1);
        if (oeeCalcID.IsNull()) return;
    
        dataSvc.GetOeeData(oeeCalcID);
      }
    }
    

As shown in the code, it only includes Refresh Keys that start with "`Oee.`". The rest of the Refresh Key is assumed to contain an `OeeCalculationID`. However, the code can be changed to use different prefixes and naming conventions as needed. The code examples above assume that the class is within the `ETS.Ts.Core.Scripting` namespace. To create the required configuration record, the following line of code can be executed. This applies to both scripting examples:
    
    
    ETS.Ts.Core.Scripting.OeePreFetch.CreateConfigSetting(this.Ets.Api);
    

**Note:** This call only needs to be executed once. After the configuration record has been created in either `tCustomSetting` (for TrakSYS 11.1.0 to 11.1.2) or `tWebConfiguration` (for TrakSYS 11.2.0+), this call can be removed.

The following code example is a sample of the OptimizedDataService Class. This should be created as a separate Web Script Class (under **Developer | Scripts | Web**). The following using statements should be added within this class:
    
    
    // add using statements
    using System.Data;
    using ETS.Core.Api.Models;
    

The code for the rest of the class is shown below. The example is the same for all applicable TrakSYS versions.
    
    
    public class OptimizedDataService
    {
      private readonly ApiService _api;
    
      /// ******************************************************************
      public OptimizedDataService(ApiService api) { _api = api; }
    
      /// ******************************************************************
      public Result<DataTable> GetOeeData(int oeeCalcID)
      {
        var date = _api.Site.GetCurrentDateTime().Date;
        string sql = @"WAITFOR DELAY '00:00:05'
                    SELECT TOP 10
                      oee.TotalDisplayUnits, SYSDATETIMEOFFSET() as DebugNow
                    FROM viewOeeInterval oee
                    WHERE oee.OeeCalculationID = {0}
                    AND oee.[Date] = {1}".FormatWith(oeeCalcID.ToSql(), date.ToSql());
        return _api.Util.Db.GetCachedDataTable(sql, 10);
      }
    }
    

Please note that the query included in the example above is for **demonstration purposes only**. In actual installations, this will need to be changed to match the implementation requirements. [The first line](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/waitfor-transact-sql) of the query ensures that it will wait 5 seconds before executing. This, paired with `SYSDATETIMEOFFSET`, helps demonstrate the functionality as well as the timing. For timing reasons, it is recommended to set the cache duration to something longer than what is expected. Since the query is artificially set to execute in the last 5 seconds, the cache seconds in this case was set to 10.

The final part of this example is shown below. The code example was placed within the `ContentPage_PartPreInit05()` method of a Visual Page Definition and will execute the query. This example is the same for all applicable TrakSYS versions.
    
    
    protected override bool ContentPage_PartPreInit05()
    {
      var dataSvc = this.Ets.Api.Create.InstanceOf<ETS.Ts.Core.Scripting.OptimizedDataService>();
      var dt = dataSvc.GetOeeData(this.OeeCalcID).ThrowIfFailed();
      this.Ets.Values["Data.Oee"] = dt;
      this.Ets.Values.AddDataTableInformation(dt, "Data.Oee", false);
    
      return true;
    }
    

**Note:** In TrakSYS 11.2.0 and newer, the TrakSYS Web will write something similar to the following message to the TrakSYS log file (tLog) on web start. This helps confirm that the Refresh Key Pre-Process functionality has been correctly configured and is loaded.
    
    
    CustomSetting 'OeePreFetch' registered 1 RefreshKeyPlugin Types.
