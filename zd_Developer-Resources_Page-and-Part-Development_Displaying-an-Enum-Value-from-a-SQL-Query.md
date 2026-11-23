# Displaying an Enum Value from a SQL Query

*Source: https://portal.parsec-corp.com/hc/en-us/articles/115001183953-Displaying-an-Enum-Value-from-a-SQL-Query*
*Last updated: 2025-05-21T22:53:06Z*

---

Applies To | TrakSYS 10+

When displaying data in a Visual Page it may be necessary to display a value that is stored in the database as an integer value, but that actually represents a TrakSYS enum. An example of this is querying the tTag table to show the value of the DataType field. The data to be displayed to the user should be "String", not `1`.

On the same page, the same raw integer value can be leveraged to build Urls, or linking to other filters. By using _Process String_ expression formatting, the data can be displayed appropriately.

### **Overview**

The Process String expression in this example is broken up into 2 parts (the Process Expression syntax has other parts/tokens for more advanced configurations):
    
    
    {Key:Format}
    

#### **Key**

The Key can be used to get the value of the field for the current row, or from the ETS Values Dictionary.

#### **Format**

The format helps to determine how to display the value specified by the `Key`. This token will be used to convert the value of `1` to "String" (DataType.String = 1). TrakSYS enums can be located in one of 2 places, either in the `ETS.Core.Enums` namespace or in `ETS.Ts.Core.Enums` for Web-specific enums.

### **Example**

The following example shows how to leverage the Process String expression syntax to display the value of a TrakSYS enum on the screen. The following steps will aid in building a custom Visual Page and displaying the name and DataType of up to 10 Tags in the database.

  * Create a Visual Content Page and add a `Custom SQL Data Table` Part (TrakSYS\Data Tables).
  * Set the SQL Property to the following:
        
        SELECT TOP 10 ID, [Name], DataType
        FROM tTag
        

  * Set the Data | Target Values Key to "Data.Tags".

  * Add a `List View` Part (TrakSYS\Lists).  
  

  * Set the Data | Source Values Key to "Data.Tags".
  * Set the Main Text to:
        
        {Name} : {DataType:Enum:ETS.Core.Enums.DataType}

  * Save and/or Preview the results.

  * Sample result: `L1.Fault : Discrete`.


