# Example Product Importer

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360009236814-Example-Product-Importer*
*Last updated: 2025-05-21T23:09:47Z*

---

Applies To | TrakSYS 10+

### **Summary**

In some scenarios, it may be desirable to import Products from an external file or application (like an Enterprise Resource Planning 'ERP' System). Importing new and updated product information into TrakSYS can save a lot of time and can be far more efficient than manually creating Products one-by-one within the TrakSYS Web. 

The code shown below provides an example of how to create a simple Product Import utility. This class can be implemented in any script within the TrakSYS Web (e.g. Logic Scripts, Web Scripts, Modules, or Global Scripts). In most scenarios, it is recommended to execute this code using a Module (which is handled by the Data Management Service) on a periodic basis. This example should help provide a starting point on creating an import tool that leverages some of the new features in TrakSYS 10 including validation.

Please note that within this example, the following assumptions are made:

  * The Product Set that is being imported already exists within the TrakSYS installation.
  * The Product Set **does not** support versioning.
  * The Products imported are assumed to have their ID set to -1.
  * The main key identifier for the imported Products will be Product Code.



This example only addresses the Product Code, Name, and Attribute fields 1 through 5, but can be easily expanded to include other values. It is possible to import Materials, Product Types, and Product Groups, but doing so creates an additional layer of complexity that this example does not provide. Additional custom coding will be required to include these extra entities.

### **Example Code**

The following is an example for the ProductImportService class:
    
    
    public partial class ProductImportService
    {
      private ApiService _api;
    
      /// ***********************************************************
      private void SetPropertiesOnProductBeingInserted(DbProduct product)
      {
        // TODO any extra customization desired for a product that is going to get inserted
      }
    
      /// ***********************************************************
      private void SetPropertiesOnProductBeingUpdated(DbProduct target, DbProduct source)
      {
        // TODO update the target product (basically the version of Product found in the database) with the imported values from source.
        // in this example the assumption is that the import source only provides values for attributes 1-5 so those are the only things
        // that should be copied onto target to prevent any clearing of actual data.
        
        target.Name = source.Name;
        target.Attribute01  = source.Attribute01;
        target.Attribute02  = source.Attribute02;
        target.Attribute03  = source.Attribute03;
        target.Attribute04  = source.Attribute04;
        target.Attribute05  = source.Attribute05;
      }
      
      /// ***********************************************************
      public Result<List<DbProduct>> ImportProducts(List<DbProduct> sourceList, DbProductSet set)
      {
        try
        {
          // validate null
          if (sourceList == null) throw new ArgumentNullException("sourceList");
          if (set == null) throw new ArgumentNullException("set");
          
          // setup
          _api = ApiService.GetInstance();
          var r = new Result<List<DbProduct>>().AsSuccess(null);
          var uow = _api.CreateUnitOfWork();
          var importContext = new List<object>();
          var importedList = new List<DbProduct>();
          
          // more validation of input
          if (sourceList.Count == 0) return r.AsError("sourceList is empty.");
          if (set.ID.IsNull()) return r.AsError("Product Set is assumed to already be created.");
          if (set.EnforceVersioning) return r.AsError("This import process does NOT support product sets that enforce versioning.");
          
          // loop through all source products to import
          int i = 0; // for displaying good error messages
          foreach (var source in sourceList)
          {
            // basic validation ProductCode is required
            if (source.ProductCode.IsNullOrWhiteSpace()) return r.AsError("Product[{0}].ProductCode is required.".FormatWith(i));
            
            // see if product exist in database or not
            var prodInDb = this.LoadProductByCode(source.ProductCode, set.ID).ThrowIfFailed();
            
            // do different things depending on if we are inserting or updating a product
            DbProduct target;
            SaveAction mode;
            if (prodInDb == null)
            {
              target = source.CreateShallowCopy();
              target.ProductSetID = set.ID;
              this.SetPropertiesOnProductBeingInserted(target);
              mode = SaveAction.Insert;
            }
            else
            {
              target = prodInDb;
              this.SetPropertiesOnProductBeingUpdated(target, source);
              mode = SaveAction.Update;
            }
            
            var validResult = this.CustomValidateProduct(target, mode, importedList, i);
            if (!validResult.Success)
            {
              r.AsErrorWithMessages(validResult.Messages);
            }
            else
            {
              var importResult = _api.Data.DbProduct.Merge(target, (mode == SaveAction.Insert), uow, /* ignoreWarnings */ true, importContext);
              if (!importResult.Success) 
              {
                r.AsError("Error importing Product '{0}'.".FormatWith(target.ProductCode));
                return r.AsErrorWithMessages(importResult.Messages);
              }
              
              importedList.Add(importResult.Return);
            }
            
            i++;
          }
          
          // did not pass validation
          if (!r.Success) return r;
          
          // save
          var uowResult = uow.ExecuteReturnsResultObject().ThrowIfFailed();
          return r.AsSuccess(importedList);
        }
        catch (Exception ex)
        {
          return Result<List<DbProduct>>.ReturnExceptionFailure(ex, null);      
        }
      }
      
      /// ***********************************************************
      private Result<DbProduct> LoadProductByCode(string productCode, int productSetID)
      {
        // this is being done instead of api.Data.DbProduct.Load.ByProductCodeAndProductSetID  
        // because if for some reason a given ProductSet has more than 1 product with   
        // the same ProductCode, then I want to error. If I use ByProductCodeAndProductSetID  
        // it will not error but return 1 of the tProducts. In this example below if more  
        // than one (i.e. the TOP 2), it will error. 
        var r = new Result<DbProduct>();
        
        string sql = "SELECT TOP 2 * FROM dbo.tProduct p WHERE p.ProductSetID = {0} AND p.ProductCode = {1}".FormatWith(productSetID.ToSql(), productCode.ToSql());
        var list = _api.Data.DbProduct.GetList.WithSql(sql);
        if (list == null) return r.AsError("An error occurred while trying to retrieve the Product Code '{0}'.".FormatWith(productCode));
        
        // it did not error, but the product code doesn't exist
        if (list.Count == 0) return r.AsSuccess(null);
        if (list.Count == 1) return r.AsSuccess(list[0]);
        
        return r.AsError("An error occurred, more than 1 Product was found for the Product Code '{0}'.".FormatWith(productCode));
      }
      
      /// ***********************************************************
      private Result<bool> CustomValidateProduct(DbProduct prod, SaveAction mode, List<DbProduct> importedList, int i)
      {
        var r = new Result<bool>().AsSuccess(true);
        int oneBased = i + 1;
        
        var hasDupeCode = importedList.Any(p => p.ProductCode.EqualsAnyCase(prod.ProductCode));
        if (hasDupeCode) return r.AsError("The ProductCode '{0}' was found more than once in the import. The first duplicate was found on row {1:N0}.".FormatWith(prod.ProductCode, oneBased));
        
        return r;
      }
    }
    
