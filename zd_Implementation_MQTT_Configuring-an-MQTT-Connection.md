# Configuring an MQTT Connection

*Source: https://portal.parsec-corp.com/hc/en-us/articles/38861856867219-Configuring-an-MQTT-Connection*
*Last updated: 2026-02-24T01:48:30Z*

---

Applies To | TrakSYS 13+

### Summary

Beginning with TrakSYS 13.0.0 it is possible to use the MQTT (Message Queuing Telemetry Transport) protocol to communicate with other devices. This protocol is designed for use with low-bandwidth, high-latency, or unreliable networks and operates on a publish-subscribe model where a central broker manages message transmission between clients. In TrakSYS, this communication is possible with anonymous, username and password, and certificate (TLS) authentication types.

While different brokers, clients, and configurations can be used with MQTT, the example in this article assumes the following prerequisites:

  * [Eclipse Mosquitto](https://mosquitto.org/) is used as the Broker. Other Brokers (such as [HiveMQ](https://www.hivemq.com/)) can also be used. Mosquitto documentation can be found [here](https://mosquitto.org/documentation/).
  * For simplicity, the Broker is on the same machine as the TrakSYS Application. TrakSYS can also communicate with Brokers on remote machines.
  * [MQTT Explorer](https://mqtt-explorer.com/) is used as a secondary client. Other clients (such as [MQTTX](https://mqttx.app/)) can also be used. This will be used to verify MQTT configuration and change values for MQTT Tags.



### General Information

This section provides additional information about the MQTT functionality included with TrakSYS.

  * TrakSYS uses MQTT v3.1.1, which is also backwards compatible with v5.0.0 brokers.
  * TrakSYS uses the MQTTnet libraries for MQTT functionality.
    * The `Core.Api.Mqtt` namespace for the TrakSYS Web uses MQTTnet version 4.3.7.
    * The `Core.Api.Mqtt` namespace for the core TrakSYS application uses MQTTnet version 5.0.1.
  * When using secure connections involving TLS, TrakSYS supports TLS 1.2 and 1.3. Previous versions of TLS are not supported due to security risks.
  * Additional logging for troubleshooting purposes can be activated by enabling [Logic Service Trace](https://portal.parsec-corp.com/hc/en-us/articles/115004185313-Enabling-Logic-Service-Trace). Logged messages from trace also include information directly from the MQTTnet libraries.
  * In TrakSYS 13.0.0, MQTT is officially supported for Logic Service and the Web. TrakSYS 14 added MQTT support for the Data Management Service and Historian Services.
  * Fast Tags, State Tags, Script Tags, and Script Class Tags also support MQTT operations.
  * When Logic Service attempts to connect to a broker, it will wait a maximum of 100 seconds, which is the default .NET socket timeout. Afterwards, it will fail the connection and a timeout error will be logged. This value is not configurable, not stored within any TrakSYS table, and is not accessible in any way.
  * Subscribing to Topics is only possible through configuring MQTT Tags within Logic Service. It is not possible to programmatically subscribe to Topics.
  * Publishing messages to a Topic is only possible through custom code. Specifically, in the `Core.Api.Mqtt` namespace with the `BulkTagOperationsMqtt` and `BulkTagOperationsConnectedMqtt` methods. These methods do not require a configured MQTT Tag. This functionality is also available within the context object using the `MqttWriteBack()` method. This method requires a configured MQTT Tag. Scripting examples for MQTT Writeback can be found [here](https://portal.parsec-corp.com/hc/en-us/articles/38861967611795-Examples-for-Native-Read-Write-for-MQTT).
  * MQTT does not support Read On Connect like OPC DA and OPC UA. When a connection is established to the Broker, and the MQTT Tag has the Use Retention option checked, it will load the previously known value. Otherwise, new MQTT Tags and MQTT Tags that do not have the Use Retention option checked will display bad quality until the first MQTT Tag value change is detected. 



### Installing and Configuring a Broker

While other Brokers can be used, this example uses [Eclipse Mosquitto](https://mosquitto.org/) to facilitate MQTT communication. The steps shown below are specific to this Broker and may differ depending on the Broker that's being used. **Note** : If an installation already has Mosquitto (or a different Broker) installed, these steps can be skipped.

[Download and install](https://mosquitto.org/download/) Eclipse Mosquitto. It can be installed on the same machine as the TrakSYS application, or on a remote server. For simplicity, Mosquitto is installed on the same machine for this example.

#### Running Mosquitto

Upon installing Mosquitto, the service should automatically start and run. However, there are additional ways to start the service which allows a verbose log output. This can assist with troubleshooting efforts if there are any issues. The following command can enable verbose logging when executed in Command Prompt (CMD):
    
    
    mosquitto.exe -v -c mosquitto.conf
    

![](https://portal.parsec-corp.com/hc/article_attachments/39515960306067)

**Note** : it is recommended to start Command Prompt as an administrator before executing this command to avoid any permissions-related issues.

A shortcut can also be created to easily execute this process. The following instructions explain how this can be accomplished:

  1. In an easily accessible location (such as the desktop), create a brand-new text file. For the purpose of this example, the text file was named run_mosquitto.txt.
  2. Open the text file and insert the following code. **Note** : ensure that the file path in the script matches the installation location:  
  

         
         @echo off
         cd /d "C:\Program Files\mosquitto"
         mosquitto.exe -v -c mosquitto.conf
         IF %ERRORLEVEL% NEQ 0 (
             echo An error occurred with error code: %ERRORLEVEL%
             taskkill /f /im mosquitto.exe
             net stop mosquitto
             pause
         ) ELSE (
             taskkill /f /im mosquitto.exe
             net stop mosquitto
         )
         

  
![](https://portal.parsec-corp.com/hc/article_attachments/39517490861843)
  3. Save the changes.
  4. Right click to rename the file and change the extension to .bat.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39517452650131)  
  

  5. Click the batch file to run the service with verbose logging. To stop the process, press Ctrl + C.



Alternatively, if running Mosquitto normally without verbose logging is desired, the following commands can be executed in Command Prompt (with elevated privileges):

**Service Start**
    
    
    net start Mosquitto
    

**Service Stop**
    
    
    net stop Mosquitto
    

#### Configuring Security

The following describes how to configure Anonymous access and Username and Password. For more secure installations that use certificates and a secure TLS connection, see [here](https://portal.parsec-corp.com/hc/en-us/articles/39621778810387).

**Anonymous Access**

  1. Access the Mosquitto root folder (typically) under **C:\Program Files\mosquitto**.
  2. Open the Mosquitto configuration file (**mosquitto.conf**) in an editor such as Notepad, VS Code, or Notepad++.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39515971673235)  
  

  3. Add the following lines within the configuration file. For the purpose of this example, these lines were added to the end of the file.  
  

         
         listener 1883
         allow_anonymous true

![](https://portal.parsec-corp.com/hc/article_attachments/39515971674771)  
  
The **listener** property specifies which port will be used to handle MQTT requests. While 1883 is the default port, a different port number can be used if needed. The **allow_anonymous** property determines whether anonymous requests will be accepted by the Broker.  
  
**Note** : When saving the changes, the file may need to be saved in a different location due to permissions restrictions. After saving the file, it can manually be moved to the root folder (**C:\Program Files\mosquitto**). Also, ensure that the file is saved with a **.conf** extension.
  4. Start or restart the Mosquitto service to apply the changes.



**Username and Password**

  1. Access the Mosquitto root folder (typically) under **C:\Program Files\mosquitto**.
  2. A password file will need to be created to configure Username and Password authentication. To do this, open Command Prompt (with elevated permissions) and execute the following command. The <new_filepath> and <new_username> parameters should be replaced with the actual file path and account username, respectively.  
  

         
         mosquitto_passwd.exe -c <new_filepath> <new_username>

     * When entering the command, it is recommended to store the resulting file at the root of the drive (e.g., `C:\`).
     * Do not encapsulate the file path in single or double quotes.
  
![](https://portal.parsec-corp.com/hc/article_attachments/39543881076243)  
  

  3. Executing this command will display an option to enter a password and to reconfirm the entry. When specifying a password, the entered values will not appear in the Command Prompt for security reasons.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39543881078675)  
  

  4. If the execution is successful, no additional messages should be displayed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39543881079059)  
  

  5. Next, access the root Mosquitto installation folder (**...\Program Files\mosquitto**) and remove the pwfile.example file.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39544204499603)  
  

  6. Open the Mosquitto configuration file (**mosquitto.conf**) in an editor such as Notepad, VS Code, or Notepad++.
  7. Add the following lines within the configuration file. For the purpose of this example, these lines were added to the end of the file. Replace the <path to the configuration file> parameter with the actual path to the generated password file.  
  

         
         password_file <path to the configuration file>
         allow_anonymous false
         

  
![](https://portal.parsec-corp.com/hc/article_attachments/39552256731283)  
  
The **password_file** setting determines which password file should be referenced when handling authentication for MQTT requests. The **allow_anonymous** property determines whether anonymous requests will be accepted by the Broker. Since username and password is being enabled, this should be set to "false" as shown above.
  8. Start or restart the Mosquitto service to apply the changes.



After setting the user credentials and creating the password file, it is possible to change the password with the following command. The <username> and <new_password> parameters should be replaced with the actual username and password values, respectively.
    
    
    mosquitto_passwd -b password_file <username> <new_password>
    

  
![](https://portal.parsec-corp.com/hc/article_attachments/39544605439891)

### Configuring TrakSYS for Use with MQTT

Once the Broker has been configured and installed, TrakSYS must be configured to communicate with the Broker. This will involve the creation of an MQTT Access Name and MQTT Tags. Multiple Access Names can be configured for the same Broker and an Access Name can be configured for each Broker if TrakSYS is meant to communicate with multiple Brokers simultaneously. This section provides the necessary steps to configure these entities.

  1. Access the TrakSYS Web and navigate to **Configuration | Tags | Access Names**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574188899347)  
  

  2. On the first slice, select the desired Access Name Group. If no Access Name Group exists, create one and then select it.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574218451347)  
  

  3. On the second slice, click the New link to create a new Access Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574188903187)  
  

  4. On the resulting page, select the "MQTT Access Name" option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574188903955)  
  

  5. Within the Access Name options, provide a Name and Broker Server. Optionally, a Key can also be provided for unique identification purposes. The Broker Server field should contain the computer name of the machine that hosts the Broker. If it is on the same machine as the TrakSYS application, a value of "localhost" can be used instead. Additionally, ensure that Port matches the port used for MQTT communication. Port 1883 is the default industry standard for insecure MQTT communication, however, a different Port can be used if needed.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40569434215187)  
  
Optionally, an Access Path can be specified for exceptionally long Topic names:  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40478593229459)  
  
Similar to OPC DA and OPC UA, MQTT Topics can be prefixed using Access Paths in Tag Groups and/or MQTT Access Names. While it can be used for longer Topic Names, it can also be used for organizational purposes where multiple Topics share the same naming structure. When this feature is used, the full MQTT Tag Topic is concatenated using the following format:  
  

         
         {access_name_access_path}{tag_group_access_path}{mqtt_tag_topic}

If an Access Name is not set, then it will be treated as an empty string  
  
**Note** : Access Paths are only available for Logic Service. They are not usable in the `BulkTagOperationsConnectedMqtt` or `BulkTagOperationsMqtt` classes when writing custom code.
  6. Finally, define a value for the Authentication Type to configure the security settings. Different options will be available depending on the type of security that is chosen. **Note** : Username and Password is only required if the Username / Password Only feature is selected. For all other security options, it is optional.  
  
If **Anonymous** security is being used, it is not required to enter a Username and Password or select any type of TLS settings.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39584860366611)  
  
If **Username / Password Only** is selected, options will appear to enter a Username and Password. However, no options will appear for TLS security.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39584860367251)  
  
If **One-Way TLS** or **Mutual TLS** is selected, options will appear to specify a Username, Password, TLS version, and Certificate Validation Mode. Full instructions on how to use MQTT in TrakSYS with these security settings can be found [here](https://portal.parsec-corp.com/hc/en-us/articles/39621778810387).  
  
![](https://portal.parsec-corp.com/hc/article_attachments/40452272897299)  
  

  7. Click Save to apply the changes.
  8. Repeat steps 3 through 7 to create additional Access Names as needed.
  9. Next, navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574218474387)  
  

  10. Select the desired Tag Group on the first slice. If a group does not exist, create one and select it.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574188911635)  
  

  11. On the second slice, click the New link to create a new Tag.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574188915987)  
  

  12. On the resulting page, select the MQTT Tag option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574188917395)  
  

  13. Within the MQTT Tag properties, provide a Name and select the desired Data Type.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574218484371)  
  

  14. In the Access Name field, select the MQTT Access Name created in steps 5 and 6. Then, provide a Topic and specify the desired Quality of Service. The Topic must adhere to [vMQTT 3.1.1 specifications](https://docs.oasis-open.org/mqtt/mqtt/v3.1.1/os/mqtt-v3.1.1-os.html), and is normally defined by the source PLC or device. For this example, a value of "tstest" has been provided. The Quality of Service (QoS) setting can be changed to determine whether extra overhead should be added to ensure the message is correctly sent. By default, this setting is set to Exactly Once (2).   
  
![](https://portal.parsec-corp.com/hc/article_attachments/39574218486291)  
  

  15. Click Save to apply the changes and create the MQTT Tag.
  16. Repeat steps 11 through 15 to create additional MQTT Tags as needed.



### Verifying Configuration and MQTT Tag Value Changes

Tag value changes can be verified by viewing the built-in Service pages within the TrakSYS Web. Normally, MQTT Tag value changes will come from Industrial IoT devices, PLC's, Smart Devices, or other device types. However, for demonstration purposes, [MQTT Explorer](https://mqtt-explorer.com/) will be used to send value changes to the "tstest" topic referenced in step 14 of the previous section. For the purpose of this example, the MQTT Explorer client has been installed on the same machine as TrakSYS.

**Note** : If Mosquitto is being used as the Broker, it is recommended to start the service with verbose logging for troubleshooting and verification purposes. The command for this is shown at the beginning of this article under **Installing and Configuring a Broker | Running Mosquito**.

  1. Start (or restart) the Logic Service. This can be accomplished with the service controls within the Services tab of the TrakSYS Installation Manager or through the [Web-based Service Control](https://portal.parsec-corp.com/hc/en-us/articles/360051708094-Enabling-Service-Management-from-the-Web).
  2. Access the TrakSYS Web and navigate to **Administration | Services | Logic**.  
**Note** : The name of the Logic page will differ depending on the [Logic Service Instance](https://portal.parsec-corp.com/hc/en-us/articles/360017372174-Configuring-a-Logic-Service-Instance) name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39583544116499)  

  3. If the connection to the Broker is successful, there should be an entry within the Access Name Status section that should show a Connected State.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39583544120339)  

  4. To check the status of the individual MQTT Tags, click the Tags link on the first slice of the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39583534438547)  

  5. On the resulting page, enter a partial or full name for a specific Tag. Then, click the Refresh button. This will show a full list of tags that match the partial or full results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39583544126739)  
  
As shown above, the MQTT Tag displays bad quality even though the MQTT Access Name shows a good connection. **If the MQTT Tag has not received a value change since Logic Service started, this is expected behavior**. While Logic Service is able to verify the connection to the Broker, it cannot verify whether Tag values from individual MQTT Tags are initially valid. Therefore, the Tag will initially start with bad quality. This is built-in, expected behavior and **cannot** be modified. **The MQTT Tag quality will change once a Tag value update is received from the Broker**.  

  6. Using the [MQTT Explorer](https://mqtt-explorer.com/) client, a value of 20 will be pushed to the "tstest" Topic. This is the same Topic that was assigned to the MQTT Tag in step 14 of the previous section.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39583534444051)  

  7. After publishing the value to the Broker the built-in Tags page now verifies that a value of 20 was received. Furthermore, the MQTT Tag's quality has been changed to good (192) now that the Topic has been verified.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/39583534445971)


