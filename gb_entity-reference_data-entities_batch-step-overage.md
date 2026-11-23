# Batch Step Overage

## Summary

### Entity Name

Batch Step Overage

### Database Table Name

`tBatchStepOverage`

### API Object Name

`DbBatchStepOverage`

### Entity Description

Each record in this table represents an amount of time a specific Batch Step exceeded its planned duration.

## Properties

`BatchStepID`

Specifies the parent Batch Step.

`DurationSeconds`

The amount of time that the Batch Step exceeded its planned duration.

`StepCategoryID`

The unique identifier (primary key) of the Category, if any, that has been assigned to the Step Overage as the main reason for exceeding its planned duration. This is a calculated field based on the available five levels of Step Categories.

`StepCategory01-05ID`

The unique identifiers (primary keys), if any, of the Categories in levels one through five that have been assigned to this Step Overage.

`StepCodeID`

The unique identifier (primary key), if any, associated with the Step Code associated with this Step Overage. This is typically associated and assigned automatically along with the Step Category.

`OeeStepType`

The OEE Step Type that is assigned to the time the Batch Step exceeded its planned duration.
