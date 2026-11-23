# Using Sparkplug B with TrakSYS

*Source: https://portal.parsec-corp.com/hc/en-us/articles/40819145320851-Using-Sparkplug-B-with-TrakSYS*
*Last updated: 2026-02-24T01:48:30Z*

---

### Summary

Sparkplug B is an MQTT-based protocol that adds structure and state management to industrial IoT communications, with support in TrakSYS starting in version 14.0.0. It defines standardized message formats, topic hierarchies, and device lifecycle management for reliable industrial data exchange. In TrakSYS, Sparkplug B is used to receive messages in a structured format that can contain multiple values within a single payload.

The example in this article assumes the following prerequisites:

  * A Broker exists and TrakSYS has been configured to connect to it. Information on configuring an MQTT connection with TrakSYS can be found [**here**](https://portal.parsec-corp.com/hc/en-us/articles/38861856867219-Configuring-an-MQTT-Connection).
  * For simplicity, the Broker is on the same machine as the TrakSYS Application. TrakSYS can also communicate with Brokers on remote machines.
  * [Node-RED](https://nodered.org/docs/getting-started/local) will be used as a separate client to send MQTT messages using Sparkplug B. Other clients can be used as needed. Note that Node-RED also needs [Node.js](https://nodered.org/docs/faq/node-versions) as a requirement to function. The full documentation for Node-RED can be found [**here**](https://nodered.org/docs/).



### General Information

  * Payloads that will be processed by Sparkplug B must comply with the [Sparkplug 3.0.0 Specification](https://sparkplug.eclipse.org/specification/version/3.0/documents/sparkplug-specification-3.0.0.pdf).
  * TrakSYS uses the following libraries for the Sparkplug B functionality:
    * Google.Protobuf (v3.31.1)
    * Grpc.Tools (v2.72.0)
    * MQTTnet (v5.0.1.1416)
  * As of TrakSYS 14.0.0, only the Logic Service uses Sparkplug B. It cannot be used with the other TrakSYS services or within the TrakSYS Web.
  * Currently, MQTT writeback with Sparkplug B is not possible. The Logic Service can only receive payloads using Sparkplug B.



### Message Types and Logic Service Integration

When sending messages that will interact with Sparkplug B, there are standardized MQTT Message Types that define the purpose of each transmission. Each of the types are listed below:

  * `NBIRTH/DBIRTH` \- Represents the birth certificates for nodes/devices.
  * `NDEATH/DDEATH` \- Represents the death certificates for nodes/devices.
  * `NDATA/DDATA` \- Represents the regular data messages with metric values.



As an example, if device data needs to be sent, the payload must follow the Data Message payload structure as defined in the [Sparkplug 3.0.0 Specification](https://sparkplug.eclipse.org/specification/version/3.0/documents/sparkplug-specification-3.0.0.pdf). Additionally, the payload must be published to a topic using the message type `DDATA`. The same concept applies to the other message Types. Each Type has its own requirements that must be fulfilled, and it must be published to the correct Topic.

When the messages are received by the Logic Service using these Types, the service will do the following:

  * `NBIRTH/DBIRTH` \- Attempts to read the metric values.
  * `NDEATH/DDEATH` \- Sets the tag quality to 0.
  * `NDATA/DDATA` \- Attempts to read the metric values.



If an MQTT Tag is assigned to an MQTT Access Name, it has the  _Use Sparkplug_ option checked on the Access Name, and the Tag is configured with a `*DATA` topic, Logic Service will automatically subscribe to its corresponding `*BIRTH` and `*DEATH` topics. If a user is subscribing to `*DATA`, it is common to want to know when a rebirth occurs and if the `*BIRTH` message contains initial values. Inversely, it would be desirable to invalidate the current Tag value if a `*DEATH` message arrives.

For example, an MQTT Tag has the following Topic:  
`spBv1.0/Plant1_Area2_Line3/DDATA/EdgeNode1/Motor_Pump_VFD`

Using this Topic, the Logic Service will also subscribe to the following:

  * `spBv1.0/Plant1_Area2_Line3/DBIRTH/EdgeNode1/Motor_Pump_VFD`
  * `spBv1.0/Plant1_Area2_Line3/DDEATH/EdgeNode1/Motor_Pump_VFD`



If a Tag is specifically subscribed to a `*BIRTH` or `*DEATH` topic, the Logic Service will not auto-subscribe to other Topics. In these cases, those are considered explicit subscriptions to those Topics only.

### Payload Requirements

In general, Sparkplug B uses Google Protocol Buffers (protobuf) to serialize message payloads into a compact binary format. The payload contains structured data such as metrics, timestamps, and metadata defined by the [Sparkplug B Protobuf Schema](https://github.com/eclipse-tahu/tahu/blob/master/sparkplug_b/sparkplug_b_c_sharp.proto). The schema can also be found in Section 6.4.1 of the [Sparkplug 3.0.0 Specification](https://sparkplug.eclipse.org/specification/version/3.0/documents/sparkplug-specification-3.0.0.pdf). When sending payloads, TrakSYS primarily handles the information provided under the Metrics object. If a client attempts to publish a Sparkplug B message that includes something unknown to the schema, it will fail to encode.

When sending a payload to be processed by Sparkplug B, it must adhere to a strict structure as defined in the [Sparkplug 3.0.0 Specification](https://sparkplug.eclipse.org/specification/version/3.0/documents/sparkplug-specification-3.0.0.pdf). It is recommended to reference Section 6.4.6 to see which fields are required under each scenario. One example of this format is shown below:
    
    
    {
      "timestamp": 1651395271000,
      "metrics": [
        {
          "name": "Temperature",
          "alias": 1001,
          "timestamp": 1651395270000,
          "datatype": 3,
          "is_historical": false,
          "is_transient": false,
          "is_null": false,
          "metadata_content_type": "text/plain",
          "metadata_description": "Temperature reading",
          "int_value": 235
        },
        {
          "name": "Pressure",
          "alias": 1002,
          "timestamp": 1651395270000,
          "datatype": 10,
          "is_historical": false,
          "is_transient": false,
          "is_null": false,
          "double_value": 101.325
        },
        {
          "name": "Status",
          "alias": 1003,
          "timestamp": 1651395270000,
          "datatype": 12,
          "is_historical": false,
          "is_transient": false,
          "is_null": false,
          "string_value": "Online"
        },
        {
          "name": "IsActive",
          "alias": 1004,
          "timestamp": 1651395270000,
          "datatype": 11,
          "is_historical": false,
          "is_transient": false,
          "is_null": false,
          "boolean_value": true
        }
      ],
      "seq": 1,
      "uuid": "d8de70b5-42dc-4919-a97e-ce0c7c199157"
    }
    

As shown above, the object has a root element called "metrics" that can contain multiple values. The fields included in the payload are explained below:

  * `alias` \- This value is used as a unique identifier.
  * `name` \- This field serves the same purpose as the `alias` field but allows a human readable value to be specified. This field is required for `*BIRTH` messages but is prohibited in `*DATA` messages.
  * `datatype` \- This is an Enum value representing different types. These types are specified in Section 6.4.16 of the [Sparkplug 3.0.0 Specification](https://sparkplug.eclipse.org/specification/version/3.0/documents/sparkplug-specification-3.0.0.pdf). For example, a value of 3 is the Enum value for int32.
  * Typed `value` (e.g., `int_value` or `boolean_value`) - This specifies the data type of the value. Only one type can be set at a time. If none of the values are set, the `is_null` field is expected to be true.
  * `timestamp` \- This is a timestamp set with epoch time.



When working with typed values, Sparkplug B expects specific datatypes to be assigned to a specific Protobuf value. For example, if the metric has an integer value (e.g., 1 for int8 or 3 for int32), then its value should be provided under the `int_value` field. Additional examples are provided below:

  * UInt64 - `long_value`
  * String - `string_value`
  * File - `bytes_value`



For a complete list of available data types, refer to Section 6.4.17 of the [Sparkplug 3.0.0 Specification](https://sparkplug.eclipse.org/specification/version/3.0/documents/sparkplug-specification-3.0.0.pdf) and the "Google Protocol Buffer Type" for each datatype.

Since the values will be saved into MQTT Tags, not all datatypes are supported. The Logic Service will recognize the following typed value fields:

  * `int_value`
  * `long_value` \- Note that this type is only compatible with MQTT Tags that have a string Data Type.
  * `float_value`
  * `double_value`
  * `boolean_value`
  * `string_value`



These values will be casted to the corresponding MQTT Tag datatype. Therefore, the following Sparkplug B datatypes are supported:

  * Int8
  * Int16
  * Int32
  * Int64
  * UInt8
  * UInt16
  * UInt32
  * UInt64
  * Float
  * Double
  * Boolean
  * String
  * Text
  * Uuid
  * DateTime



Other types not included in this list are not supported as the values cannot be provided for an MQTT Tag in TrakSYS.

### Configuring Sparkplug B in TrakSYS

The following instructions assume that TrakSYS can [establish a successful connection](https://portal.parsec-corp.com/hc/en-us/articles/38861856867219-Configuring-an-MQTT-Connection) to the Broker and at least one MQTT Access Name has been configured. While Sparkplug B can be used with any of the supported security types, Anonymous Authentication will be used in this example.

  1. Access the TrakSYS Web and navigate to **Configuration | Tags | Access Names**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42473697109011)  

  2. On the first slice, select the desired Access Name Group. On the second slice, select the configured MQTT Access Name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42473691864211)  

  3. On the third slice, click the Edit button.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42473697110931)  

  4. Within the Access Name configuration, check the "Use Sparkplug" option at the bottom of the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42473691866259)  

  5. Click Save to apply the changes.
  6. Next, the MQTT Tags will need to be created. If the MQTT Tags have been created, skip to Step 9. Otherwise, to do this, navigate to **Configuration | Tags**.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42494495731091)  

  7. Select the desired Tag Group on the first slice. On the second slice, click the New link to create a new Tag.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42494522077331)  

  8. On the resulting page, select the MQTT Tag option.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42494495732499)  

  9. The MQTT Tag should contain the [proper security settings and Tag configuration](https://portal.parsec-corp.com/hc/en-us/articles/38861856867219-Configuring-an-MQTT-Connection) to communicate with the Broker. For the purpose of this example, the settings outlined in the article have been applied to the MQTT Tag. Within the General tab, a Sparkplug Metric can be specified. This should be the Alias of the Metric value contained within the data payload. For the example below, a value of "Temperature" has been specified.  
  
**Note:** This field will only appear in the MQTT Tag properties if the selected Access Name has the "Use Sparkplug" option checked.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42494495732755)  

  10. Click Save to apply the changes.
  11. Repeat Steps 7 through 10 to add additional MQTT Tags as needed. Each Tag should contain its own Sparkplug Metric to retrieve the values from the payload. For the purpose of this example, three different MQTT Tags with different Sparkplug Metrics have been created.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42494522081939)



### Verifying Configuration and MQTT Tag Value Changes Using Sparkplug B

Tag value changes can be verified by viewing the built-in Service pages within the TrakSYS Web. Normally, MQTT Tag value changes will come from Industrial IoT devices, PLC's, Smart Devices, or other device types. However, for demonstration purposes, [Node-RED](https://nodered.org/docs/getting-started/local) will be used to send value changes. For the purpose of this example, the Node-Red client has been installed on the same machine as TrakSYS.

In this example, all three tags shown in Step 11 of the previous section are using the following Topic:

`spBv1.0/TestGroup/DDATA/TestName/TestDevice`

Each Tag contains the alias defined in the SparkPlug Metric field of the Tag configuration for each value in the Payload. As an example, the following settings have been defined for the "MQTT Pressure Tag":

![](https://portal.parsec-corp.com/hc/article_attachments/42664927189011)

The following payload is being used to send the values to the Tags using Sparkplug B. Note that the format for the payload is slightly different than the format shown in the Payload Requirements section of this article. This is because Node-Red has slightly different requirements that deviate from the original required format.
    
    
    {
        "timestamp": 1651395271000,
        "metrics": [
            {
                "name": "Temperature",
                "alias": 1001,
                "timestamp": 1651395270000,
                "datatype": 3,
                "is_historical": false,
                "is_transient": false,
                "is_null": false,
                "value": 235,
                "type": "Int32"
            },
            {
                "name": "Pressure",
                "alias": 1002,
                "timestamp": 1651395270000,
                "datatype": 10,
                "is_historical": false,
                "is_transient": false,
                "is_null": false,
                "value": 101.325,
                "type": "Double"
            },
            {
                "name": "Status",
                "alias": 1003,
                "timestamp": 1651395270000,
                "datatype": 12,
                "is_historical": false,
                "is_transient": false,
                "is_null": false,
                "value": "Online",
                "type": "String"
            },
            {
                "name": "IsActive",
                "alias": 1004,
                "timestamp": 1651395270000,
                "datatype": 11,
                "is_historical": false,
                "is_transient": false,
                "is_null": false,
                "value": true,
                "type": "Boolean"
            }
        ],
        "seq": 1,
        "uuid": "d8de70b5-42dc-4919-a97e-ce0c7c199157"
    }
    

The following steps show how to validate values sent to Tags using the Sparkplug B functionality:

  1. Start (or restart) the Logic Service. This can be accomplished with the service controls within the Services tab of the TrakSYS Installation Manager or through the [Web-based Service Control](https://portal.parsec-corp.com/hc/en-us/articles/360051708094-Enabling-Service-Management-from-the-Web).
  2. Access the TrakSYS Web and navigate to **Administration | Services | Logic**.  
**Note** : The name of the Logic page will differ depending on the [Logic Service Instance](https://portal.parsec-corp.com/hc/en-us/articles/360017372174-Configuring-a-Logic-Service-Instance) name.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42664927192979)  

  3. If the connection to the Broker is successful, there should be an entry within the Access Name Status section that should show a Connected State.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42664927194003)  

  4. To check the status of the individual MQTT Tags, click the Tags link on the first slice of the page.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42664966237459)  

  5. On the resulting page, enter a partial or full name for a specific Tag. Then, click the Refresh button. This will show a full list of tags that match the partial or full results.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42664966242451)  
  
As shown above, the MQTT Tag displays bad quality even though the MQTT Access Name shows a good connection. **If the MQTT Tag has not received a value change since Logic Service started, this is expected behavior**. While Logic Service is able to verify the connection to the Broker, it cannot verify whether Tag values from individual MQTT Tags are initially valid. Therefore, the Tag will initially start with bad quality. This is built-in, expected behavior and **cannot** be modified. **The MQTT Tag quality will change once a Tag value update is received from the Broker**.  

  6. Using [Node-RED](https://nodered.org/docs/getting-started/local), the full payload containing multiple values will be pushed to the "`spBv1.0/TestGroup/DDATA/TestName/TestDevice`" Topic. As shown in the original payload, the Pressure value is 101.325, the Status value is "Online," and the Temperature value is 235.
  7. After publishing the payload, the built-in Tags page now verifies that all three Tags received the individual values. Furthermore, the MQTT Tag quality for all three tags has been changed to good (192) now that the Topic has been verified.  
  
![](https://portal.parsec-corp.com/hc/article_attachments/42664927200659)


