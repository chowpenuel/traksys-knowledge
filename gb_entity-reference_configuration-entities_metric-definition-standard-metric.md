# Metric Definitition Standard Metric

## Summary

### Entity Name

Metric Definition Standard Metric

### Database Table Name

`tMetricDefinitionStandardMetric`

### API Object Name

`DbMetricDefinitionStandardMetric`

### Entity Description

Each row in this table represents a Standard Metric for a configured Metric Definition.

## Properties

`Metric Definition ID [ MetricDefinitionID ]`

The unique identifier of the related Metric Definition.

`Metric Scheme Column ID [ MetricSchemeColumnID ]`

The unique identifier for the Metric Scheme Column contained within the Metric Definition.

`Standard Metric Type [ StandardMetricType ] : ETS.Core.Enums.StandardMetricType`

The type of Standard Metric to be used. These types include OEE, Availability, Performance, Quality, TEEP, etc.
