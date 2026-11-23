# Configuring an OPC UA Connection

*Source: https://portal.parsec-corp.com/hc/en-us/articles/360022312634-Configuring-an-OPC-UA-Connection*
*Last updated: 2025-05-21T22:45:32Z*

---

Applies To | TrakSYS 10.2.0+

### Summary

Beginning with TrakSYS version 10.2.0 it is possible to use the OPC Unified Architecture (UA) protocol to communicate with OPC servers that support it. Starting with TrakSYS version 10.2.3, Installation Manager was enhanced to simplify this process.

In TrakSYS 11.0.2, the ability to create a certificate-less connection was added. This also includes the ability to select a Preferred Security level. This article describes the procedure for configuring a connection for each type.

### Creating an OPC UA Connection Using Certificates

A two-way certificate exchange is required to connect TrakSYS to an OPC UA server:

  1. OPC UA server certificate imported into TrakSYS.
  2. Logic Service certificate imported into OPC UA server.
  3. **Optional (recommended)** : OPC Test Tool certificate imported into OPC UA server.
  4. **Optional** : Historian Service certificate imported into the OPC UA server.
  5. **Optional (TrakSYS 12+ only)** : Data Management Service certificate imported into the OPC UA server.
  6. **Optional (TrakSYS 12+ only)** : Workflow Service certificate imported into the OPC UA server.



#### Exporting the OPC UA Server certificate (Kepware)

The steps for exporting the certificate will vary depending on the OPC UA server. For the purpose of this article, Kepware is used as an example.

  1. Open the OPC UA Configuration Manager.
  2. In the Server section of the Instance Certificates tab, click on Export Server Certificate:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18691376399507)  
  

  3. Save the Certificate and copy the file to the TrakSYS server.



#### Exporting the TrakSYS Certificates Using the TrakSYS Web (TrakSYS 13+ Only)

Starting with TrakSYS 13.0.0, this method only applies to the Logic Service. The certificates for the other services (Historian, Workflow, and Data Management) must use the previous method explained in the next section. This method also assumes that a [Logic Service Instance](https://portal.parsec-corp.com/hc/en-us/articles/360017372174-Configuring-a-Logic-Service-Instance) has been configured.

  1. Access the TrakSYS Web and navigate to **Configuration | Services | Logic Services**.
  2. Select the configured Logic Service Instance on the first slice. Then, click the Edit link at the top of the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40814191222803)  
  

  3. On the resulting page, navigate to the Certificate tab. Check the Generate Certificate checkbox and specify a value for the Certificate Lifetime (Months) field. The value for this field must be a valid integer number between 1 and 120. The default value is 36 months (3 years).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40814191224211)  
  

  4. Click Apply to save the changes.
  5. Start the Logic Service. This process will generate the certificate file.
  6. Refresh the Logic Service Instance configuration page to verify that a certificate was created. If the process is successful, values should now appear in the Certificate Expiration Date and Certificate Last Modified fields.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40814194055443)  
  

  7. Click the Save button to confirm the changes.
  8. On the Logic Services page, click the Download Certificate link on the second slice.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40814194057491)  
  

  9. On the resulting page, ensure that the Certificate Type has the .der extension selected. Then, click Download.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40814194059155)  
  

  10. Save the certificate to an easily accessible location (such as the Desktop).
  11. Copy the certificate to the OPC Server.



#### Exporting the TrakSYS Certificates

  1. Open Installation Manager.
  2. Generate the Certificates for the Logic Service, Historian Service, Data Management Service, Workflow Service, and OPC Test Utility as needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18692128703763)  
  

  3. **TrakSYS 12+ only** : When generating certificates, an option will be provided to specify the lifetime of the certificate in months. The number of months must be a value between 1 and 120. The default value for each certificate is 36 months.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18692248086803)  
  

  4. The Certificates will be saved to the TrakSYS installation folder. For TrakSYS 11.2.4 and older, this will typically be under **...Program Files (x86)\Parsec\TrakSYS**. For TrakSYS 12, this will typically be under **...Program Files\Parsec\TrakSYS**.
  5. Copy all Certificates to the OPC UA Server.



#### Importing the OPC UA Server certificate into the TrakSYS server

  1. Open the TrakSYS Installation Manager on the TrakSYS server.
  2. Navigate to the Certificates tab.
  3. Select a certificate entry that has been generated and click Details.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18692517594003)  
  

  4. On the resulting dialog, information will be displayed about the selected service certificate. Any certificates that have been previously imported will appear within the list (as shown below). To import a new certificate, click the Import button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18692652763155)  
  

  5. If the import is successful, a new entry for the certificate will appear in the list.



In addition, you can verify the KEPServer certificate is present by checking the Trusted UA Applications folder in Windows Certificate Manager.

![](https://portal.parsec-corp.com/hc/article_attachments/360034088053)

#### Importing the TrakSYS certificates into the OPC UA server

Again, the steps will for importing the certificates will vary depending on the OPC UA server. For the purpose of this article, Kepware is used as an example.

  1. Open the OPC UA Configuration Manager.
  2. In the Trusted Clients tab, click on Import:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18693620993939)  
  

  3. Select the Logic Service Certificate file that was saved above.
  4. Repeat step 2 and 3 for the OPC Test Tool, Historian service, Data Management Service, and Workflow Service.
  5. After importing, the certificates should all appear in the list of trusted clients:
  6. Re-initialize the KEPServer Runtime (KEPServerEX Configuration, in the Runtime menu).



Once re-initialization of the KEPServer is complete, the Logic Service, Historian Service, Data Management Service, Workflow Service, and the OPC Test Tool will be able to connect to the OPC UA server.

At this point, any configured OPC UA Access Names in TrakSYS should connect successfully. Note that when creating and assigning OPC UA tags, the item name in the tag's configuration must match what appears in the OPC Test Tool. 

### Creating a Certificate-less OPC UA Connection (TrakSYS 11.0.2+)

This connection type does not require a certificate exchange and is considered an unsecure connection:

  1. Security is turned off and unsecured connections are allowed by the OPC UA server.
  2. Access Names and OPC Test Utility is configured to use the lowest security settings.



**Note:** When using a Certificate-less OPC UA Connection, the certificates for each of the services will still have to be generated using the TrakSYS Installation Manager. However, they do not need to be exchanged with the OPC Server to make a connection. This process generates the configuration files required to use the OPC UA functionality. After the certificates are created, the configuration files are stored within the root TrakSYS installation folder.

#### Configuring the OPC UA Server to Allow Insecure Connections

The steps for modifying security will be different depending on the OPC UA server. For the purpose of this article, Kepware is used as an example.

  1. Open the OPC UA Configuration Manager.
  2. In the Server Endpoints tab, select the existing endpoint URL and click Edit...  
  
![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/360104515933)  
  

  3. Make sure the None (Insecure) option is checked. **Note** : it is possible to enable the other security policies while None (Insecure) is selected. However, this is not necessary since unsecure connections are being allowed.  
  
![mceclip2.png](https://portal.parsec-corp.com/hc/article_attachments/360102345254)  
  

  4. Click OK to save the changes.
  5. Re-initialize the KEPServer Runtime (KEPServerEX Configuration, in the Runtime menu).



Similar to the secured connection, the Logic Service, Historian Service, Data Management Service, Workflow Service, and the OPC Test Tool will be able to connect to the OPC UA server after the re-initialization is complete.

#### Making a Certificate-less Connection to an OPC UA Server

The steps below explain how to make a certificate-less connection using the OPC Test Utility. The same settings can also be used for OPC UA Access Names.

  1. Navigate to the TrakSYS Installation folder and open the OPC Test Utility.
  2. Select an OPC UA connection. Then enter the endpoint URL and choose the security settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/18694247457555)  
  

  3. Click the Connect button to establish the connection.
  4. If the connection is a success, a message should display on the results pane.  
  
![mceclip4.png](https://portal.parsec-corp.com/hc/article_attachments/360102347774)



### Preferred Security Settings and Authentication Options

The Preferred Security Settings allow users to specify the Highest or Lowest security settings when connecting to an OPC UA server. Note that these settings will use the most or least secure options allowed by the OPC UA server. These options are available on the OPC Test Utility and on OPC UA Access Names.

Additionally, the available authentication options allow a user to choose whether to make an Anonymous connection or use a configured account. Anonymous connections must be allowed on the OPC Server in order for the connection to succeed. When using the Username/Password option, the user must be configured within the OPC Server and needs to have sufficient permissions to allow TrakSYS to connect.

For the most secure setup, using the Highest Preferred Security setting with Username/Password Authentication is recommended.  
  


![mceclip0.png](https://portal.parsec-corp.com/hc/article_attachments/360102385094)  
  


For installations that do not use certificates, the Lowest setting with Anonymous Authentication is recommended.  
  


![mceclip1.png](https://portal.parsec-corp.com/hc/article_attachments/1500003552701)  
  


### Troubleshooting

In the event there are connectivity issues, additional logging can be enabled on the OPC Test Tool's UA connection attempts as follows:

  1. Navigate to the TrakSYS installation folder.
  2. Locate the OpcTest.Ua.Config.xml file and open it.
  3. Scroll down to the Trace Configuration section and specify a file name for the `OutputFilePath` tag (it will be empty by default). In this example, we have used "UAConnectionLog.txt".  
  
![](https://portal.parsec-corp.com/hc/article_attachments/360034095933)  
  

  4. Save and close the xml file.
  5. Open the OPC Test tool (use Run as Administrator). If the tool was already open, close and reopen.



Now whenever a connection is attempted to a UA endpoint, available details will be logged in this file. Note that the file is overwritten each time a new connection is attempted. If issues still persist, the [OPC Connection Troubleshooting Guide](https://portal.parsec-corp.com/hc/en-us/articles/9981933021843-OPC-Connection-Troubleshooting-Guide) can be used for additional troubleshooting advice and ideas.
