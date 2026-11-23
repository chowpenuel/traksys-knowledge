# API Excel Export Example

*Source: https://portal.parsec-corp.com/hc/en-us/articles/12995481363347-API-Excel-Export-Example*
*Last updated: 2025-05-21T22:49:45Z*

---

Applies To | TrakSYS 11.2.2+

### Summary

Starting in [TrakSYS 11.2.2](https://portal.parsec-corp.com/hc/en-us/articles/4415790284819-TrakSYS-11-2-Update-2), the ability to export Excel spreadsheets using the API was implemented. This is useful for scenarios where complex requirements or logic must be considered when creating an Excel document. it can also be useful in other scenarios where a spreadsheet needs to be exported from different areas of the application (such as a Module).

### Examples

#### Example 1: Exporting an Excel File

The following code provides an example of how to use the API to export an Excel spreadsheet. This example was created within the On Server Click method of a [Buttons Part](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/content-reference/content-part-reference/buttons.html) on a Visual Page Definition. 
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create a query to provide data
        string sql = "SELECT ID, Name FROM tSystem";
        // Specify a file path and file name for the export
        string targetFilePath = @"C:\Users\Public\Documents\ExceFile.xlsx";
              
        // Create an instance of the ExcelDataService
        var excelSvc = this.Ets.Api.Create.InstanceOf<ETS.Core.Services.Data.ExcelDataService>();
        var workbook = excelSvc.CreateWorkbook();
        // Retrieve the data using the query and populate the workbook object with the results 
        using (var dt = this.Ets.Api.Util.Db.GetDataTable(sql).ThrowIfFailed())
        {
          excelSvc.FillWorkbookData(workbook, "A1", dt, /* includeHeaders */ true, /* insertAndShiftDown */ false).ThrowIfFailed();
        }
        // Export the workbook to the file location
        excelSvc.SaveWorkbookToFile(workbook, targetFilePath).ThrowIfFailed();
      }
      catch (Exception ex)
      {
        // Throw errors if the process fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

As the code comments suggest, the example queries the ID and Name fields in the `tSystem` table. Then, the data is retrieved using the API, the workbook object is populated with the results, and the Excel file is created in the specified file path. Note that the correct permissions must be given to the folder included in the file path so that the Excel file can be created.

The `FillWorkbookData` method identifies how a DataTable should be added to workbook. These parameters are very similar to the properties that are available in the built-in [Excel Export](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/content-reference/content-part-reference/excel/excel-export.html) part. Note that the `workbook` object included in the example above does not have any type of functionality. The logic used to process the document must be performed using the methods included within the `ExcelDataService`.

#### Example 2: Referencing an External Excel Template File

The following code example expands on the code shown above and shows how to reference a template Excel file when exporting an Excel spreadsheet. This example uses the `GetWorkbookFromStream()` method instead of the `CreateWorkbook()` method used in the first example. The core logic of the example requires the source template Excel file to be downloaded into a [System.IO.Stream](https://learn.microsoft.com/en-us/dotnet/api/system.io.stream?view=netframework-4.8) object. The example provides two different ways of referencing an Excel template file: from a local file or from a URL. Similar to the first example, this example was also used in a button handler method on a Visual Page Definition.
    
    
    // Add Using statements
    using ETS.Core.Services.Data;
    using ETS.Core.Models.Data;
    
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        bool shouldDownloadFileFromUrl = false; //Should return true if retrieving Excel file from a URL;
        // Populate with a URL if the Excel file comes from a URL
        string url = "YourURLHere";
        // Populate if the Excel file comes from a local directory
        string excelFullFilePath = @"C:\Users\Public\Documents\ExcelTemplate.xlsx";
    
        byte[] excelByteArray;
        if (shouldDownloadFileFromUrl)
        {
          // get Excel from URL
          using (var webClient = new System.Net.WebClient())
          {
            excelByteArray = webClient.DownloadData(url);
          }
        }
        else
        {
          // get Excel from local file
          excelByteArray = System.IO.File.ReadAllBytes(excelFullFilePath);
        }
    
        // Create an instance of the ExcelDataService
        var excelSvc = this.Ets.Api.Create.InstanceOf<ExcelDataService>();
        ExcelWorkbookInfo workbook;
        using (var stream = new System.IO.MemoryStream(excelByteArray))
        {
          workbook = excelSvc.GetWorkbookFromStream(stream).ThrowIfFailed();
        }
    
        // Create a query to provide data
        string sql = "SELECT ID, Name FROM tSystem";
        // Specify a file path and file name for the export
        string targetFilePath = @"C:\Users\Public\Documents\ExceFile.xlsx";
    
        // Retrieve the data using the query and populate the workbook object with the results 
        using (var dt = this.Ets.Api.Util.Db.GetDataTable(sql).ThrowIfFailed())
        {
          excelSvc.FillWorkbookData(workbook, "A1", dt, /* includeHeaders */ true, /* insertAndShiftDown */ false).ThrowIfFailed();
        }
        // Export the workbook to the file location
        excelSvc.SaveWorkbookToFile(workbook, targetFilePath).ThrowIfFailed();
      }
      catch (Exception ex)
      {
        // Throw errors if the process fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

#### Example 3: Referencing an Excel Template File Stored as a Library Item

The following example is a variant of the second example shown above and shows how to reference a template Excel file that has been stored as a [Library Item](https://portal.parsec-corp.com/hc/en-us/articles/360009367873-Adding-a-Library-Item). Before the solution can be used, a [Library Item Link](https://portal.parsec-corp.com/hc/en-us/articles/115004358707-Creating-a-Link-for-a-Library-Item) must be created. This helps the API Excel Export functionality point to the source template when generating the Excel file. Similar to the previous examples, This example was created within the On Server Click method of a [Buttons Part](https://support.parsec-corp.com/refdocs/11/traksys/tsweb/content-reference/content-part-reference/buttons.html) on a Visual Page Definition. 

Once the Library Item Link is known, the beginning of the code example builds out the full URL using the Values Dictionary for the beginning of the link. The rest of the URL is specified based on the configuration of the Library Item. In this example, a Library Item Group was configured with a key of "**Files** " while the Excel Template file was stored as a Library Item with a file name of "**ExcelTemplate.xlsx**." Finally, the full URL is converted to an absolute Uri so the Library Item can be properly referenced.

**Note** : the worksheet name used in the `FillWorkbookData()` method should match the worksheet name used in the original template. The example below uses “Sheet1” but this should be changed based on the actual name included within the Excel file.
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        bool shouldDownloadFileFromUrl = true; //Should return true if retrieving Excel file from a URL;
                                                
        // Populate with a URL if the Excel file comes from a URL
        string urlLib = this.Ets.Values.GetAsString("ETS.LibraryUrl"); // available in 11.2.2+
        string urlEx = @"{0}/Files/ExcelTemplate.xlsx".FormatWith(urlLib);
        string url = new Uri(HttpContext.Current.Request.Url, this.Ets.ProcessExpressionUrl(urlEx)).AbsoluteUri;
    
        // Populate if the Excel file comes from a local directory
        string excelFullFilePath = @"";
    
        byte[] excelByteArray;
        if (shouldDownloadFileFromUrl)
        {
          // get Excel from URL
          using (var webClient = new System.Net.WebClient())
          {
            excelByteArray = webClient.DownloadData(url);
          }
        }
        else
        {
          // get Excel from local file
          excelByteArray = System.IO.File.ReadAllBytes(excelFullFilePath);
        }
    
        // Create an instance of the ExcelDataService
        var excelSvc = this.Ets.Api.Create.InstanceOf<ExcelDataService>();
        ExcelWorkbookInfo workbook;
        using (var stream = new System.IO.MemoryStream(excelByteArray))
        {
          workbook = excelSvc.GetWorkbookFromStream(stream).ThrowIfFailed();
        }
    
        // Create a query to provide data
        string sql = "SELECT ID, Name FROM tSystem";
        // Specify a file path and file name for the export
        string targetFilePath = @"C:\Users\Public\Documents\ExceFile.xlsx";
    
        // Retrieve the data using the query and populate the workbook object with the results 
        using (var dt = this.Ets.Api.Util.Db.GetDataTable(sql).ThrowIfFailed())
        {
          excelSvc.FillWorkbookData(workbook, "Sheet1", dt, /* includeHeaders */ true, /* insertAndShiftDown */ false).ThrowIfFailed();
        }
        // Export the workbook to the file location
        excelSvc.SaveWorkbookToFile(workbook, targetFilePath).ThrowIfFailed();
      }
      catch (Exception ex)
      {
        // Throw errors if the process fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    
