# Storing Secrets in TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/52163935783571-Storing-Secrets-in-TrakSYS*
*Last updated: 2026-06-04T18:26:19Z*

---

Applies To | TrakSYS 12.0.0+

### Summary

In some cases, it may be desirable to store sensitive information (such as passwords or API credentials) in the TrakSYS database. While values can be obfuscated on TrakSYS Web pages, the information could still be viewable as plaintext within the database. Starting with TrakSYS 12.0.0, secret management functionality was implemented directly within the TrakSYS software. This means the legacy Parsec.Utils App is now considered obsolete and should not be used for newer TrakSYS versions.

The secret management feature provides API methods to encrypt, decrypt, and retrieve secrets stored in the database. This means that the following is no longer needed to securely store secret values:

  * External .dll files
  * General text files
  * Environment variables (e.g., traksys_iv, traksys_key, etc.)



### General

Secrets are stored as a JSON payload inside a single record in the tCustomData table. Each secret key is stored as plain text while each secret value is encrypted. The encryption and decryption processes are handled entirely by the TrakSYS core code. This design offers an easier way to track which keys exist and can provide a more secure storage location for secret values. It also ensures there is a separation of duties between developer and production credentials.

In general, it is recommended to ensure that developers do not have access to production secrets. This is true even when working with multiple databases between environments (e.g., backing up and restoring databases or performing Database Transfers from one environment to another). To assist with this, all access to secrets is done with Dependency Injection using the TrakSYS API.

When using the built-in functionality, the following service is available to access programmatically:
    
    
    ETS.Core.Services.Security.CustomDataKeyVaultService
    

This service encrypts values before storage and decrypts them as they are retrieved. When the service is used, it will read secrets that are stored within the tCustomData table. Records stored within the tCustomData table must be stored using a specific format (shown below).

**Note** : Each secret must be stored within its own record within tCustomData. If multiple secrets are needed, it is recommended to create an individual record for each one.

**Field** | **Required Value**  
---|---  
Key | secrets (mandatory)  
DataText | JSON dictionary of encrypted values  
  
As an example, something similar to the following and be provided. This example uses JSON format in the DataText field:
    
    
    {
      "SourceXUser": "base64encryptedvaluehere",
      "SourceXPass": "base64encryptedvaluehere"
    }
    

When storing the secret, the Key value must contain "secrets". If a different value is provided, then the `GetSecret()` method will return NULL.

### Examples

#### Creating and Using Secrets Using a Page Definition

The following example uses a Visual Page Definition to demonstrate how this functionality can be used within the TrakSYS Web. For the purpose of this example, the code block below has been placed within the `ContentPage_Init()` method. This example demonstrates how to encrypt values, store them in tCustomData, and how to retrieve them using the CustomDataKeyVaultService.
    
    
    var vault = this.Ets.Api.Create.InstanceOf<ETS.Core.Services.Security.CustomDataKeyVaultService>();
    
    var secretsDictionary = new Dictionary<string, string>();
    secretsDictionary.Add("SecretA", vault.EncryptValue("Test Value A"));
    secretsDictionary.Add("SecretB", vault.EncryptValue("Test Value B"));
    
    DbCustomData customData = this.Ets.Api.Data.DbCustomData.Load.ByKey("secrets");
    
    // Add and encrypt new secret values
    if (customData == null)
    {
      customData = new ETS.Core.Api.Models.Data.DbCustomData();
      customData.Name = "Application Secrets";
      customData.Key = "secrets"; // MUST be "secrets"
      customData.DataText = this.Ets.ToJson(secretsDictionary);
      
      // Store new secret values in tCustomData
      this.Ets.Api.Data.DbCustomData.Save.InsertAsNew(customData).ThrowIfFailed();
    }
    
    // Get secret values
    string secretA = vault.GetSecret("SecretA");
    string secretB = vault.GetSecret("SecretB");
    
    // Store them in the Values Dictionary for debugging purposes
    this.Ets.Values["A"] = secretA;
    this.Ets.Values["B"] = secretB;
    

When the code is executed, the raw (decrypted) values will appear in the Values Dictionary. If the tCustomData table is queried, the full encrypted value will be stored within the `tCustomData.DataText` field.

**Note** : Placing the raw (unencrypted) value within the Values Dictionary was done in this example to demonstrate this functionality. Unless this is a requirement for the page, it is not recommended to store the raw (unencrypted) value as a security best practice.

In general, accessing secret values using custom code can be done using the following code:
    
    
    var vault = this.Ets.Api.Create.InstanceOf<ETS.Core.Services.Security.CustomDataKeyVaultService>();
    
    string user = vault.GetSecret("SourceXUser");
    string pass = vault.GetSecret("SourceXPass");
    

This code can be used for all Logic Service Script Classes and web content (such as Page Definitions and Web Script Classes). Additionally, this code can be used in Shared Script Classes only for installations using TrakSYS 12.0.1 and newer. If any version of TrakSYS 10 or 11 is used, the [Parsec.Utils App](https://portal.parsec-corp.com/hc/en-us/articles/6824635275155-Storing-Secrets-in-the-Database-using-the-Parsec-Utils-App) will need to be used instead.

### Implementing a Custom Solution

Currently, this built-in functionality only supports encrypting, storing, and retrieving secrets using the TrakSYS database. Custom file-based or environment-based vaults are not recommended or supported. However, if a custom storage method outside the database is needed, it must be implemented independently using standard .NET cryptography. A solution with this level of complexity is not supported TrakSYS secret framework.
