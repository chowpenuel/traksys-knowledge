# MQTT Connection Troubleshooting Guide

*Source: https://portal.parsec-corp.com/hc/en-us/articles/38862002645011-MQTT-Connection-Troubleshooting-Guide*
*Last updated: 2026-02-24T01:48:30Z*

---

Applies To | TrakSYS 13+

### Summary

This article contains several troubleshooting techniques for MQTT-related connection issues. The methods are in no particular order but can be used to verify different aspects of the MQTT configuration (such as permissions, network connectivity, configuration changes, and more).

**Note** : Some methods may require changes to TrakSYS configuration or the Broker. In TrakSYS, Logic Service will need to be restarted so that changes can take effect. If changes are made to the Broker, this may also require a Broker restart. If these techniques are being used in production environments, it is highly recommended to wait for a period of planned downtime to avoid potential data loss.

### Troubleshooting Techniques

  * **Restart Logic Service** \- This is a simple way to check if the MQTT connection is reset by a service restart. This might be difficult to do in live production scenarios, so it is only recommended during periods of planned downtime.  

  * **Verify that the Broker is running** \- MQTT messages and value changes cannot be communicated if the Broker is not actively processing them.  

  * **Ensure that correct Broker configuration file is being referenced and used** \- If testing is being performed on a Broker with multiple configuration files to test different security options, ensure that the correct configuration file is loaded. Depending on the Broker used, changing the contents of a single configuration file or switching between multiple configuration files may require a Broker restart.  

  * **Send a test value to a configured Topic through the Broker** \- If there are specific Tags that are showing bad quality (while others are showing good quality), sending a value to the Topic can help verify whether the Tag is actually displaying bad quality. **If the MQTT Tag has not received a value change since the Logic Service started, this is expected behavior**. While the Logic Service is able to verify the connection to the Broker, it cannot verify whether Tag values from individual MQTT Tags are initially valid. Therefore, the Tag will initially start with bad quality. This is built-in, expected behavior and **cannot** be modified. **The MQTT Tag quality will change once a Tag value update is received from the Broker**.  

  * **Check if all tags under a specific Access Name have connection/quality issues** \- If **all** tags under a single Access Name cannot connect or are bad, there are two reconnect settings that can be configured to drop and reset the connection without restarting the Logic Service:  
  
The **Re-Connect Inactivity (Seconds)** setting in the Access Name properties can be used to automatically drop and reset the connection to the Broker without restarting the Logic Service. **Note:** This option will not be triggered if some tags are working while others are not and all of them are under the same Access Name. Changing this setting requires a Logic Service restart.  
  
The **Re-Connect While True Tag** setting provides a manual option to reset the MQTT connection without restarting the Logic Service. A Discrete Tag can be assigned to the property to trigger it. Changing this setting requires a Logic Service restart.  

  * **Create a new MQTT Tag that points to an existing Topic** \- Creating a new tag can test if only the existing configuration is affected or if the new configuration is also affected. Verify that an existing Topic is valid and is actively communicating values. Create a new tag with the same Topic and see if it is also able to display good quality in TrakSYS. This test is especially useful in situations where multiple Access Names are used and only 1 Access Name is experiencing issues. This test requires a Logic Service restart.  

  * **Create a new Access Name and assign a tag with a known good Topic underneath it** \- This test works well in scenarios where only a single Access Name is used. This assists in determining whether the issue is coming from the current Access Name or if all Access Names are affected. This test requires a Logic Service restart.  

  * **Try different Windows Service accounts** \- By default, the Logic Service uses LocalSystem as the Log On account in Services.msc. Modifying the account in Services.msc or running the service in [**Console Mode**](https://portal.parsec-corp.com/hc/en-us/articles/115002857413-Running-Logic-Service-in-Console-Mode) can help determine if the issue is account or permissions related. It is recommended to use an administrative account that has full access to Windows and the Broker software.  
  
**Note** : if the Log On account is modified for the Logic Service, then a Logic Service restart is required to apply the change. Additionally, using a full administrative service account is only recommended for testing purposes. For security reasons, it is not recommended to use this type of account as a long-term solution.  

  * **If a distributed installation is being used, ping the TrakSYS Application and Broker Servers** \- Using the command prompt in Windows, perform a ping test from the TrakSYS application server to the Broker Server. Then perform the same test in the opposite direction (from the Broker Server to the TrakSYS Application Server). This helps ensure that both servers can communicate with each other. This test does not apply to scenarios where the TrakSYS Application and Broker are on the same machine.  

  * **Check the Firewall and Port settings** \- The MQTT functionality requires specific ports to be open in order to function. TrakSYS uses the following ports by default:  
  

    * The default TrakSYS port is `80`.
    * The SQL Server TCP port is `1433`.
    * The default MQTT port is `1883`.
    * Access Names that use TLS authentication may use `8883`.
  * **Disable the Firewall on both the TrakSYS application and Broker servers** \- This is especially useful for verifying whether the firewall or ports are a potential root cause. If MQTT connectivity starts working, then use the test above and check specific ports. This test is not applicable for scenarios where the TrakSYS application and Broker are on the same machine. **Note** : This is only meant to be a temporary test for root cause analysis. For security reasons, it is not recommended to leave the firewall off as a long-term solution.  

  * **Enable Trace for the Logic Service** - See [here](https://portal.parsec-corp.com/hc/en-us/articles/115004185313-Enabling-Logic-Service-Trace) for how to enable Trace. This option logs everything the Logic Service does (even MQTT connections and tag read/writes) on each scan. The results are outputted to the tTrace table. **Note:** This table can fill up very quickly so it's only recommended to leave this on for a short period of time. This change will require a Logic Service restart.  

  * **Check the Broker logs** \- Client IDs are not configurable in TrakSYS and are set within the application core code. However, Clients used by Logic Manager Service have Client IDs with format:  
  
`ETSLMS_ID_{logic_service_id}_{access_name_id}`  
  
Clients used by `Core.Api.Mqtt` have Client IDs with format:  
  
`ETSCOREAPI_ID_{random_guid}`  
  
Therefore, when viewing Broker logs, it is recommended to view entries with the `ETSLMS_ID_` and `ETSCOREAPI_ID_` prefixes for troubleshooting purposes.  

  * **Disable all root areas in the installation** \- This is useful in scenarios where most other factors have been eliminated and a root cause has not been located. Disabling all Root Areas in the installation turns off **all** configuration and can help eliminate a large number of factors. From here, ensure that either the [Load All Tags](https://portal.parsec-corp.com/hc/en-us/articles/115004469754-Enabling-Load-All-Tags) setting is enabled or [at least 1 tag is assigned to the Logic Service Instance](https://portal.parsec-corp.com/hc/en-us/articles/115004469774-Assigning-Tags-to-Systems-and-Logic-Service). If a successful connection is established in this scenario, then enable Areas (and Systems) one-by-one until the connection issues reappear. This helps narrow down the cause to the specific Area, System, Sub-System, etc. While this can be a repetitive process, it is highly effective in narrowing down the root cause. **Note** : Multiple Logic Service restarts will be required for every Area and System that is enabled or disabled.



### MQTT TLS (One-Way and Mutual)

  * **Ensure that the correct permissions are explicitly stated within the Broker** \- Since Username and Password authentication is optional, it may be required to explicitly state whether this feature should be used. For example, to allow anonymous authentication in the Mosquitto broker while using TLS, the **`allow_anonymous true`** property **must** be specified in the configuration file. Otherwise, the Broker will default to use Username and Password authentication along with the TLS protocol.
  * **Ensure all certificates have been correctly generated and signed** \- Using TLS with MQTT requires prior knowledge of properly generating and signing certificates. This process can vary depending on the program used to create and sign the certificates. See [here](https://portal.parsec-corp.com/hc/en-us/articles/39621778810387-Configuring-an-MQTT-Connection-Using-Certificates) for steps to create and sign **untrusted** certificates using OpenSSL. Do not use these certificates for production, they are for **testing purposes only**. If there are issues with the certificates, one possible test could include regenerating and signing the certificates. 
  * **Ensure Broker certificates are generated with correct Metadata** \- An error may be produced if the incorrect metadata such as Common Name (CN) is provided.
  * **Ensure Broker is correctly configured** \- While certain MQTT certificate properties are configured through the TS Web, additional configuration is also required at the Broker level. This typically involves pointing at the certificate files, enabling certificate usage, setting the TLS protocol, and more. Note that not all Brokers are configured the same and may require different steps.
  * **Verify the TLS version used for the connection** \- MQTT functionality in TrakSYS supports TLS 1.2 and 1.3. It is recommended to verify which TLS version that the Broker is using. Some Brokers may allow multiple versions of TLS simultaneously. If the Broker only uses a specific version of TLS, then the MQTT Access Name must also be configured to use that TLS version. Note that any changes to the MQTT Access Name will require a Logic Service restart.


