# Why do OPC Tags stop receiving Tag value updates while a good connection is established?

*Source: https://portal.parsec-corp.com/hc/en-us/articles/34175208339603-Why-do-OPC-Tags-stop-receiving-Tag-value-updates-while-a-good-connection-is-established*
*Last updated: 2025-01-07T18:32:45Z*

---

Applies To | All Versions

There may be rare situations where the Access Name(s) and Tags will show a good connection to the OPC Server (and good quality), but no OPC Tag values are being received by the Logic Service. This type of scenario is typically caused by a severed subscription between the OPC Server and the TrakSYS software.

When the Logic Service is first started, it will perform a synchronous connection to the OPC Server and subscribe to all configured Tags that match the configuration within TrakSYS. Once the subscription is created, TrakSYS will wait for the OPC Server to send values. After the first scan, the Logic Service does not actively poll the OPC Server for Tag value updates. The active subscription is the mechanism that keeps this process running as intended.

In some cases, environment-related issues (such as network instability, firewall or group policy changes, power outages, etc.) can sever the link created for this subscription. TrakSYS will periodically attempt to re-establish a connection to the OPC Server if it detects an issue with the connection, however, this does not apply to all cases. If the Access Name still shows good quality, then this reconnection logic is not executed. Instead, performing a Logic Service restart can help provide a full reset in the connection.

Another less intrusive way to accomplish this is to specify a value for the Re-Connect Inactivity (Seconds) field:

![](https://portal.parsec-corp.com/hc/article_attachments/34283686772883)

While an OPC UA Access Name is shown above, this option is also available for OPC DA Access Names. When a value is provided for this field, the Logic Service will monitor all Tags configured for this Access Name. If the specified number of seconds elapses with no Tag value changes, the Access Name connection is assumed to be bad, and a reconnection is automatically initiated. The caveat to this setting is that **all** Tags under the Access Name need to be affected in order for this setting to trigger. It does not address scenarios where only a specific Tag (or a specific number of Tags) within the the same Access Name stop receiving Tag updates.

For instances where only specific Tags under the same Access Name stop receiving updates, another option could be to assign a Discrete Virtual Tag to the Re-Connect While True Tag setting in the Access Name properties.

![](https://portal.parsec-corp.com/hc/article_attachments/34283929987219)

This is a manual setting that is used to reset the connection to the OPC Server. When the Tag returns a value of 1 (or True), the OPC connection will be closed and reopened for the specific Access Name. Once the connection is successfully reset, the Tag value will need to be changed back to 0 (or False). The benefit to both of these options is that they perform a reconnect to the OPC Server without having to restart the Logic Service.

**Note** : It is possible to configure both the Re-Connect Inactivity (Seconds) and Re-Connect While True Tag settings simultaneously on a single Access Name. This would ensure that the connection for each Access Name would automatically reset if no Tag value changes are detected **and** would allow a manual option to reset the connection at any time.

### See Also

  * [OPC Connection Troubleshooting Guide](https://portal.parsec-corp.com/hc/en-us/articles/9981933021843-OPC-Connection-Troubleshooting-Guide)
  * [Using the OPC Test Tool](https://portal.parsec-corp.com/hc/en-us/articles/360040611814-Using-the-OPC-Test-Tool)


