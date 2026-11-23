# Creating an OEE Adjustment for Multiple Intervals Using the API

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360005709414-Creating-an-OEE-Adjustment-for-Multiple-Intervals-Using-the-API*
*Last updated: 2025-05-21T22:52:45Z*

---

Applies To | TrakSYS 10+

### **Summary**

This article provides a sample script for creating an OEE Adjustment for multiple intervals using the TrakSYS API. For simplicity, the example assumes the necessary parameters are passed in to the Values Dictionary on page load via the query string (in an actual implementation, some of these values would come from user input on a form). The adjustment is then saved when a button is clicked on the page. The script below defines a class with this button's click event handler:

  * `Save_Click(object sender, EventArgs e)`



This method leverages the `Kpi` service of the TrakSYS API to create a new `DbOeeAdjustment` object for a given amount of units and OEE Calculation ID. It also selects the list of intervals to adjust based on a given Job ID, distributes the units amongst those intervals, and records the changes to the database.

Not only can the list of intervals be selected by Job ID (as shown in the script), but they can also be selected by Shift History ID, Production Date Range, or from an existing adjustment:

  * `GetIntervalsForJobID(int jobID, int oeeCalculationID)`
  * `GetIntervalsForShiftHistoryID(int shiftHistoryID, int oeeCalculationID)`
  * `GetIntervalsByProductionDateRange(DateTime startDate, DateTime endDate, int oeeCalculationID)`
  * `GetIntervalsFromAdjustment(DbOeeAdjustment adjustment)`



Prior to inserting the OEE Adjustment, the adjustment units need to be distributed amongst the specified list of intervals. The units can be distributed either by production time or by actual counts.

  * `DistributeCountsByActualCounts(DbOeeAdjustment adjustment, List<DbOeeAdjustmentInterval> intervalAdjustments)`
  * `DistributeCountsByProductionTime(DbOeeAdjustment adjustment, List<DbOeeAdjustmentInterval> intervalAdjustments)`



More info on the OEE Adjustment methods can be found in the [API Reference](https://docs.parsec-corp.com/api-reference/api-services-reference/api.kpi/adjustment) section of the TrakSYS Reference Documentation under **API Services Reference | Api.Kpi | Adjustment**.

### **Example**

The code block below creates an OEE Interval adjustment for multiple intervals. Note: advanced scripting requires a PRO license.
    
    
    /// ***********************************************************
    public partial class OeeAdj : ContentPageBase
    {
    /// Automatically map the decorated property to incoming Ets.Values data (typically QueryString variables).
    /// The name of the property is used as the Key in accessing the Ets.Values collection during mapping.
    [ValuesProperty()]
    public int KpiCalculationID { get; set; } = -1;
    
    // ENUM: 2 for good, 3 for bad
    [ValuesProperty()]
    public int KpiCounterType { get; set; } = -1;
    
    [ValuesProperty()]
    public int AdjustmentUnitCount { get; set; } = -1;
    
    // either "Correction" or "Addition"
    [ValuesProperty()]
    public string AdjustmentType { get; set; } = "Addition";
    
    [ValuesProperty()]
    public int JobID { get; set; } = -1;
    
      /// ***********************************************************
      protected void Save_Click(object sender, EventArgs e)
      {
        var api = this.Ets.Api;
        
        //create model object
        var oeeAdjustment = new ETS.Core.Api.Models.Data.DbOeeAdjustment();
        
        //create result object
        Result<DbOeeAdjustment> result = new Result<DbOeeAdjustment>();
        
        try 
        {        
          // create DbOeeAdjustment object depending on type of adjustment being passed in
          
          if(AdjustmentType == "Correction" && KpiCounterType == 3)
          {
            result = api.Kpi.Adjustment.CreateNewCorrectionForBadUnits(  
                                 AdjustmentUnitCount, KpiCalculationID);
          }
          else if(AdjustmentType == "Addition" && KpiCounterType == 3)
          {
            result = api.Kpi.Adjustment.CreateNewAdditionForBadUnits(  
                               AdjustmentUnitCount, KpiCalculationID);
          }
          else if(AdjustmentType == "Correction" && KpiCounterType == 2)
          {
            result = api.Kpi.Adjustment.CreateNewCorrectionForGoodUnits(  
                                  AdjustmentUnitCount, KpiCalculationID);
          }
          else if(AdjustmentType == "Addition" && KpiCounterType == 2)
          {
            result = api.Kpi.Adjustment.CreateNewAdditionForGoodUnits(  
                                AdjustmentUnitCount, KpiCalculationID);
          }
          if(!result.Success) { this.Ets.Debug.FailFromResultMessages(result.Messages); }
          
          oeeAdjustment = result.Return;
          
          // interval list can be loaded by shift history, job id, or date range
          var intervalList = api.Kpi.Adjustment.GetIntervalsForJobID(  
                                             JobID, KpiCalculationID).ThrowIfFailed();
                  
          // distribute the units
          api.Kpi.Adjustment.DistributeCountsByActualCounts(  
                                oeeAdjustment, intervalList).ThrowIfFailed();
          
          //create unit of work for transaction
          var uow = api.CreateUnitOfWork();
          
          api.Kpi.Adjustment.InsertAsNew(oeeAdjustment, intervalList, uow).ThrowIfFailed();
          
          //execute uow
          uow.ExecuteReturnsResultObject().ThrowIfFailed();
          
          //if uow executes successfully redirect to success
          this.Ets.Pages.RedirectToSuccessUrl();
        } 
        catch(Exception ex)
        {
          this.Ets.Debug.FailFromException(ex);
        }
      }  
    }
