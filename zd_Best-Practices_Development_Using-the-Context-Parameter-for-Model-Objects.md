# Using the Context Parameter for Model Objects

*Source: https://portal.parsec-corp.com/hc/en-us/articles/34175406363411-Using-the-Context-Parameter-for-Model-Objects*
*Last updated: 2025-08-07T21:52:32Z*

---

Applies To | All Versions

### Summary

When [Loading](https://docs.parsec-corp.com/api-reference/api-services-reference/api.data/api.data.db-entity/api.data.db-entity-.load/byid), [Inserting](https://docs.parsec-corp.com/api-reference/api-services-reference/api.data/api.data.db-entity/api.data.db-entity-.save/insertasnew), [Updating](https://docs.parsec-corp.com/api-reference/api-services-reference/api.data/api.data.db-entity/api.data.db-entity-.save/updateexisting), and [Deleting](https://docs.parsec-corp.com/api-reference/api-services-reference/api.data/api.data.db-entity/api.data.db-entity-.delete/byid) data from built-in TrakSYS tables, it is always recommended to use Model Objects. Each instance represents a one to one mapping of a table, with a `Db` prefix and the removal of the `t` database prefix. For example, the Model Object for the `tSystem` table is `DbSystem`.

In TrakSYS, there are several child entities that may rely on the existence of parent entities. In order to insert these child entities, the parent entities must already exist. For some complex scenarios, it may be desirable to insert the parent and child entities in a single transaction. Other scenarios may require simultaneous modifications to multiple entities. In either case, each method (linked above) for modifying data has an optional `context` list parameter that can be used. This article explains how to properly use this parameter when modifying multiple Model Objects in a single transaction.

### Simple Example and Explanation

When creating multiple different entities using Model Objects, an object should be created for each entity. For this example, an Area and System will be created. In code, a separate Model Object will need to be created for both entities. While creating a System for an existing Area is certainly possible, the optional `context` list parameter also makes it possible to do so in a single transaction. To show why this parameter is needed, the code below has been written to try and insert both entities using Model Objects without the `context` list parameter. This code was written within a Button Click handler on a Visual Page Definition:
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create the Unit of Work object
        var uow = this.Ets.Api.CreateUnitOfWork();
        // Create the Area Model Object
        var area = new ETS.Core.Api.Models.Data.DbArea();
        // Populate the Object Model properties
        area.Name = "Generated Area";
        area.Key = "Generated Key";
        area.SiteID = 1;
        area.LogicManagerID = 1;
        // Add the changes to the Unit of Work object
        this.Ets.Api.Data.DbArea.Save.InsertAsNew(area, uow).ThrowIfFailed();
    
        // Create the System Model Object
        var system = new ETS.Core.Api.Models.Data.DbSystem();
        // Populate the Object Model properties
        system.Name = "Generated System";
        system.Key = "Generated Key";
        system.AreaID = area.ID;
        system.S95SystemType = ETS.Core.Enums.S95SystemType.ProductionLine;
        // Add the changes to the Unit of Work object
        this.Ets.Api.Data.DbSystem.Save.InsertAsNew(system, uow).ThrowIfFailed();
    
        // Push the final changes to the database
        uow.ExecuteReturnsResultObject().ThrowIfFailed();
      }
      catch (Exception ex)
      {
        // Throw errors if the process fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

As shown, both Model Objects have been correctly created. Since the System is a child of the Area, the `area.ID` value has been provided for the AreaID property of the System Model Object. After saving the changes, the code can now be executed. However, on execution, the following error message will appear:

![](https://portal.parsec-corp.com/hc/article_attachments/34896672690835)

This happens because the AreaID property of the System is referencing the ID of the Area Model Object. This is an issue because the Area does not exist in the database even though a Model Object has been created for it.

This issue can be resolved using the `context` list parameter. This parameter adds all objects to a list for processing. When the Unit of Work object executes and tries to process the transaction, the references for parent and child entities are automatically resolved since they do not exist within the TrakSYS database. This allows the process to continue and either insert the entities into the database or fail due to other reasons. The original code example has been revised to use the `context` parameter below:
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Create Unit of Work object and a list for the context parameter
        var uow = this.Ets.Api.CreateUnitOfWork();
        **var context = new List<object>();**
    
        // Create the Area Model Object
        var area = new ETS.Core.Api.Models.Data.DbArea();
        // Populate the Object Model properties
        area.Name = "Generated Area";
        area.Key = "Generated Key";
        area.SiteID = 1;
        area.LogicManagerID = 1;
        // Add the changes to the Unit of Work object
        this.Ets.Api.Data.DbArea.Save.InsertAsNew(area, uow, false, **context**).ThrowIfFailed();
    
        // Create the System Model Object
        var system = new ETS.Core.Api.Models.Data.DbSystem();
        // Populate the Object Model properties
        system.Name = "Generated System";
        system.Key = "Generated Key";
        system.AreaID = area.ID;
        system.S95SystemType = ETS.Core.Enums.S95SystemType.ProductionLine;
        // Add the changes to the Unit of Work object
        this.Ets.Api.Data.DbSystem.Save.InsertAsNew(system, uow, false, **context**).ThrowIfFailed();
    
        // Push the final changes to the database
        uow.ExecuteReturnsResultObject().ThrowIfFailed();
      }
      catch (Exception ex)
      {
        // Throw errors if the process fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

After saving the changes and previewing the page, the code can successfully execute. To verify the results, the user can navigate to **Configuration | Systems**. Both the Area and System should be displayed within the configuration.

![](https://portal.parsec-corp.com/hc/article_attachments/34897051387283)

### Complex Example

This example will include combining multiple Task-related entities all within a single transaction using the `context` parameter. While this example will focus on Tasking entities, this same concept can be used with any other built-in parent/child TrakSYS entities. When configuring Tasking functionality, the following entities are required:

  * Task Form Item Group Group
  * Task Form Item Group
  * Task Form Item
  * Task Definition
  * Task Definition Task Form Item Group



There are other higher level entities (such as Site, Area, and System) that are also required, but not included in this example. Therefore, the assumption is that these entities already exist within the configuration. The example code below includes all of the listed entities using the full Model Object structure. Note that each entity only has the bare minimum populated for each property. In an actual implementation, it is recommended to specify the rest of the properties as needed. Similar to the previous example, this example was placed in a Button Click method on a Visual Page Definition. However, similar code can be used in other areas of the application (with slight syntax changes):
    
    
    private void ButtonClick(object sender, EventArgs e)
    {
      try
      {
        // Provide a valid SystemID
        int systemID = -1;
    
        // Create Unit of Work object and a list for the context parameter
        var uow = this.Ets.Api.CreateUnitOfWork();
        var context = new List<object>();
    
        //Create the Task Form Item Group Group Model Object
        var taskFormItemGroupGroup = new ETS.Core.Api.Models.Data.DbTaskFormItemGroupGroup();
        // Populate the Model Object Properties
        taskFormItemGroupGroup.Name = "Generated Task Form Item Group Group";
        taskFormItemGroupGroup.Key = "GeneratedGroupGroupKey";
        taskFormItemGroupGroup.SiteID = this.Ets.Api.Site.GetCurrentSiteID();
        // Save the Task Form Item Group Group to the Unit of Work object
        this.Ets.Api.Data.DbTaskFormItemGroupGroup.Save.InsertAsNew(taskFormItemGroupGroup, uow, false, context).ThrowIfFailed();
    
        // Create the Task Form Item Group Model Object
        var taskFormItemGroup = new ETS.Core.Api.Models.Data.DbTaskFormItemGroup();
        // Populate the Model Object Properties
        taskFormItemGroup.Name = "Generated Task Form Item Group";
        taskFormItemGroup.Key = "GeneratedKey";
        taskFormItemGroup.TaskFormItemGroupGroupID = taskFormItemGroupGroup.ID;
        // Save the Task Form Item Group
        this.Ets.Api.Data.DbTaskFormItemGroup.Save.InsertAsNew(taskFormItemGroup, uow, false, context).ThrowIfFailed();
    
        // Create the Task Form Item Model Object
        var taskFormItem = new ETS.Core.Api.Models.Data.DbTaskFormItem();
        // Populate the Model Object Properties
        taskFormItem.Name = "Generated Task Form Item";
        taskFormItem.TaskFormItemGroupID = taskFormItemGroup.ID;
        taskFormItem.Key = "GeneratedTFIKey";
        taskFormItem.DataType = ETS.Core.Enums.DataType.String;
        // Save the Task Form Item
        this.Ets.Api.Data.DbTaskFormItem.Save.InsertAsNew(taskFormItem, uow, false, context).ThrowIfFailed();
    
        // Create the Task Definition Model Object
        var taskDefinition = new ETS.Core.Api.Models.Data.DbTaskDefinition();
        // Populate the Model Object Properties
        taskDefinition.Name = "Generated Task Definition";
        taskDefinition.Key = "GeneratedKey";
        taskDefinition.SystemID = systemID;
        // Save the Task Definition
        this.Ets.Api.Data.DbTaskDefinition.Save.InsertAsNew(taskDefinition, uow, false, context).ThrowIfFailed();
    
        // Create the Task Definition Task Form Item Group Model Object
        var taskDefinitionTaskFormItemGroup = new ETS.Core.Api.Models.Data.DbTaskDefinitionTaskFormItemGroup();
        // Populate the Model Object Properties
        taskDefinitionTaskFormItemGroup.TaskDefinitionID = taskDefinition.ID;
        taskDefinitionTaskFormItemGroup.TaskFormItemGroupID = taskFormItemGroup.ID;
        // Save the Task Definition Task Form Item Group
        this.Ets.Api.Data.DbTaskDefinitionTaskFormItemGroup.Save.InsertAsNew(taskDefinitionTaskFormItemGroup, uow, false, context).ThrowIfFailed();
    
        // Push the final changes to the database
        uow.ExecuteReturnsResultObject().ThrowIfFailed();
      }
      catch (Exception ex)
      {
        // Throw errors if the process fails
        this.Ets.Debug.FailFromException(ex);
      }
    }
    

As the code comments explain, a Model Object is created for each of the entities. The properties are filled out for each entity and added to the `context` list of the Unit of Work object. The list helps resolve all of the dependencies temporarily as there are several layers of parent/child entities. After all changes have been added, the Unit of Work object is executed and will save all entities in a single transaction.

To verify the results, the configuration for the Task Form Item Group Group, Task Form Item Group, and Task Form Item can be found under **Configuration | Miscellaneous | Task Form Items**. As shown, all three entities have been successfully created with the values provided within each property:

![](https://portal.parsec-corp.com/hc/article_attachments/34931997673363)

The results for the Task Definition can be verified by navigating to **Configuration | Systems**. After selecting the desired Area and System, the Task Definitions can be viewed. As shown below, an entry has been successfully generated for the Task Definition:

![](https://portal.parsec-corp.com/hc/article_attachments/34932018884883)

Finally, the association between the Task Definition and the Task Form Item Group can be verified by selecting the newly created Task Definition and selecting the Task Form Item Groups link on the third slice:

![](https://portal.parsec-corp.com/hc/article_attachments/34932018886931)

As shown an entry was successfully created and properly links both entities:

![](https://portal.parsec-corp.com/hc/article_attachments/34932018888211)
