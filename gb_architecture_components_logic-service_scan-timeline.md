# Scan Timeline

The Logic Service operates by regularly executing processing scans (typically once per second, but based on the exact configuration settings). The following diagram and descriptions illustrate the significant processing events in the life cycle of a single Logic Service scan.

## Between Scans

### OPC Tag Changes

Between the end of one scan and the start of the next, there is a period of idle time for the Logic Service. During this gap, the OPC data source events are allowed into the application. OPC Tags are subscribed to on Logic Service startup. The OPC servers "notify" the Logic Service whenever any of the subscribed Tags change. These Tag changes are only allowed in to the application between scans. Once a scan starts, the OPC Tag landscape is frozen for the duration of the scan.

OPC Tag changes that occur and are sent to the Logic Service while in mid-scan are not lost. The messaging is simply blocked until the end of the scan, when those Tag change events are processed during the next mid-scan gap.

## Scan

The following sections are listed in order, as they occur during the Logic Service scan.

### Shift Schedule Updates

Each scan, the Logic Service determines if a Shift Schedule has changed and automatically loads the new configuration from the database. This process is optimized and the check only occurs if a currently active Shift is about to end (new Shift Schedule information can only take effect after the current Shift ends).
