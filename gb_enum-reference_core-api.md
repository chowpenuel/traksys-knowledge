# Core API

The following is a list of Enums in the `ETS.Core.Enums` namespace. These enums are available in all TrakSYS Scripts including Logic Service, Data Management Service, and TrakSYS Web Pages.

## AccessNameConnectionStatus

Disconnected = 0

Connecting = 1

Connected = 2

Disconnecting = 3

NotLoaded = 4

## AccessNameType

Opc = 1

OleDb = 3

OpcHda = 4

OpcUa = 5

Mqtt = 6

## AccessPathInheritType

None = 0

Append = 1

UseParent = 2

## AgentOperationState

Unknown = 0

Created = 1

Running = 2

Success = 3

Failure = 4

## AgentOperationType

Unknown = 0

AssistantSync = 1

DatabaseImport = 2

DatabaseExport = 3

AssistantDelete = 4

ServiceStatus = 5

ScheduleSiteInfo = 6

ScheduleTelemetryDaily = 7

ScheduleTelemetryWeekly = 8

ScheduleTelemetryMonthly = 9

## AuditAuthenticationType

None = 0

EtsUser = 1

WindowsUser = 2

EtsAndWindows = 3

## AuditDetailOperationType

Insert = 1

Update = 2

Delete = 3

## AuditNotesType

Hide = 1

Optional = 2

Required = 3

## AuditSignatureType

None = 1

Auto = 2

NameOnly = 3

Single = 4

Dual = 5

## AutoCorrectMode

On = 0

Off = 1

Code = 2

## BatchState

None = 0

Pending = 1

InProgress = 2

Suspended = 3

Aborted = 4

Completed = 5

## Boolean

False = 0

True = 1

## CalculateFirstWeekRule

FirstDay = 0

FirstFourDayWeek = 2

FirstFullWeek = 1

## CloudDatabaseMode

Normal = 0

AzureSql = 1

AmazonRds = 2

## ConnectDataType

Object = 0

String = 1

Integer = 2

Double = 3

Boolean = 4

DateTime = 5

DateTimeOffset = 6

Enum = 7

Long = 8

## ContainerServiceRequest

None = 0

Restart = 2

Stop = 3

## ContainerServiceState

UseServiceState = 0

RestartingAsAContainer = 1

RunningAsAContainer = 2

StoppingAsAContainer = 3

## ContentPageMode

Visual = 0

Open = 1

Key = 2

## ContentPropertyGroup

\_GENERAL = 0

\_TEXT = 1

\_BAND = 2

\_VALUES = 3

\_CENTER = 4

\_UCL = 5

\_LCL = 6

\_USL = 7

\_LSL = 8

\_CUSTOM\_UPPER = 9

\_CUSTOM\_LOWER = 10

\_RAW\_VALUES = 11

\_APPEARANCE = 12

\_BEHAVIOR = 13

\_CONTENT = 14

\_CHART\_APPEARANCE = 15

\_CHART\_PIE = 16

\_CHART\_RADAR = 17

\_CHART\_LEGEND = 18

\_CHART\_AXIS\_VALUE = 19

\_CHART\_AXIS\_GROUP = 20

\_CHART\_PARETO = 21

\_CHART\_NORMAL\_DIST = 22

\_CHART\_POINT = 23

\_CHART\_CLICK = 24

\_CHART\_SERIES = 25

\_CHART\_STRIP = 26

\_CHART\_LIMITS = 27

\_TREE\_NODE\_BRANCH = 28

\_TREE\_NODE\_LEAF = 29

\_TRACEABILITY\_NODE\_FOCUS = 30

\_TRACEABILITY\_NODE\_BACKWARD = 31

\_TRACEABILITY\_NODE\_FORWARD = 32

\_DATA = 33

\_DATA\_DASH = 34

\_IMAGE = 35

\_FORMAT = 36

\_LINKS = 37

\_CHARTS = 38

\_MISC = 39

\_TIMEOUT = 40

\_OUTPUT = 41

\_SIMULATION = 42

\_RESPONSIVE = 43

\_ADVANCED = 44

\_INTERFACE = 45

## ContentPropertySubGroup

\_GENERAL\_TITLE = 0

\_GENERAL\_UPPER = 1

\_GENERAL\_LOWER = 2

\_GENERAL\_APPEARANCE = 3

\_GENERAL\_ICON = 4

\_GENERAL\_CLICK = 5

\_GENERAL\_URL = 6

\_GENERAL\_RANGE = 7

\_GENERAL\_FILTERS = 8

\_GENERAL\_FILTER\_SPECIFIC = 9

\_GENERAL\_FIELDS = 10

\_GENERAL\_SORT = 11

\_GENERAL\_SELECTED = 12

\_GENERAL\_BEHAVIOR = 13

\_GENERAL\_TEXT = 14

\_GENERAL\_COLUMN\_WIDTHS = 15

\_GENERAL\_COLOR = 16

\_GENERAL\_DATA = 17

\_GENERAL\_CHART = 18

\_GENERAL\_DESELECT = 19

\_GENERAL\_ADVANCED = 20

\_GENERAL\_TARGET = 21

\_GENERAL\_DEFAULT = 22

\_GENERAL\_BUTTON = 23

\_GENERAL\_GENERAL = 24

\_GENERAL\_CHECK\_EVERY = 25

\_GENERAL\_POLL\_INTERVAL = 26

\_GENERAL\_POST\_EXECUTION = 27

\_GENERAL\_SOURCE = 28

\_GENERAL\_STATE = 29

\_GENERAL\_TARGET\_01 = 30

\_GENERAL\_TARGET\_02 = 31

\_GENERAL\_TARGET\_03 = 32

\_GENERAL\_TARGET\_04 = 33

\_GENERAL\_TARGET\_05 = 34

\_GENERAL\_TIMEOUT\_AFTER = 35

\_GENERAL\_TAG\_01 = 36

\_GENERAL\_TAG\_02 = 37

\_GENERAL\_TAG\_03 = 38

\_GENERAL\_TAG\_04 = 39

\_GENERAL\_TAG\_05 = 40

\_GENERAL\_TASK\_COMPLETION = 41

\_GENERAL\_PROPERTY\_01 = 42

\_GENERAL\_PROPERTY\_02 = 43

\_GENERAL\_PROPERTY\_03 = 44

\_GENERAL\_PROPERTY\_04 = 45

\_GENERAL\_PROPERTY\_05 = 46

\_GENERAL\_TRANSFORM\_01 = 47

\_GENERAL\_TRANSFORM\_02 = 48

\_GENERAL\_TRANSFORM\_03 = 49

\_GENERAL\_TRANSFORM\_04 = 50

\_GENERAL\_TRANSFORM\_05 = 51

\_GENERAL\_TAGS = 52

\_GENERAL\_ARGUMENTS = 53

\_APPEARANCE\_CONTAINER = 54

\_APPEARANCE\_DIAGRAM = 55

\_TEXT\_UPPER = 56

\_TEXT\_LOWER = 57

\_TEXT\_OTHER = 58

\_BAND\_TOP = 59

\_BAND\_BOTTOM = 60

\_BAND\_LEFT = 61

\_BAND\_RIGHT = 62

\_VALUES\_LINE = 63

\_VALUES\_VIOLATIONS = 64

\_CENTER\_LINE = 65

\_UCL\_LINE = 66

\_LCL\_LINE = 67

\_USL\_LINE = 68

\_LSL\_LINE = 69

\_CUSTOM\_UPPER\_LINE = 70

\_CUSTOM\_LOWER\_LINE = 71

\_RAW\_VALUES\_LINE = 72

\_CONTENT\_ALLOW = 73

\_CONTENT\_EDIT = 74

\_CHART\_APPEARANCE\_FILL = 75

\_CHART\_APPEARANCE\_LINE\_BORDER = 76

\_CHART\_APPEARANCE\_LAYOUT = 77

\_CHART\_APPEARANCE\_MARKER = 78

\_CHART\_APPEARANCE\_SERIES = 79

\_CHART\_PIE\_GROUP = 80

\_CHART\_PIE\_COLLECT = 81

\_CHART\_PIE\_EXPLODED = 82

\_CHART\_PIE\_DOUGHNUT = 83

\_CHART\_AXIS\_VALUE\_LABEL = 84

\_CHART\_AXIS\_VALUE\_SCALE = 85

\_CHART\_AXIS\_VALUE\_BAND = 86

\_CHART\_AXIS\_VALUE\_INTERVAL = 87

\_CHART\_AXIS\_GROUP\_LABEL = 88

\_CHART\_AXIS\_GROUP\_INTERVAL = 89

\_CHART\_AXIS\_GROUP\_BAND = 90

\_CHART\_PARETO\_LABEL = 91

\_CHART\_PARETO\_TIP = 92

\_CHART\_PARETO\_LINE\_BORDER = 93

\_CHART\_PARETO\_MARKER = 94

\_CHART\_NORMAL\_DIST\_LINE\_BORDER = 95

\_CHART\_POINT\_LABEL = 96

\_CHART\_POINT\_LABEL\_1 = 97

\_CHART\_POINT\_LABEL\_2 = 98

\_CHART\_POINT\_TIP = 99

\_CHART\_POINT\_COLOR = 100

\_CHART\_POINT\_SELECTED = 101

\_CHART\_POINT\_MARKER\_1 = 102

\_CHART\_POINT\_MARKER\_2 = 103

\_CHART\_POINT\_MARKER\_3 = 104

\_CHART\_POINT\_MARKER\_4 = 105

\_CHART\_CLICK\_VALUE = 106

\_CHART\_CLICK\_VIOLATION = 107

\_CHART\_CLICK\_COLLECTION = 108

\_CHART\_SERIES\_CLICK = 109

\_CHART\_SERIES\_TOTAL\_CLICK = 110

\_CHART\_STRIP\_LINE = 111

\_CHART\_LIMITS\_LIMIT1 = 112

\_CHART\_LIMITS\_LIMIT2 = 113

\_CHART\_LIMITS\_LIMIT3 = 114

\_CHART\_LIMITS\_LIMIT4 = 115

\_TREE\_NODE\_BRANCH\_CLICK = 116

\_TREE\_NODE\_BRANCH\_CLICK\_DBL = 117

\_TREE\_NODE\_BRANCH\_APPEARANCE = 118

\_TREE\_NODE\_BRANCH\_FIELDS = 119

\_TREE\_NODE\_BRANCH\_KEYS = 120

\_TREE\_NODE\_LEAF\_CLICK = 121

\_TREE\_NODE\_LEAF\_CLICK\_DBL = 122

\_TREE\_NODE\_LEAF\_APPEARANCE = 123

\_TREE\_NODE\_LEAF\_FIELDS = 124

\_TREE\_NODE\_LEAF\_KEYS = 125

\_TRACEABILITY\_NODE\_FOCUS\_CLICK = 126

\_TRACEABILITY\_NODE\_FOCUS\_CLICK\_DBL = 127

\_TRACEABILITY\_NODE\_FOCUS\_APPEARANCE = 128

\_TRACEABILITY\_NODE\_BACKWARD\_CLICK = 129

\_TRACEABILITY\_NODE\_BACKWARD\_CLICK\_DBL = 130

\_TRACEABILITY\_NODE\_BACKWARD\_APPEARANCE = 131

\_TRACEABILITY\_NODE\_BACKWARD\_KEYS = 132

\_TRACEABILITY\_NODE\_FORWARD\_CLICK = 133

\_TRACEABILITY\_NODE\_FORWARD\_CLICK\_DBL = 134

\_TRACEABILITY\_NODE\_FORWARD\_APPEARANCE = 135

\_TRACEABILITY\_NODE\_FORWARD\_KEYS = 136

\_DATA\_SOURCE = 137

\_DATA\_FIELDS = 138

\_DATA\_SOURCE\_FIXED = 139

\_DATA\_FIELDS\_FIXED = 140

\_DATA\_SOURCE\_AXIS = 141

\_DATA\_FIELDS\_AXIS = 142

\_DATA\_TARGET = 143

\_DATA\_SELECTED = 144

\_DATA\_PAGING = 145

\_DATA\_SET\_01 = 146

\_DATA\_SET\_02 = 147

\_DATA\_SET\_03 = 148

\_DATA\_SET\_04 = 149

\_DATA\_SET\_05 = 150

\_DATA\_SET\_06 = 151

\_DATA\_SET\_07 = 152

\_DATA\_SET\_08 = 153

\_DATA\_SET\_09 = 154

\_DATA\_SET\_10 = 155

\_DATA\_SET\_11 = 156

\_DATA\_SET\_12 = 157

\_DATA\_SET\_13 = 158

\_DATA\_SET\_14 = 159

\_DATA\_SET\_15 = 160

\_DATA\_SET\_16 = 161

\_DATA\_SET\_17 = 162

\_DATA\_SET\_18 = 163

\_DATA\_SET\_19 = 164

\_DATA\_SET\_20 = 165

\_DATA\_SOURCE\_DATABASE = 166

\_LINKS\_SHOW = 167

\_LINKS\_ACTION\_01 = 168

\_LINKS\_ACTION\_02 = 169

\_LINKS\_ACTION\_03 = 170

\_LINKS\_ACTION\_04 = 171

\_LINKS\_ACTION\_05 = 172

\_CHARTS\_SHOW = 173

\_RESPONSIVE\_VISIBLE = 174

\_RESPONSIVE\_WIDTH = 175

\_RESPONSIVE\_HEIGHT = 176

\_TIMEOUT\_TIMEOUT\_AFTER = 177

\_ADVANCED\_FORMAT = 178

\_ADVANCED\_URL = 179

\_INTERFACE\_WEBSERVICE\_PERMISSIONS = 180

\_INTERFACE\_WEBSERVICE\_AUTHENTICATION = 181

\_INTERFACE\_WEBSERVICE\_GENERAL = 182

\_INTERFACE\_FILESERVICE\_GENERAL = 183

\_INTERFACE\_FILESERVICE\_PERMISSIONS = 184

## CSharpIdentifierStrictnessMode

Compatible = 0

Strict = 5

## CssMode

Default = 0

Ts11Compatible = 11

## CustomPropertyEntity

Area = 0

EventCategory = 1

EventCode = 2

EventDefinition = 3

FunctionDefinition = 5

ItemDefinition = 6

ItemLogDefinition = 7

JournalCategory = 8

Location = 9

LogicManager = 10

Material = 11

OeeCalculation = 12

OeeCountCategory = 13

OeeCounter = 14

ParameterDefinition = 15

Product = 16

Recipe = 17

RecipeStepDefinition = 18

SampleCategory = 19

SampleDefinition = 20

SampleDefinitionRuleDefinition = 21

Shift = 22

Site = 23

StepCategory = 24

StepCode = 25

System = 26

Tag = 27

TaskDefinition = 28

TaskFormItem = 29

Team = 30

TransferDefinition = 31

User = 32

EventDefinitionGroup = 100

FunctionDefinitionGroup = 101

RecipeStepDefinitionMaterial = 102

TaskDefinitionGroup = 103

TaskFormItemGroup = 104

TransferDefinitionGroup = 105

Device = 106

RecipeParameter = 107

MaterialGroup = 108

LookupSet = 109

LookupValue = 110

ProductCoTypeSet = 200

ProductCoType = 201

PsSet = 202

ProcessDefinition = 203

ProcessStepDefinition = 204

ProductVariation = 205

Role = 300

PayloadDefinition = 400

PayloadFieldDefinition = 401

MaterialConsumptionMethod = 410

TaskForm = 420

## DataType

None = 0

String = 1

Integer = 2

Double = 3

Boolean = 4

## DataTypeValid

String = 1

Integer = 2

Double = 3

Boolean = 4

## DbActionType

Insert = 1

Update = 2

Delete = 3

Execute = 4

## DbTransferMode

None = 0

Ui = 1

Config = 2

UiAndConfig = 3

## DbTransferSiteMode

Full = 0

SingleSite = 1

## DeviceIdentifierType

Guid = 1

ComputerName = 2

IPv4 = 3

MacAddress = 5

## EventCategoryGroupScopeType

GlobalFirst = 0

Normal = 1

GlobalLast = 2

## EventEdgeType

Start = 0

End = 1

## EventIsolationType

None = 0

System = 1

## EventState

None = 0

Sent = 1

Displayed = 2

UserAcknowledged = 3

AutoAcknowledged = 4

SentNeverDisplayed = 5

## FormValidationMode

None = 0

Warning = 1

Error = 2

## HaRequest

None = 0

Start = 1

SwitchToHost = 2

SwitchToHostHa = 3

Shutdown = 4

Stop = 5

RestartContainer = 6

## HaState

NotRunning = 0

StartingHost = 1

StartingHostHa = 2

SwitchingToHost = 3

SwitchingToHostHa = 4

RunningAsHost = 5

RunningAsHostHa = 6

Stopping = 7

Stopped = 8

Restarting = 9

## HistorianManagerState

Stopped = 0

Starting = 1

Running = 2

Stopping = 3

Unknown = 1000

## HorizontalTextAlign

None = 0

Left = 1

Right = 2

Center = 3

## HostType

ComputerName = 1

IpAddress = 2

User = 3

Identifier = 4

MacAddress = 5

## InheritableBoolean

False = 0

True = 1

Inherit = 2

## InheritableCssMode

Default = 0

Inherit = 1

Ts11Compatible = 11

## InheritableSidebarMode

Off = 0

On = 1

Inherit = 2

Toggle = 3

## InterfaceDefinitionType

Custom = 0

WebServiceCall = 1

WebServiceEndpoint = 3

FilePush = 5

FilePull = 6

## InterfaceHttpMethodType

Get = 0

Post = 1

Put = 2

Delete = 3

## InterfaceTransactionStateType

InProgress = 0

Success = 1

Failed = 2

## IqAssistantStatus

NotSynced = 0

Syncing = 1

Synced = 2

## IqAssistantThreadItemAnswerType

Text = 0

Sql = 1

Chart = 2

## IqAssistantViewColumnArgKey

Description = 0

LookupName = 1

ReferencedColumnName = 2

EnumName = 3

EnumValues = 4

UnitOfMeasureName = 5

ViewNameDotColumnName = 6

JoinPurpose = 7

## IqAssistantViewColumnType

Open = 0

ReferenceTableByUniqueID = 1

ReferenceTableByForeignKeyID = 2

ReferenceTableByForeignKeyIDLookup = 3

ReferenceTableByForeignKeyName = 4

ForeignKeyCode = 5

Enumeration = 6

MetricWithUnit = 7

Date = 8

DateTime = 9

Site = 10

BooleanWhenZero = 11

BooleanWhenOne = 12

ReferenceTableByUniqueIDView = 13

ReferenceTableByForeignKeyIDView = 14

## JobCaptureOnType

None = 0

JobRecordCreation = 1

JobActivation = 2

JobDeactivation = 3

## JobType

Discrete = 0

Batch = 1

## LogCategoryType

None = 0

Startup = 1

Shutdown = 2

Oee = 3

Schedule = 4

## LogicManagerScanType

ScanNone = 0

ScanFirst = 1

ScanNormal = 2

ScanCheckDB = 3

ScanLast = 4

ScanHighAvailabilityBackup = 5

## LogicManagerState

Stopped = 0

Starting = 1

Running = 2

Stopping = 3

StalledOnStarting = 21

StalledOnRunning = 22

Unknown = 1000

## LogType

Information = 1

Warning = 2

Error = 3

## LogTypeCustom

Information = 1

Debug = 2

Warning = 3

Error = 4

Critical = 5

## MaintenanceServiceState

Stopped = 0

Running = 1

## MetricEntityType

None = 0

Area = 1

System = 2

OeeCalculationID = 3

## MetricState

None = 0

RecalculateRequested = 1

## ModuleManagerState

Stopped = 0

Starting = 1

Running = 2

Stopping = 3

## ModuleState

NotRunning = 0

Starting = 1

Running = 2

Stopping = 3

## ModuleStepErrorMode

Nothing = 0

Abort = 1

## ModuleStepType

Script = 1

Sql = 2

MetricCalculator = 3

ConnectPull = 4

## MqttAuthenticationType

Anonymous = 0

UserNamePasswordOnly = 1

OneWayTls = 2

MutualTls = 3

## MqttCertificateValidationMode

NoCheck = 0

Online = 1

Offline = 2

## MqttQualityOfService

AtMostOnce = 0

AtLeastOnce = 1

ExactlyOnce = 2

## MqttTlsVersion

Tls12 = 0

Tls13 = 1

## MqttWritebackReasonCode

Success = 0

Failure = 1

NotImplemented = 2

InvalidArgument = 3

Busy = 4

NoMatchingSubscribers = 16

UnspecifiedError = 128

ImplementationSpecificError = 131

NotAuthorized = 135

TopicNameInvalid = 144

PacketIdentifierInUse = 145

QuotaExceeded = 151

PayloadFormatInvalid = 153

## MtbfType

Failure = 1

NonFailure = 2

Excluded = 3

## NotificationAlertState

NotRead = 0

Read = 1

## NotificationArgumentDataType

None = 0

Number = 10

DateTime = 20

String = 30

Boolean = 40

Enum = 50

## NotificationDefinitionMessageType

EmailLegacy = 0

EmailRetrieveAndEmbedLegacy = 1

AlertLegacy = 10

WebHook = 20

## NotificationDefinitionStatusType

None = 0

Success = 1

Information = 2

Warning = 3

Error = 4

## NotificationDistributionListType

Email = 0

Alert = 1

## NotificationEventDefinitionType

OnStart = 1

OnEnd = 2

## NotificationFunctionDefinitionType

OnStart = 1

OnEnd = 2

OnOver = 3

## NotificationLogicManagerType

OnStart = 1

OnStartFail = 2

OnStartComplete = 3

OnStop = 4

OnStalled = 5

## NotificationModuleStepType

OnStart = 1

OnSuccess = 2

OnFail = 3

OnComplete = 4

## NotificationModuleType

OnRunStart = 1

OnRunEnd = 2

OnExecuteStart = 3

OnExecuteSuccess = 4

OnExecuteFail = 5

OnExecuteComplete = 6

## NotificationSampleDefinitionRuleDefinitionType

OnRule = 1

## NotificationStateType

Pending = 1

CompleteOK = 2

CompleteError = 3

## NotificationSystemType

OnEventDefinitionStart = 1

OnEventDefinitionEnd = 2

OnFunctionDefinitionStart = 3

OnFunctionDefinitionEnd = 4

OnFunctionDefinitionOver = 5

OnTaskDefinitionCreate = 6

OnTaskDefinitionLate = 7

OnTaskDefinitionComplete = 8

OnTaskDefinitionPass = 10

OnTaskDefinitionFail = 11

OnSampleDefinitionRule = 12

## NotificationTagType

OnValueEqualTo = 1

OnValueLessThan = 2

OnValueGreaterThan = 3

## NotificationTaskDefinitionType

OnCreate = 1

OnLate = 2

OnComplete = 3

OnUserStateChange = 4

OnPass = 5

OnFail = 6

## NotificationWorkflowManagerType

OnStart = 1

OnStop = 2

OnStalled = 3

## OeeAdjustmentType

Correction = 0

Addition = 1

## OeeCounterDetailType

Normal = 0

Rollover = 1

ExceededMaxPlus = 2

QualityChanged = 4

FlowChanged = 8

## OeeCounterType

Total = 1

Good = 2

Bad = 3

## OeeEventType

None = 0

PerformanceLoss = 1

AvailabilityLoss = 2

SystemNotScheduled = 3

LegalLoss = 4

## OeeEventTypeAssign

None = 0

PerformanceLoss = 1

AvailabilityLoss = 2

SystemNotScheduled = 3

LegalLoss = 4

## OeeIntervalEdgeType

Start = 0

End = 1

## OeeStepType

None = 0

PerformanceLoss = 1

AvailabilityLoss = 2

SystemNotScheduled = 3

## OeeStepTypeAssign

None = 0

PerformanceLoss = 1

AvailabilityLoss = 2

SystemNotScheduled = 3

## OpcReadOnConnectType

No = 0

Sync = 1

SyncOnReconnect = 2

## OpcReadType

Cache = 1

Device = 2

## OpcUaAuthenticationType

Anonymous = 0

UserNamePassword = 1

## OpcUaPreferredSecurityLevel

Lowest = 0

Highest = 1

## PackageLocation

Root = 0

Web = 1

Both = 2

## PackageSearchMode

Browse = 0

Installed = 1

Updates = 2

## PackageSearchOnlineSource

Parsec = 0

NuGet = 1

## PackageSearchSourceType

Local = 0

Online = 2

Auto = 100

## PackageSource

Local = 0

Online = 2

## PageDefinitionInstanceType

None = 0

CustomScript = 1

PageDefInstance = 100

SystemByAreaKey = 101

## PageDefinitionLevel

Site = 0

Section = 1

Hub1 = 2

Hub2 = 3

Hub3 = 4

Spoke = 100

## PageParameterType

Form = 0

QueryString = 1

## PagePermissionAccess

NoAll = 0

YesAll = 1

YesSingle = 2

## PageRecoveryMode

RedirectOnError = 0

DebugMode = 1

RedirectOnErrorSecure = 2

## PassFail

Unknown = -1

Fail = 0

Pass = 1

## PayloadContentType

RawStringContent = 0

FormUrlEncoded = 1

## PayloadCsvImportRowSeparatorMode

CrLf = 0

NewLine = 1

## PayloadFieldIsRequiredMode

Required = 0

NotRequired = 1

NotRequiredNullable = 2

## PayloadType

Custom = 0

Xml = 1

Json = 2

Csv = 3

StringOnly = 4

QueryString = 6

## PayloadXmlImportAttributeMode

No = 0

Yes = 1

YesWithRootAttributes = 2

## PeriodicFrequencyType

Second = 0

Minute = 1

Hour = 2

## PeriodRollupType

None = 0

Hour = 1

Date = 2

Week = 3

Month = 4

Year = 5

Shift = 6

Job = 7

Batch = 8

## PermissionSetType

Flat = 0

Grid = 1

## ProcessPathLabelMode

Smart = 0

Normal = 1

Verbose = 2

## ProcessPathOperatorType

Equals = 0

LessThan = 1

LessThanEqual = 2

GreaterThan = 3

GreaterThanEqual = 4

NotEqual = 5

## ProcessSinkType

ForceStepCheck = 0

KillProcess = 1

## ProcessState

Executing = 0

CompleteSuccess = 10

CompleteKilled = 11

CompleteFailed = 12

## ProcessStepErrorActionType

EndProcess = 0

ResumeWithFailed = 1

## ProcessStepExecutionState

None = 0

ExecutingInScript = 1

ExecutingAndWaiting = 2

ExecuteComplete = 10

CompleteSuccess = 100

CompleteTimeOut = 101

CompleteError = 102

## ProcessStepGroup

\_GENERAL = 0

\_ENTITY = 1

\_JOB = 2

\_MISCELLANEOUS = 3

\_NOTIFICATION = 4

\_PROCESS = 5

\_SQL = 6

\_TAG = 7

\_TASK = 8

\_COMMON = 9

\_SM = 10

## ProcessStepResultState

Unknown = 0

Success = 1

TimeOut = 2

FailEndProcess = 10

FailResumeWithFailed = 11

Canceled = 20

## ProcessStepRunExecutionType

FirstRun = 0

Retry = 1

FirstRerun = 2

## PsSetType

Discrete = 0

Batch = 1

## QuoteOption

None = 0

Single = 1

Double = 2

## ReferentialIntegrityCheckFailureActionType

Rollback = 1

Prompt = 2

## ReferentialIntegrityCheckLevel

None = 0

All = 1

ExcludeData = 2

## RemoteServiceRequest

None = 0

Start = 1

Restart = 2

Stop = 3

## ReportGroupPermissionRole

Deny = 0

Publisher = 1

Browser = 2

NoAccess = 3

## ResourceTranslationMode

All = 0

ServerOnly = 1

ClientOnly = 2

## ResultMessageType

Warning = 0

Error = 1

## S95AreaType

None = 0

Enterprise = 1

Site = 2

Area = 3

## S95SubSystemType

None = 0

WorkCell = 1

Unit = 2

## S95SystemType

ProductionLine = 1

ProcessCell = 2

ProductionUnit = 3

StorageZone = 4

## SampleDefinitionCalculationType

VariableControl = 1

AttributeControl = 2

## SampleSubGroupSinkType

Create = 1

## SaveAction

Insert = 0

Update = 1

Merge = 2

## SchedulePatternItemColorType

ShiftColor = 1

TeamColor = 2

## ScriptCompileType

Core = 0

Framework = 1

Both = 2

## ScriptGroupType

Shared = 0

Module = 1

LogicManager = 2

Web = 3

DatabaseTransfer = 4

WorkflowManager = 5

## SelectPartType

Checkbox = 0

RowSelect = 1

## ShiftHistoryDateType

ShiftStart = 0

ShiftEnd = 1

PreviousDayShiftStart = 2

NextDayShiftEnd = 3

## SidebarMode

Off = 0

On = 1

Toggle = 3

## SmartTagWriteBackState

Pending = 0

Sent = 1

Canceled = 2

Success = 10

Timeout = 15

Fail = 20

## SmtpAuthenticationType

None = 0

UsernamePassword = 1

Microsoft365 = 2

## SpcRuleDefinitionType

CustomScript = 0

CustomRule = 1

FourteenConsecutivePointsAlternating = 100

TwoOutOfLast3AboveSigma2 = 101

TwoOutOfLast3BelowNegativeSigma2 = 102

FourOutOfLast5AboveSigma1 = 103

FourOutOfLast5BelowNegativeSigma1 = 104

SixConsecutivePointsTrendingDown = 105

SixConsecutivePointsTrendingUp = 106

EightConsecutivePointsAboveCenterLine = 107

EightConsecutivePointsBelowCenterLine = 108

AnyPointAboveSigma3 = 109

AnyPointBelowNegativeSigma3 = 110

## SqlAggregateOperation

None = 0

Sum = 1

Count = 2

Avg = 3

Min = 4

Max = 5

## SqlBuilderSiteMode

None = 0

SiteAndRoot = 1

SiteOnly = 2

## SqlDataType

Int = 2

Nvarchar = 1

Date = 0

Datetime = 5

DatetimeOffset = 6

Bit = 4

Float = 3

TableInt = 7

TableString = 8

## SqlJoinType

Inner = 0

LeftOuter = 1

## SqlObjectType

Unknown = 0

FunctionInlineTableValued = 1

FunctionScalar = 2

FunctionTableValued = 3

StoredProcedure = 4

View = 5

## SqlWhereOperation

Equals = 0

LessThan = 1

LessThanEqual = 2

GreaterThan = 3

GreaterThanEqual = 4

NotEqual = 5

In = 6

Contains = 7

Between = 8

## StandardMetricType

None = 0

Oee = 1

Availability = 2

Performance = 3

Quality = 4

Teep = 5

CycleTime = 6

TotalUnits = 7

GoodUnits = 8

BadUnits = 9

AvailabilityLossDuration = 10

ProductionDuration = 11

NetOperationDuration = 12

SystemNotScheduledDuration = 13

PerformanceLossDuration = 14

RateLossDuration = 15

RunTimeDuration = 16

TotalDuration = 17

TotalNetOpCalculationUnitsPerHour = 18

GoodNetOpCalculationUnitsPerHour = 19

BadNetOpCalculationUnitsPerHour = 20

Mttr = 21

Mtrbf = 22

Mtbf = 23

Oee2 = 24

Availability2 = 25

Teep2 = 26

## StepCategoryGroupScopeType

GlobalFirst = 0

Normal = 1

GlobalLast = 2

## SubscriptionRequestMode

Auto = 0

Manual = 1

## SubscriptionValidationStatus

Unknown = 0

Valid = 1

UpdateRequired = 2

UpdateRequiredUnsafe = 3

Shutdown = 4

InstanceExists = 5

## TagAggregateOperation

Sum = 0

Average = 1

Min = 2

Max = 3

Concatenate = 4

## TagAssignCondition

WhileTrue = 0

OnTrue = 1

## TagAssignOperation

Equals = 0

Add = 1

Subtract = 2

Multiply = 3

Divide = 4

Modulus = 5

Concatenate = 6

## TagBooleanOperation

And = 1

Or = 2

Xor = 3

Nand = 4

Nor = 5

Xnor = 6

## TagCalculationOperation

Add = 1

Subtract = 2

Multiply = 3

Divide = 4

Modulus = 5

Concatenate = 6

Left = 7

Right = 8

Random = 9

## TagCompareOperation

Equal = 1

NotEqual = 2

GreaterThan = 3

GreaterThanEqualTo = 4

LessThan = 5

LessThanEqualTo = 6

## TagHistoryIntervalType

LastValue = 0

Slope = 1

Average = 2

## TagHistoryMode

Manual = 0

Periodic = 1

DeviationIsPercent = 5

DeviationIsFixed = 6

## TagMaskOperation

None = 0

And = 1

Or = 2

Xor = 3

## TagOrConstantType

Tag = 1

Constant = 2

Calculated = 4

## TagQualityDescription

Bad = 0

Good = 1

BadVariantCast = 2

BadOpcCast = 3

BadVirtualRead = 4

BadCalculationEvaluation = 5

BadCompareEvaluation = 6

BadCompareTagTypeMismatch = 7

BadCompareBooleanTypeMismatch = 8

BadCompareInvalidConfiguration = 9

BadCompareNoTag = 10

BadLatchConfiguration = 11

BadOpcOperation = 12

BadOpcOverflow = 15

BadOpcConnection = 16

BadValueIsNull = 17

BadValueIsNanOrInfinity = 18

BadMqttCast = 19

BadMqttOverflow = 20

BadMqttSparkplugUnspecifiedMetric = 21

BadMqttSparkplugDeathCertificate = 22

BadMqttSparkplugMissingMetric = 23

BadMqttSparkplugInvalidMetricValue = 24

BadMqttSparkplugUnsupportedMetricDataType = 25

BadMqttSparkplugNullMetricValue = 26

## TagScriptType

SingleLineVbNet = 0

MultiLineCSharp = 1

## TagType

Opc = 1

OleDb = 3

Virtual = 4

State = 5

Compare = 6

Calculation = 7

Switch = 8

Latch = 9

Boolean = 10

Counter = 11

Script = 12

Aggregate = 13

Template = 14

OpcHda = 15

OpcUa = 16

Smart = 17

InMemory = 18

ScriptClass = 19

Mqtt = 20

## TargetRateUnitType

SecondsPerUnit = 1

UnitsPerMinute = 2

## TaskFormItemRenderType

Default = 0

Textbox = 1

TextboxMulti2 = 2

TextboxMulti3 = 3

TextboxMulti4 = 4

TextboxMulti5 = 5

Checkbox = 10

Dropdown = 20

RadioButtons = 30

MultiSelectList = 40

DateTime = 80

Date = 81

Time = 82

Custom = 100

## TaskSinkType

Create = 1

Late = 2

Complete = 3

UserStateChange = 4

Pass = 5

Fail = 6

## TaskTriggerType

Tag = 1

OnDemand = 2

Scheduled = 3

EveryNMinutesAndTag = 4

EveryNMinutesWhileTag = 5

JobStart = 6

JobEnd = 7

BatchStart = 8

BatchEnd = 9

ShiftStart = 10

ShiftEnd = 11

FunctionStart = 12

FunctionEnd = 13

EventStart = 14

EventEnd = 15

## TeaGetPackageVersionState

NotFound = 0

Older = 1

Same = 2

Newer = 3

## TemplateDefinitionImportCompareType

None = 0

Insert = 1

UpdateNoChange = 2

UpdateChange = 3

Delete = 4

Obsolete = 5

Skip = 6

## TemplateDefinitionImportState

Preview = 0

Importing = 1

Success = 2

Fail = 3

## TemplateExportState

Exporting = 0

Success = 1

Fail = 2

## TemplateExportType

Template = 0

Branch = 1

Merge = 2

## TemplateImportCompareType

None = 0

Insert = 1

UpdateNoChange = 2

UpdateChange = 3

Delete = 4

Obsolete = 5

## TemplateImportState

Preview = 0

Importing = 1

Success = 2

Fail = 3

## TestRunResultType

Inconclusive = 0

Skipped = 1

Passed = 2

Warning = 3

Failed = 4

## TransferDirectionType

In = 1

Out = 2

Set = 3

## TransferEdgeType

Start = 0

End = 1

## TransferSinkType

Create = 1

Complete = 2

## TriggerModeType

None = 0

Periodic = 1

Daily = 2

## TsColor

Default = 0

Primary = 1

Success = 2

Warning = 3

Alert = 4

Active = 5

Inactive = 6

Page = 10

Card = 11

Blue = 100

BlueLight = 101

BlueBright = 102

BlueDark = 103

BlueGray = 104

Gray = 105

GrayLight = 106

GrayDark = 107

Green = 108

GreenLight = 109

GreenDark = 110

Slate = 111

Orange = 112

OrangeLight = 113

Gold = 114

Red = 115

RedLight = 116

RedBright = 117

Magenta = 118

Cream = 119

Brown = 120

White = 121

Black = 122

Yellow = 123

## UserAuthenticatePermissionResult

Error = 0

AccessGranted = 1

AccessDenied = 2

LoginFailed = 3

## UserLogAction

Error = 0

Login = 1

Logout = 2

LoginFailed = 3

LogoutKicked = 4

LogoutInactive = 5

## UserType

WindowsUser = 1

WindowsGroup = 2

EtsUser = 3

EtsGroup = 4

IpAddress = 5

ComputerName = 6

Identifier = 7

Everyone = 8

OidcUser = 9

OidcGroup = 10

ApiUser = 11

SamlUser = 12

SamlGroup = 13

## ValidationCompareType

GreaterThan = 0

GreaterThanEqual = 1

LessThan = 2

LessThanEqual = 3

Equal = 4

NotEqual = 5

## ValuesItemDataType

String = 1

Integer = 2

Double = 3

Boolean = 4

## VersionState

Draft = 1

Active = 2

Retired = 3

Approval = 4

Obsolete = 5

## WebApiSecurityMode

None = 0

OriginOnly = 1

OriginOnlyAuthenticated = 2

SecuredByPermission = 3

## WebCompileOnStartMode

Default = 0

AlwaysCheckOnStartup = 1

ManualOnly = 2

## WebIFrameOption

Allow = 0

Deny = 1

SameOrigin = 2

## WebResourceEditorType

None = 0

Css = 1

Js = 2

Xml = 3

PlainText = 4

AspnetView = 5

AspnetCodeBehind = 6

## WebResourceIncludeType

None = 0

GlobalCss = 1

GlobalJs = 2

## WebServiceAuthenticationType

None = 0

Bearer = 1

Basic = 2

## WindowsGroupTranslateMode

FullTranslate = 0

TranslateForConfig = 1

## WorkflowManagerState

Stopped = 0

Starting = 1

Running = 2

Stopping = 3

Stalled = 21
