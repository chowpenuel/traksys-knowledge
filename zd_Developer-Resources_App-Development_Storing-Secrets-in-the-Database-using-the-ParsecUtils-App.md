# Storing Secrets in the Database using the Parsec.Utils App

*Source: https://portal.parsec-corp.com/hc/en-us/articles/6824635275155-Storing-Secrets-in-the-Database-using-the-Parsec-Utils-App*
*Last updated: 2025-06-05T23:58:30Z*

---

Applies To | Parsec.Utils 3.1.2+

### Summary

In some cases, it may be desirable to store sensitive information (such as passwords or personal infromation) in the TrakSYS database. While the information can be obfuscated on pages within the TrakSYS Web, the information will still be viewable as plaintext within the database. The Parsec.Utils App (Parsec.Utils.TsRoot or Parsec.Utils.TsWeb) offers functionality that allows users to safely store sensitive information.

The App offers 3 potential options for storing secrets using the Parsec.Utils framework:

  * Storing secrets in the TrakSYS database.
  * Storing secrets in an external file with encryption keys stored as environmental variables.
  * Implementing a custom solution leveraging the built in logic.



### General

For all options the secrets are stored as a JSON payload, where the secret key is stored as plain text, but the actual value is encrypted. This allows for easier editing of settings and seeing which keys are being used. The general pattern for using the App in code includes using Dependency Injection to retrieve the values.

One of the general principles that are supported with this infrastructure (as a general infosec policy) is that developers should not have access to the actual production keys. This implies the use of Database Transfer with development and production environments while ensuring the developers do not have access to the production secrets.
    
    
    public class MyCustomDataService
    {
      private readonly IVaultService _vaultSvc;
      public MyCustomDataService(ExternalKeyVaultService vaultSvc)
      {
        _vaultSvc = vaultSvc;
      }
      
      public Result<DataTable> GetExternalData(int parameterID)
      {
        string user = _vaultSvc.GetSecret("SourceXUser");
        string pass = _vaultSvc.GetSecret("SourceXPass");
    
        //..
      }
    }
    

To use the class, something similar to the following can be used:
    
    
    var dataSvc = api.Create.InstanceOf<MyCustomDataService>();
    var dt = dataSvc.GetExternalData(externalID).ThrowIfFailed();
    

If the user simply wants to access the secret values from the TrakSYS Web, something similar to the following can be used:
    
    
    var vaultSvc = this.Ets.Api.Create.InstanceOf<Parsec.Utils.Services.Security.ExternalKeyVaultService>();
    string user = vaultSvc.GetSecret("SourceXUser");
    this.Ets.Values["SourceXUser.Secure"] = user;
    

This method assumes that the JSON secrets are stored using something similar to the following format:
    
    
    {
      "SourceXUser": "base64encryptedvaluehere",
      "SourceXPass": "base64encryptedvaluehere"
    }

### Options

The following is a high level overview of the options that are available when using the Parsec.Utils App. Note that none of these options have any built-in configuration pages and are accomplished purely through custom code.

#### Storing Secrets in the TrakSYS Database

For this option, the `Parsec.Utils.Services.Security.CustomDataKeyVaultService` class can be used to store the secrets in the `tCustomData` table. The values are stored in a table with a key value of 'secrets'. This class has a method called `EncryptValue(string value)`, which can simplify the process of modifying the values. However, the record still needs to be created and populated manually. This option is commonly used when a Visual Page Definition will be used to add and edit secret values. This option is the easiest to set up and use, however, the caveat is that it's the least secure. The encryption keys are embedded directly in the App. Therefore, if a user has access to the `tCustomData.DataText` field, they could simply use the Parsec.Utils app to decrypt the values.

#### Storing secrets in an External File with Encryption Keys Stored as Environmental Variables

For this option, the `Parsec.Utils.Services.Security.ExternalKeyVaultService` class can be used to store the secrets in a file outside the database. More specifically, the file will be stored under `C:\parsec\secrets.txt`. The encryption keys are stored as environmental variables as `traksys_iv` and `traksys_key`. In general, if the values are stored as System Level Environmental Values, then changing the values will force a server reboot every time. Therefore, storing the encryption keys simply as environmental values will only require a single machine reboot. To generate a traksys_iv and traksys_key pair something similar to the following code can be used to get the values:
    
    
    byte[] iv;
    byte[] key;
    using (var aes = new System.Security.Cryptography.AesCryptoServiceProvider())
    {
      aes.GenerateIV();
      aes.GenerateKey();
      iv = aes.IV;
      key = aes.Key;
    }
    var ivandkey = Tuple.Create(Convert.ToBase64String(iv), Convert.ToBase64String(key));
    

This should store the values in the following Environmental Variables:

`traksys_iv = ivandkey.Item1  
traksys_key = ivandkey.Item2`

For troubleshooting purposes, the traksys_iv value is always shorter than the traksys_key value. An example traksys_iv and traksys_key pair is shown below:

`traksys_iv: UywhTUlBlp9H1Nacsd7fKg==`  
`traksys_key: LUu2Q3FAdjSDBX/NRwzjQtujarqnK+yG945yjJ2D32c=`

To encrypt the values, it's strongly recommended to have a separate console .NET App that encrypts values and can get the encrypted values with the appropriate keys. Within the App, something similar to the following code can be used to encrypt the values:
    
    
    string encryptedValueBase64 = Parsec.Utils.Services.Security.VaultServiceBase.AesEncryptValue("p@$$w0rd", ivandkey);
    // using the encryption keys above the result is
    // mJBQpeIxJvCxLnlW+3v1GQ==
    

The traksys_iv and traksys_key pair are stored in the Tuple as shown above. Now that the original value is encrypted, the resulting value can now be stored in the secrets.txt file.
    
    
    {
      "examplepassword": "mJBQpeIxJvCxLnlW+3v1GQ=="
    }

#### Implementing a Custom Solution Leveraging Built-In Logic

There are several abstract base classes that the 2 classes above (mentioned in the 2 previous options) inherit from. Those classes can be leveraged for custom implementations as needed. The following is an example of how to create a custom instance of the `ExternalKeyVaultService` class:
    
    
    /// store secrets instead of 'C:\parsec\secrets.txt' store in 'C:\mysecrets\custom.txt'
    // and use the environment values of mykey_iv and mykey_key
    public class MyCustomVault : ExternalKeyVaultServiceBase
    {
      public sealed override string SecretsFilePath { get; } = @"C:\mysecrets\custom.txt";
      public sealed override string EnvironmentPrefix { get; } = "mykey";
    }
    
