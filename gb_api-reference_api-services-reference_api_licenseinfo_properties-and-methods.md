# Properties and Variables

## Properties

`bool AllowAdvancedScripting`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Advanced Scripting feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowAudit`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Audit feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowBatch`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Function Definition feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowChangeoverMatrix`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Changeover Matrix feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowConnect`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Connect feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowContainers`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Containers feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowEvent`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Event Definition feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowHighAvailability`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS High Availability feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowHistorian`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Historian feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowItemManagement`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Item Management feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowJournal`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Journal feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowMaterialManagement`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Material Management feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowModules`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Data Management Service feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowOpcWriteBack`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS OPC Writeback feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowProductionScheduling`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Production Scheduling Systems feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowRootSite`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Multi Site feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowSpc`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Sample Definitions feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowStorage`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Transfer Definitions feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowTagOleDb`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS External Database Connector feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowTaskManagement`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Task Definitions feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowTraceability`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Material and Traceability (MMT) feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`bool AllowWorkflow`

Returns a Boolean value that determines whether the TrakSYS License has the TrakSYS Workflow Service feature line. A value of 1 means the feature is present while a value of 0 means it is not.

`string CompanyName`

Contains the Company Name that is associated with the TrakSYS License. This value is typically displayed in the top left corner of the TrakSYS Web.

`int ConcurrentUsersCount`

Contains the total number of allowed concurrent users for the TrakSYS License.

`int ConfiguredWebHostCount`

Contains the total number of allowed TrakSYS Web Applications for the TrakSYS License.

`int EventDefinitionCount`

Contains the total number of allowed Event Definitions for the TrakSYS License.

`DateTime ExpirationDate`

Contains the Date and Time of when the current TrakSYS License will expire.

`string ExpirationStatus`

Contains the the current Status of the License and will return the Expiration Date of the TrakSYS License.

`int FunctionDefinitionCount`

Contains the total number of allowed Function Definitions for the TrakSYS License.

`DateTime GracePeriodDate`

Contains the Date and Time of the Grace Period given to the TrakSYS License after it has expired. After this Date and Time, all TrakSYS features will cease to function.

`bool HasFeatures`

Returns a Boolean value that determines whether the TrakSYS License has additional feature lines aside from the core functionality. A value of 1 means additional feature lines have been added, while a value of 0 means it does not.

`bool HasSubscription`

Returns a Boolean value that determines whether the TrakSYS License is a Subscription or Perpetual License. A Boolean value of 1 means that it is Subscription, while a value of 0 means it is Perpetual.

`bool HasSubscriptionUpdate`

Returns a Boolean value that determines whether the TrakSYS License is an Online Subscription License. A value of 1 means that it is an Online Subscription License while a value of 0 means it is an Offline Subscription License.

`bool HasValidSubscription`

Returns a Boolean value that determines whether the TrakSYS License has an active Subscription. A value of 1 means the Subscription is valid, while a value of 0 means the Subscription is invalid or expired.

`bool HasWarning`

Returns a Boolean value that determines whether the TrakSYS License has started displaying warnings due to an expiring Subscription. A value of 1 means the warnings are being displayed, while a value of 0 means they are not.

`int InterfaceDefinitionsCount`

Contains the total number of allowed Interface Definitions for the TrakSYS License.

`bool IsActivationRequired`

Returns a Boolean value that determines whether the TrakSYS License needs to be activated. A value of 1 means that license still needs to be activated while a value of 0 means it does not.

`bool IsDeveloper`

Returns a Boolean value that determines whether the TrakSYS License is a Development License. A value of 1 means it is a Development License, while a value of 0 means it is a Production License.

`bool IsExpired`

Returns a Boolean value that determines whether the TrakSYS License is expired. A value of 1 means the License is expired, while a value of 0 means it is not.

`bool IsLicensePresent`

Returns a Boolean value that determines whether the TrakSYS License is present in the database. A value of 1 means the License is present, while a value of 0 means it is not.

`bool IsValid`

Returns a Boolean value that determines whether the TrakSYS License is valid. A value of 1 means it is valid, while a value of 0 means it is not.

`string LicenseName`

Contains the name of the License, which is provided on License creation.

`string LicenseStatus`

Contains the current License Status. This information is typically displayed within the License tab of the TrakSYS Installation Manager.

`DateTimeOffset NextValidationDateTime`

Contains the next Date and Time that a License validation check will be performed.

`string Notes`

Contains the Notes for the current License, which are provided on License creation.

`string PartNumber`

Contains the Part Number that is assigned on License creation. This property is mainly used for internal purposes.

`int PayloadDefinitionsCount`

Contains the total number of allowed Payload Definitions for the TrakSYS License.

`int ProcessDefinitionFamiliesCount`

Contains the total number of allowed Process Definitions for the TrakSYS License.

`int ProductionSchedulingSystmesCount`

Contains the total number of allowed Production Scheduling Systems for the TrakSYS License.

`string Revision`

Contains the Revision Number assigned to the License on creation. This property is mainly used for internal purposes.

`int SampleDefinitionsCount`

Contains the total number of allowed Sample Definitions for the TrakSYS License.

`string SerialNumber`

Contains the License Serial Number that is assigned on License creation. The value will typically use a format of SN00000XXXXX.

`bool ShouldShowExpirationWarnings`

Returns a Boolean value that determines whether the TrakSYS License will display expiration warnings when a License is about to expire.

`bool ShowExpirationWarning1`

Returns a Boolean value that determines whether the TrakSYS License will display a warning message when the License is 30 days or less from expiring. A value of 1 means the warning message will be displayed, while a value of 0 means it will not.

`bool ShowExpirationWarning2`

Returns a Boolean value that determines whether the TrakSYS License will display a warning message when the License is 10 days or less from expiring. A value of 1 means the warning message will be displayed, while a value of 0 means it will not.

`int SitesCount`

Contains the total number of allowed Sites for the TrakSYS License.

`int TagHistorianDefinitionsCount`

Contains the total number of allowed Tag History Definitions for the TrakSYS License.

`int TaskDefinitionsCount`

Contains the total number of allowed Task Definitions for the TrakSYS License.

`int TransferDefinitionsCount`

Contains the total number of allowed Transfer Definitions for the TrakSYS License.

`string Version`

Contains the current TrakSYS version of the License.

`string WarningMessage`

Contains any current warnings relating to the License, Subscription, and Cloud connection.
