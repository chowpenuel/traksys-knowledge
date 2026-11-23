# Custom Operations

Custom Operations are used to define extensible actions on various Entities within TrakSYS. The Operations become available below the Actions menu of the selected Entity, similar to where Move and Delete Actions appear on Configuration items, under a new label called "Custom".

## Configuring

### Name

The Operation Name is used strictly for reference in the Configuration of the Custom Operation.

### Entity Name

The Entity Name determines TrakSYS Entity on which the Custom Operation will appear. Note that the Entity Name must be written in this field with no spaces, such as EventDefinition. See the bottom of this page for the list of available Entities.

### Data

The Data defines the Caption, Icon, Link, and Parameters of the Custom Operation. The field accepts XML in the following format:

```xml
<Operations>
  <Custom>
    <Operation Caption="" Icon="" Url="">
      <Param Name="" Value="" />
      <Param Name="" Value="" />
    </Operation>
  </Custom>
</Operations>
```

{% hint style="info" %}
The Url field is optional, if a Parameter is provided for **"c"** (Content >Page Key) which will redirect to to a Content Page. However, if a Parameter is not provided for **"c"**, then a **Url** will be required in order for the Operation to link somewhere.
{% endhint %}

Below is an example of the XML Data for an EventDefinition Custom Operation which links to the a non-standard Content Page while passing the ID of the currently selected Event Definition.

```xml
<Operations>
  <Custom>
    <Operation Caption="View Event Definition" Icon="fa fa-arrow-down" Url="../">
      <Param Name="c" Value="View_EventDefinition" />
      <Param Name="EventDefinitionID" Value="{ID}" />
    </Operation>
  </Custom>
</Operations>
```

#### Common Operations

Common Operations appear at the top of the Slice, directly below the title of the Entity, typically where an Edit button appears. The Custom Operation Data field can also be populated with XML for a Common Operation, for example:

```xml
<Operations>
  <Common>
    <Operation Caption="" Icon="" Url="">
      <Param Name="" Value="" />
      <Param Name="" Value="" />
    </Operation>
  </Common>
</Operations>
```

#### Other Operations

Other Operations appear below the Actions menu of the selected Entity, however, unlike Custom Operations, which appear under the "Custom" label. The Data field can also be populated with XML for an Other Operation, for example:

```xml
<Operations>
  <Other>
    <Operation Caption="" Icon="" Url="">
      <Param Name="" Value="" />
      <Param Name="" Value="" />
    </Operation>
  </Other>
</Operations>
```

## Available Entities

* AccessName
* AccessNameGroup
* AccessNameMqttComposite
* AccessNameOleDbComposite
* AccessNameOleDbParameter
* AccessNameOpcComposite
* AccessNameOpcHdaComposite
* AccessNameOpcUaComposite
* Area
* AreaType
* AuditDetail
* BatchQualityLossCategory
* BatchQualityLossCategoryGroup
* ContentPage
* ContentPageGroup
* ContentPart
* ContentPartGroup
* Conversion
* ConversionGroup
* CustomProperty
* CustomPropertyEnum
* CustomPropertyGroup
* CustomPropertyScheme
* Device
* DeviceGroup
* DeviceGroupReadOnly
* DeviceReadOnly
* DeviceType
* EntityOperation
* EventCategory
* EventCategoryGroup
* EventCategoryScheme
* EventCategorySchemeLevel
* EventCategoryType
* EventCode
* EventCodeGroup
* EventCodeType
* EventDefinition
* EventDefinitionEventMonitor
* EventDefinitionGroup
* EventDefinitionTagRelationship
* EventDefinitionType
* EventVtrDefinition
* FastUpdateSet
* FastUpdateTag
* FunctionDefinition
* FunctionDefinitionGroup
* FunctionDefinitionTagRelationship
* FunctionDefinitionType
* HistorianManager
* InterfaceDefinition
* InterfaceDefinitionGroup
* IqAssistant
* IqAssistantGroup
* IqAssistantLookup
* IqAssistantView
* IqAssistantViewColumn
* ItemDefinition
* ItemDefinitionGroup
* ItemDefinitionType
* ItemLogDefinition
* ItemLogDefinitionGroup
* ItemLogDefinitionType
* JobCaptureScheme
* JobCaptureSchemeColumn
* JobCaptureTag
* JobType
* JournalCategory
* JournalCategoryGroup
* JournalCategoryType
* LibraryItem
* LibraryItemGroup
* Location
* LocationType
* LogicManager
* LookupSet
* LookupSetType
* LookupValue
* LookupSetType
* Material
* MaterialAlternate
* MatterialAttribute
* MaterialComponent
* MaterialConsumptionMethod
* MaterialConsumptionMethodGroup
* MaterialConsumptionMethodType
* MaterialGroup
* MaterialScheme
* MaterialSet
* MaterialType
* Measure
* MeasureGroup
* MetricDefinition
* MetricDefinitionStandardMetric
* MetricScheme
* MetricSchemeColumn
* Module
* ModuleManager
* ModuleStep
* ModuleStepConnectPullComposite
* ModuleStepMetricCalculatorComposite
* ModuleStepScriptComposite
* ModuleStepSqlComposite
* NotificationDefinition
* NotificationDefinitionAttachment
* NotificationDefinitionGroup
* NotificationDistributionList
* NotificationDistributionListGroup
* NotificationEventDefinition
* NotificationFunctionDefinition
* NotificationLogicManager
* NotificationModule
* NotificationModuleStep
* NotificationSampleDefinitionRuleDefinition
* NotificationSystem
* NotificationTag
* NotificationTarget
* NotificationTargetGroup
* NotificationTargetUser
* NotificationTaskDefinition
* NotificationWorkflowManager
* OeeCalculation
* OeeCalculationType
* OeeCalculationView
* OeeCaptureScheme
* OeeCaptureSchemeColumn
* OeeCaptureTag
* OeeCountCategory
* OeeCountCategoryGroup
* OeeCountCategoryType
* OeeCounter
* OeeCounterComposite
* OeeCounterDerivedComposite
* OeeCounterType
* OeeInput
* OeeVtrDefinition
* PageDefinition
* PageDefinitionInstance
* PageDefinitionSectionGroup
* ParameterDefinition
* ParameterDefinitionType
* PayloadDefinition
* PayloadDefinitionGroup
* PayloadDefinitionType
* PayloadFieldDefinition
* PayloadFieldDefinitionType
* PermissionAction
* PermissionItem
* PermissionSet
* ProcessDefinition
* ProcessDefinitionGroup
* ProcessParameterDefinition
* ProcessPathDefinition
* ProcessStepDefinition
* Product
* ProductAttribute
* ProductCoFamily
* ProductCoFamilyGroup
* ProductCoType
* ProductCoTypeSet
* ProductGroup
* ProductMap
* ProductMapItem
* ProductMaterial
* ProductScheme
* ProductSet
* ProductSpec
* ProductSpecDefinition
* ProductSpecDefinitionGroup
* ProductType
* ProductVariation
* PsSet
* Recipe
* RecipeDurationRange
* RecipeParameter
* RecipeParameterRange
* RecipeStepDefinition
* RecipeStepDefinitionDurationRange
* RecipeStepDefinitionMaterial
* RecipeStepDefinitionType
* RecipeType
* ResourceGroup
* ResourceItem
* ResourceLocale
* ResourceTranslation
* Role
* RolePageDefinitionPermission
* RoleReadOnly
* SampleCategory
* SampleCategoryType
* SampleCategoryGroup
* SampleDefinition
* SampleDefinitionRuleDefinition
* SampleDefinitionType
* Schedule
* ScheduleGroup
* ScheduleItem
* SchedulePattern
* SchedulePatternItem
* Script
* ScriptGroup
* Shift
* ShiftGroup
* Site
* StateMachine
* StateMachineGroup
* StateMachineState
* StateMachineTransition
* StepCategory
* StepCategoryGroup
* StepCategoryScheme
* StepCategorySchemeLevel
* StepCategoryType
* StepCode
* StepCodeGroup
* StepCodeType
* System
* SystemBatchComposite
* SystemBatchSubComposite
* SystemCaptureScheme
* SystemCaptureSchemeColumn
* SystemCaptureTag
* SystemDiscreteComposite
* SystemDiscreteSubComposite
* SystemEventMonitor
* SystemStorageComposite
* SystemTagRelationship
* SystemType
* SystemView
* Tag
* TagAggregateComposite
* TagBooleanComposite
* TagCalculationComposite
* TagCompareComposite
* TagCounterComposite
* TagGroup
* TagHistoryDefinition
* TagInMemoryComposite
* TagLatchComposite
* TagMqttComposite
* TagOleDbComposite
* TagOpcComposite
* TagOpcHdaComposite
* TagOpcUaComposite
* TagScriptClassComposite
* TagScriptComposite
* TagSmartComposite
* TagStateComposite
* TagSwitchCase
* TagSwitchComposite
* TagTemplateComposite
* TagType
* TagVirtualComposite
* TaskDefinition
* TaskDefinitionGroup
* TaskDefinitionGroupType
* TaskDefinitionType
* TaskForm
* TaskFormGroup
* TaskFormGuide
* TaskFormGuideType
* TaskFormItem
* TaskFormItemEnum
* TaskFormItemGroup
* TaskFormItemGroupGroup
* TaskFormItemGroupType
* TaskFormItemType
* TaskFormType
* TaskVtrDefinition
* Team
* TeamGroup
* TemplateDefinition
* TransferDefinition
* TransferDefinitionGroup
* TransferDefinitionType
* User
* UserReadOnly
* UserType
* WorkflowManager
