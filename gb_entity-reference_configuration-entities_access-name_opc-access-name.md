# OPC Access Name

## Summary

### Entity Name

OPC Access Name

### Database Table Name

`tAccessName` + `tAccessNameOpc`

### API Object Name

`DbAccessNameOpcComposite`

### Entity Description

An OPC Access Name defines a connection to an OPC server running on a specified Node. Any OPC Tags that are related to an OPC Access Name will use its connection to receive value updates.

## Properties

`Access Name [ AccessNameID ]`

Specifies the related `tAccessName.ID` value for this Access Name.

`Node [ Node ]`

Name of the computer hosting the OPC server.

`OPC Server [ OpcServer ]`

Specifies the the ProgID of the target OPC server (refer to your OPC server's documentation for more information). The browse button fills the list with the OPC server ProgIDs that are available on the server specified by the Node property above.

`Access Path [ AccessPath ]`

A string prefix the Logic Service will append to the front of every OPC item name. For example, if a complete OPC Item Name is \[ML1500]N10:1, you can set this value to \[ML1500] and then simply specify N10:1 as the OPC Tag's Item Name.

`Use Alternate [ UseAlternate ]`

When checked, enables the use of an alternate fall-back OPC server to use when communication with the primary OPC server fails. Ideally, such a backup OPC server should reside on a different computer than the primary OPC server.

`Alternate Node [ AlternateNode ]`

Name of the computer hosting the alternate OPC server.

`Alternate OPC Server [ AlternateOpcServer ]`

ProgID of the alternate OPC server (refer to your OPC server's documentation for more information).

`Alternate Access Path [ AlternateAccessPath ]`

String prefix for OPC item names when using the alternate OPC server.

`Refresh Milliseconds [ RefreshMs ]`

This is the number of milliseconds that the OPC server will poll the physical device for new value changes. Note that this setting is passed to the OPC server as a suggestion, it is not mandatory that an OPC server abide by this request.

`Re-Connect While True [ ReConnectTagID ]`

Used to manually trigger the OPC connection to be re-attempted, this setting specifies a Boolean condition by pointing at a discrete Tag. When True, the OPC connection will be closed and reopened.

`Re-Connect Wait Seconds [ ReConnectWaitSeconds ]`

Once a manual reconnect is triggered (see above), the Logic Service will wait this number of seconds before checking the trigger condition again.

`ReConnect Inactivity Seconds [ ReConnectInactivitySeconds ]`

When this setting is non-zero, the Logic Service will monitor all Tags configured for this Access Name. If the specified number of seconds elapses with none of the Tags changing value, the Access Name connection will be assumed to be bad and a reconnection will be initiated.

`Read on Connect [ ReadOnConnect ]`

When the Sync option is selected, the Logic Service forces a read from all the Tags under the Access Name when the connection is first made during Logic Service Startup. This option is typically used only in scenarios where the OPC server is not behaving as it should (i.e. a successful connection to the OPC Server is made but the Tags subscription does not return the current values).

{% hint style="warning" %}
Depending on the number of configured OPC Tags this setting can cause significant delays in Logic Service Startup times.
{% endhint %}

When the Sync On Reconnect option is selected, the Logic Service forces a read from all the Tags under the Access Name whenever a reconnection to the Access Name takes place. A forced read will not occur on Logic Service Startup and should not negatively affect Logic Service scan times.

{% hint style="warning" %}
OPC Servers that comply with the OPC Specification typically return current Tag values on connection even if the options above are not enabled. It is general best practice to have Read On Connect set to No.
{% endhint %}

`Read on Connect Type [ ReadOnConnectType ]`

When the Read on Connect option is selected, this property determines the type of synchronous read that occurs. The `Cache Read` option reads values from the OPC server's memory (the last known value that has been read from the device). The `Device Read` option forces the OPC server to query the physical device for the current value (this option can be slower).

`Expose Values Since Last Scan [ ExposeValuesSinceLastScan ]`

Determines whether the Logic Service will attempt to retrieve the last known value for a specific OPC DA Tag. This typically happens after a disconnection from the OPC Server occurs or if the Logic Service is restarted.
