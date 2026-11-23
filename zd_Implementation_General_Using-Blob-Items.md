# Using Blob Items

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360035630493-Using-Blob-Items*
*Last updated: 2025-05-21T22:09:01Z*

---

Applies To | TrakSYS 10.1.3+

**Summary**

Similar to Library Items, Blob Items can store many different types of files in various formats. These files can then be referenced by creating links from different areas of the TrakSYS application. Although Library Items have similar functionality, the main difference with Blob Items is that they **are not** included in the [Database Transfer](https://portal.parsec-corp.com/hc/en-us/articles/115004492907) process. 

Blob Items are purposely excluded from this process so files can be safely stored within the installation without the possibility of being overwritten. This is important if certain files such as pictures taken from the plant floor, purchase orders in .pdf format, and XML documents from external ERP systems are stored within the production environment.

Please note that Blob Items are used purely for extensibility purposes. There is nothing within TrakSYS that uses Blob Items by default and there are no built-in configuration pages that allow users to add/create them. This article provides an example of how to add Blob Items and reference them in the configuration.

**Example**

The code example shown below was taken from the New Attachment Visual Page Definition available within the [TrakSYS 12 Demonstration Database](https://portal.parsec-corp.com/hc/en-us/articles/26911164101779-TrakSYS-12-0-Demonstration-Backup). Although the example shown uses Tasks, Blob Items can be used for other entities and purposes as well.

This example creates a Task Model Object, and allows users to upload attachments as Blob Items in order to associate them with a specific Task. As shown, the code will create a Blob Item Group called "Maintenance Attachments" if one does not exist already. It will then create a Blob Item record for the attachment and relate it to the Task.
    
    
    // Load Task Model Object using the TaskID
    _task = this.Ets.Api.Data.DbTask.Load.ByID(this.TaskID);
    if (_task == null) this.Ets.Debug.FailContentPage("Could not load Task for ID {0}".FormatWith(this.TaskID));
    
    // Check if a Blob Item Group exists
    var blobGroup = this.Ets.Api.Data.DbBlobItemGroup.Load.ByKeyAndSiteID("MaintenanceAttachments", this.Ets.Api.Site.GetCurrentSiteID());
    if(blobGroup == null)
    {
      // If no group exists, create one
      blobGroup = this.Ets.Api.Data.DbBlobItemGroup.Create.FromParentNone();
      // Set the name of the Blob Item Group
      blobGroup.Name = "Maintenance Attachments";
      // Set the Key of the Blob Item Group
      blobGroup.Key = "MaintenanceAttachments";
      // Save the Blob Item Group
      blobGroup = this.Ets.Api.Data.DbBlobItemGroup.Save.InsertAsNew(blobGroup).ThrowIfFailed();
    }
    
    // Get the uploaded file from the Values Dictionary
    var postedFile = this.Ets.Values.GetAs("Attachment.PostedFile", (HttpPostedFile)null);
    
    // Create the Blob Item
    var blobItem = this.Ets.Api.Data.DbBlobItem.Create.FromParentBlobItemGroupAndHttpPostedFile(blobGroup, postedFile);
    this.Ets.Form.UpdateModelWithKeyPrefix(blobItem, "Model.");
    if(blobItem.Name.IsNullOrWhiteSpace())
    {
      // Produce an error is no attachment is found
      this.Ets.Form.AddValidationError("Attachment Name is Required.", "Model.Name");
      return;
    }
    
    // Relate the BlobItem to a Task using the Task ID
    blobItem.GenericLinkID = _task.ID;
    blobItem.LinkType = "TaskID";
    
    // Save the file as a Blob Item
    blobItem = this.Ets.Api.Data.DbBlobItem.Save.InsertAsNew(blobItem).ThrowIfFailed();
    

**Referencing Blob Items**

Creating a link to a Blob Item is nearly identical to [creating links for Library Items](https://portal.parsec-corp.com/hc/en-us/articles/115004358707). The general format for creating a link to a Blob Item is as follows:

`~/blob/{siteKey}/{blobGroupKey}/{blobItemName}`

For example, an installation has a Site Key of "home" and a user programmatically uploads an image as a Blob Item called "Sample1.png" within a Blob Item Group with a Key of "MaintenanceAttachments." The user can then create the following link to reference that Blob Item:

`~/blob/home/MaintenanceAttachments/Sample1.png`

**See Also**

  * [Creating a Link for a Library Item](https://portal.parsec-corp.com/hc/en-us/articles/115004358707-Creating-a-Link-for-a-Library-Item)
  * [How To Add a Library Item](https://portal.parsec-corp.com/hc/en-us/articles/360009367873-How-To-Add-a-Library-Item)
  * [Database Transfer Guide](https://portal.parsec-corp.com/hc/en-us/articles/115004492907-TrakSYS-10-Database-Transfer-Guide)


