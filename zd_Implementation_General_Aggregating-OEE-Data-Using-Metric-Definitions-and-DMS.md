# Aggregating OEE Data Using Metric Definitions and DMS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360035484054-Aggregating-OEE-Data-Using-Metric-Definitions-and-DMS*
*Last updated: 2025-05-21T22:08:55Z*

---

Applies To | TrakSYS 10+

### **Summary**

In many scenarios, it is desirable to perform data aggregation pertaining to a specific TrakSYS entity, e.g. KPI Calculations. The TrakSYS Data Management Service provides this type of roll-up functionality through the use of Metric Definitions. 

A Metric Definition describes a structured way of calculating and aggregating one or more values for a specified type of TrakSYS entity on a periodic or manually triggered basis. The definition includes the specific types of values that will be stored, as well as the SQL queries used to retrieve and calculate the data. The results of a Metric Definition execution are stored in the `tMetric` table of the TrakSYS database.

This kind of planned aggregation serves to maintain application performance by eliminating the need to query the data on-demand, potentially in multiple user interfaces throughout the application. Instead, the data is rolled up once and available anywhere it is needed.

This article describes how to execute a roll-up of OEE data by SystemID and Production Date.

### **Procedure**

#### **Define the Metric Scheme**

Metric Schemes define the available Attributes for Metric Definitions, ultimately determining what will be stored in the `tMetric` record. A Metric Scheme is a set of 20 Metric Attributes or Metric Scheme Columns. Empty Attributes are created automatically when a Metric Scheme is created.

  1. In the Configuration section, browse to the Miscellaneous...Metric Definitions hub.
  2. In Slice 1, under Schemes, click New.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18548883151251)  
  

  3. Give the Scheme a name and save. In this example, the name is "OEE Scheme." 
  4. In Slice 3, click on the Columns link for the Scheme.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18548917988883)  
  

  5. Configure the columns with the Names and Data Types shown below. Ensure that "Enabled" is checked for each column. Specifying the Name here allows re-usable reports to display the appropriate label for each value.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18548894594835)



#### **Create the Metric Definition**

The Metric Definition helps define how the Metric records will be populated and is considered a child of the Scheme record. In this example, the Metric Definition will roll up data by Date using the standard OEE KPIs. 

  1. Click the Metric Definitions link for the Scheme created above.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18548926088339)  
  

  2. Click New under Metric Definitions.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18548989094547)  
  

  3. Configure the Metric Definition with the following General tab properties:  
  
_Name:_ OEE By Production Date  
 _Key:_ Oee.ByDate  
 _Entity Type:_ System  
 _Rollup Type:_ Date
  4. In the SQL tab, enter the following Parameter SQL:  
  

         
         DECLARE @metricSystemID int = 2
         
         SELECT 
          @metricSystemID AS EntityID,
          @metricSystemID AS SystemID
         

Parameter SQL is designed to query the configuration tables that are necessary to retrieve the data. The EntityID field is required and exists for extensibility. The SystemID field is also required so the Standard Metrics can retrieve the specified data. In this example, the SystemID has been hardcoded.  
  
As a further example, for a daily roll-up of all the systems for a given AreaID, the following Parameter SQL would be used (this assumes a KPI Calculation exists for each system):   
  

         
         DECLARE @metricAreaID int = 1
         
         SELECT
          s.ID AS EntityID,
          s.ID AS SystemID
         FROM tSystem s
         WHERE s.AreaID = @metricAreaID
         AND s.Enabled = 1
         AND s.ParentSystemID IS NULL
         AND s.S95SystemType = 1 /* Discrete System */
         ORDER BY s.DisplayOrder
         

  5. Click on the Standard Metrics link under the Metric Definition.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18549031122451)  
  

  6. Double-click each Scheme attribute under Standard Metrics and set the programmatic value for each KPI by selecting it from the drop-down.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18549110717203)  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18549140325779)  
  
The Metrics should be configured as shown below:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18549176441491)



#### **Create the Module**

The module's trigger mode can be set to anything, regardless of Metric Definition Rollup Type, as the Metric Engine is designed to take that into account. For example, Trigger Mode can be set to Periodically every 4 hours. Note that the module will not execute every 4 hours exactly, a few extra seconds are included by design in order to allow Logic Service to correctly save all the OEE data. This ensures the Metric is as accurate as possible.

  1. Create a DMS Module with the following properties:  
  
_Trigger Mode:_ Periodic  
 _Periodic Interval:_ 4  
 _Periodic Frequency:_ Hour  
  
This mode will aggregate the data every 4 hours for the current day but the frequency can be decreased to daily or increased to aggregate more often. 



#### **Create the Module Step**

  1. For the Module created above, create a new Module Step of type Metric Definition Module Step and specify a Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18549251501075)   
  

  2. Assign the Metric Definition configured above.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18549271689747)  
  
Note that Parameter SQL should be left blank. This field is used to override the default Metric Definition Parameter SQL.



#### **Run the Module**

Once the module is running, data will start to be aggregated according the specified configuration. When the module step is executed, a Metric record will be created for the current date for each system in the Parameter SQL. A `tMetric` record looks as follows:

![mceclip15.png](https://portal.parsec-corp.com/hc/article_attachments/360046256734)

#### **Updating`tMetric` Records**

If any data changes occur which impact past OEE calculations (e.g. additional Availability Loss seconds, adjusted interval counts), the Metric record should be re-calculated. In this example, data changes took place on Monday, July 29th 2019. 

  1. Identify the impacted tMetric record and mark it to be updated using the query below (or similar):  
  

         
         DECLARE @metricDate date = '2019-07-29'
         
         UPDATE tMetric
         SET [State] = 1
         WHERE StartDateTime = @metricDate
         AND MetricDefinitionID = 1
         AND SystemID = 2
         




The `tMetric.State` value of 1 represents the enumeration `MetricState.RecalculateRequested` which marks this record as needing recalculation.

DMS includes a special "System" module that looks for a trigger key named `ETS.RECALC`. It will require passing in the args Dictionary either the `MetricDefinitionID` or the `MetricDefintionKey`. For example, if a Module Trigger with the `Key` "ETS.RECALC" is created and it contains an args Dictionary Key of `MetricDefinitionID` = 1, the module will look for all Metric records for that `MetricDefinitionID` and a `State` of 1 and recalculate them. This approach is useful when updating multiple `tMetric` records is required.

If updating a single record is required, the same Module Trigger Key can be used, but the args Dictionary only needs to contain the `MetricID` with the value of the record that need to be updated. In this scenario, the value of State can be 0 (i.e. `MetricState.None`).

**See Also**

  * [Programmatically Triggering a DMS Module](https://portal.parsec-corp.com/hc/en-us/articles/360035503214-Using-a-Logic-Service-Script-Class-to-Trigger-a-DMS-Module)


