# Orchestration

While TrakSYS Connect provides a configuration-driven, low-code framework for data exchange with external systems, how that data is used (e.g. mapping to TrakSYS data structures) must be orchestrated in script, most commonly via Data Management Service Modules or Workflow Process Definitions. Each Interface Definition contains Key fields for specifying which Module or Process Definition to run post execution.

## Post Execution

Once the Interface Transaction is complete, post procesing is triggered via execution of the configured Module or Process Definition. Ultimately, both the Module and Process Definition are intended for the same purpose: retrieval of the payload from the Interface Transaction record and executing the required processing.

### Module Trigger Key

The Module Trigger Key that will be used to execute the specified DMS Module.

### Process Def Key

The Process Definition Key that will be used to execute the specified Workflow Process Definition.

## Connect Pull Module Step

The built-in Connect Pull Module Step is intended to facilitate the implementation of a File Pull Interface Definition. When the Module Step executes, it will run the configured File Pull Interface Definition and provide the next Module Step with the following in the `ctx.Args` dictionary:

* `ConnectPull.{INTERFACEDEF.KEY}`: Model object of type `TsConnectInterfaceItem<List<{PAYLOADDEFINITION.KEY}>>`
* `ConnectPull.{INTERFACEDEF.KEY}.Count`: The number of pulled models in the list above
* `ConnectPull.{INTERFACEDEF.KEY}.HasData`: If there is any data
* `ConnectPull.{INTERFACEDEF.KEY}.HasNoData`: If there is no data

{% hint style="warning" %}
When using the Connect Pull Module Step, it is not necessary to specify a Module Trigger Key in the associated File Pull Interface Definition. In this scenario, the Connect Pull Module Step will execute the Interface Definition and pass the relevant data to the next Module Step for post processing.
{% endhint %}
