# Script Module Step

## Summary

### Entity Name

Script Module Step

### Database Table Name

`tModuleStepScript`

### API Object Name

`DbModuleStepScript`

### Entity Description

The Script Module Step allows the execution of .C# script within a Data Management Service Module.

## Properties

`Module Step [ ModuleStepID ]`

Specifies the parent Module Step.

`Script [ Script ]`

Specifies the script to be executed for this step. The Script property will contain the definition for a C# class that must inherit from the ModuleStepBase class. There are two methods that can be overridden. The template for the class will be generated and the class name and declaration should not be modified. This class is instantiated when the Data Management Service starts the parent Module. The instance is held in memory until the Module is stopped or the service is stopped/restarted.

**Load** - Code placed in the Load method is executed one time when the parent Module is first loaded/started by the Data Management Service. Any initialization and setup of local private variables should be placed in this method.

**Run** - Code placed in the Run method is executed each time this Module Step is run.
