# Test Run Result

## Summary

### Entity Name

Test Run Result

### Database Table Name

`tTestRunResult`

### API Object Name

`DbTestRunResult`

### Entity Description

Test Runs Result provides a structure for storing individual test result data related to automated testing with NUnit. This table is for extensibility purposes as there is nothing built into TrakSYS that automatically interfaces with NUnit.

## Properties

`TestRunID`

Specifies the parent Test Run associated with the current Test Run Result record.

`Result`

Specifies the over result of the test (e.g., Inconclusive, Skipped, Passed, Warning, or Failed).

`Name`

Contains the test method name at the time of execution.

`Description`

Contains the description set by the individual Attributes. It is strongly recommended to specify Attributes to generate description values.

`TestType`

Contains a enumeration value provided by the NUnit platform.

`ParentTestRunResultID`

Specifies the parent Test Run Result ID for the current result. This is typically populated when nested tests are configured.

`Messages`

Contains a full output of messages and other serialized output from the NUnit test.

`PassCount`

Specifies the number of tests that have passed the Test, Group, or Suite.

`FailCount`

Specifies the number of tests that have failed the Test, Group, or Suite.

`SkipCount`

Specifies the number of tests that have been skipped for the Test, Group, or Suite.

`WarningCount`

Specifies the number of warnings generated from the Test, Group, or Suite.

`InconclusiveCount`

Specifies the number of tests that have inconclusive results for the Test, Group, or Suite.

`RunDurationSeconds`

Specifies the time (in seconds) that it took for the current test to run.
