# Programmatically Creating and Updating Product and Material Versions

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360023028613-Programmatically-Creating-and-Updating-Product-and-Material-Versions*
*Last updated: 2025-05-21T23:10:41Z*

---

Applies To | TrakSYS 10+

### **Summary**

In some scenarios, it may be desirable to programmatically manage Product and Material Versions using the TrakSYS API. This can be useful in scenarios where a separate custom edit form is used to manage these entities instead of using the built-in configuration pages. Doing so can give more control over the behavior of the page by providing the ability to add functionality that is not be included in the built-in pages.

The examples below show how to programmatically create new Drafts of Products and Materials as well as setting the new Draft as the Active Version. Each example includes best practices such as using the Unit of Work pattern and error handling with `ThrowIf` extension methods.

### **Programmatically Creating a New Draft**

The following code examples show how to programmatically create a new Draft of a Product or Material using the TrakSYS API. Note that these examples assume that a Product or Material already exists and Versioning has been enabled for either the Product Set or Material Group.

In the examples below, the `productID` and `materialID` variables hold the ID values for the respective entities. How these variables are set will depend on the page's implementation (e.g. querystring, user form input).

#### **Products Example**
    
    
    // Create Unit of Work
    var uow = this.Ets.Api.CreateUnitOfWork();  
    
    // Load the Product Model Object
    var source = this.Ets.Api.Data.DbProduct.Load.ByID(productID)  
      .ThrowIfLoadFailed("Product.ID", productID);  
    
    // Create a new Draft of the Product
    var newDraft = this.Ets.Api.Data.DbProduct.Do.DuplicateToNewVersion(source, uow)  
      .ThrowIfFailed();  
    
    // Execute the Unit of Work
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
    

#### **Materials Example**
    
    
    // Create Unit of Work
    var uow = this.Ets.Api.CreateUnitOfWork();  
    
    // Load the Material Model Object
    var source = this.Ets.Api.Data.DbMaterial.Load.ByID(materialID)  
      .ThrowIfLoadFailed("Material.ID", materialID);  
    
    // Create a new Draft of the Material
    var newDraft = this.Ets.Api.Data.DbMaterial.Do.DuplicateToNewVersion(source, uow)  
      .ThrowIfFailed();  
    
    // Execute the Unit of Work
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
    

After executing the code, a new Draft should appear for the Product or Material. However, it will not be the Active Version.

### **Setting a Draft as the Active Version**

After a Draft has been created for a Product or Material, the following code examples can be used to automatically retire the current version and set the Draft as the new active version. Note that these examples assume that a Draft has already been created for the Product or Material.

#### **Products Example**
    
    
    // Create Unit of Work
    var uow = this.Ets.Api.CreateUnitOfWork();  
    
    // Load the Product Model Object
    var newProductVersion = this.Ets.Api.Data.DbProduct.Load.ByID(productID)  
      .ThrowIfLoadFailed("Product.ID", productID);  
    
    // Activate new Version of the Product
    this.Ets.Api.Data.DbProduct.Do  
      .ActivateVersion(newProductVersion, "User Name Here", "Notes Here", uow)  
      .ThrowIfFailed();  
    
    // Execute the Unit of Work
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
    

#### **Materials Example**
    
    
    // Create Unit of Work
    var uow = this.Ets.Api.CreateUnitOfWork();  
    
    // Load the Material Model Object
    var newMaterialVersion = this.Ets.Api.Data.DbMaterial.Load.ByID(materialID)  
      .ThrowIfLoadFailed("Material.ID", materialID);  
    
    // Activate new Version of the Material
    this.Ets.Api.Data.DbMaterial.Do  
      .ActivateVersion(newMaterialVersion, "User Name Here", "Notes Here", uow)  
      .ThrowIfFailed();  
    
    // Execute the Unit of Work
    uow.ExecuteReturnsResultObject().ThrowIfFailed();
    
