# OPC HDA Access Name

## Summary

### Entity Name

OPC HDA Access Name

### Database Table Name

`tAccessName` + `tAccessNameOpcHda`

### API Object Name

`DbAccessNameOpcHdaComposite`

### Entity Description

An OPC HDA Access Name defines a connection to an OPC HDA server running on a specified Node. Any OPC HDA Tags that are related to an OPC HDA Access Name will use its connection to receive value updates.

## Properties

`Access Name [ AccessNameID ]`

Specifies the related `tAccessName.ID` value for this Access Name.

`Node`

Name of the computer hosting the OPC HDA server.

`OPC Server [ OpcServer ]`

Specifies the the ProgID of the target OPC HDA server (refer to your OPC server's documentation for more information). The browse button fills the list with the OPC server ProgIDs that are available on the server specified by the Node property above.

`Access Path [ AccessPath ]`

A string prefix the Logic Service will append to the front of every OPC HDA item name. For example, if a complete OPC HDA Item Name is \[ML1500]N10:1, you can set this value to \[ML1500] and then simply specify N10:1 as the OPC Tag's Item Name.

`Poll Interval Seconds [ IntervalSeconds ]`

The delay Logic Service will wait before polling the data source. This interval determines how frequently the Logic Service updates Tag values for this Access Name.

`Re-Connect While True [ ReConnectTagID ]`

Used to manually trigger the OPC HDA connection to be re-attempted, this setting specifies a Boolean condition by pointing at a discrete Tag. When True, the OPC HDA connection will be closed and reopened.

`Re-Connect Wait Seconds [ ReConnectWaitSeconds ]`

Once a manual reconnect is triggered (see above), the Logic Service engine will wait this number of seconds before checking the trigger condition again.
