# MQTT Access Name

## Summary

### Entity Name

MQTT Access Name

### Database Table Name

`tAccessName` + `tAccessNameMqtt`

### API Object Name

`DbAccessNameMqttComposite`

### Entity Description

An MQTT Access Name defines a connection to an OPC server running on a specified Node. Any OPC Tags that are related to an OPC Access Name will use its connection to receive value updates.

## Properties

`Broker Server [ BrokerServer ]`

Contains the base domain of the Broker URL used to connect to the Broker (e.g., https://Broker.com).

`Port [ Port ]`

Specifies the Port used to connect to the MQTT Broker. By default, this value is set to 1883.

`Access Path [ AccessPath ]`

A string prefix the Logic Service will append to the front of every Topic name. For example, if a complete Topic Name is \[ML1500]N10:1, you can set this value to \[ML1500] and then simply specify N10:1 as the MQTT Tag's Topic.

`Authentication Type [ AuthenticationType ]`

Specifies the type of authentication that will be used to connect to the MQTT Broker. This field has the following possible values:

* **Anonymous**
* **Username / Password Only**
* **One-Way TLS**
* **Mutual TLS**

`TLS Version [ TlsVersion ]`

Specifies the version of TLS that will be used when connecting to the MQTT Broker. This option will only be available if One-Way TLS or Mutual TLS is selected for the Authentication Type.

`Certificate Validation Mode [ CertificateValidationMode ]`

Specifies the type of validation that will be applied to the provided certificate when connecting to the MQTT Broker. This option will only be available if One-Way TLS or Mutual TLS is selected for the Authentication Type. This field has the following possible values:

* **No Check**
* **Online**
* **Offline**

`Username [ Login ]`

Contains the Username that is used to connect to the MQTT Broker. This option will only be available if Username / Password Only, One-Way TLS, or Mutual TLS is selected for the Authentication Type.

`Password [ PaswordHash ]`

Contains the password hash that is used to connect to the MQTT Broker. This value is created as a one-way hash and cannot be retrieved through a reverse hash. This option will only be available if Username / Password Only, One-Way TLS, or Mutual TLS is selected for the Authentication Type.

`Keep Alive (Seconds) [ KeepAliveSeconds ]`

Specifies the number of seconds that the Logic Service will broadcast a Keep Alive message to ensure that the Topic is still valid from the MQTT Broker.

`Expose Values Since Last Scan [ ExposeValuesSinceLastScan ]`

Determines whether the Logic Service will attempt to retrieve the last known value for a specific MQTT Tag. This typically happens after a disconnection from the MQTT Broker occurs or if the Logic Service is restarted.

`Clean Session [ CleanSession ]`

Determines whether the Logic Service will discard any Topic updates that were in queue while the service was not running.

`Re-Connect While True [ ReConnectTagID ]`

Used to manually reset the connection to the MQTT Broker. This setting specifies a Boolean condition by pointing at a discrete Tag. When True, the MQTT connection will be closed and reopened.

`Re-Connect Wait Seconds [ ReConnectWaitSeconds ]`

Once a manual reconnect is triggered (see above), the Logic Service will wait this number of seconds before checking the trigger condition again.

`ReConnect Inactivity Seconds [ ReConnectInactivitySeconds ]`

When this setting is non-zero, the Logic Service will monitor all Tags configured for this Access Name. If the specified number of seconds elapses with none of the Tags changing value, the Access Name connection will be assumed to be bad and a reconnection will be initiated.

`Use Sparkplug [ UseSparkplug ]`

Specifies whether the MQTT Access Name will expect payloads to use Sparkplug formatting.
