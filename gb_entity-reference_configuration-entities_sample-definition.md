# Sample Definition

## Summary

### Entity Name

Sample Definition

### Database Table Name

`tSampleDefinition`

### API Object Name

`DbSampleDefinition`

### Entity Description

A Sample Definition is a placeholder for SPC values to be recorded while defining the targets for the process. A System may contain many Sample Definitions for different measurements. Samples and Sample Sub-Groups relate back to a Sample Definition.

## Properties

`System ID [ SystemID ]`

Specifies the parent System.

`Sub-System ID [ SubSystemID ]`

Specifies the parent SubSytem, if any.

`Calculation Type [ CalculationType ] : ETS.Core.Enums.SampleDefinitionCalculationType`

This is an enumeration representing the Calculation Type of the Sample Definition.

* **VariableControl** = 1
* **AttributeControl** = 2

**Variable Control** - Examples include values that are quantitative, such as weight, height, thickness, temperature, etc.

**Attribute Control** - Examples include values that are qualitative, such as broken, ripped, defective, etc. These categories are defined by Sample Categories.

`Sample Category Group ID [ SampleCategoryGroupID ]`

Specifies the unique identifier (primary key) of the Sample Category Group which provide the choice of Sample Categories when a Sample is recorded.

`Sample Count [ SampleCount ]`

Specifies the expected number of samples to be entered in a single measurement session. For Variable Control type Definitions, this is the number of items measured. For Attribute Control type Definitions, this is the total number of items to be inspected.

`Interval Minutes [ IntervalMinutes ]`

An extensibility field that is commonly used to define how often a Sample should be taken. This field is not enforced by the Logic Service, but can be used for visualization and extensible enforcement.

`Precision [ Precision ]`

Determines the Precision of the measurement, or number of decimal places to display/record after the decimal separator.

`Product Spec Definition [ ProductSpecDefinitionID ]`

Specifies the Product Spec Definition assigned to this Sample Definition. When assigned, Sample Sub Groups created from this Sample Definition will use the relevant Product Spec to determine Limits and Targets. The matching limit and target properties below are ignored when a Product Spec Definition is assigned.

`Process Target Source Type [ ProcessTargetSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Target Constant [ ProcessTargetConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Target Tag ID [ ProcessTargetTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process LCL Source Type [ ProcessLclSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process LCL Constant [ ProcessLclConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process LCL Tag ID [ ProcessLclTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process UCL Source Type [ ProcessUclSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process UCL Constant [ ProcessUclConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process UCL Tag ID [ ProcessUclTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process LSL Source Type [ ProcessLslSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process LSL Constant [ ProcessLslConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process LSL Tag ID [ ProcessLslTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process USL Source Type [ ProcessUslSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process USL Constant [ ProcessUslConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process USL Tag ID [ ProcessUslTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process LCSL 1 Name [ ProcessLcsl1Name ]`

The name of the Custom Lower Limit as defined in the Configuration of this Sample Definition.

`Process LCSL 1 Source Type [ ProcessLcsl1SourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process LCSL 1 Constant [ ProcessLcsl1Constant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process LCSL 1 Tag ID [ ProcessLcsl1TagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process UCSL 1 Name [ ProcessUcsl1Name ]`

The name of the Custom Upper Limit as defined in the Configuration of this Sample Definition.

`Process UCSL 1 Source Type [ ProcessUcsl1SourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process UCSL 1 Constant [ ProcessUcsl1Constant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process UCSL 1 Tag ID [ ProcessUcsl1TagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Range Target Source Type [ ProcessRangeTargetSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Range Target Constant [ ProcessRangeTargetConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Range Target Tag ID [ ProcessRangeTargetTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Range LCL Source Type [ ProcessRangeLclSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Range LCL Constant [ ProcessRangeLclConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Range LCL Tag ID [ ProcessRangeLclTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Range UCL Source Type [ ProcessRangeUclSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Range UCL Constant [ ProcessRangeUclConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Range UCL Tag ID [ ProcessRangeUclTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Sigma Target Source Type [ ProcessSigmaTargetSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Sigma Target Constant [ ProcessSigmaTargetConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Sigma Target Tag ID [ ProcessSigmaTargetTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Sigma LCL Source Type [ ProcessSigmaLclSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Sigma LCL Constant [ ProcessSigmaLclConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Sigma LCL Tag ID [ ProcessSigmaLclTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Sigma UCL Source Type [ ProcessSigmaUclSourceType ]`

Determines the source type for this value.

1 – Tag\
2 – Constant

`Process Sigma UCL Constant [ ProcessSigmaUclConstant ]`

The constant value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Process Sigma UCL Tag ID [ ProcessSigmaUclTagID ]`

The unique identifier (primary key) of the Tag which holds the value that will be used for this Target when a Sample Sub-Group is displayed/recorded.

`Script Class Name [ ScriptClassName ]`

Specifies the class name which contains code that will execute for this Sample Definition. The class name specified here must be implemented as a Sample Definition Script in the Logic Scripts Developer Section.
