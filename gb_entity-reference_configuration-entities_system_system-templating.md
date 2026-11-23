# System Templating

## Summary

A System Template is a specially marked System in the configuration from which other Systems can inherit. Systems that inherit from a System Template receive nearly all of the parent's configuration settings as well as the sub-entities (Event/Function/Task Definitions, KPI Calculations, etc…) and their settings. Properties that must be System specific (like Tags and other select settings) are unlocked at the inheriting System level for individual configuration. Changes made at the System Template are propagated to all of the associate children. System Templates and their children are not loaded by Logic Service and are not counted against the license limits.

### Creating System Templates

Creating a System Template is similar to creating non-template Systems. However there are special menu options for creating New Batch and Discrete System Templates (available when right-clicking on an Area node). Additionally, a System Template may be created from a non-Template System by using the `Create Template Parent System` button in the System Configuration.

### Creating new Systems from Templates

A special menu option called `Create New System from Template` is used to create a new inheriting System from an existing System Template. Once created, all of the applicable parent System Templates changes and configuration children are propagated to the new System.

### Adding children under a System Template

Once a System Template and inheriting Systems are created, any new configuration entities that are added to the parent System Template are propagated to the associated inheriting Systems. In turn, deleted entities under the System Template are removed from the inheriting Systems.

### Assigning Tags from Template Parents

A special technique exists for assisting in assigning Tags to inheriting Systems based on Tag naming conventions and Template Tags assigned to the parent System Template. A Tag Type called `Template Tag` allows for placeholder Tags to be created with the appropriate data types and assigned to the various Tag properties at the System Template level. A setting in the Advanced Tab of the System properties allows the specification of a `Template Tag Prefix`. This setting stores the common prefix characters for all Tags uses at the System Template level. In turn the `Template Tag Prefix` setting on the inheriting Systems is set with the common prefix characters for all Tags that will be assigned respectively. The Template Tags are created and assigned to the System Template entities. Real Tags are created for each child System. A special menu option called `Assign Tags from System Template` uses the Template Tag Prefix settings from the Template and inheriting Systems to match Tags and auto assign the appropriate Tags to the inheriting children and their sub-entities. The following example illustrates a simple scenario.

A System Template is created called `Packaging Template`. Its Template Tag Prefix setting is configured as `PT_`. A Template Tag is created called `PT_JOB` and assigned as the Job Tag in the System Template.

Two inheriting Systems are created called `Packaging Line 1` and `Packaging Line 2`. Their Template Tag Prefix settings are set to P1\_ and P2\_ respectively. Real OPC Tags are created called `P1_JOB` and `P2_JOB`.

Selecting `Assign Tags from System Template` on the inheriting Systems will auto find and assign the `P1_JOB` and `P2_JOB` Tags to the System properties. The results of the Tag assignments are displayed in a dialog and can be optionally exported to a CSV file for review.
