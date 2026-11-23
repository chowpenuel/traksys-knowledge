# Using the Paging Content Part

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360007564074-Using-the-Paging-Content-Part*
*Last updated: 2025-05-21T22:43:40Z*

---

Applies To | TrakSYS 10+

### **Summary**

When a dataset has the potential to contain a tremendous amount of rows, using Paging is a great way to make the page rendering process more efficient. This functionality can be accomplished in TrakSYS by leveraging the built-in Paging Content Part, which is cataloged alongside the other List Content Parts. The example below selects all OEE interval data for a given day and should serve as a guideline when implementing pagination into a custom page.

### **Procedure**

  1. From a Visual Page definition, add a Paging part:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18658619848211)  
  

  2. Navigate to the Data tab in the Paging Part Editor and set the Source Values Key. **TIP:** Remember the key chosen since it will be used further on in this process.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18658666104595)  
  
Please note, the Paging part only shows a navigational bar and is **not** a standalone solution to display a resultset with pagination:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18659056084243)  
  

  3. Because of this, the use of another List Content Part is required to show the data (i.e. Table View, List View, etc.):  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18658676140947)  
  

  4. The Values Key within the Data properties of that list should be identical to the Key chosen in the Paging Content Part set in step 2:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18658807154963)  
  

  5. Since the Paging part is not currently compatible with the built-in Data Tables, additional scripting is required. Although the script is not required to be in `ContentPage_PartPreInit05`, Data Tables are typically initialized around this time. The script would resemble the following:


    
    
    /// ***********************************************************
    protected override bool ContentPage_PartPreInit05()
    {
      DateTime sd = this.Ets.SiteNow.Date;
      
      string sql = @"SELECT 
                          ID
                        , StartDateTime
                        , EndDateTime
                        , OeeCalculationID
                      FROM tOeeInterval
                      WHERE [Date] = {0}
                      ORDER BY StartDateTime DESC".FormatWith(sd.ToSql());
      
      // this is the data key configured in the parts
      string dataKey = "Data.Oee";
      
      var data = this.Ets.Values.GetPagedDataInformation(dataKey);
      
      var dt = this.Ets.Api.Util.Db.GetPagedDataTable(sql, data.PageIndex, data.PageSize).ThrowIfFailed();
      
      this.Ets.Values.AddPagedDataInformation(dt, dataKey);
      
      this.Ets.Values[dataKey] = dt.Data;
      
      return true;
    }
    

In this example, the data being populated into the Table View is all the OEE Interval data from the current day.

Additional information about the Paging part can be found in the [TrakSYS Reference Documentation](https://docs.parsec-corp.com/tsweb/content-reference/content-part-reference/lists/paging). Some notes listed there will reference the `GetPagedDataTable` method from the API, which only returns a data table with rows based on a page size. This is why the `AddPagedDataInformation` is necessary to place the paging info into into the Values Dictionary.

The resulting page would resemble the following:

![](https://portal.parsec-corp.com/hc/article_attachments/18660993304083)
