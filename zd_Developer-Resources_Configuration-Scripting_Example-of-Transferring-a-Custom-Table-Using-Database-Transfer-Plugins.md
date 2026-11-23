# Example of Transferring a Custom Table Using Database Transfer Plugins

*Source: https://portal.parsec-corp.com/hc/en-us/articles/12746233996307-Example-of-Transferring-a-Custom-Table-Using-Database-Transfer-Plugins*
*Last updated: 2025-05-21T23:09:30Z*

---

Applies To | TrakSYS 11+

### Summary

In TrakSYS 11, the ability to add Database Transfer Plugins was added. Using these plugins allows users to customize the Database Transfer Import and Export process to help meet specific requirements. While the built-in [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-Database-Transfer-Guide) process only transfers data for built-in TrakSYS tables, Database Transfer Plugins can be used to further extend this functionality to transfer data for custom tables as well.

This article contains a basic example of how Database Transfer Plugins can be used to transfer data for a single custom table. Additional custom code can be written to transfer data between multiple custom tables or to perform more complex operations during the Database Transfer process. Note that this is only one possible option (out of many). Ultimately, how the data is transferred will depend on a project's requirements.

### Example

#### **Initial Setup**

For the purpose of this example, a single custom table called `_tCustomTable` was created on the development and production environments. The table consists of two columns and has the following structure:

![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/12765082027411)

When viewing the table design in SQL Server Management Studio, the following design information is displayed:

![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/12765095382291)

In this example, there are 3 rows of data in the development database that will need to be transferred to production. The data within these 3 records is shown below:

![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/12765382753939)

In order to transfer the data between both environments, an **Export Plugin** and **Import Plugin** will have to be created. Plugins can be created within the TrakSYS Web under **Developer | Scripts | Database Transfer**.

#### **Export Plugin**

In general, it is expected that the Export Plugin will retrieve the data from the custom table in the development environment and add it to the XML of the .transfer file (created in the Database Transfer Export process). The code below retrieves the information from the custom tables, loops through the individual rows, and adds them to the .transfer file. Note that this code retrieves all records from a single table. Additional coding can be added to only retrieve information or rows based on specific conditions.
    
    
    public override bool PostExportTables(XDocument doc, IDatabaseTransferExportContext context)
    {
       // Query the information from the custom table
      DataTable tableData = context.Api.Util.Db.GetDataTable("SELECT * FROM _tCustomTable").ThrowIfFailed();
      // Create your own XElements as needed
      XElement customTable = new XElement("customtables");
      XElement customData = new XElement("table");
      customData.Add(new XAttribute("name", "customvalues"));
      // Loop through the data and add the values to the .transfer XML file
      foreach (DataRow row in tableData.Rows)
      {
        XElement customDataRow = new XElement("row");
        customDataRow.Add(new XAttribute("ID", row["ID"]));
        customDataRow.Add(new XAttribute("Value", row["Value"]));
        customData.Add(customDataRow);
      }
    
      customTable.Add(customData);
      doc.Root.Add(customTable);
      return true;
    }

#### **Import Plugin**

When creating an Import Plugin, it is expected that the plugin will take the custom data from the XML in the .transfer file and insert it into the custom table in the production database. Similar to the Export Plugin, the code below retrieves the information from the .transfer file, loops through the elements, and uses raw SQL to insert the data into the custom table. Custom coding can be added to include more complex logic that determines when and how records are added to a table.

**Note:** Raw SQL must be used to add the records to the table. The TrakSYS [Model Object](https://support.parsec-corp.com/refdocs/11/traksys/api-reference/api-models-reference/api-models/data/db-entity.html) structure cannot be used in this case as it only applies to built-in TrakSYS tables and entities.
    
    
    public override bool PreImportTables(XDocument doc, IUnitOfWork uow, IDatabaseTransferImportContext context)
    {
      // Access the elements of the XML file containing the custom data
      var root = doc.ElementOrThrow("transfer").ElementOrThrow("customtables").ElementOrThrow("table");
      var rowValues = root.Elements("row");
      // Loop through the elements to find the individual values per row
      foreach (XElement ele in rowValues)
      {
        // Retrieve the ID
        int ID = ele.GetAttributeValueAsInt("ID", -1);
        // Retrieve the Value
        string value = ele.GetAttributeValue("Value", "");
        // Use SQL to insert the data into the custom table
        string sql = @"INSERT INTO _tCustomTable
                      VALUES ({0}, {1})".FormatWith(ID.ToSql(), value.ToSql());
        // Execute the SQL Statement
        context.Api.Util.Db.ExecuteSql(sql).ThrowIfFailed();
      }
      return true;
    }

#### **Creating References for Plugins**

Now that the Transfer Import and Export Plugins have been created, they will need to be referenced so that the Database Transfer process will use them when a transfer is initiated. These references can be created within the TrakSYS Installation Manager and only have to be specified in the development environment. This can be done by clicking the **Overview** tab and clicking the **TrakSYS Settings** button. Within the Settings dialog, place the respective class names within the **CustomExportClassName** and **CustomImportClass** fields under the Database Transfer section.

**Note** : These fields should contain the Script Class names of the Plugin, not the name provided for the Plugin within the configuration.

![mceclip3.png](https://portal.parsec-corp.com/hc/article_attachments/12769401120147)

#### **Verifying the Results**

Once the Plugins have been created and correctly referenced, it is possible to view the elements within the .transfer file for testing and verification purposes. When a Transfer Export is performed on the development environment, a program such as Notepad, NotePad++, or Visual Studio Code can be used to view the raw XML within the file. If the process is successful, the custom elements should be present within the file. For the purpose of this example, the following XML is expected based on the code provided for the Transfer Export Plugin:
    
    
    <customtables>
      <table name="customvalues">
        <row ID="1" Value="Value1" />
        <row ID="2" Value="Value2" />
        <row ID="3" Value="Value3" />
      </table>
    </customtables>
    

When viewing the raw XML in the generated .transfer file, these elements are present in the file, indicating that the export process is a success.

![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/12769996352019)

From here, a Database Transfer Import can be initiated on the production server using the generated .transfer file. If the process is successful, the entries should be present within the custom table. For this example, the image below shows the newly created records in Management Studio after the import was executed:

![mceclip5.png](https://portal.parsec-corp.com/hc/article_attachments/12770157202579)

As mentioned in the beginning of this article, this is only one possible way to transfer data for custom tables using Database Transfer Plugins. The example simply retrieves all data for a custom table from the development database and inserts it into the same table in the production database. For more advanced logic and complex implementation requirements, it is recommended to use LINQ to selectively choose which values should (and should not) be transferred.

### Additional Considerations and Best Practices

#### **Logging Operations to the TrakSYS Installation Manager**

When creating Transfer Import and Export Plugins, it is recommended to provide ample error handling to display detailed messages during the Transfer Import and Export Plugin execution process. Using the `context` object within the methods, It is possible to programmatically log errors, warnings, and informational messages to the TrakSYS Installation Manager. The code example below demonstrates how each type of message can be generated:
    
    
    public override bool PreImport(XDocument doc, IDatabaseTransferImportContext context)
    {
      context.ReportError("This is an error");
      context.ReportWarning("This is a Warning");
      context.ReportInformation("This is an Informational message");
      return true;
    }
    

When the transfer is initiated, the messages will be logged to the TrakSYS Installation Manager. In the image shown below, each of these messages was logged by a Transfer Import Plugin when a Database Transfer Import was executed.

![mceclip7.png](https://portal.parsec-corp.com/hc/article_attachments/12774821344275)

Additionally, when a copy of the Results are exported, these messages will be displayed. This is especially useful for troubleshooting purposes if the Database Transfer process fails for any reason.

![mceclip8.png](https://portal.parsec-corp.com/hc/article_attachments/12774899319187)

#### **Executing Code Based on Selected Database Transfer Options**

When executing a Database Transfer Export, there are 3 possible scenarios:

  * Transfer only the Configuration.
  * Transfer only the UI.
  * Transfer both the Configuration and the UI.



Depending on the implementation requirements, there may be special conditions that need to be considered when transferring data. For more complex requirements such as these, the `context` object within the methods has a `TransferMode` property that can be referenced based on the options that were selected for the Database Transfer Export. The following code can be used to execute specific logic based on the 3 scenarios listed above.
    
    
    // To execute code only on Configuration transfer
    if(context.TransferMode == DbTransferMode.Config)
    {
      // Your code here
    }
    
    // To execute code only on UI transfer
    if(context.TransferMode == DbTransferMode.Ui)
    {
      // Your code here
    }
    
    // To execute code on Configuration and UI transfer
    if(context.TransferMode == DbTransferMode.UiAndConfig)
    {
      // Your code here
    }
    
